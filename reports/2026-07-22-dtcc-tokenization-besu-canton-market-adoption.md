# DTCC 토큰화 서비스와 Besu·Canton 기관 채택 현황

- 작성일: 2026-07-22
- 작성 목적: DTCC의 DTC 보관자산 토큰화 발표를 해석하고, Besu와 Canton의 구조적 차이·기관 채택·시장 지위를 팀 공유용으로 정리
- 출발 기사: [토큰포스트 — DTCC, DTC 보관자산 토큰화로 실제 미국 거래 처리 성공](https://www.tokenpost.kr/news/blockchain/379355)
- 핵심 1차 자료: [DTCC 2026년 7월 15일 공식 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality)
- 규제 자료: [SEC의 DTC 토큰화 비조치 의견 관련 성명](https://www.sec.gov/newsroom/speeches-statements/peirce-121125-tokenization-trending-statement-division-trading-markets-no-action-letter-related-dtcs-development)

> **용어 범위:** 국내에서 STO는 보통 ‘토큰증권 발행’을 뜻하지만, 본 리포트는 DTCC 발표의 실제 범위에 맞춰 토큰화 증권, 디지털 트윈, 레포·담보, 토큰화 예금과 결제 인프라까지 포함한 **기관형 토큰화 금융 인프라**를 분석한다. 레포 거래액이나 결제액을 STO 발행잔액으로 간주하지 않는다.

## 1. 한 줄 요약

DTCC는 DTC 보관증권의 디지털 트윈을 Besu 기반 자체 AppChain과 Canton 같은 승인된 외부 네트워크에서 발행·활용하는 멀티체인 전략을 추진하고 있으며, 현재 공개적으로 관측되는 기관형 토큰증권·레포 생태계는 Canton이 앞서지만 Besu는 기관 자체망과 결제 인프라에서 강해 두 기술은 경쟁과 보완 관계를 동시에 가진다.

## 2. 핵심 메시지 3개

- **“Besu 토큰을 Canton으로 연결했다”는 구조는 확인되지 않는다:** 공식 자료는 DTC 보관자산의 디지털 전환이 Besu와 Canton에서 이뤄졌다고 설명하며, Canton 파트너십 자료는 DTC 보관 미국 국채를 Canton에 직접 발행(mint)한다고 밝힌다. 동일 토큰의 Besu→Canton 브리지 여부는 공개되지 않았다.
- **Canton 선택의 핵심은 단순 외부 접속이 아니라 기존 공유시장에 대한 배포다:** Besu로도 외부 기관이 참여하는 컨소시엄을 만들 수 있지만, Canton에는 이미 레포, 담보, 거래, 토큰화 현금과 기관 애플리케이션이 존재한다. DTCC는 자체망을 확장하는 것과 별도로 DTC 자산을 외부 공동 생태계에 공급하려는 것으로 해석된다.
- **기관 채택은 용도별로 갈린다:** 토큰증권·디지털 채권·레포·담보의 공유 생태계에서는 Canton의 생산 사례가 더 두드러진다. 반면 Besu는 DTCC AppChain, Swift 공유원장, Fnality 같은 기관 통제형 네트워크와 결제 레일에서 강하다.

## 3. 배경과 문제의식

토큰화 증권 시장을 평가할 때는 세 가지를 구분해야 한다.

1. **블록체인 소프트웨어:** Besu처럼 기관이 자체 네트워크를 구축할 때 사용하는 클라이언트 소프트웨어
2. **공유 네트워크:** Canton처럼 여러 독립 기관과 애플리케이션이 공통 인프라에 연결되는 네트워크
3. **업무 플랫폼:** DTCC Tokenization Service, Broadridge DLR, Goldman Sachs GS DAP, LSEG DiSH처럼 실제 자산·거래 업무를 처리하는 서비스

Besu는 하나의 네트워크가 아니므로 모든 Besu 사설망의 자산과 거래량을 합산하기 어렵다. Canton은 공유 네트워크이기 때문에 일부 활동을 네트워크 단위로 관측할 수 있다. 따라서 두 기술의 시장점유율을 단일 숫자로 비교하면 구조적으로 왜곡된다.

또한 기관형 토큰화에서는 다음 수치를 혼동하면 안 된다.

- DTC가 보관하는 전체 전통자산 규모
- DTCC가 전통시장에서 처리하는 연간 거래액
- 블록체인에 실제 발행된 토큰증권 잔액
- 레포·담보 플랫폼이 일정 기간 처리한 누적 거래액
- 원증권을 외부 장부에 표현한 represented asset value

이 리포트는 공식적으로 네트워크가 명시된 시스템과 실제 운영·거래 사례를 우선하며, 단순 컨소시엄 가입이나 validator 참여는 보조 신호로만 취급한다.

## 4. DTCC 발표에서 확인되는 사실

### 4.1 실제 운영 거래

DTCC는 2026년 7월 15일 DTC 보관자산을 토큰으로 전환해 실제 생산환경 거래에 사용했다고 발표했다. 30곳이 넘는 전통 금융기관과 디지털자산 기업이 참여했으며, DTCC의 당일 라이브 페이지는 약 40개사의 참여라고 표현한다. 집계 시점 또는 범위 차이가 있을 수 있으므로 본문에서는 공식 보도자료의 ‘30곳 이상’을 기준으로 삼는다. [DTCC 보도자료](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality), [DTCC 라이브 업데이트](https://www.dtcc.com/digital-assets/tokenization/live-production-trades)

검증한 업무는 다음과 같다.

- 담보 제공
- 증권 대차
- 미국 국채·레포 인도대금동시결제(DVP)
- 주식 DVP
- 주식 인도동시결제(DVD)
- 주식 토큰 이전
- 중앙청산소(CCP) 마진 업무

정식 DTCC Tokenization Service 출시는 2026년 10월로 예정돼 있다. [DTCC 공식 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality)

### 4.2 디지털 트윈 구조

DTCC의 토큰은 원증권과 별개의 신규 경제적 권리를 만드는 것이 아니라, DTC에 보관된 증권 포지션을 블록체인에 표현하는 **디지털 트윈**이다. DTC 보관증권은 전통 형태와 토큰화 형태 사이에서 전환될 수 있고, 참가자가 선택한 등록 지갑으로 전달된다. [DTCC Tokenization Service](https://www.dtcc.com/digital-assets/tokenization)

DTCC는 전통 형태와 토큰화 형태가 동일한 CUSIP와 법적·경제적 권리 및 투자자 보호를 유지한다고 설명한다. 토큰에는 mint, burn, 강제이전, clawback, 일시정지, 동결 같은 규제·통제 기능이 포함될 예정이다. DTCC의 ComposerX LedgerScan은 여러 전통·블록체인 원장의 소유권 정보를 통합·조정하는 역할을 맡는다. [DTCC Tokenization Service](https://www.dtcc.com/digital-assets/tokenization)

### 4.3 규제 기반

SEC 거래시장국은 2025년 12월 DTC의 제한적·자발적 증권 토큰화 프로그램에 비조치 의견을 냈다. 등록된 지갑을 가진 적격 DTC 참가자가 지원 블록체인에서 토큰화된 entitlement를 이전할 수 있고, DTC 시스템이 공식 장부와 기록을 추적하는 구조다. 비조치 의견은 법률의 일반적 승인이나 영구적 면제가 아니라, 제출된 사실관계와 조건 아래 집행조치를 권고하지 않겠다는 제한적 입장이다. [SEC 성명](https://www.sec.gov/newsroom/speeches-statements/peirce-121125-tokenization-trending-statement-division-trading-markets-no-action-letter-related-dtcs-development), [SEC 비조치 의견서](https://www.sec.gov/files/tm/no-action/dtc-nal-121125.pdf)

## 5. Besu와 Canton은 발표에서 어떻게 사용됐나

DTCC는 “digital conversions occurred on LFDT’s Besu (DTCC’s private network) and Canton (a public network)”라고 밝혔다. 이어 이를 복원력, 확장성, 참여자 선택권을 확보하기 위한 멀티체인 전략이라고 설명했다. [DTCC 공식 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality)

### 5.1 Besu의 의미

LFDT는 **Linux Foundation Decentralized Trust**의 약칭이다. Besu는 LFDT 산하의 오픈소스 이더리움 실행 클라이언트로, 퍼블릭 이더리움뿐 아니라 프라이빗·퍼미션드 네트워크에도 사용할 수 있다. 과거 명칭은 Hyperledger Besu였으며, LFDT 출범 후 프로젝트 공식 명칭이 Besu로 변경됐다. [LFDT 출범 발표](https://www.lfdecentralizedtrust.org/announcements/linux-foundation-decentralized-trust-launches-with-17-projects-100-founding-members), [Besu 공식 소개](https://www.lfdecentralizedtrust.org/projects/besu)

따라서 ‘Besu가 프라이빗’인 것이 아니다. 이번에 DTCC가 Besu로 구성한 **DTCC AppChain 인스턴스가 프라이빗**한 것이다. DTCC는 이를 규제된 기업 업무를 위한 이더리움 호환·퍼미션드 AppChain으로 소개한다. [DTCC 지원 네트워크](https://www.dtcc.com/digital-assets/tokenization)

### 5.2 Canton의 의미

Canton은 공식적으로 public network 또는 public L1을 표방하지만 이더리움과 같은 완전 공개·완전 투명·익명 permissionless 체인과는 다르다. 네트워크 참여는 개방형이지만 현재 validator 신청에는 스폰서십이 필요하고, 각 애플리케이션은 접근권한을 permissioned 또는 permissionless로 설정할 수 있다. 거래 데이터는 이해관계자에게만 선택적으로 전달된다. [Canton FAQ](https://www.canton.network/faq), [Canton 공식 문서](https://docs.canton.network/overview/understand/what-is-canton)

가장 정확한 표현은 **공개형이지만 애플리케이션·거래 단위로 권한과 프라이버시를 적용하는 public-permissioned network**다. Canton 백서도 broader decentralized public permissioned network라고 정의한다. [Canton 백서](https://www.canton.network/hubfs/Canton/Canton%20Network%20-%20White%20Paper.pdf)

여기서 public은 단순히 인터넷망을 사용한다는 뜻이 아니다. 외부 독립기관이 공통 네트워크와 거버넌스에 연결될 수 있다는 의미다. 프라이빗 Besu 컨소시엄도 인터넷을 통해 외부 기관을 연결할 수 있지만, 네트워크의 참가 승인·운영·거버넌스를 특정 기관이나 컨소시엄이 통제한다는 차이가 있다.

## 6. 실제 구조에 대한 최선의 해석

공개 자료를 종합하면 다음 구조가 가장 타당하다.

```text
DTC 중앙 장부·보관자산
          │
DTCC Tokenization Service / ComposerX
          ├── DTCC AppChain: Besu 기반 사설망
          ├── Canton Network: 승인된 외부 공유 네트워크
          └── Stellar: 2027년 상반기 지원 예정
```

DTCC는 2025년 12월 DTC 보관 미국 국채의 일부를 Canton Network에 직접 mint하는 파트너십을 발표했다. 2026년 5월에는 Stellar를 두 번째 외부 블록체인 연결 대상으로 발표했다. DTCC의 현재 네트워크 페이지도 Besu 기반 AppChain, Canton, Stellar를 별도 네트워크로 나열한다. [DTCC–Canton 파트너십](https://www.dtcc.com/news/2025/december/17/dtcc-and-digital-asset-partner-to-tokenize-dtc-custodied-us-treasury-securities), [DTCC–Stellar 발표](https://www.dtcc.com/news/2026/may/27/tokenization-service-to-connect-with-stellar-public-blockchain-as-dtc-advances-multi-chain-strategy), [DTCC 지원 네트워크](https://www.dtcc.com/digital-assets/tokenization)

따라서 다음과 같이 구분해야 한다.

| 판단 | 상태 | 설명 |
|---|---|---|
| DTC 보관자산의 디지털 트윈이 Besu와 Canton에서 발행·처리됐다 | 확인 | DTCC가 두 네트워크에서 digital conversion이 이뤄졌다고 발표 |
| Besu에 있던 동일 토큰을 Canton이 외부기관과 연결했다 | 미확인 | 브리지 또는 Besu→Canton 이전 구조는 발표에 없음 |
| 같은 증권 포지션을 두 네트워크에 동시에 복제했다 | 미확인 | 자산·네트워크별 배치와 중복 방지 방식 미공개 |
| Besu↔Canton 전환이 burn-and-mint 방식이다 | 미확인 | 구체적 전환 프로토콜 미공개 |
| Zenith를 사용했다 | 미확인 | DTCC 공식 발표와 지원 네트워크 자료에서 Zenith 언급을 찾을 수 없음 |

Zenith는 Canton 생태계의 EVM·SVM 실행 레이어를 표방하지만, Besu가 EVM이라는 사실만으로 DTCC가 Zenith를 사용했다고 추정할 수 없다. 사용됐다면 Canton 측 구현과 관련될 가능성이 있으나, 현재 확인 가능한 근거는 없다. [Zenith의 자체 기술 설명](https://zenith.network/ecosystem)

## 7. 왜 Besu 컨소시엄만 쓰지 않고 Canton도 사용했나

Besu로 외부 기관이 참여하는 컨소시엄을 만드는 것은 기술적으로 가능하다. Canton 사용은 Besu가 외부 연결을 지원하지 못해서가 아니다.

### 7.1 DTCC가 공식적으로 밝힌 이유

DTCC가 명시한 이유는 다음과 같다.

- 복원력
- 확장성
- 참여자의 네트워크 선택권
- 전통 금융과 디지털 생태계 간 상호운용성

[DTCC 공식 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality)

### 7.2 실질적인 차이

DTCC가 외부 기관을 Besu AppChain에 초대하면 참가자는 늘어나지만, 여전히 DTCC가 운영·승인하는 하나의 컨소시엄 네트워크다. 반면 Canton에는 이미 독립된 금융기관과 거래·담보·현금 애플리케이션이 연결돼 있다.

Canton에서는 2025년부터 미국 국채를 활용한 업무시간 외 금융, stablecoin 결제, 실시간 담보 재사용과 온체인 레포가 수행됐다. 참여 기관에는 Bank of America, Circle, Citadel Securities, DRW, Société Générale, Tradeweb, Virtu 등이 포함됐다. [Digital Asset의 2025년 미국 국채 금융 발표](https://blog.digitalasset.com/press-release/digital-asset-and-industry-working-group-complete-groundbreaking-on-chain-us-treasury-financing-on-canton-network), [후속 담보 재사용 발표](https://blog.digitalasset.com/press-release/the-canton-networks-industry-working-group-demonstrates-next-phase-of-onchain-u.s.-treasury-financing-on-canton-network)

Canton은 DTC 참가자뿐 아니라 Canton 애플리케이션 사업자가 DTCC Tokenization Service로 생성된 자산을 활용하는 경로도 안내한다. [Canton의 DTC·Fed 적격증권 안내](https://www.canton.network/dtc-and-fed-eligible-securities-on-canton)

**추론:** Canton의 가장 큰 가치는 단순한 노드 접속이 아니라, DTC 토큰화 자산을 이미 존재하는 외부 거래·현금·레포·담보 생태계에 배포할 수 있다는 점이다. DTCC는 모든 기능을 자체 Besu 컨소시엄에 다시 구축하는 대신, 자체망과 외부 공유망을 동시에 지원해 네트워크 종속을 줄이고 시장별 선택권을 제공하려는 것으로 보인다.

## 8. 기관별 네트워크 선택 현황

### 8.1 판정 기준

- **운영 채택:** 실제 상품·거래·결제 시스템에 네트워크가 명시됨
- **구축/출시 단계:** 생산 전환 또는 초기 사용을 준비 중
- **거래 참여:** 해당 네트워크에서 실제 거래에 참여했지만 자체 핵심 플랫폼을 그 네트워크로 정했다고 보기는 어려움
- **회원/validator:** 네트워크 거버넌스 참여 신호일 뿐, 업무 플랫폼 채택으로 계산하지 않음

### 8.2 주요 기관과 플랫폼

| 기관·플랫폼 | 네트워크 | 상태 | 적용 분야 | 근거 |
|---|---|---|---|---|
| DTCC Tokenization Service | Besu AppChain + Canton | 실제 생산거래, 2026년 10월 출시 예정 | DTC 보관 증권 디지털 트윈 | [DTCC](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality) |
| DTCC Collateral AppChain | Besu | 생산 전환 단계 | 멀티자산 담보 관리 | [DTCC](https://www.dtcc.com/digital-assets/collateral-appchain) |
| Broadridge DLR | Canton | 상용 운영 | 기관 레포·토큰화 담보 | [Broadridge](https://www.broadridge.com/article/capital-markets/dlr-transacts-1-trillion-a-month) |
| Goldman Sachs GS DAP | Canton/Daml 생태계 | 상용 운영 | 디지털 채권·MMF 미러 토큰 | [Canton FAQ](https://www.canton.network/faq), [Goldman Sachs·BNY](https://www.goldmansachs.com/pressroom/press-releases/2025/bny-goldman-sachs-launch-tokenized-money-market-funds-solution) |
| BNY LiquidityDirect | GS DAP 연결 | 상용 운영 | 토큰화 MMF | [BNY](https://www.bny.com/corporate/global/en/about-us/newsroom/company-news/bny-and-goldman-sachs-launch-tokenized-money-market-funds-solution.html) |
| LSEG DiSH | Canton | 출시·초기 운영 | 토큰화 은행예금, 현금 결제 | [LSEG](https://www.lseg.com/en/media-centre/press-releases/2026/lseg-launches-digital-settlement-house) |
| Tradeweb | Canton | 실제 거래 참여 | 미국 국채·레포 거래 실행 | [Digital Asset](https://blog.digitalasset.com/press-release/digital-asset-and-industry-working-group-complete-groundbreaking-on-chain-us-treasury-financing-on-canton-network) |
| Bank of America·Citadel·Goldman 등 | Canton | 실제 거래 참여 | 온체인 미국 국채 금융 | [Canton 사례](https://www.canton.network/blog/the-weekend-revolution-collateral-is-finally-working-overtime) |
| Swift Shared Ledger | Besu | 초기 사용 준비 | 토큰화 예금 기반 국경 간 결제 | [Swift 기술 발표](https://www.swift.com/news-events/news/swifts-blockchain-based-shared-ledger-progresses-mvp-implementation), [17개 은행 초기 사용](https://www.swift.com/news-events/press-releases/swifts-blockchain-ledger-ready-use-17-banks-set-pioneer-tokenised-cross-border-payments-trusted-global-infrastructure) |
| Fnality Payment System | Besu | 영국 상용 운영 | 중앙은행 예치금 기반 도매 결제 | [Fnality](https://fnality.com/home), [LFDT 사례](https://lf-hyperledger.atlassian.net/wiki/display/CMSIG/2021-05-05) |
| HKMA Project Evergreen | Besu + Canton/Daml | 토큰화 녹색채권 발행 완료 | 채권·현금 토큰, 발행·결제 | [HKMA 보고서](https://www.hkma.gov.hk/media/eng/doc/key-information/press-release/2023/20230824e3a1.pdf) |

### 8.3 혼합 구조가 보여주는 점

HKMA의 Project Evergreen은 Besu와 Canton을 경쟁 제품으로만 볼 수 없음을 보여준다. 보고서상 Layer 1의 Hyperledger Besu는 P2P 네트워킹과 ordering consensus를 담당하고, Layer 2의 Canton Domain과 Daml 스마트계약은 토큰화 증권·현금과 업무 로직을 담당했다. 두 계층 모두 해당 프로젝트에서는 private permissioned 방식이었다. [HKMA 보고서](https://www.hkma.gov.hk/media/eng/doc/key-information/press-release/2023/20230824e3a1.pdf)

J.P. Morgan Kinexys는 자체 private permissioned Ethereum/Quorum 계열 플랫폼으로 운영되고 있지만, 최신 공식 자료가 현재 실행 클라이언트를 Besu라고 명시하지 않으므로 Besu 채택 기관 수에는 포함하지 않았다. Kinexys는 누적 3조 달러 이상의 거래를 처리했다고 밝히지만 이는 Besu 또는 Canton의 점유율로 귀속할 수 없다. [J.P. Morgan Kinexys](https://www.jpmorgan.com/kinexys/index)

HSBC Orion 역시 디지털 채권을 실제 발행·결제하는 주요 플랫폼이지만 공개 공식 자료에서 현재 기반 네트워크를 Besu 또는 Canton 중 하나로 단정하기 어려워 본 비교 집계에서 제외했다. [HSBC 디지털자산 소개](https://www.hsbc.com/who-we-are/hsbc-and-digital/hsbc-and-digital-assets-and-currencies)

## 9. 시장점유율 데이터와 한계

### 9.1 Canton에서 관측되는 규모

RWA.xyz의 2026년 7월 22일 Canton 페이지는 다음을 표시한다.

- represented asset value: 약 **3,133억8,000만 달러**
- distributed asset value: 0달러
- 추적 RWA: 1개
- 추적 플랫폼: Broadridge DLR 1개

[RWA.xyz Canton](https://app.rwa.xyz/networks/canton)

같은 데이터 서비스의 네트워크 전체 페이지는 represented asset value 총액을 약 3,594억 달러로 표시한다. 두 페이지의 기준 시점이 완전히 일치하지 않을 수 있지만 단순 비율은 약 87%다. 그러나 이를 ‘Canton의 STO 시장점유율 87%’라고 표현해서는 안 된다. [RWA.xyz Networks](https://app.rwa.xyz/networks)

이유는 다음과 같다.

- Canton 수치가 사실상 Broadridge DLR 한 플랫폼에 집중돼 있다.
- DLR 수치는 주식·채권 STO 발행잔액이 아니라 기관 레포의 represented asset value다.
- private ledger의 모든 거래를 일반 퍼블릭 체인처럼 직접 관측하는 지표가 아니다.
- RWA.xyz의 Canton 데이터는 BETA로 표시된다.

Broadridge는 DLR이 2025년 8월 하루 평균 2,800억 달러, 월 5조9,000억 달러의 레포를 처리했다고 발표했고, 이후 자체 허브에서는 2026년 6월 처리액을 7조5,000억 달러로 제시한다. 이는 Canton의 실제 기관 거래 활용도를 보여주지만 STO 발행 시가총액은 아니다. [Broadridge 2025년 발표](https://www.broadridge.com/press-release/2025/billions-in-average-daily-processed-trade-volumes-on-broadridge-dlt-repo-platform), [Broadridge 토큰화 허브](https://www.broadridge.com/hub/tokenization)

### 9.2 Besu의 점유율을 계산하기 어려운 이유

Besu는 하나의 공유 네트워크가 아니라 소프트웨어다. DTCC, Swift, Fnality 또는 개별 은행이 만든 Besu 기반 네트워크는 서로 다른 원장과 참가자, 자산을 가진다. 대부분 사설망이라 잔액과 거래량을 공개하지 않는다.

따라서 RWA.xyz에 ‘Besu Network’가 없다는 사실은 Besu 사용량이 0이라는 뜻이 아니다. 공개 수치가 없는 Besu 사설망을 Canton의 공개 집계액과 직접 비교하면 Canton의 상대적 비중이 과대평가된다.

### 9.3 DTCC 수치를 시장점유율에 넣을 때의 주의점

DTCC의 전통시장 규모를 토큰화 시장 규모로 간주하면 안 된다. DTCC는 2025년 자회사들이 4.7 quadrillion 달러 규모의 증권 거래를 처리하고 DTC가 약 114조 달러의 증권을 수탁했다고 설명하지만, 이 전체가 Besu나 Canton에서 토큰화된 것이 아니다. [DTCC–Stellar 발표의 회사 현황](https://www.dtcc.com/news/2026/may/27/tokenization-service-to-connect-with-stellar-public-blockchain-as-dtc-advances-multi-chain-strategy)

2026년 7월 실거래 발표도 네트워크별 발행금액, 거래량, 자산 배치를 공개하지 않았다. 따라서 현재 DTCC 물량을 이용해 Besu와 Canton의 점유율을 나눌 수 없다.

## 10. 최종 판정

### 10.1 지표별 결론

| 비교 기준 | 판정 | 근거 |
|---|---|---|
| 공개적으로 관측되는 기관형 토큰화 거래 규모 | **Canton 우위** | Broadridge DLR의 대규모 상용 레포 처리 |
| 토큰증권·채권·MMF·담보 애플리케이션의 공유 생태계 | **Canton 우위** | GS DAP, Broadridge DLR, LSEG DiSH, Tradeweb, DTCC 외부망 연결 |
| 기관 자체 통제형 AppChain 구축 | **Besu 우위 또는 강점** | DTCC AppChain처럼 EVM 호환 사설망 구축에 적합 |
| 토큰화 예금·도매결제·오케스트레이션 | **Besu 강세** | Swift Shared Ledger, Fnality |
| 전체 Besu 배포 규모 | **판정 불가** | 사설망이 분산돼 있고 통합 공시가 없음 |
| DTCC 내 Besu 대 Canton 점유율 | **판정 불가** | 네트워크별 발행·거래 데이터 미공개 |
| 좁은 의미의 STO 발행잔액 | **판정 불가** | 레포·담보·디지털 트윈 수치와 공모·사모 증권 발행잔액을 분리한 공통 통계 부재 |

### 10.2 최종 판단

**현재 기관 선택을 실제 운영 시스템 기준으로 보면 토큰증권·디지털 채권·레포·담보의 외부 공유시장에서는 Canton이 앞서 있다.** 특히 Broadridge DLR의 상용 거래량과 GS DAP, LSEG DiSH, Tradeweb, DTCC의 연결은 네트워크 효과가 형성되고 있음을 보여준다.

**Besu는 뒤처진 단일 네트워크가 아니라 다른 층의 경쟁력을 가진 기반 소프트웨어다.** 기관은 Besu로 자체 통제형 EVM AppChain을 만들 수 있고, Swift와 Fnality처럼 결제·오케스트레이션 인프라에도 채택하고 있다. 사설 배포가 분산돼 있어 시장 규모가 덜 보일 뿐이다.

**DTCC의 전략은 승자독식형 선택이 아니다.** Besu 기반 자체 AppChain을 운영하면서 Canton을 첫 외부 네트워크로, Stellar를 추가 외부 네트워크로 연결하는 프로토콜 중립·멀티체인 전략이다. DTCC Collateral AppChain도 여러 퍼블릭·프라이빗 네트워크에서 발행된 자산을 활용할 수 있는 중간 레이어를 지향한다. [DTCC Collateral AppChain](https://www.dtcc.com/digital-assets/collateral-appchain)

**추론:** 단기적으로는 ‘Canton 대 Besu’보다 **Canton 같은 공유 유동성·애플리케이션 네트워크와 Besu 같은 기관 소유 AppChain이 어떻게 연결되는가**가 더 중요한 경쟁축이 될 가능성이 높다. 기관들은 자산 발행, 현금 결제, 담보 활용, 공식 장부와 규제 책임을 하나의 체인에 모두 집중하기보다 용도별 네트워크를 결합하고 있다.

## 11. 중요한 숫자와 사실

| 항목 | 내용 | 해석상 주의점 |
|---|---|---|
| DTCC 실거래일 | 2026년 7월 15일 | 생산환경 거래를 시작한 날 |
| DTCC 서비스 출시 예정 | 2026년 10월 | 현재 점유율보다 출시 후 상시 잔액·거래량이 중요 |
| DTCC 참여기관 | 공식 보도자료 30곳 이상, 라이브 페이지 약 40곳 | 집계 범위 차이 가능 |
| DTCC 사용 네트워크 | Besu 기반 프라이빗 AppChain, Canton | 네트워크별 물량 미공개 |
| Stellar 지원 예정 | 2027년 상반기 | DTCC의 멀티체인 전략을 뒷받침 |
| Canton represented asset value | 약 3,133억8,000만 달러 | Broadridge DLR 중심이며 STO 발행잔액이 아님 |
| Broadridge DLR | 2026년 6월 약 7조5,000억 달러 처리 | 기간 거래흐름이며 보유자산·시가총액이 아님 |
| Swift Besu 공유원장 | 17개 은행 초기 사용 준비 | 증권 발행이 아니라 토큰화 예금 결제 |
| Kinexys | 누적 3조 달러 이상 처리 | Besu 또는 Canton으로 귀속 불가 |

## 12. 공유용 요약

### 짧은 버전

DTCC는 DTC 보관증권의 디지털 트윈을 Besu 기반 자체 AppChain과 Canton 같은 승인된 외부 네트워크에서 발행·활용하는 멀티체인 구조를 추진하고 있다. “Besu 토큰을 Canton으로 브리지했다”는 근거는 없으며, 두 네트워크에서 각각 디지털 전환과 거래가 이뤄졌다고 보는 것이 정확하다. 현재 공개적으로 관측되는 기관형 토큰증권·레포 생태계는 Broadridge DLR, GS DAP, LSEG DiSH 등이 모인 Canton이 앞선다. 반면 Besu는 DTCC AppChain, Swift, Fnality처럼 기관 자체망과 결제 인프라에서 강하다. 따라서 최종 구조는 한쪽의 승자독식보다 Besu 기반 사설망과 Canton 같은 공유망의 공존에 가깝다.

### 조금 긴 버전

DTCC는 2026년 7월 15일 DTC 보관자산을 토큰화해 담보, 증권대차, 국채·레포 및 주식 결제 등 실제 생산거래를 처리했다. 디지털 전환은 DTCC의 Besu 기반 프라이빗 AppChain과 Canton에서 이뤄졌다. 공개 자료에는 Besu의 동일 토큰을 Canton으로 브리지했다는 설명이 없으며, DTC 자산의 디지털 트윈을 각 승인 네트워크에 발행하는 구조로 보는 것이 타당하다. Besu는 기관이 사설·컨소시엄 네트워크를 만드는 오픈소스 EVM 클라이언트이고, Canton은 애플리케이션별 권한과 거래 프라이버시를 유지하는 public-permissioned 공유 네트워크다. Besu로도 외부기관 컨소시엄을 만들 수 있지만 Canton에는 이미 거래, 레포, 담보, 현금 애플리케이션과 독립 기관이 연결돼 있다는 차이가 있다. 기관 채택 사례를 보면 Broadridge DLR, Goldman Sachs GS DAP, BNY, LSEG DiSH, Tradeweb 등 토큰증권·담보 생태계는 Canton 쪽이 더 강하다. Besu는 DTCC Collateral AppChain, Swift 공유원장, Fnality 같은 기관 통제형 결제·오케스트레이션 분야에서 강점을 보인다. RWA.xyz가 Canton에서 약 3,134억 달러를 집계하지만 거의 전부 Broadridge DLR의 represented asset value이므로 STO 발행점유율로 해석하면 안 된다. Besu는 사설 배포가 분산돼 통합 거래량을 관측할 수 없다. 현재 결론은 Canton이 외부 공유시장 활동에서 우세하지만, 전체 Besu 대 Canton 점유율이나 DTCC 내부 네트워크별 비중은 공개 자료로 판정할 수 없다는 것이다.

## 13. 시사점

- **투자자:** Canton의 큰 거래액은 기관 채택 신호지만 STO 시가총액이나 네트워크 수익과 동일하지 않다. 거래흐름, 자산잔액, 수수료, 토큰 가치포착을 분리해야 한다.
- **창업자/빌더:** 기관 고객에게는 EVM 호환성만큼 공식 장부 연계, 프라이버시, 권한관리, 강제이전·동결, 기업행위, 멀티체인 조정 기능이 중요하다.
- **기업/금융사:** 자체 통제망이 필요한 업무는 Besu AppChain, 외부 자산·거래·현금 생태계 접근은 Canton 같은 공유망이라는 이중 전략을 검토할 수 있다.
- **정책/규제 담당자:** 디지털 트윈의 법적 권리, 공식 장부 우선순위, 네트워크 간 중복발행 방지, 장애·포크 시 복구, 개인정보와 감독기관 접근권한을 명확히 해야 한다.

## 14. 더 생각해볼 질문

1. 2026년 10월 출시 후 DTCC는 네트워크별 발행잔액과 거래량을 공개할 것인가?
2. 동일 DTC 포지션이 여러 네트워크에 걸쳐 이동할 때 소각·재발행과 중복방지는 어떻게 수행되는가?
3. DTC 공식 장부, ComposerX LedgerScan, 각 네트워크 상태가 불일치할 때 어떤 기록이 법적 우선권을 갖는가?
4. Canton의 대규모 레포 흐름이 실제 네트워크 수수료·유동성·토큰증권 2차시장으로 얼마나 연결되는가?
5. Besu 기반 Swift·Fnality 결제자산이 Canton의 증권·담보 애플리케이션과 어떤 방식으로 원자적 결제를 구현할 것인가?
6. Stellar 추가 이후 DTCC는 네트워크를 어떤 기술·규제·유동성 기준으로 승인할 것인가?
7. 기관형 토큰화 시장의 경쟁 단위는 블록체인 자체인가, 아니면 자산·현금·장부·규제를 연결하는 서비스 계층인가?

## 15. 출처 목록

### DTCC·규제

- [DTCC — U.S. Trades Successfully Processed Using DTC-Tokenized Assets](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality)
- [DTCC — Tokenization Service와 지원 네트워크](https://www.dtcc.com/digital-assets/tokenization)
- [DTCC — Tokenization Live Production Trades](https://www.dtcc.com/digital-assets/tokenization/live-production-trades)
- [DTCC — Canton 파트너십](https://www.dtcc.com/news/2025/december/17/dtcc-and-digital-asset-partner-to-tokenize-dtc-custodied-us-treasury-securities)
- [DTCC — Stellar 연결 계획](https://www.dtcc.com/news/2026/may/27/tokenization-service-to-connect-with-stellar-public-blockchain-as-dtc-advances-multi-chain-strategy)
- [DTCC — Collateral AppChain](https://www.dtcc.com/digital-assets/collateral-appchain)
- [SEC — DTC 토큰화 비조치 의견 관련 성명](https://www.sec.gov/newsroom/speeches-statements/peirce-121125-tokenization-trending-statement-division-trading-markets-no-action-letter-related-dtcs-development)
- [SEC — DTC No-Action Letter](https://www.sec.gov/files/tm/no-action/dtc-nal-121125.pdf)

### 기술·네트워크

- [LFDT — 출범과 Besu 명칭 변경](https://www.lfdecentralizedtrust.org/announcements/linux-foundation-decentralized-trust-launches-with-17-projects-100-founding-members)
- [LFDT — Besu](https://www.lfdecentralizedtrust.org/projects/besu)
- [Canton — FAQ](https://www.canton.network/faq)
- [Canton — 공식 기술 문서](https://docs.canton.network/overview/understand/what-is-canton)
- [Canton — 백서](https://www.canton.network/hubfs/Canton/Canton%20Network%20-%20White%20Paper.pdf)
- [HKMA — Project Evergreen 토큰화 채권 보고서](https://www.hkma.gov.hk/media/eng/doc/key-information/press-release/2023/20230824e3a1.pdf)

### 기관 채택·시장 데이터

- [Broadridge — DLR 거래규모](https://www.broadridge.com/press-release/2025/billions-in-average-daily-processed-trade-volumes-on-broadridge-dlt-repo-platform)
- [Broadridge — Tokenization Hub](https://www.broadridge.com/hub/tokenization)
- [Goldman Sachs·BNY — 토큰화 MMF](https://www.goldmansachs.com/pressroom/press-releases/2025/bny-goldman-sachs-launch-tokenized-money-market-funds-solution)
- [BNY — LiquidityDirect와 GS DAP](https://www.bny.com/corporate/global/en/about-us/newsroom/company-news/bny-and-goldman-sachs-launch-tokenized-money-market-funds-solution.html)
- [LSEG — Digital Settlement House](https://www.lseg.com/en/media-centre/press-releases/2026/lseg-launches-digital-settlement-house)
- [Swift — Besu 기반 Shared Ledger](https://www.swift.com/news-events/news/swifts-blockchain-based-shared-ledger-progresses-mvp-implementation)
- [Swift — 17개 은행 초기 사용](https://www.swift.com/news-events/press-releases/swifts-blockchain-ledger-ready-use-17-banks-set-pioneer-tokenised-cross-border-payments-trusted-global-infrastructure)
- [Fnality — Payment Systems](https://fnality.com/home)
- [RWA.xyz — Canton](https://app.rwa.xyz/networks/canton)
- [RWA.xyz — Networks](https://app.rwa.xyz/networks)
- [Digital Asset — Canton 미국 국채 금융](https://blog.digitalasset.com/press-release/digital-asset-and-industry-working-group-complete-groundbreaking-on-chain-us-treasury-financing-on-canton-network)
- [Digital Asset — 후속 온체인 담보 재사용](https://blog.digitalasset.com/press-release/the-canton-networks-industry-working-group-demonstrates-next-phase-of-onchain-u.s.-treasury-financing-on-canton-network)
