# [Design Spec] 3.1 Provenance System (Item History)
**Parent Module:** [03_Economy](../03_Economy/README.md)

## 1. Concept
아이템의 가치를 '현재 성능'이 아닌 '누적된 역사'로 평가하는 시스템입니다.

## 2. Data Structure (Provenance Node)
모든 아이템은 아래의 메타데이터를 포함하는 `History Log` 배열을 가집니다.

```json
{
  "item_uuid": "1234-5678-abcd",
  "provenance_log": [
    {
      "timestamp": "Year 102, Day 5",
      "event_type": "CRAFTED",
      "actor": "Blacksmith_Kael",
      "note": "Created during the Great Winter storm."
    },
    {
      "timestamp": "Year 102, Day 50",
      "event_type": "KILL_BOSS",
      "actor": "Warrior_Joon",
      "target": "Red Dragon",
      "note": "Delivered the final blow."
    },
    {
      "timestamp": "Year 103, Day 1",
      "event_type": "STOLEN",
      "actor": "Thief_Rat",
      "prev_owner": "Warrior_Joon",
      "note": "Stolen in the chaotic market."
    }
  ]
}
```

## 3. History Valuation (가치 산정)
NPC 상점이나 경매장은 이 기록을 바탕으로 가치를 책정합니다.

*   **Celebrity Premium:** 유명 랭커가 소유했던 기록이 있으면 가격 +200%.
*   **Bloodlust Value:** PK 기록이 많을수록 '저주받은 무기' 컬렉터에게 높은 가격에 팔림.
*   **Epic Moment:** 최초의 레이드 클리어 등 서버 기록과 연동된 아이템은 유물(Artifact) 등급으로 자동 승격.

## 4. UI Representation
*   인벤토리에서 아이템 우클릭 시 '역사 보기' 탭 활성화.
*   타임라인 형태로 아이템의 이동 경로 시각화.
