# [Design Spec] 2.1 Character Genetics & Traits
**Parent Module:** [02_Character](../02_Character/README.md)

## 1. Overview
캐릭터 생성 시 결정되는 선천적 능력치(Nature)와 환경적 요인(Nurture)을 정의합니다. 모든 캐릭터는 "불완전"하며, 특정 역할에 특화된 형태를 가집니다.

## 2. Genetic Traits (유전적 특성)
유전적 특성은 3개의 슬롯(Major 1, Minor 2)을 가집니다.

### 2.1 Physical Traits (신체적 특성)
*   **Heavy Bones (강골):**
    *   *Effect:* 최대 소지 무게 +20%, 낙하 데미지 감소 -10%
    *   *Drawback:* 이동 속도 -5%, 수영 속도 -15%
    *   *Usage:* 광부, 중갑 전사
*   **Eagle Eye (매의 눈):**
    *   *Effect:* 시야 거리 +15%, 원거리 명중률 보정 +5%
    *   *Drawback:* 근거리 피격 시 패닉(화면 흔들림) 발생 확률 증가
    *   *Usage:* 정찰병, 궁수

### 2.2 Mental Traits (정신적 특성)
*   **Paranoid (편집증):**
    *   *Effect:* 은신한 적 탐지 확률 +20%, 수면 중 기습당할 확률 감소
    *   *Drawback:* NPC와의 우호도 상승 속도 -20%
*   **Greedy (탐욕):**
    *   *Effect:* 루팅 속도 +30%, 거래 시 협상 보너스
    *   *Drawback:* 파티 분배 시 자신의 몫을 몰래 챙길 확률(자동 트리거) 존재

## 3. Environmental Factors (출생지 효과)
출생지는 초기 스킬의 '학습 효율(Learning Efficiency)'을 결정합니다.

| Biome | Advantage (Learning x 1.5) | Disadvantage (Learning x 0.5) |
| :--- | :--- | :--- |
| **Highlands (고산지대)** | Mining, Climbing, Lung Capacity | Farming, Swimming |
| **Wetlands (습지대)** | Alchemy (Poison), Herbalism | Smithing (Humidity issue) |
| **Urban (도시)** | Politics, Commerce, Law | Survival, Hunting |

## 4. Inheritance Logic
*   **Direct Lineage:** 선대 캐릭터가 '자연사' 했을 경우, 선대의 가장 높은 숙련도를 가진 스킬 관련 Trait이 50% 확률로 유전됨.
*   **Mutation:** 선대 캐릭터가 '방사능/마법' 등으로 사망했을 경우, 무작위 돌연변이(희귀 Trait) 발생 확률 10%.
