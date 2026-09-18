# STO 테스트 구조와 Babylon E2E 방식 비교 분석

- 출처: `wnjoon/babylon` 및 로컬 STO 저장소 8개
- 분석일: 2026-09-18
- Babylon 기준 커밋: `0de36afadb84fec624c80b07d743a0d9f5341722`
- 원문: <https://github.com/wnjoon/babylon/tree/main/test>

## 1. 한 줄 요약

Babylon의 “테스트가 Docker topology의 생성·준비·검증·정리를 직접 소유하는 방식”은 STO에 적용할 가치가 크지만, STO는 polyrepo이므로 메타레포를 없애기보다 **저장소별 component E2E를 이동하고 메타레포에는 소수의 full-journey E2E만 남기는 하이브리드 구조**가 적합하다.

## 2. 핵심 메시지 3개

- **Babylon을 그대로 복제하면 안 된다:** Babylon은 애플리케이션·테스트·Docker image build가 한 커밋에 묶인 monorepo다. STO는 여러 저장소와 서로 다른 release cadence를 가지므로 각 저장소가 전체 stack을 소유하면 bootstrap, DB schema, ABI, Kafka topic, mock이 중복된다.
- **저장소별 Docker 테스트는 필요하다:** 현재 STO의 개별 MR은 자기 변경이 실제 MySQL/Kafka/EVM과 맞는지 즉시 판정하기 어렵다. `event-listener`에 이미 있는 Testcontainers 기반 integration test가 좋은 출발점이다.
- **메타레포의 역할은 축소하되 유지해야 한다:** `sto-api → Kafka → orchestrator → EVM → block-syncer → tx/event-listener → callback`과 `legacy → application → blockchain` 전체 흐름은 어느 한 서비스의 책임 경계를 넘는다. 이 조합·부팅 순서·버전 호환성은 별도 composition owner가 필요하다.

## 3. 배경과 문제의식

현재 `sto` 메타레포는 공통 인프라, 블록체인 서비스, application 서비스, mock, contract 배포, fixture, 시나리오 러너를 모두 소유한다. 확인된 규모는 다음과 같다.

- `e2e/` tracked file: 120개
- `infra/` tracked file: 54개
- shell scenario: 39개
- shell helper: 22개
- scenario/helper shell 합계: 약 7,590줄
- 블록체인 compose는 여러 sibling repository source tree를 직접 build context로 사용한다.
- 고정 container name과 고정 host port를 사용해 동일 호스트에서 독립 test run을 병렬로 띄우기 어렵다.
- 개발용 Dockerfile은 각 서비스 저장소가 아니라 메타레포에 따로 있어 운영 Dockerfile과 이중 관리된다.

이 구조의 장점은 한 곳에서 전체 시스템을 직접 볼 수 있다는 점이다. 반면 저장소 MR과 E2E의 소유권이 분리되고, 현재 checkout 조합이 암묵적이며, 작은 서비스 변경도 큰 stack을 준비해야 한다.

## 4. Babylon 방식의 실제 구조

Babylon은 단순히 “Docker Compose로 테스트한다”가 아니다.

1. 일반 unit test는 보통의 `go test`로 실행한다.
2. E2E만 `e2e` build tag로 분리한다.
3. 현재 checkout으로 `babylond:latest` 이미지를 한 번 build한다.
4. CI는 이미지를 artifact로 저장해 여러 E2E job이 재사용한다.
5. Go test 안의 manager가 테스트별 Docker network, node container, relayer, 임시 디렉터리와 port를 관리한다.
6. 각 scenario는 Go assertion과 `Eventually`로 chain state가 수렴하는지를 검증한다.
7. 신규 `e2ev2`는 `t.TempDir`, `t.Cleanup`, 고유 network ID, 동적 port와 `t.Parallel`을 사용한다.
8. upgrade scenario는 과거 version image와 현재 checkout image를 함께 사용한다.

따라서 Babylon에서 가져와야 할 핵심은 **unit test의 컨테이너화**가 아니라 **component/E2E 환경의 programmatic lifecycle, 격리, 자동 정리, 이미지 재사용**이다.

### Babylon의 장점

- 테스트 코드와 topology 설정이 한 언어와 한 테스트 리포트에 묶인다.
- 테스트마다 독립 network와 임시 data를 만들 수 있다.
- readiness와 상태 수렴을 polling assertion으로 표현한다.
- CI에서 image build를 한 번 하고 scenario job을 병렬 fan-out한다.
- 현재 버전과 과거 버전의 upgrade 호환성까지 동일 framework에서 검증한다.

### Babylon의 한계

- 구형 `test/e2e`는 중단 시 container/network가 남는 문제가 README에 명시돼 있고, `clean-e2e`는 호스트의 모든 container를 지우는 광범위한 정리를 사용한다.
- 기본 image tag가 `latest`라서 CI job 안에서는 artifact로 일치하더라도 장기 재현성에는 digest/SHA manifest가 더 안전하다.
- 테스트당 여러 node와 relayer를 띄워 비용이 높고 timeout이 60분이다.
- CLI command의 문자열 출력에 의존하는 assertion이 있어 구조화된 API assertion보다 취약한 부분이 있다.
- monorepo에서 자연스러운 방식이므로 polyrepo에 그대로 복제하면 공유 fixture와 환경 정의가 흩어진다.

## 5. 현재 STO 테스트 상태

| 저장소 | 현재 로컬 테스트 자산 | 현재 공백 |
|---|---|---|
| `sto-smart-contract` | Forge test 16개, ABI/storage gate, in-process `ScenarioE2E` | clean Anvil 배포와 외부 client 관점 artifact 검증은 메타레포 의존 |
| `tx-listener` | Go unit test 5개 | Kafka·MySQL·callback을 함께 쓰는 component test 없음 |
| `event-listener` | Go test 14개, Testcontainers MySQL integration, callback server | Kafka 입력부터 callback까지의 service boundary 확대 필요 |
| `block-syncer` | Go unit test 20개 | 실제 EVM→receipt→Kafka→checkpoint component test 없음 |
| `orchestrator` | Go unit test 23개, 별도 live TSM integration tag | Anvil·Kafka·MySQL·Redis를 묶은 기본 component test 없음 |
| `sto-api` | Go test 72개, integration build tag | integration test가 localhost 고정 포트와 외부 bootstrap state에 의존하고 self-contained하지 않음 |
| Java `iss-api` | Mockito 중심 Java test 18개 | 실제 Spring·MySQL·외부 API adapter component test 없음 |
| `st-app` | Go test 86개, store integration test 다수 | 실제 application journey와 blockchain stack 결합은 메타레포 의존 |

중요한 현재 상태: 메타레포의 application compose에서는 Java `iss-api`/`iss-ap`가 deprecated 처리돼 있고, `st-app`이 `iss-api` alias와 포트를 인수한다. 신규 E2E 투자 대상을 Java `iss-api`로 할지 `st-app`으로 할지 먼저 확정해야 한다.

## 6. 현재 구조와 목표 구조 비교

| 항목 | 현재 메타레포 중심 | Babylon식 전면 분산 | 권장 하이브리드 |
|---|---|---|---|
| MR 변경 피드백 | 느림·간접적 | 빠름 | 빠름 |
| 전체 업무 흐름 신뢰 | 높음 | 저장소별 사각지대 발생 | 높음 |
| 테스트/서비스 소유권 | 분리 | 명확 | 명확 |
| bootstrap/fixture 중복 | 중앙 집중 | 매우 커질 수 있음 | 공통 artifact로 통제 |
| 병렬 실행 | 고정 port/name 때문에 어려움 | 가능 | 가능 |
| 실패 원인 격리 | 어려움 | 쉬움 | 쉬움 |
| cross-repo version 재현 | 현재는 암묵적 | 각 저장소 구현에 따라 다름 | SHA/digest manifest로 명시 |
| 운영 topology 검증 | 가능 | 약해짐 | 메타레포에서 유지 |
| 유지보수 비용 | 메타레포에 집중 | 모든 저장소에서 반복 | 책임별 분산 |

## 7. 권장 테스트 계층과 소유권

### 7.1 Unit test

- 각 저장소가 소유한다.
- 외부 process나 Docker가 없어야 한다.
- Go는 `go test -race ./...`, Java는 JUnit/Mockito, Solidity는 Forge unit/fuzz/invariant를 유지한다.
- unit test 자체를 Docker 안에서 실행하는 것은 CI toolchain 고정에는 유용하지만 테스트 격리의 핵심은 아니다. 로컬 fast loop를 느리게 만들지 않도록 기본 gate는 native runner로 둔다.

### 7.2 Contract test

- ABI selector/event/error, Kafka envelope, callback DTO, HTTP API surface, DB migration compatibility를 producer와 consumer가 함께 검증한다.
- 원칙적으로 Docker 없이 빠르게 실행한다.
- 상류 변경 시 하류 consumer contract test를 trigger한다.

### 7.3 Component integration/E2E

- 각 서비스 저장소가 소유한다.
- SUT는 현재 commit에서 build하거나 test process로 실행한다.
- 실제로 필요한 최소 의존성만 ephemeral container로 기동한다.
- `integration` build tag 또는 별도 Maven profile로 unit test와 분리한다.

### 7.4 Full-journey E2E

- `sto` 메타레포가 소유한다.
- 운영과 유사한 network, topic, migration, 부팅 순서, 서비스 버전 조합을 검증한다.
- 서비스 내부의 상세 matrix는 제거하고 5~10개의 중요 업무 여정만 유지한다.
- 사용 image와 contract artifact는 commit SHA 또는 digest manifest로 고정한다.

## 8. 저장소별 권장 범위

| 저장소 | 유지/추가할 테스트 | Docker 의존성 | 메타레포에 남길 검증 |
|---|---|---|---|
| `sto-smart-contract` | unit/fuzz/invariant, clean deploy smoke, ABI/storage snapshot | Anvil 1개 | 실제 서비스들이 동일 artifact를 소비하는지 |
| `tx-listener` | receipt 성공/revert, callback retry/idempotency | Kafka, MySQL, callback test server | 실제 block-syncer가 만든 message와 최종 sto-api callback |
| `event-listener` | event family decode, DB 저장, callback retry/idempotency | Kafka, MySQL, callback test server | 실제 contract log부터 application callback까지 |
| `block-syncer` | block gap, restart, duplicate receipt, producer failure recovery | Anvil, Kafka, MySQL | orchestrator가 전송한 실제 transaction의 최종 수렴 |
| `orchestrator` | wallet/sign/nonce/send/revert/retry | Anvil, Kafka, MySQL, Redis, dev KMS | block-syncer/listener를 거친 최종 완료와 callback |
| `sto-api` | `read`, `wallet`, 핵심 `tx` profile | Anvil 및 profile별 검증된 dependency image | 전체 pipeline과 application 연계 golden flow |
| Java `iss-api` 또는 `st-app` | Spring/Go service + DB + WireMock/mock adapter component test | MySQL, 외부 API stub | 실제 sto-api stack과 legacy/KSD를 잇는 full journey |

`orchestrator + smart contract`만으로 검증되는 것은 “서명·전송 component E2E”다. transaction의 최종 성공·실패와 callback까지 검증하려면 block-syncer와 tx-listener가 반드시 포함돼야 한다. event payload까지 보면 event-listener도 포함해야 한다.

## 9. 구현 방향

### Container framework

STO는 `testcontainers-go`를 우선 사용하는 것이 합리적이다.

- `event-listener`가 이미 동일 library와 MySQL module을 사용한다.
- 새 공통 추상화와 학습 비용을 줄일 수 있다.
- Babylon의 lifecycle 원칙은 library와 독립적이므로 `ory/dockertest`를 그대로 선택할 필요는 없다.

Java 서비스는 Testcontainers Java를 사용하고, 공통 계약은 library code 복사보다 image/fixture/schema artifact로 공유한다.

### 공통 testkit

다음은 저장소별로 복사하지 않는다.

- `Deploy.s.sol`과 contract artifact
- ABI snapshot
- DB migration/seed
- Kafka topic과 message schema
- callback envelope
- KSD account/ISIN fixture schema
- 검증된 dependency image manifest

형태는 독립 `sto-testkit` Go module 하나로 강제하기보다, 언어 중립적인 versioned artifact를 중심에 둔다.

- `contract-fixture:<contract-sha>` image 또는 deploy CLI
- `db-schema:<migration-sha>` image/artifact
- JSON Schema/fixture bundle
- `stack-manifest.yaml` with image digest
- 언어별 얇은 adapter: Go Testcontainers, Java Testcontainers

### Image 정책

- SUT: MR commit으로 local build
- 의존 서비스: 검증된 commit SHA tag 또는 digest
- `latest`, `development`, branch name은 개발 편의 입력으로만 허용
- 테스트 시작 시 resolved manifest를 artifact로 저장
- contract SHA와 ABI SHA도 같은 manifest에 포함

## 10. 단계적 전환안

1. **용어와 gate 분리**
   - `unit`, `contract`, `component`, `journey`를 CI job과 문서에서 명확히 구분한다.
   - Docker를 쓰는 테스트를 unit test로 부르지 않는다.

2. **event-listener 파일럿 확대**
   - 현재 MySQL Testcontainers helper를 유지한다.
   - Kafka를 추가하고 실제 consumer input부터 callback까지 검증한다.
   - 동적 port, 자동 cleanup, 실패 log 수집 패턴을 표준화한다.

3. **tx-listener와 block-syncer로 확장**
   - 작은 topology로 높은 결함 검출 효과를 얻기 쉽다.
   - listener는 synthetic receipt/event를 주입하고, syncer는 Anvil block을 생성한다.

4. **orchestrator component E2E**
   - Anvil + Kafka + MySQL + Redis + dev KMS로 성공/revert/nonce/retry를 검증한다.
   - 실제 TSM/HSM은 기본 MR gate가 아닌 보호된 integration profile로 유지한다.

5. **sto-api profile 분리**
   - `read`: EVM + contract
   - `wallet`: orchestrator + MySQL + Redis
   - `tx-smoke`: 핵심 1~3개 transaction + final callback
   - 상세 handler/API matrix는 unit/contract test로 이동한다.

6. **application 구현체 확정**
   - Java `iss-api` 유지인지 `st-app` 전환 완료인지 결정한다.
   - 유지 대상에 MySQL + external API stub component test를 만든다.

7. **메타레포 감량**
   - 저장소 component test가 안정화된 뒤 중복 `bc-*` scenario를 삭제한다.
   - 메타레포는 발행, 말소, 제한/해제, revert/retry, event callback, 재기동 같은 golden journey만 유지한다.

## 11. 변경 가치 판정

### 판정

- **Babylon의 lifecycle/격리 방식을 STO에 도입:** 가치 높음, 권장
- **각 저장소가 component E2E를 소유:** 가치 높음, 권장
- **unit test 전체를 Docker container 안에서만 실행:** 가치 낮음, 비권장
- **sto 메타레포의 E2E를 완전히 제거:** 위험이 더 큼, 비권장
- **메타레포를 full-journey와 version manifest 전용으로 축소:** 가치 매우 높음, 강력 권장

### 기대 효과

- MR에서 결함 발생 경계를 바로 알 수 있다.
- 고정 port와 공유 state 없이 병렬 CI가 가능해진다.
- 서비스 저장소의 변경과 테스트가 같은 review/merge 단위가 된다.
- 메타레포의 shell scenario와 서비스별 Dockerfile 중복을 줄일 수 있다.
- 장애 재현 시 사용한 image/contract 조합을 artifact로 남길 수 있다.

### 주요 비용과 위험

- 초기에는 기존 meta E2E와 신규 component E2E가 동시에 존재해 CI 비용이 일시적으로 증가한다.
- 공통 fixture와 bootstrap을 복사하면 장기 유지비가 현재보다 커진다.
- private base image와 사내 registry 접근을 CI/개발 환경에서 해결해야 한다.
- Kafka topic, consumer group, DB schema, EVM chain state를 test run별로 격리해야 한다.
- 현재 운영 Dockerfile은 prebuilt binary와 사내 base image를 전제로 하므로 repo-local test image target을 별도로 정리해야 한다.
- Java `iss-api`와 `st-app`의 중복 투자 가능성을 먼저 제거해야 한다.

## 12. 의사결정 제안

최종 제안은 다음과 같다.

> **도입한다. 단, “Babylon처럼 각 저장소가 자기 component topology를 테스트 코드로 관리”하는 부분만 도입하고, `sto` 메타레포는 제거하지 않는다. 메타레포는 full-journey E2E와 검증된 image/contract 조합 manifest의 소유자로 축소한다.**

첫 구현 대상은 이미 Testcontainers가 있는 `event-listener`, 두 번째는 경계가 단순한 `tx-listener`, 세 번째는 `block-syncer`, 네 번째는 `orchestrator`, 마지막으로 full pipeline 비용이 큰 `sto-api`가 적합하다.

## 13. 중요한 숫자와 사실

| 항목 | 내용 | 의미 |
|---|---|---|
| Babylon 기준 커밋 | `0de36af` | 2026-08-04 상태 기준 분석 |
| Babylon E2E timeout | 주요 target 60분 | 무거운 topology를 MR에서 모두 직렬 실행하면 비효율적 |
| STO meta E2E tracked files | 120개 | 테스트 소유권과 유지보수 부담이 중앙 집중 |
| STO shell scenario/helper | 61개, 약 7,590줄 | 서비스 저장소와의 변경 drift 가능성이 큼 |
| STO smart-contract tests | 16개 | 이미 contract 내부 business journey가 존재 |
| STO Go service tests | tx 5, event 14, block 20, orchestrator 23, sto-api 72 | unit 자산은 있으나 component boundary가 약함 |
| Java iss-api tests | 18개 | Mockito 중심, 실제 service topology 검증은 부족 |
| st-app tests | 86개 | 현재 application compose의 실제 활성 구현체 |

## 14. 공유용 요약

### 짧은 버전

Babylon 방식은 STO에 적용할 가치가 높다. 다만 Babylon은 monorepo이고 STO는 polyrepo라서, 각 저장소가 전체 E2E stack을 복제하면 bootstrap·fixture·ABI·DB schema가 더 많이 중복된다. 권장안은 unit/contract/component test를 각 저장소로 옮기고, `sto` 메타레포에는 여러 저장소를 관통하는 소수의 full-journey E2E와 image SHA manifest만 남기는 것이다. `event-listener`의 기존 Testcontainers integration test를 파일럿으로 확대하는 것이 가장 안전하다.

### 조금 긴 버전

Babylon의 핵심은 unit test를 Docker로 감싸는 것이 아니라, Go test가 Docker network·container·임시 data의 lifecycle을 직접 소유하는 데 있다. 이 방식은 STO의 개별 저장소 MR 피드백과 병렬 실행, 실패 원인 격리에 큰 도움이 된다. 하지만 Babylon은 한 저장소의 한 commit으로 바이너리와 테스트가 함께 움직이는 monorepo다. STO는 `sto-api`, orchestrator, syncer/listener, contract, application이 나뉜 polyrepo라서 각 저장소에 전체 stack을 복제하면 공통 bootstrap과 fixture가 흩어진다. 따라서 tx-listener는 Kafka·MySQL·callback, block-syncer는 Anvil·Kafka·MySQL처럼 최소 topology만 자기 저장소에서 검증해야 한다. orchestrator도 contract 전송까지만 자기 component 경계이고, 최종 receipt/callback까지는 full pipeline 검증이 필요하다. `sto` 메타레포는 제거 대상이 아니라, 발행·말소·revert·event callback 같은 핵심 업무 여정과 버전 조합을 보증하는 composition repo로 축소하는 것이 맞다. 또한 현재 application compose는 Java `iss-api` 대신 `st-app`을 활성 구현체로 사용하므로 신규 투자 대상을 먼저 확정해야 한다.

## 15. 시사점

- 개발팀: 저장소 MR에서 실제 dependency 연동 실패를 빠르게 발견할 수 있다.
- 플랫폼/DevOps: SHA/digest image manifest와 test artifact 보존 정책이 필요하다.
- QA: 상세 기능 matrix는 서비스 component test로 이동하고, full journey는 사용자 업무 기준으로 단순화할 수 있다.
- 아키텍처 담당자: 메타레포는 코드 집합이 아니라 composition·compatibility의 명시적 소유자가 된다.

## 16. 더 생각해볼 질문

1. Java `iss-api`는 실제 유지 대상인가, 아니면 `st-app`으로 완전히 대체되는가?
2. 공통 fixture·contract deploy·DB schema를 어떤 versioned artifact로 배포할 것인가?
3. MR 필수 gate의 시간 예산은 몇 분이며, 어느 component smoke를 포함할 것인가?
4. private registry의 commit SHA image 보존 기간과 접근 방식은 무엇인가?
5. 실제 TSM/HSM·사내 legacy 연동 테스트를 기본 CI와 어떻게 분리할 것인가?
6. 메타레포 golden journey의 최소 집합과 release gate는 무엇인가?

## 17. 근거 링크

- Babylon test tree: <https://github.com/wnjoon/babylon/tree/0de36afadb84fec624c80b07d743a0d9f5341722/test>
- Babylon legacy container manager: <https://github.com/wnjoon/babylon/blob/0de36afadb84fec624c80b07d743a0d9f5341722/test/e2e/containers/containers.go>
- Babylon e2ev2 test manager: <https://github.com/wnjoon/babylon/blob/0de36afadb84fec624c80b07d743a0d9f5341722/test/e2ev2/tmanager/manager.go>
- Babylon CI image build/fan-out: <https://github.com/wnjoon/babylon/blob/0de36afadb84fec624c80b07d743a0d9f5341722/.github/workflows/ci.yml>
- Babylon Makefile E2E targets: <https://github.com/wnjoon/babylon/blob/0de36afadb84fec624c80b07d743a0d9f5341722/Makefile>
