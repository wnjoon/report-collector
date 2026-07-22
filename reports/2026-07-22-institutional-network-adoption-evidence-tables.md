# Besu·Canton 기관 채택 근거 분류표

- 작성일: 2026-07-22
- 목적: 기관의 네트워크 채택, 실제 거래 참여, 생태계 참여를 구분해 공신력과 해석 범위를 검토
- 관련 리포트: `2026-07-22-dtcc-tokenization-besu-canton-market-adoption.md`

아래처럼 나누면 “네트워크 채택”, “거래 참여”, “생태계 참여”가 섞이지 않는다.

근거 등급은 다음과 같다.

- **A:** 기관·플랫폼 운영사의 공식 발표
- **B:** 네트워크·기술 제공사 또는 공식 파트너 발표
- **보류:** 현재 운영사의 최신 공식 자료로 기술 기반을 확인하기 어려움

## 1. 기반 네트워크가 공식적으로 확인된 플랫폼·프로젝트

이 표만이 기관의 기술 선택을 비교하는 핵심 근거로 사용될 수 있다.

| 운영기관·플랫폼 | 확인된 네트워크 | 상태·용도 | 근거 수준 | 출처 |
|---|---|---|---|---|
| DTCC Tokenization Service | DTCC AppChain(Besu) + Canton | DTC 보관증권 디지털 트윈, 2026년 7월 생산거래 | A | [DTCC 실거래 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality), [지원 네트워크](https://www.dtcc.com/digital-assets/tokenization) |
| DTCC Collateral AppChain | Besu 기반 DTCC AppChain | 멀티자산 담보 관리, 생산 전환 단계 | A | [DTCC Collateral AppChain](https://www.dtcc.com/digital-assets/collateral-appchain), [DTCC 지원 네트워크](https://www.dtcc.com/digital-assets/tokenization) |
| Broadridge DLR | Canton | 상용 기관 레포·토큰화 담보 플랫폼 | A | [Broadridge의 Canton 이전 설명](https://www.broadridge.com/article/capital-markets/dlr-transacts-1-trillion-a-month), [거래량 발표](https://www.broadridge.com/press-release/2025/billions-in-average-daily-processed-trade-volumes-on-broadridge-dlt-repo-platform) |
| LSEG DiSH | Canton | 토큰화 은행예금·결제 시스템 | A | [LSEG 공식 발표](https://www.lseg.com/en/media-centre/press-releases/2026/lseg-launches-digital-settlement-house) |
| Swift Shared Ledger | Hyperledger Besu | 토큰화 예금 기반 국경 간 결제·오케스트레이션 | A | [Swift 기술 발표](https://www.swift.com/news-events/news/swifts-blockchain-based-shared-ledger-progresses-mvp-implementation), [초기 사용 발표](https://www.swift.com/news-events/press-releases/swifts-blockchain-ledger-ready-use-17-banks-set-pioneer-tokenised-cross-border-payments-trusted-global-infrastructure) |
| HKMA Project Evergreen | Besu Layer 1 + Canton/Daml Layer 2 | 2023년 홍콩 정부 토큰화 녹색채권 발행·결제 | A | [HKMA 공식 보고서](https://www.hkma.gov.hk/media/eng/doc/key-information/press-release/2023/20230824e3a1.pdf) |
| Goldman Sachs GS DAP | Canton/Daml 생태계 | 디지털 채권·MMF 미러 토큰 플랫폼 | B | [Goldman Sachs·BNY 발표](https://www.goldmansachs.com/pressroom/press-releases/2025/bny-goldman-sachs-launch-tokenized-money-market-funds-solution), [Canton FAQ](https://www.canton.network/faq) |

주의할 점:

- GS DAP은 Goldman Sachs 공식 자료에서 Digital Asset 기술을 활용한다고 확인된다.
- 하지만 “GS DAP이 Canton에서 운영된다”는 직접적인 분류는 Canton 측 자료가 더 명확하므로 근거 등급을 B로 두는 것이 안전하다.
- HKMA Project Evergreen은 지속 운영 플랫폼이 아니라 완료된 발행 프로젝트이므로 별도 표시해야 한다.

## 2. 특정 네트워크·플랫폼에서 실제 거래·발행에 참여한 기관

이 표는 실제 사용 경험을 보여주지만, 해당 기관이 그 네트워크를 전략적 표준으로 채택했다는 뜻은 아니다.

| 거래·프로젝트 | 참여 기관 | 사용 환경 | 확인되는 사실 | 출처 |
|---|---|---|---|---|
| DTCC 2026년 7월 생산거래 | BlackRock, BNP Paribas Securities, Circle, Citadel Securities, CME, Goldman Sachs, J.P. Morgan, Nasdaq, NYSE, State Street, Vanguard, Virtu 등 30곳 이상 | Besu + Canton | 기관들이 DTCC 토큰화 거래에 참여. 단, 기관별 사용 네트워크는 미공개 | [DTCC 공식 발표](https://www.dtcc.com/news/2026/july/15/dtcc-turns-tokenization-into-reality) |
| Canton 미국 국채 온체인 금융 | Bank of America, Circle, Citadel Securities, Cumberland DRW, Digital Asset, DTCC, Hidden Road, Société Générale, Tradeweb, Virtu | Canton | 온체인 국채와 USDC를 이용한 실제 금융·결제 수행 | [Digital Asset 공식 발표](https://blog.digitalasset.com/press-release/digital-asset-and-industry-working-group-complete-groundbreaking-on-chain-us-treasury-financing-on-canton-network) |
| Canton 후속 국채 레포·담보 재사용 | Bank of America, Brale, Circle, Citadel Securities, Cumberland DRW, Digital Asset, M1X Global, Société Générale, Tradeweb, Virtu | Canton | 실시간 담보 재사용 및 후속 온체인 레포 수행 | [Digital Asset 후속 발표](https://blog.digitalasset.com/press-release/the-canton-networks-industry-working-group-demonstrates-next-phase-of-onchain-u.s.-treasury-financing-on-canton-network) |
| BNY·GS DAP 토큰화 MMF | BlackRock, BNY Investments Dreyfus, Federated Hermes, Fidelity Investments, Goldman Sachs Asset Management | GS DAP | MMF 지분의 미러 토큰화 초기 출시에 참여 | [BNY 공식 발표](https://www.bny.com/corporate/global/en/about-us/newsroom/company-news/bny-and-goldman-sachs-launch-tokenized-money-market-funds-solution.html) |
| HKMA 토큰화 녹색채권 | 홍콩 정부, Bank of China (Hong Kong), Crédit Agricole CIB, Goldman Sachs, HSBC | Besu + Canton/Daml 결합 | HK$8억 규모 토큰화 녹색채권 발행·결제 | [HKMA 공식 보고서](https://www.hkma.gov.hk/media/eng/doc/key-information/press-release/2023/20230824e3a1.pdf) |
| LSEG DiSH PoC·출시 | LSEG 및 참여 금융기관 컨소시엄 | Canton | 상업은행 예금을 Canton에서 토큰화해 현금 결제 수단으로 사용 | [LSEG 공식 발표](https://www.lseg.com/en/media-centre/press-releases/2026/lseg-launches-digital-settlement-house) |

이 표에서는 다음과 같이 표현해야 한다.

- 가능: “Bank of America가 Canton 기반 실제 국채 금융 거래에 참여했다.”
- 불가: “Bank of America가 Canton을 자사의 토큰증권 표준 네트워크로 선택했다.”
- 가능: “BlackRock이 GS DAP의 토큰화 MMF 출시에 참여했다.”
- 불가: “BlackRock의 자체 토큰화 플랫폼은 Canton 기반이다.”

## 3. 회원·validator·워킹그룹·파일럿 참여

이 표는 관심과 생태계 관여를 보여줄 뿐, 실제 업무 플랫폼 채택이나 거래량을 입증하지 않는다.

| 생태계·프로그램 | 참여 기관 | 참여 형태 | 해석상 한계 | 출처 |
|---|---|---|---|---|
| Canton Foundation | DTCC | Euroclear와 공동 의장 | 거버넌스 참여는 확인되지만 모든 DTCC 업무가 Canton으로 이전된 것은 아님 | [DTCC 공식 발표](https://www.dtcc.com/news/2025/december/17/dtcc-and-digital-asset-partner-to-tokenize-dtc-custodied-us-treasury-securities) |
| Global Synchronizer Foundation | Goldman Sachs, HKFMI, Moody’s Ratings 등 | 재단 회원 | 회원 가입만으로 실제 자산 발행·거래 시스템 채택을 의미하지 않음 | [Canton 발표](https://www.canton.network/canton-network-press-releases/goldman-sachs-hkfmi-and-moodys-ratings-join-the-global-synchronizer-foundation) |
| Canton RWA 파일럿 | BNY Mellon, Broadridge, DRW, EquiLend, Goldman Sachs, Paxos 등 | 애플리케이션 제공·시장 전문성 제공·모의거래 | 생산거래와 파일럿 참여를 구분해야 함 | [Canton 파일럿 결과](https://www.canton.network/canton-network-press-releases/the-canton-network-completes-the-most-comprehensive-blockchain-pilot-to-date-for-tokenized-real-world-assets) |
| DTCC Industry Working Group | 50곳 이상의 금융기관·시장 참여자 | 서비스 설계·운영 준비 협력 | 특정 기관이 Besu와 Canton 중 어느 네트워크를 선택했는지 알 수 없음 | [DTCC 워킹그룹 발표](https://www.dtcc.com/news/2026/may/04/dtcc-advances-development-of-new-tokenization-service) |
| Swift Shared Ledger 초기 그룹 | 17개 은행 | 초기 사용·파일럿 거래 준비 | Swift가 Besu를 선택한 것은 확인되지만 각 은행이 자체 플랫폼으로 Besu를 채택한 것은 아님 | [Swift 발표](https://www.swift.com/news-events/press-releases/swifts-blockchain-ledger-ready-use-17-banks-set-pioneer-tokenised-cross-border-payments-trusted-global-infrastructure) |
| Canton Network 초기 참여그룹 | BNP Paribas, Deutsche Börse, Goldman Sachs, Broadridge, Cboe, EquiLend 등 | 네트워크 출범·상호운용성 테스트 참여 | 기관별 실제 생산 시스템과 거래 규모를 별도로 확인해야 함 | [Canton 출범 발표](https://www.canton.network/canton-network-press-releases/canton-network-press-release) |

## 4. 현재 표에서 제외하거나 보류해야 할 사례

| 기관·플랫폼 | 보류 이유 |
|---|---|
| Fnality | Besu 사용은 LFDT의 과거 기술자료에서 확인되지만 현재 Fnality 공식 제품 페이지가 기반 기술을 명시하지 않음 |
| J.P. Morgan Kinexys | Quorum 계열 private permissioned Ethereum 플랫폼이라는 점은 확인되지만 현재 실행 클라이언트가 Besu인지 공식적으로 확인되지 않음 |
| HSBC Orion | 디지털 채권 플랫폼의 운영은 확인되지만 최신 공식 자료에서 기반 네트워크를 Besu 또는 Canton으로 단정하기 어려움 |
| Nasdaq·NYSE·Vanguard 등 DTCC 참가사 | DTCC 거래 참여는 확인되지만 Besu 또는 Canton 중 어느 환경을 이용했는지 공개되지 않음 |

## 5. 활용 원칙

이렇게 분리하면 최종 판정의 근거는 주로 **첫 번째 표**에서 가져오고, 두 번째 표는 실제 활용도를 보완하며, 세 번째 표는 생태계 모멘텀만 보여주는 방식이 적절하다.

- 첫 번째 표: 기관·플랫폼의 기술 선택을 판단하는 핵심 근거
- 두 번째 표: 실제 거래·발행 경험을 보여주는 보조 근거
- 세 번째 표: 네트워크 관심과 생태계 확장성을 보여주는 참고 근거

기관별 네트워크 채택이나 시장점유율을 평가할 때는 세 표의 항목을 단순 합산하면 안 된다. 동일 기관이 여러 프로젝트에 중복 참여할 수 있고, 거래 참여 또는 재단 가입이 해당 기관의 핵심 시스템 채택을 의미하지 않기 때문이다.
