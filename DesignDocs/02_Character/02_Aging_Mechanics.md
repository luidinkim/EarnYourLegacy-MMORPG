# [Design Spec] 2.2 Aging Mechanics
**Parent Module:** [02_Character](../02_Character/README.md)

## 1. Life Circle (생애주기)
캐릭터의 수명은 현실 시간 약 90일(3개월)로 설정됩니다.

### Phase 1: Youth (0~20일)
*   **Growth:** 스탯 상승폭이 가장 큼.
*   **Buff:** `Fast Recovery` (HP/ST 회복 속도 +50%)
*   **Activity:** 전투 튜토리얼, 기본 자원 확보, 세계 탐험.

### Phase 2: Prime (21~50일)
*   **Peak Performance:** 신체 능력치(STR, DEX)가 최대치에 도달.
*   **Buff:** `Peak Condition` (모든 물리 판정 +10%)
*   **Activity:** 세력 전쟁, 레이드, 길드 창설.

### Phase 3: Middle Age (51~75일)
*   **Decline Starts:** 신체 스탯 서서히 감소 (매일 -0.5%).
*   **Shift:** 지능/지혜 스탯 상승, 제작/정치 스킬 효율 증가.
*   **Buff:** `Authority` (NPC 고용 비용 할인, 발언권 강화).

### Phase 4: Elder (76~90일)
*   **Rapid Decline:** 최대 HP 70% 수준으로 고정. 질병 저항력 급감.
*   **Unique Action:** `Mentoring` (타인에게 스킬 전수 가능), `Will Drafting` (유언장 작성).
*   **Buff:** `Sage's Eye` (아이템 감정 레벨 MAX, 숨겨진 속성 파악).

## 2. Aging Penalties & Diseases
노화는 단순한 디버프가 아닌 관리 요소입니다.

*   **Arthritis (관절염):** 비오는 날씨에 이동 속도 -30%. (치료 불가, 진통제로 일시 완화)
*   **Dementia (치매):** 미니맵이 간헐적으로 사라지거나 퀘스트 마커가 오작동함.

## 3. Anti-Aging (수명 연장)
*   **Elixir:** 연금술 최고 등급 아이템. 수명을 7일 연장 (최대 3회 가능). 부작용으로 랜덤 Trait 변이 발생.
