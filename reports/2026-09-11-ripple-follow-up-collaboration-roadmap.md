# Ripple 후속 협업 방향 및 실행 로드맵

- 작성일: 2026-09-11
- 출처: 싱가포르 Ripple 미팅 녹취, 미래에셋증권 후속 질의 메일, 공개자료
- 목적: 기존 기술 질의를 실제 협업 과제와 단계별 의사결정으로 전환

## 1. 한 줄 결론

**향후 Ripple과의 협업은 Besu–XRPL 브리지 구축을 출발점으로 삼기보다, 싱가포르 규제형 MMF·T-bill을 XRPL에서 발행하고 RLUSD 결제, 환매, 담보·repo까지 연결하는 사업 PoC를 중심으로 추진하며, 브리지는 법적 필요성이 확인된 뒤 별도 검토하는 것이 적절하다.**

## 2. 미팅과 후속 메일에서 확인된 내용

### 후속 메일이 잘 다룬 부분

- Besu와 XRPL 간 lock-and-mint 구조의 기술적 가능성
- 양방향 상환과 총발행량 일치 문제
- bridge·relayer·유동성 비용
- 국가별 규제 구현 사례
- 하나의 금융상품을 두 네트워크에 배포할 때의 권리 일관성

이는 Ripple의 기술 역량과 답변 수준을 확인하는 좋은 1차 질의다.

### 후속 메일에서 상대적으로 약해진 부분

출장 미팅에서 Ripple 측이 더 강하게 강조한 내용은 다음이었다.

1. **왜 자산을 브리지해야 하는가:** 공용망에서 활용하려면 직접 발행이 더 단순할 수 있다는 문제 제기
2. **법적 소유권:** 온체인 보유자가 펀드의 법적 소유자로 인정되는 digital-native issuance
3. **2차 효용:** 단순 토큰화보다 담보, repo, 대출, margin 활용이 핵심
4. **결제:** RLUSD를 현금 leg로 사용하는 DvP
5. **현지 파트너:** Ripple 자체는 싱가포르 증권 유통에 필요한 CMS 라이선스를 갖고 있지 않으며, 별도의 licensed partner가 필요
6. **기관 인프라:** 기존 리테일 지갑을 넘어서는 Ripple Custody 검토
7. **Ripple의 역할:** XRPL 기술지원뿐 아니라 custody, stablecoin, OTC liquidity, distribution partner를 묶는 통합 사업자

따라서 다음 접촉에서는 브리지 관련 답변만 기다리기보다, 이 일곱 가지를 구체적인 공동 과제로 전환해야 한다.

## 3. 권고 협업 포트폴리오

| 우선순위 | 협업 과제 | 목표 | 판단 |
|---|---|---|---|
| 1 | Singapore Institutional RWA Utility PoC | MMF·T-bill 발행부터 DvP, 환매, 담보까지 검증 | 핵심 과제 |
| 2 | Institutional Custody Fit Assessment | 미래에셋의 멀티체인 기관 지갑·정책통제 요건 검증 | 빠른 보조 과제 |
| 3 | Besu–XRPL Interoperability Study | canonical record, supply control, bridge trust model 설계 | 연구 과제 |
| 4 | Ripple Managed Interoperability 검토 | 유동성·환전·커스터디·SLA를 묶은 서비스 가능성 확인 | 조건부 사업 검토 |

### 과제 1. Singapore Institutional RWA Utility PoC

#### 핵심 질문

> 싱가포르에서 규제된 MMF 또는 T-bill 상품을 XRPL에 발행하면, 적격 기관투자자가 stablecoin으로 24시간 청약·환매하고 해당 상품을 담보로 활용할 수 있는가?

#### 권고 범위

- 싱가포르 VCC 기반 MMF·단기국채 펀드 또는 feeder 구조
- XRPL에서 법적 권리와 연결된 tokenized share class 발행
- RLUSD 및 native USDC를 이용한 DvP 비교
- 허용된 기관지갑만 청약·이전 가능하도록 통제
- NAV, 명의개서, 온체인 잔액의 실시간 또는 일중 대사
- 환매 후 stablecoin 수령과 법정화폐 회수까지 검증
- 은행 또는 Ripple 생태계 참여자를 통한 담보·repo 모의 또는 제한적 실행

#### 기존 사례와의 차별점

DBS·Franklin Templeton·Ripple은 2025년 sgBENJI를 XRPL에서 RLUSD와 거래하고 향후 담보·repo로 활용하는 계획을 발표했다. 따라서 미래에셋 PoC가 ‘XRPL에서 MMF 토큰 발행’에 그치면 차별성이 없다. [DBS–Franklin Templeton–Ripple 발표](https://www.dbs.com/newsroom/DBS_and_Franklin_Templeton_to_launch_trading_and_lending_solutions_powered_by_tokenised_money_market_funds_and_Ripples_RLUSD_stablecoin)

미래에셋의 차별점은 다음 중 최소 두 가지여야 한다.

- 한국 또는 아시아계 자산운용사의 실제 상품
- 싱가포르와 한국 또는 다른 아시아 법인 간 기관 유통
- RLUSD와 native USDC의 dual cash leg 비교
- 실제 환매와 법정화폐 회수
- 담보 인정 또는 repo 실행
- Arc·EVM·Canton과 동일 KPI 비교

### 과제 2. Institutional Custody Fit Assessment

출장 미팅에서 Ripple은 미래에셋의 현재 지갑이 리테일 수준이라는 설명에 대해 Ripple Custody 검토를 제안했다. 이는 XRPL 채택과 독립적으로도 가치가 있을 수 있다.

평가 범위는 다음과 같다.

- 온프레미스, 클라우드, MPC, HSM 구성
- hot·warm·cold wallet 정책
- 역할 분리와 다중 승인
- 체인별 자산 및 스마트계약 지원 범위
- 키 분실·유출·퇴직자·재해복구 시나리오
- KYT·AML 솔루션 연계
- Besu, XRPL, Arc/EVM 및 향후 Canton 지원 전략
- 국내 규제와 망분리·내부통제 요건
- 라이선스 비용, 도입기간, 운영인력

Ripple 공개자료는 MPC/HSM, 온프레미스 또는 SaaS, 정책 오케스트레이션 및 다중 custodian 연계를 제공한다고 설명한다. 실제 지원 체인과 국내 적용 가능성은 제안서와 데모를 통해 확인해야 한다. [Ripple Custody](https://ripple.com/products/custody/)

### 과제 3. Besu–XRPL Interoperability Study

이 과제는 당장 bridge를 만드는 PoC가 아니라, 다음 질문에 답하는 4~6주 설계 연구로 한정하는 것이 좋다.

1. Besu와 XRPL 중 어느 원장이 법적·운영상 canonical record인가?
2. 반대편 토큰은 법적 증권인가, 예탁증서형 표현인가, 단순 settlement receipt인가?
3. lock 사실을 누가 확인하고 mint를 승인하는가?
4. validator, witness, multisig signer 및 운영자의 이해관계는 어떻게 분리되는가?
5. bridge 장애·해킹·체인 정지 시 환매 책임은 누가 부담하는가?
6. 두 네트워크의 총발행량과 명의개서부는 어떻게 대사하는가?
7. 동결, 압류, 상속, 키 분실, 법원명령은 양쪽 원장에 어떻게 반영하는가?
8. 동일 상품의 양쪽 시장가격이 달라질 경우 누가 유동성을 공급하는가?

#### 권고 원칙

- 규제가 Besu 선발행을 요구하지 않는다면 XRPL 직접 발행이 더 단순하다.
- 한국 법률상 Besu가 원본 원장이어야 한다면 XRPL 토큰의 법적 성격부터 정의해야 한다.
- 초기에는 증권 자체를 bridge하기보다 보유증명·결제상태·환매지시를 연동하는 방식도 비교한다.
- 브리지 비용보다 bridge operator의 책임, 보험, SLA 및 실패 복구를 우선 평가한다.
- 기술적 lock-and-mint 성공만으로 사업 PoC를 완료한 것으로 보지 않는다.

### 과제 4. Ripple Managed Interoperability 검토

Ripple을 범용 메시지 relayer로 전제하지 않는다. 대신 다음 요소를 하나의 계약상 서비스로 제공할 수 있는지 확인한다.

- RLUSD 또는 다른 결제자산의 네트워크 간 조달
- OTC를 통한 stablecoin·법정화폐 환전
- 기관 custody와 정책 통제
- AML·KYT 및 거래 모니터링 연계
- licensed distributor·transfer agent 소개
- 장애 대응, 환매 및 실패 거래 처리 SLA
- Ripple Prime 또는 파트너를 통한 담보 활용

**추론:** Ripple이 이 요소들의 상당 부분을 직접 제공하거나 책임 있는 주계약자로 조정할 수 있다면, 기술적 relayer가 아니더라도 미래에셋의 멀티네트워크 운영 복잡성을 낮추는 가치가 있다. 반대로 각 구간을 제3자에게 넘기고 Ripple이 책임지지 않는다면 ‘One Ripple’의 실질적 이점은 제한된다.

## 4. Ripple과 합의해야 할 공동 목표

다음 문장을 양사의 공동 목표로 제안한다.

> Mirae Asset and Ripple will jointly assess whether a Singapore-regulated tokenized MMF or T-bill product can achieve institutional-grade issuance, stablecoin DvP settlement, redemption, custody, and collateral utility on the XRP Ledger, while defining how it may interoperate with Mirae Asset's existing Besu infrastructure.

이 문장은 XRPL 사용을 미리 확정하지 않으면서도, 단순 기술검토보다 높은 수준의 사업 목표를 제시한다.

## 5. 단계별 실행안

### Phase 0 — Use-case Alignment (2주)

**미래에셋 준비사항**

- 후보 상품 1개 선정
- 발행 국가와 법적 구조
- 목표 투자자 유형과 예상 거래규모
- 현행 청약·환매·명의개서 절차
- Besu가 반드시 canonical record여야 하는지에 대한 내부 의견

**Ripple 요청사항**

- DBS·Franklin 사례의 실제 운영 범위와 계획 범위 구분
- 적용 가능한 싱가포르 CMS·transfer agent·custody 파트너 제시
- RLUSD와 USDC의 거래·환매 경로
- XRPL mainnet에서 현재 가능한 규제 통제 기능 목록
- Ripple Custody 데모 및 적용 범위

**산출물**

- 2~3페이지 공동 use-case charter
- 참여기관과 역할표
- PoC의 법적·기술적 선결조건
- PoC 진행 여부 1차 decision gate

### Phase 1 — Legal & Architecture Design (4~6주)

- 온체인 토큰과 법적 펀드 지분의 연결 구조
- transfer agent 및 공식 명부 정의
- XRPL 직접 발행과 Besu–XRPL mirrored issuance 비교
- RLUSD·USDC DvP 및 환매 구조
- custody와 키 복구 운영모델
- 개인정보와 거래기밀 보호 방안
- 각 참여자의 라이선스와 책임
- 장애·파산·브리지 실패 시 처리 절차

**산출물**

- target operating model
- 법률·규제 issue list
- solution architecture
- RACI 및 책임 경계
- KPI와 테스트 시나리오
- 비용·일정 견적

### Phase 2 — Controlled PoC (8~12주)

- 적격투자자 onboarding과 wallet allowlist
- 상품 발행 또는 제한된 tokenized representation
- RLUSD·USDC 청약 및 DvP
- 이전 제한, 동결, 회수, 키 복구
- NAV·명의개서·온체인 잔액 대사
- 환매와 현금 회수
- 담보 설정·해제 또는 모의 repo
- Arc/EVM 비교 시나리오 실행

**성공 KPI**

- 비허용 지갑 차단 100%
- 자산·현금 한쪽만 이전되는 결제 실패 0건
- 온체인 잔액과 공식 명부 100% 일치
- 주문부터 사용 가능한 토큰 수령까지 10분 이내 또는 기존 대비 80% 단축
- 환매 후 stablecoin 수령 당일, 목표 30분 이내
- 실제 기관 2곳 이상 참여
- 담보 수용기관 최소 1곳의 정책 검토 또는 제한적 실행

### Phase 3 — Commercial Pilot

다음 조건이 충족된 경우에만 상용 파일럿으로 진행한다.

- 상품의 법적 권리와 온체인 기록이 명확하다.
- licensed distributor와 custody 구조가 확정됐다.
- 실제 투자자 수요와 거래규모가 확인됐다.
- RLUSD·USDC의 유동성과 법정화폐 회수 비용이 수용 가능하다.
- 담보·repo 또는 24시간 환매 중 하나 이상이 실현된다.
- 비교망보다 총비용, 처리시간 또는 신규 수익 측면의 우위가 있다.

## 6. 양사 역할 제안

### 미래에셋

- 후보 상품 및 운용구조
- 법적 권리와 명의개서 요구사항
- 싱가포르·한국 내부 법무 및 컴플라이언스
- Besu 플랫폼과 기존 지갑 연계
- 투자자·판매채널 및 실제 업무 시나리오
- 네트워크 중립적 KPI와 비교평가

### Ripple

- XRPL 발행 및 DvP reference design
- 현재 mainnet 기능에 대한 확정적 기술 설명
- RLUSD와 native USDC 유동성·환매 구조
- Ripple Custody 설계와 데모
- CMS distributor, transfer agent, custodian 및 담보 파트너 소개
- Ripple Prime·OTC 적용 가능성
- PoC 엔지니어링 지원
- 서비스별 가격, SLA, 장애 책임 및 상용화 조건

### 공동 파트너

- 싱가포르 CMS 라이선스 보유 유통기관
- transfer agent 또는 fund administrator
- 자산 수탁기관 및 디지털자산 custodian
- 기관투자자 또는 accredited investor
- 담보·repo를 검토할 은행·prime broker

Ripple Markets APAC은 MAS상 Major Payment Institution이며 계좌발급, 국내·국경간 송금, e-money 발행 및 digital payment token 서비스를 등록하고 있다. 이는 securities distribution용 CMS 라이선스와는 다르므로, 증권 유통에는 별도 licensed partner가 필요하다. [MAS Financial Institutions Directory](https://eservices.mas.gov.sg/fid/institution/detail/415143-RIPPLE-MARKETS-APAC-PTE-LTD)

## 7. 다음 working session에서 받을 답변

다음 회의는 회사소개가 아닌 90분 실무 세션으로 제안한다.

### Agenda

1. 미래에셋 후보상품과 목표 투자자 설명 — 15분
2. Ripple의 유사사례와 실제 운영범위 — 15분
3. XRPL 직접 발행 vs Besu mirrored asset — 20분
4. RLUSD·USDC DvP, 환매 및 유동성 — 15분
5. CMS·transfer agent·custody·collateral 파트너 — 15분
6. PoC 범위, 역할, 일정, 비용 합의 — 10분

### 회의 전 Ripple에 요청할 자료

- Besu–XRPL 권고 reference architecture
- bridge trust model 및 운영 책임 예시
- DBS·Franklin 및 한국 금융사 PoC의 공개 가능한 상세 범위
- XRPL의 현재 mainnet 규제 기능 matrix
- RLUSD·USDC liquidity 및 on/off-ramp 구조
- Ripple Custody 기술·가격·배포 옵션
- 싱가포르 CMS·transfer agent 파트너 후보
- Ripple의 엔지니어링 투입 범위와 PoC 지원 조건

## 8. 현재 메일에 대한 최종 평가

현재 메일은 기술 due diligence의 출발점으로 적절하다. 특히 total supply, double issuance, bidirectional redemption 및 regulatory consistency를 묻는 부분은 반드시 답변을 받아야 한다.

다만 이 메일의 질문만 따라가면 ‘가능한 브리지를 설계하는 것’이 협업 목표가 될 위험이 있다. 다음 단계에서는 아래 순서로 논의를 재정렬해야 한다.

1. 판매할 상품과 투자자를 선정한다.
2. 법적 소유권과 canonical record를 정한다.
3. XRPL에서 얻을 24시간 결제·환매·담보 효용을 정의한다.
4. Ripple이 실제로 제공할 custody·liquidity·distribution을 확인한다.
5. 그 후에만 Besu와 XRPL 사이의 bridge가 필요한지 판단한다.

## 9. 경영진 공유용 요약

Ripple과는 Besu–XRPL 브리지 자체보다 싱가포르 기관상품의 실제 발행·결제·환매·담보 활용을 중심으로 협업하는 것이 바람직하다. Ripple은 미팅에서 XRPL 기술뿐 아니라 RLUSD, custody, OTC 유동성 및 현지 licensed partner 연결을 하나의 강점으로 제시했다. 우선 싱가포르 VCC 기반 MMF 또는 T-bill 상품을 선정하고, XRPL 직접 발행과 RLUSD·USDC DvP, 환매 및 담보 활용을 검증하는 PoC를 제안할 수 있다. Besu–XRPL 브리지는 법적 원본 원장과 운영 책임이 정해진 뒤 별도의 아키텍처 연구로 진행하는 것이 안전하다. 최종적으로 Arc·EVM·Canton과 총비용, 투자자 접근성, 유동성 및 규제 통제를 비교해 상용화 여부를 결정해야 한다.

## 10. 참고자료

- 싱가포르 Ripple 미팅 녹취 및 미래에셋증권 후속 질의 메일
- [DBS·Franklin Templeton·Ripple의 sgBENJI·RLUSD 협업](https://www.dbs.com/newsroom/DBS_and_Franklin_Templeton_to_launch_trading_and_lending_solutions_powered_by_tokenised_money_market_funds_and_Ripples_RLUSD_stablecoin)
- [Ripple의 ZILO·Licuido 투자 및 transfer agency·collateral 전략](https://ripple.com/ripple-press/ripple-strengthens-digital-capital-markets-infrastructure-with-investments-in-zilo-and-licuido/)
- [Ripple Custody](https://ripple.com/products/custody/)
- [MAS: Ripple Markets APAC licence](https://eservices.mas.gov.sg/fid/institution/detail/415143-RIPPLE-MARKETS-APAC-PTE-LTD)

