# [Design Spec] 5.1 Social Evolution Loop
**Parent Module:** [05_Politics](../05_Politics/README.md)

## 1. Phase Mechanics
서버의 생태계는 고정되어 있지 않고, 유저들의 행동 총량에 따라 3단계로 변이합니다.

## 2. Phase Details

### Phase 1: Age of Anarchy (혼돈의 시대)
*   **Trigger:** 서버 오픈 초기 또는 혁명 성공 직후.
*   **Features:**
    *   모든 지역이 PvP 가능 구역.
    *   법률 시스템 비활성화 (보안관 없음).
    *   건설물 파괴가 매우 쉬움 (내구도 50% 보정).
*   **Goal:** 자원을 모아 `Charter Stone`(국가석)을 제작하여 질서를 선포하는 것.

### Phase 2: Age of Order (질서의 시대)
*   **Trigger:** Charter Stone이 활성화되고 헌법이 선포됨.
*   **Features:**
    *   안전지대(Safe Zone) 생성.
    *   법률 에디터 활성화, 세금 징수 시작.
    *   경제 활동 및 무역 보너스 +20%.
*   **Crisis:** 질서가 오래 지속될수록 부의 불평등(Gini Coefficient)이 상승함.

### Phase 3: Age of Revolution (혁명의 시대)
*   **Trigger:** 불평등 지수 0.7 이상 또는 독재 법안(세율 50% 이상 등) 통과.
*   **Mechanics:**
    *   도시 외곽에 `Revolutionary Camp` NPC 생성.
    *   반란군 가입 시 머리 위에 붉은 표식 생성 (ID 감춤).
    *   **Guillotine (단두대):** 광장에 설치 시 국왕/영주 강제 소환 의식 시작.
*   **End Condition:** 국왕 처형 성공 시 -> Anarchy로 리셋. 반란 진압 성공 시 -> Order 유지 (독재 강화).
