# [Module 06] 기술 아키텍처 (Technical Architecture)
## 6.1 SpacetimeDB & Logic-in-Database

수천 명의 유저가 동시에 상호작용하고, 복잡한 법률 연산(이동할 때마다 법률 체크)을 수행하기 위해 **SpacetimeDB** 구조를 채택합니다.

*   **기존 방식의 문제:** Application Server ↔ Database 간의 왕복 레이턴시로 인해 실시간 법률 적용이 불가능.
*   **해결책:** 게임 로직(Rust/Wasm)을 DB *내부*에서 실행합니다. 데이터 조회와 로직 처리가 메모리 상에서 원자적(Atomic)으로 이루어져 **Zero Latency** 법률 집행이 가능합니다.

## 6.2 하이브리드 그래프 데이터 (Lineage Graph)

아이템과 가문의 족보를 추적하기 위해 관계형 데이터와 그래프 데이터를 혼합하여 사용합니다.
*   **Nodes:** 플레이어, 아이템, 사건(Event)
*   **Edges:** CREATED_BY, KILLED, STOLEN_FROM, INHERITED_BY
*   이를 통해 유저는 자신의 가문이나 아이템의 역사를 시각적인 그래프로 열람할 수 있습니다.

## 6.3 보안과 정보전 (RLS as Gameplay)

SpacetimeDB의 **Row Level Security (RLS)** 기능을 게임플레이 메커니즘으로 승화시킵니다.
*   **기본:** 유저는 자신의 인벤토리와 계약서만 볼 수 있습니다.
*   **스파이 활동:** '첩보' 스킬을 가진 유저는 일시적으로 특정 테이블의 RLS 권한을 우회하여 타인의 유언장 내용을 엿보거나, 길드 금고의 입출금 내역을 감시할 수 있습니다.
