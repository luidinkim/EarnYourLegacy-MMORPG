# [Design Spec] 2.3 Death Types & Permadeath
**Parent Module:** [02_Character](../02_Character/README.md)

## 1. Permadeath Philosophy
죽음은 데이터 삭제가 아닌 '상태 변화'입니다. 캐릭터는 [Active Entity]에서 [Historical Object]로 변환됩니다.

## 2. Death Categories

### Type A: Violent Death (비명횡사)
*   **Trigger:** HP 0 도달 (PvP, PvE, 낙사).
*   **State:** `Corpse` 상태로 10분간 유지.
    *   이 시간 동안 동료가 `Resurrection Ritual`(매우 비쌈)을 시도하면 부활 가능성 있음 (후유증 영구 남음).
    *   실패 시 확정 사망.
*   **Loot:**
    *   **Inventory:** 100% 바닥에 드랍. 누구나 획득 가능.
    *   **Equipped:** 내구도 50% 손상된 상태로 시체에 남음. (약탈 가능)
*   **Legacy Penalty:** 상속세 +50% 가산. 영혼석 생성 불가.

### Type B: Natural Death (자연사)
*   **Trigger:** 수명 종료.
*   **Scene:** 접속 시 "운명의 날" 이벤트 발생. 침대에서 평온하게 사망하는 컷신.
*   **Legacy Benefit:** 상속세 면제(기본 세금만 적용). 대성공(Great Success) 등급의 영혼석 생성.

### Type C: Ascended Retirement (승천/은퇴)
*   **Trigger:** 만레벨 + 특정 업적 달성 후 '차원문'을 통해 떠남.
*   **Effect:** 캐릭터는 사라지지만 NPC(가문 수호자)로 전직하여 길드 홀에 상주.
*   **Bonus:** 다음 캐릭터에게 `Hero's Descendant` 칭호와 초기 명성 보너스 부여.

## 3. Funeral System (장례 시스템)
*   **Burial:** 시체를 수습하여 묘지에 묻으면 `Grave Marker` 생성.
*   **Visiting:** 후손이 묘를 방문하면 `Ancestor's Blessing` 버프 획득. 버프 내용은 생전의 업적에 따라 다름.
