# [Design Spec] 3.2 Dynamic Crafting
**Parent Module:** [03_Economy](../03_Economy/README.md)

## 1. No Fixed Recipes
"철 2개로 검을 만든다"는 같지만, 결과물은 재료의 출처와 환경에 따라 완전히 달라집니다.

## 2. Material Genetics (재료 유전자)
모든 채집물은 채집 당시의 환경 데이터를 저장합니다.

*   **Iron Ore (North):** `Cold_Resistance +5` 속성 내재.
*   **Iron Ore (Volcano):** `Heat_Resistance +5` 속성 내재.
*   **Oak Wood (Blessed Forest):** `Mana_Conductivity +10%` (마법 지팡이 제작 시 유리).

## 3. The Crafting Moment (제작의 순간)
제작 버튼을 누르는 순간의 변수들이 최종 옵션을 결정합니다.

*   **Time of Day:** 밤에 제작하면 '암속성' 부여 확률 증가.
*   **Weather:** 비오는 날 대장장이질을 하면 급랭(Quenching) 효과로 내구도 증가.
*   **Crafter's Emotion:**
    *   캐릭터가 최근 전투에서 승리함(Confident) → `Critical Chance` 증가.
    *   캐릭터가 배고픔/부상 상태(Misery) → `Curse` 옵션 부여 확률 증가.

## 4. Masterpiece System (걸작 시스템)
*   제작 숙련도 100 달성 시, 자신만의 고유 브랜드(Brand)를 아이템 이름에 접두사로 붙일 수 있음. (예: "Tjdql's Longsword")
*   브랜드 아이템은 동급 아이템 대비 10%의 히든 스탯 보너스를 가짐.
