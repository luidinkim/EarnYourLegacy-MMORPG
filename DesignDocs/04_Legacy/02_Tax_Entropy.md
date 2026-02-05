# [Design Spec] 4.2 Tax & Entropy
**Parent Module:** [04_Legacy](../04_Legacy/README.md)

## 1. Entropy (Item Decay)
모든 장비는 주인을 바꿀 때마다 영혼이 닳습니다.

*   **Inheritance Penalty:** 상속 시 최대 내구도(Max Durability) -20%.
*   **Trade Penalty:** 경매장 거래 시 최대 내구도 -5%.
*   **Result:** 아무리 전설적인 검이라도 4~5대(Generation)를 넘기면 부서지기 쉬운 관상용 유물이 됩니다. 이는 제작자가 지속적으로 필요한 이유입니다.

## 2. Inheritance Tax (상속세)
정부(Government)는 재정 확보를 위해 상속세를 걷습니다.

*   **Formula:** `Tax = (Total_Asset_Value * Tax_Rate) - Deduction`
*   **Progressive Tax:** 자산이 많을수록 세율이 급격히 증가 (누진세).
*   **Payment:** 현금(Gold)으로 납부해야 하며, 부족할 경우 아이템이 강제 압류되어 국고 경매로 넘어갑니다.

## 3. Evasion (탈세)
*   **Burial Method:** 아이템을 땅에 묻고 좌표를 보물지도로 남기는 방식. 상속세를 0으로 만들지만, 다른 도굴꾼 유저가 파갈 위험이 큼.
*   **Laundering:** '기부' 형태로 자산을 길드 창고에 넣었다가 다시 빼는 방식. 길드 창고 입출금 기록이 남으며, 감사(Audit) 스킬을 가진 공무원 유저에게 걸리면 압수됨.
