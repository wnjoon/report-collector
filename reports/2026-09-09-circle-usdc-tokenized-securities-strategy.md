# Circle 미팅 후속 전략: MKRW·USDC·Besu·Canton을 어떻게 연결할 것인가

- 기준일: 2026-09-09
- 출처: Circle 미팅 녹취록 및 화이트보드 사진, Circle 공식 문서, 금융위원회 공식 발표
- 작성자: 미상(회의 분석 및 전략 제안)
- 원문: [Circle Bridged USDC Standard](https://www.circle.com/bridged-usdc)

> 주의: 회의록은 자동 전사본으로 보이며 `Besu`, `Canton`, `CCTP`, `xReserve`, `MKRW` 등이 일부 잘못 표기되어 있다. 아래에서는 문맥에 따라 용어를 정규화했다. 법률·규제 판단은 별도 법률검토가 필요하다.

## 1. 한 줄 요약

지금은 프라이빗 Besu용 “USDC 인프라”를 크게 구축할 때가 아니라, **2027년 국내 토큰증권 1단계에 맞는 기관전용 MMF·사채 DvP 시나리오를 정하고, 공개체인의 네이티브 USDC를 담보로 한 bridged USDC를 Besu에 넣는 최소 PoC로 규제·운영 가능성을 먼저 검증할 때**다.

## 2. 핵심 메시지 3개

- **문제의 핵심은 기술이 아니라 법적 경계와 사업 목적이다.** Circle 측은 회의 내내 “왜 프라이빗 네트워크여야 하는가”, “MKRW의 법적·회계적 성격은 무엇인가”, “공개체인 참여는 왜 허용되는가”를 확인하려 했다. 이 질문에 답하지 못하면 어떤 구조를 택해도 PoC 이후로 진전하기 어렵다.
- **단기 권고안은 `native USDC → lock → Besu의 bridged USDC → burn/unlock` 구조다.** Circle이 제공한 Bridged USDC Standard는 EVM 체인에서 초기 유동성을 만들고 장래 native 전환 가능성을 남기는 규격이다. 다만 bridged USDC는 Circle 발행물이 아니고, CCTP와 호환되지 않으며, 향후 native 전환도 Circle의 의무가 아니다.
- **장기 구조는 public-first로 열어 두되 Arc·StableFX를 현재 전제로 삼으면 안 된다.** 2026-09-09 현재 Circle Mint와 CCTP 문서에서 Arc는 testnet/sandbox로 표시되고, StableFX가 명시적으로 지원하는 것은 USDC·EURC이며 로컬 스테이블코인은 향후 확대 대상이다. MKRW/StableFX와 Arc 메인넷을 생산환경 전제로 잡는 것은 시기상조다.

## 3. 회의에서 확인된 목표와 쟁점

### 우리가 제시한 목표

- 한국의 프라이빗 Besu 네트워크에서 MKRW를 발행·관리한다.
- USDC를 결제자산으로 사용해 국내외 토큰화 증권을 거래한다.
- 한국 자산을 해외에서 거래하거나, 반대로 해외 자산을 한국으로 들여와 거래한다.
- Canton 등 외부 네트워크와 연계해 단일 네트워크 종속을 피한다.
- 장기적으로 공개체인과 StableFX를 통한 MKRW/USDC 환전 및 결제를 검토한다.

### Circle이 반복해서 제기한 질문

- MKRW는 예금토큰, 스테이블코인, 증권사 내부 장부상의 청구권 중 무엇인가?
- 1:1 원화 담보는 어느 법인·어느 계정에 있고, 누가 상환의무를 지는가?
- 한국 규제가 금지하는 것은 “공개체인 보유”인지, “국내 발행·유통”인지, “외환·가상자산 거래”인지?
- 공개체인 또는 Canton에서 거래가 가능하다면 프라이빗 Besu에 USDC를 별도로 둘 실익은 무엇인가?
- PoC가 단기 규제 설명용이라면 xReserve 수준의 인프라를 새로 구축할 경제성이 있는가?

### 회의에서 도출된 실질적 합의

1. USDC의 원천은 공개체인이다. 미래에셋 뉴욕 법인 등이 USD를 Circle Mint를 통해 네이티브 USDC로 전환하는 흐름이 제시됐다.
2. 공개체인의 USDC를 브리지 계약에 잠그고, 동일 수량의 bridged USDC를 Besu에서 발행한다.
3. Besu 내부에서 MKRW와 bridged USDC를 교환하거나 토큰증권 DvP(증권과 대금의 동시결제)에 사용한다.
4. 외부 이동 시 Besu의 bridged USDC를 소각하고 공개체인의 네이티브 USDC를 해제한다.
5. Canton으로 갈 때는 Besu에서 Canton으로 직접 이동시키기보다, 공개체인으로 되돌린 뒤 Circle의 공식 경로를 이용한다.

화이트보드 사진도 `Mirae New York → USD → Circle Mint → USDC → bridge → Besu`와 `Canton/USDCx`를 분리해서 그린 것으로 보이며 이 해석을 뒷받침한다.

## 4. 현재 공식 자료가 바꾼 판단

### Bridged USDC Standard의 의미와 한계

Circle의 [Bridged USDC Standard](https://www.circle.com/bridged-usdc)는 제3자가 EVM 체인에 bridged USDC를 배포하고, 다른 체인에 잠긴 USDC로 이를 뒷받침하는 방식이다. 표준을 처음부터 적용하면 장래 Circle이 계약 소유권을 넘겨받아 native USDC로 전환할 선택지가 생긴다.

그러나 다음 한계를 전제로 해야 한다.

- bridged USDC는 Circle이 발행한 네이티브 USDC가 아니다.
- 브리지 운영·보안·상환 책임은 기본적으로 제3자 구조에 남는다.
- CCTP와 호환되지 않는다.
- Circle은 native 전환 의무가 없고, 전환 판단 시 법률·규제·기술·운영·전략 실사를 한다.
- 기존 계약에 사후적으로 표준을 적용할 수 없으므로 첫 배포부터 표준 준수가 필요하다.
- Circle Mint는 bridged USDC 입금을 지원하지 않는다고 명시하므로, 반드시 burn/unlock을 거쳐 지원 체인의 네이티브 USDC로 복귀해야 한다.

따라서 이 표준은 **규제기관에 end-to-end 흐름을 보여주는 Besu PoC의 현실적 도구**이지, 곧바로 Circle 보증 상품이나 장기 상용 아키텍처가 되는 것은 아니다.

### xReserve와 Canton은 이미 상용 경로가 생겼다

Circle의 [xReserve](https://developers.circle.com/xreserve)는 공개체인에 USDC를 보관하고 원격 체인에서 1:1 USDC-backed stablecoin을 발행하는 구조다. 현재 [지원 네트워크 문서](https://developers.circle.com/xreserve/references/supported-blockchains-and-domains)에는 Ethereum이 메인넷 source chain, Canton이 메인넷 remote chain이며 Canton의 자산은 `USDCx`로 기재되어 있다.

이는 회의 당시의 불확실성을 일부 해소한다. Canton 유동성은 별도 자체 브리지보다 공식 xReserve 경로를 우선 검토하는 것이 맞다. 반면 Besu는 현재 공개된 xReserve remote chain 목록에 없다. 따라서 `Besu ↔ xReserve`는 일반 개발자가 바로 붙이는 기능이 아니라 **Circle과의 파트너 온보딩·실사 가능성을 먼저 확인해야 하는 별도 트랙**이다.

### CCTP는 Besu 또는 bridged USDC의 이동수단이 아니다

[CCTP 지원 체인](https://developers.circle.com/cctp/concepts/supported-chains-and-domains)은 네이티브 USDC가 발행된 지원 네트워크들이다. 프라이빗 Besu는 목록에 없고 Bridged USDC Standard 페이지도 bridged USDC는 CCTP 비호환이라고 명시한다.

그러므로 `Besu bridged USDC → CCTP → Canton`으로 이해하면 안 된다. 실제 경로는 다음과 같다.

`Besu bridged USDC burn → 공개체인 native USDC unlock → xReserve deposit → Canton USDCx mint`

### Arc·StableFX는 미래 옵션이다

[StableFX](https://developers.circle.com/stablefx)는 Arc 기반의 기관용 RFQ·온체인 PvP 결제 엔진이다. 공개 문서상 현재 지원 자산은 USDC·EURC이고 로컬 스테이블코인은 확대 예정이다. 또한 [Circle Mint 지원 체인 문서](https://developers.circle.com/circle-mint/references/supported-chains-and-currencies)는 Arc를 sandbox/testnet 전용으로 표시한다.

따라서 회의에서 언급된 `MKRW ↔ USDC on StableFX`는 제품 로드맵 후보이지 현재 사용 가능한 확정 기능이 아니다. Circle과 maker 온보딩, MKRW 상장 기준, Arc 메인넷 일정, 프라이버시 기능의 상용 SLA를 별도로 확인해야 한다.

### 한국 정책은 “MMF 우선, 스테이블코인 결제는 후순위”를 말한다

금융위원회의 [2026-09-04 토큰증권 정책방향](https://www.fsc.go.kr/no010101/87650)은 2027년 2월 1단계에서 기관투자자 전용 사모 MMF·사채와 비상장주식 신탁방식 토큰화를 우선 추진하고, 스테이블코인 기반 온체인 결제는 3단계로 배치했다. 3단계 시점은 1단계 안정성, 시장의 기술혁신, 스테이블코인 법제화 등에 따라 가변적이라고 밝혔다. 서로 다른 토큰증권 원장과 스테이블코인 원장의 연계도 브리지 기관 또는 메인넷 연계 방식으로 추가 실증 검토할 과제로 명시했다.

이 정책은 두 가지를 의미한다.

- **긍정적:** 기관전용 사모 MMF는 당장 제도 로드맵과 가장 잘 맞는 첫 상품이다.
- **제약:** USDC/MKRW를 실제 결제수단으로 상용화하는 것은 1단계 출시 범위로 단정할 수 없다. 당분간은 기술검증·규제협의·샌드박스 성격으로 설계해야 한다.

## 5. 권고 아키텍처

### 단기 PoC: 두 원장을 분리하고, 공개체인을 필수 앵커로 둔다

```text
[한국 / permissioned Besu]
토큰증권 + MKRW + bridged-USDC + DvP
                │
          burn / mint bridge
                │
[공개체인 / native USDC]
Circle Mint 자금화 + reserve lock/unlock
                │
          xReserve (공식 경로)
                │
[Canton / USDCx]
해외 토큰화 자산 결제·유동성
```

핵심 설계 원칙은 다음과 같다.

- Besu의 토큰은 네이티브 USDC처럼 표시하지 말고 `bridged USDC`임을 명확히 한다.
- 브리지 준비금은 공개체인에서 100% 온체인 검증 가능하게 한다.
- mint/burn, pause, blacklist, allowlist, recovery 권한을 분리하고 다중승인·감사로그를 둔다.
- Besu와 Canton을 직접 연결하지 않는다. 네이티브 USDC로 돌아오는 공개체인 경계를 공통 허브로 둔다.
- 거래자산과 결제자산 원장을 분리하되 DvP의 원자성, 실패·롤백, 결제완결성 규칙을 명시한다.
- 환율은 스마트컨트랙트가 “보장”하는 것이 아니다. 가격제공자, 유동성공급자, 체결주체, 손실부담 주체를 계약상 분리한다.

### 첫 상품: 상장주식보다 기관전용 사모 MMF 또는 사모사채

회의에서는 SK하이닉스·삼성전자 등 한국 주식을 해외에서 거래하는 비전이 언급됐지만, 현재 정책의 1단계와는 거리가 있다. 첫 PoC는 다음 순서가 더 현실적이다.

1. 기관전용 사모 MMF 토큰 또는 사모사채
2. Besu 내부에서 제한된 참여자 간 발행·양도·상환
3. MKRW와 bridged USDC를 각각 사용한 DvP 비교
4. USDC 결제는 실제 상용화가 아니라 규제기관 관찰 하의 제한된 테스트
5. 동일 USDC 유동성을 공개체인으로 복귀시킨 후 Canton USDCx 경로 시연

이렇게 하면 국내 정책의 첫 허용 상품, Circle의 실제 제품, 회사의 장기 국제 유통 비전을 한 번에 연결할 수 있다.

## 6. 선택지 비교

| 선택지 | 장점 | 핵심 한계 | 권고 |
|---|---|---|---|
| Besu에 Bridged USDC Standard 적용 | 가장 빠른 EVM PoC, 온체인 준비금 증명, 장래 전환 옵션 | Circle 발행물이 아님, 브리지 책임, CCTP 비호환, native 전환 미보장 | **단기 PoC 1순위** |
| Besu를 xReserve remote chain으로 온보딩 | Circle attestation, USDC 네트워크와 1:1 상호운용, 장기 구조에 유리 | 공개 지원 대상 아님, 파트너 심사·개발·운영비용, 일정 불명 | **Circle 사전승인 후 2단계** |
| Canton USDCx 직접 활용 | 이미 메인넷 지원, Circle 공식 경로, 해외 자산 결제에 적합 | 한국 Besu의 MKRW/토큰증권과 직접 연결되지 않음 | **해외 레그 우선 채택** |
| Arc + StableFX | 기관용 RFQ/PvP, 향후 MKRW 마켓메이킹 잠재력 | Arc가 현재 testnet/sandbox, MKRW 미지원, 한국 규제 3단계 사안 | **옵션 보존, 생산 의존 금지** |
| 프라이빗 Besu에 별도 native-like USDC 구축 | 국내 통제와 폐쇄형 운영 | 실익 불명확, Circle 규제·감사 모델과 충돌, 중복 인프라 | **권고하지 않음** |

## 7. 실행 로드맵

### Gate 0 — 2~4주: 규제·사업 정의

코드를 만들기 전에 5쪽 이내의 “규제 경계 메모”를 확정한다.

- MKRW 법적 성격, 1:1 준비자산, 상환청구권, 도산절연, 회계처리
- 미래에셋 한국·뉴욕, Circle, 하나금융 등 각 법인의 역할
- USD→USDC, USDC→MKRW가 외환거래·가상자산거래·증권결제 중 어디에 해당하는지
- 한국 거주자/비거주자, 기관/개인별 허용 범위
- 공개체인 USDC 보유와 프라이빗 원장상 표현의 규제 차이
- 토큰증권 원장과 결제 원장의 결제완결성 및 원장 간 불일치 처리

**통과 기준:** 준법·법무·재무가 동일한 자금 흐름도에 서명하고, 규제기관에 설명할 문장이 하나로 통일돼야 한다.

### Gate 1 — 4~6주: Circle의 서면 확인

아래 질문에 서면 답변을 받는다.

1. Bridged USDC Standard를 permissioned Besu에 적용할 수 있는가?
2. Circle은 해당 구조에서 토큰 명칭·심볼·브랜딩을 어떻게 요구하는가?
3. 장래 native 전환 대상에 permissioned chain도 포함될 수 있는가? 실사 기준은 무엇인가?
4. Besu를 xReserve remote chain으로 온보딩할 수 있는가? 최소 거래량, 비용, 기간, 운영 SLA는?
5. 미래에셋 뉴욕의 Circle Mint 계정이 reserve origin 및 회수 창구가 될 수 있는가?
6. Besu에서 burn 후 Ethereum native USDC를 해제하고 Canton USDCx로 전환하는 공식 권고 흐름은?
7. remote-chain 간 USDC-backed stablecoin 이동 시 적용 수수료·한도·완결성·장애처리는?
8. StableFX에 MKRW를 추가하고 미래에셋이 maker가 되기 위한 법적·기술적 조건은?
9. Arc 메인넷 및 기관 프라이버시 기능의 상용 일정과 보장 범위는?
10. Circle이 PoC 코드·브리지 감사를 지원하거나 승인한다는 표현을 사용할 수 있는가?

**통과 기준:** `Circle 제공 기능`, `미래에셋 책임`, `제3자 브리지 책임`이 계약·발표자료에서 분리되어야 한다.

### Gate 2 — 6~10주: 제한된 PoC

- 자산: 기관전용 사모 MMF 또는 사모사채 1종
- 참여자: 허가된 기관 2~3곳
- 네트워크: Besu 테스트 환경 + 공개 테스트넷 + Canton TestNet
- 기능: KYC allowlist, 발행·양도·상환, MKRW/bridged USDC DvP, bridge mint/burn, 준비금 조회, 비상정지
- 테스트: 이중발행, replay, 원장 reorg/지연, bridge 장애, 키 분실, sanctions/blacklist, 잔액 불일치, 환율 급변

**성공 지표:**

- 모든 bridged USDC가 공개체인 준비금과 1:1로 대사된다.
- DvP는 한쪽만 결제되는 상태를 만들지 않는다.
- mint/burn부터 최종 결제까지 추적 가능한 단일 감사 trail이 생성된다.
- 장애 시 자금 손실 없이 정지·복구·수동조정이 가능하다.
- 규제기관이 온쇼어/오프쇼어 경계와 각 주체의 책임을 설명받고 재현할 수 있다.

### Gate 3 — 2027년 이후: 상용화 판단

- 국내 1단계 제도 시행과 예탁원 연계 요건을 충족하면 MMF/사채부터 상용 검토
- Circle이 Besu xReserve 온보딩을 수용하면 자체 브리지에서 공식 구조로 전환 검토
- 공개체인 사용이 허용되고 Arc 메인넷·StableFX MKRW 지원이 확정될 때만 public MKRW와 FX 마켓메이킹 추진
- 상장주식·해외 개인투자자 유통은 별도 시장구조·권리관리·외환규제 트랙으로 분리

## 8. 중단 조건과 주요 리스크

- **법적 성격 불명확:** MKRW가 상환 가능한 결제수단인지 내부 정산용 토큰인지 정의되지 않으면 중단한다.
- **브랜드 오인:** bridged USDC를 Circle 발행·보증 자산처럼 표시해야만 사업성이 성립한다면 중단한다.
- **운영주체 부재:** 브리지 키, attester, 준비금 지갑, 상환창구의 24/7 운영 책임자를 정하지 못하면 중단한다.
- **한 방향 유동성:** 한국→해외만 설계하고 환매·회수·장애 시 reverse path가 완성되지 않으면 중단한다.
- **규제 목적 없는 프라이빗 체인:** “정부가 원할 것 같다” 외에 폐쇄망의 명확한 통제·감사·참여자 보호 이점이 없으면 Besu 전용 USDC 투자를 확대하지 않는다.
- **Arc 선행 의존:** Arc 메인넷이나 MKRW StableFX 지원이 지연돼도 핵심 PoC가 동작하도록 한다.

## 9. 중요한 사실과 판단

| 항목 | 확인된 사실 | 전략적 의미 |
|---|---|---|
| Bridged USDC | 제3자 발행, 다른 체인의 USDC가 담보 | Circle 신용이 아니라 브리지 구조의 위험을 별도 관리 |
| CCTP | bridged USDC와 비호환 | Besu에서 직접 CCTP 사용 불가 |
| Circle Mint | bridged USDC 입금 미지원 | 반드시 native USDC로 복귀 후 입금 |
| xReserve | Ethereum 메인넷 source, Canton 메인넷 remote 지원 | Canton은 공식 USDCx 경로 우선 |
| Besu | 공개 xReserve 지원 목록에 없음 | 파트너 온보딩 여부를 먼저 확인 |
| Arc | Circle Mint상 sandbox/testnet | 당장 생산 의존 불가 |
| StableFX | 현재 USDC·EURC, 로컬 스테이블코인은 확대 예정 | MKRW 지원을 확정 사실로 전제하지 말 것 |
| 한국 토큰증권 1단계 | 2027년 2월 기관전용 사모 MMF·사채 우선 | 첫 상품을 MMF/사채로 좁힐 근거 |
| 스테이블코인 온체인 결제 | 정책상 3단계, 시점 가변 | PoC와 상용화를 분리해야 함 |

## 10. 공유용 요약

### 짧은 버전

Circle 미팅의 결론은 프라이빗 Besu에 큰 USDC 인프라를 먼저 만들지 말고, 공개체인 USDC를 잠가 Besu에서 bridged USDC로 쓰는 최소 PoC부터 하자는 것입니다. 현재 공식 문서상 Canton에는 xReserve 기반 USDCx가 이미 있으므로 Canton 레그는 이를 우선 사용해야 합니다. 한국의 2026년 9월 정책도 2027년 1단계에서 기관전용 사모 MMF·사채를 먼저 허용하고 스테이블코인 결제는 후속 단계로 두고 있습니다. 따라서 첫 상품은 상장주식이 아니라 기관 MMF/사채, 첫 과제는 개발이 아니라 MKRW와 온쇼어–오프쇼어 법적 구조 확정입니다.

### 조금 긴 버전

Circle은 기술적으로 프라이빗 Besu에 USDC 유사 토큰을 넣는 것은 가능하지만, 단기 규제 설명용이라면 xReserve급 인프라는 과도하다고 봤습니다. 제안된 현실적 흐름은 미래에셋 뉴욕 등이 Circle Mint로 공개체인 USDC를 확보하고, 이를 잠근 뒤 Besu에서 bridged USDC를 발행해 MKRW 또는 토큰증권과 DvP하는 구조입니다. 회수 시에는 Besu 토큰을 소각하고 공개체인 USDC를 해제합니다. Canton으로 이동할 때는 Besu에서 직접 연결하지 않고, 공개체인으로 돌아온 뒤 xReserve를 통해 Canton USDCx를 사용하는 것이 공식 제품 구조에 맞습니다. Bridged USDC는 Circle 발행물이 아니며 CCTP와 호환되지 않고 native 전환도 보장되지 않는다는 점을 명확히 해야 합니다. 2026년 9월 현재 Arc는 Circle 문서상 testnet/sandbox이고 StableFX의 명시 지원 자산은 USDC·EURC이므로 MKRW/StableFX를 당장 전제로 삼으면 안 됩니다. 국내 정책은 2027년 2월 기관전용 사모 MMF·사채를 우선 토큰화하고 스테이블코인 결제는 3단계로 미뤘습니다. 따라서 향후 2~4주는 MKRW의 법적 성격, 준비금, 상환권, 외환·가상자산·증권결제 규제를 정리하고 Circle의 서면 확인을 받는 데 써야 합니다. 그 후 기관 MMF/사채 한 종목과 소수 참여자를 대상으로 bridge, DvP, 준비금 대사, 장애복구를 검증하는 제한된 PoC를 진행하는 것이 가장 합리적입니다.

## 11. 시사점

- **경영진:** “프라이빗 USDC 구축”이 아니라 “2027년 기관 토큰증권 결제 인프라 옵션 확보”로 투자 목적을 재정의해야 한다.
- **사업팀:** 해외 상장주식보다 기관전용 MMF·사모사채 또는 해외 토큰화 MMF의 국내 유통 시나리오를 먼저 구체화해야 한다.
- **개발팀:** Besu 직접-Canton 연결을 피하고, native USDC를 공통 허브로 둔 adapter 구조와 교체 가능한 브리지 인터페이스를 설계해야 한다.
- **법무·준법:** MKRW의 청구권과 준비금, 해외법인 역할, 외환·가상자산·증권결제 경계를 하나의 자금흐름도로 확정해야 한다.
- **규제대응:** 스테이블코인 상용 결제 허용을 전제로 설명하지 말고, 제3단계 정책과 연계한 제한적 실증으로 제시해야 한다.

## 12. 더 생각해볼 질문

1. 고객이 해결하고 싶은 실제 문제는 국내 토큰증권 결제인가, 해외 자산 접근인가, 환전 비용 절감인가?
2. MKRW는 누구에게 언제 원화 상환청구권을 주며 준비자산은 도산절연되는가?
3. 프라이빗 Besu가 제공해야 할 통제는 참여자 허가, 거래 가시성, 자산 동결, 규제기관 조회 중 무엇인가?
4. bridged USDC의 bridge operator가 파산하거나 키가 탈취됐을 때 누가 손실을 부담하는가?
5. 첫 PoC의 성공이 규제 승인, 비용 절감, 결제시간 단축, 신규상품 출시 중 어느 KPI로 측정되는가?

## 최종 권고

**권고안은 `규제·사업 정의 → Circle 서면 확인 → Besu bridged-USDC 최소 PoC → Canton USDCx 연계 → 제도 변화 후 xReserve/Arc/StableFX 확대`의 순서다.**

지금 승인할 예산은 대규모 상용 인프라가 아니라 Gate 0~2까지다. 특히 첫 상품을 기관전용 사모 MMF 또는 사모사채로 좁히고, Arc와 StableFX는 인터페이스만 열어 둔 미래 옵션으로 관리하는 것이 가장 낮은 비용으로 가장 많은 규제·기술 불확실성을 해소한다.
