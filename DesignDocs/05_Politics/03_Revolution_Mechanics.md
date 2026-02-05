# [Design Spec] 5.3 Revolution & Guillotine Mechanics
**Parent Module:** [05_Politics](../05_Politics/README.md)

## 1. The Guillotine (단두대)
혁명의 상징이자 가장 강력한 시스템 병기입니다.

### 1.1 Construction
*   **Requirement:** `Age of Revolution` 페이즈 도달 시, 반란군 진영에서 레시피 자동 해금.
*   **Materials:** 서버 내 존재하는 희귀 자원 + 에센스(Essence). 매우 비쌈.

### 1.2 Execution Ritual (처형 의식)
1.  반란군이 도심 광장에 단두대를 설치하고 30분간 방어에 성공해야 함 (공성전).
2.  설치 완료 시, 대상(왕/영주) 플레이어는 강제로 단두대 위로 텔레포트됨 (소환 거부 불가).
3.  **The Severing:** 단두대 칼날이 떨어지면, 대상은 HP와 관계없이 즉사.
4.  **Effect:** 대상의 계정 내 모든 자산(창고 포함)이 50% 소멸, 50%는 주변 시민들에게 골드 비(Rain of Gold) 형태로 뿌려짐.

## 2. Revolutionary Buffs
하층민(자산 하위 50%)이 혁명군에 가담 시 받는 버프:
*   **Voice of the People:** 상위 10% 부자에게 가하는 데미지 +100%.
*   **Anonymous:** 채팅 및 캐릭터 이름이 "성난 시민(Angry Mob)"으로 가려짐.

## 3. Aftermath
*   혁명 성공 시 모든 법률 데이터베이스 `DROP TABLE`.
*   모든 필드의 소유권 초기화 (Homeless 상태).
*   서버는 다시 `Phase 1 (Anarchy)`로 즉시 전환.
