# [Design Spec] 4.3 Ascension Perks
**Parent Module:** [04_Legacy](../04_Legacy/README.md)

## 1. Legacy Score
캐릭터 사망 시 생전의 모든 활동이 점수로 환산됩니다.

*   **Exploration:** 밝힌 지도 면적, 발견한 던전 수.
*   **Combat:** 처치한 보스, PvP 킬/데스 비율(KDA).
*   **Social:** 제정한 법률 수, 맺은 계약 수, 받은 추천 수.

Total Score = `(Exp_Score * 0.5) + (Combat_Score * 1.0) + (Social_Score * 1.5)`

## 2. Ascension Shop (환생 상점)
다음 캐릭터 생성 시, 획득한 Legacy Score를 화폐로 특전(Perk)을 구매합니다.

*   **Silver Spoon (금수저):** 초기 자금 1000G + 도시 시민권 보유 상태로 시작. (Cost: 500 Legacy)
*   **Polyglot (다개국어):** 고대 비석이나 타 종족 언어를 별도 학습 없이 이해. (Cost: 300 Legacy)
*   **Prodigy (신동):** 특정 스킬(랜덤 1종)의 숙련도 상승 속도 +50% 영구 버프. (Cost: 800 Legacy)
*   **Family Connection:** 특정 NPC 가문과 '우호' 관계에서 시작. (Cost: 400 Legacy)

## 3. Philosophy
Perk는 "더 강하게 시작하는 것"이 아니라 "다른 기회를 가지고 시작하는 것"에 초점을 맞춥니다.
직접적인 전투력 보너스(공격력 +10%)는 상점에 존재하지 않습니다.
