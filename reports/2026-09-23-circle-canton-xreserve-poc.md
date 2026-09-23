# Circle–Canton xReserve PoC 협의 내용

## 1. 한 줄 요약
Sepolia 구간은 Circle 지원 없이 자체 테스트가 가능하며, Canton 구간은 Digital Asset의 별도 온보딩이 필요하고, 당사는 DTCC 연계 실사용 시나리오 검증을 위해 Canton을 우선 적용할 계획입니다.

## 2. 핵심 메시지 3개
- **Sepolia 테스트:** Circle의 Public Faucet에서 테스트 USDC를 받아 MetaMask로 자체 진행할 수 있으며, Circle Mint Sandbox는 필수가 아닙니다.
- **Canton 테스트:** Testnet USDCx 발급과 Canton Party ID 온보딩은 Circle이 아닌 Digital Asset(Canton 측)을 통해 진행해야 합니다.
- **당사 방향:** Arc가 구현 측면에서는 간편하지만, 미국에서 추진 중인 DTCC 관련 이니셔티브와의 정합성 및 한·미 인프라 간 기관 결제 흐름을 검증하기 위해 Canton을 목표 환경으로 유지합니다.

## 3. 공유용 요약

### 짧은 버전
Circle에 Sepolia–Canton Testnet 간 xReserve PoC 진행 요건을 문의했습니다. Circle 확인 결과, Sepolia 구간은 Public Faucet의 테스트 USDC와 MetaMask를 활용해 독립적으로 테스트할 수 있으며 Circle Mint Sandbox는 필수가 아닙니다. 반면 Canton Testnet의 USDCx와 Canton Party ID는 Digital Asset을 통해 별도 온보딩이 필요합니다. Circle은 EVM 호환성으로 구현이 간편한 Arc도 제안했으나, 당사는 미국에서 추진 중인 DTCC 관련 이니셔티브와의 정합성 및 기관 결제·자산이전 흐름 검증을 위해 Canton을 우선 적용할 예정입니다. 향후 Digital Asset과 Canton 환경 프로비저닝을 협의하고, 필요 시 Circle과 Arc 아키텍처도 추가 검토할 계획입니다.

### Slack 공유안
*[Circle 협의 내용 공유 – Canton xReserve PoC]*

Circle에 **Sepolia–Canton Testnet 간 xReserve PoC** 진행을 위한 지원 및 사전 프로비저닝 필요사항을 문의했습니다.

*1. Circle 확인사항*
- **Sepolia/Ethereum:** Public Faucet에서 테스트 USDC를 받아 MetaMask로 자체 테스트 가능
- **Circle Mint Sandbox:** Minting Flow 자체를 시험할 때만 선택적으로 사용하며, 이번 PoC에는 필수 아님
- **테스트 물량:** 대량의 테스트 USDC가 필요할 경우 Circle에서 별도 지원 가능
- **Canton:** Testnet USDCx 발급 및 Canton Party ID 온보딩은 Circle이 아닌 **Digital Asset(Canton 측)**을 통해 진행 필요

*2. Circle 제안*
- EVM 호환으로 구현이 상대적으로 간단한 **Arc** 활용을 제안하며 Canton 선택 배경을 문의

*3. 당사 입장*
- Canton 선택은 단순한 구현 편의성보다 **미국에서 추진 중인 DTCC 관련 이니셔티브와의 정합성 검증**이 목적
- 한국 측 인프라와 DTCC가 활용하는 Canton 환경 간 상호운용성 및 기관 결제 흐름을 검증할 계획
- Arc 아키텍처도 검토 가능하나, 현 단계에서는 **Canton을 최종 결제·자산이전 대상 환경으로 하는 DTCC 연계 시나리오 검증이 우선**

*4. 후속 조치*
- Digital Asset 측과 Testnet USDCx 및 Canton Party ID 발급·온보딩 협의
- Sepolia 구간은 Public Faucet을 활용해 자체 테스트 착수
- 필요 시 Circle에 대량 테스트 USDC 지원 요청 및 Arc 아키텍처 별도 검토
