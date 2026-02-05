# [Design Spec] 4.1 Last Will & Smart Contracts
**Parent Module:** [04_Legacy](../04_Legacy/README.md)

## 1. System Overview
죽음은 갑작스럽게 찾아오지만, 자산의 이전은 철저히 계산되어야 합니다. 유언장은 서버가 보증하는 절대적 계약입니다.

## 2. Contract Types

### 2.1 Simple Transfer (단순 양도)
*   **Logic:** `ON DEATH -> TRANSFER [Item_ID] TO [Beneficiary_ID]`
*   **Cost:** 자산 가치의 5% 공증비.
*   **Usage:** 부계정이나 절친한 친구에게 아이템을 넘길 때.

### 2.2 Conditional Legacy (조건부 상속)
*   **Condition:** "내 캐릭터가 [A 가문] 사람에게 살해당할 경우에만 발동."
*   **Effect:** 전 재산을 [A 가문의 적대 길드]에게 군자금으로 기부.
*   **Purpose:** 죽음 이후에도 정치적 영향력을 행사하기 위함(Dead Man's Switch).

### 2.3 Revenge Contract (복수 계약)
*   **Logic:**
    1.  사망 시 킬러(Killer)의 정보를 현상수배소에 등록.
    2.  재산의 50%를 현상금(Bounty)으로 예치 (Escrow).
    3.  킬러를 죽이고 증표를 가져오는 사람에게 현상금 자동 지급.

## 3. Drafting UI (작성 인터페이스)
*   게임 내 `노트` 아이템에 텍스트로 작성하는 것이 아니라, `계약서` UI에서 드래그 앤 드롭으로 조건을 설정.
*   변호사(Laywer) 직업을 가진 유저가 작성 대행 시 수수료 할인 및 복잡한 로직 구현 가능.
