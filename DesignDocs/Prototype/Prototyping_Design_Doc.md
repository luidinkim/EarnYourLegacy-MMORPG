# Earn Your Legacy: Prototyping Design Document (Vertical Slice)

> **Phase:** Prototype Alpha
> **Goal:** Validate the core loop of "Life, Death, and Legacy".
> **Target:** Minimal Playing Version (MPV)

## 1. Prototype Scope: The "One Hour Life" Loop

프로토타입은 방대한 MMO 세계가 아닌, **단일 캐릭터의 생애주기와 상속 메커니즘**을 검증하는 데 집중합니다.

### Core Loop
1.  **Birth:** 유전 특성(Trait)을 선택하고 캐릭터 생성.
2.  **Live:** 자원 채집 및 기본 아이템 제작 (Dynamic Crafting).
3.  **Age:** 시간 가속을 통해 노화(Aging) 경험.
4.  **Die:** 사망 후 통계(Legacy Score) 확인.
5.  **Inherit:** 다음 캐릭터 생성 시 이전 캐릭터의 아이템을 상속받음.

## 2. Key Features to Implement

### 2.1 Character System (Mini)
*   **Traits:** `Strong (Inv +2)` vs `Weak (Inv -2)` 두 가지 특성만 구현.
*   **Aging:** 1분 = 1년으로 설정. 10분 플레이 시 노년기 진입.
*   **Stats:** HP, Stamina, Age.

### 2.2 Economy System (Mini)
*   **Resource:** `Iron Ore`, `Wood`.
*   **Crafting:** `Iron Sword` 제작.
    *   **Logic:** 제작 시점의 시간(초)을 Seed로 하여 `Attack Power`와 `Durability`가 변동됨.
    *   **Provenance:** 아이템 툴팁에 "Created by [PlayerName] at Age [XX]" 표시.

### 2.3 Legacy System (Mini)
*   **Permadeath:** HP 0이 되거나 'Suicide' 버튼 클릭 시 캐릭터 삭제.
*   **The Will:** 사망 직전 인벤토리의 아이템 1개를 '상속 상자'에 저장.
*   **Next Gen:** 새 캐릭터 생성 시 '상속 상자'의 아이템을 가지고 시작.

## 3. Technical Requirements (Dev Spec)

### 3.1 Client (Unity)
*   **Scene:** `Prototype_Scene` (Small 50x50 Terrain).
*   **UI:** Character Creation Panel, Inventory Panel, Death/Legacy Panel.
*   **Controller:** Basic WASD Movement + Interaction Key (F).

### 3.2 Data Structure (JSON/Local DB)
서버 연동 전, 로컬 JSON으로 데이터 구조를 검증합니다.

```json
// character_data.json
{
  "id": 1,
  "name": "Alpha_01",
  "status": "DEAD",
  "legacy_score": 150,
  "inventory": []
}

// inheritance_data.json
{
  "from_char_id": 1,
  "to_char_id": null, // Pending
  "items": [{ "uuid": "...", "name": "Iron Sword", "history": [...] }]
}
```

## 4. Success Metrics (검증 목표)
*   [ ] 캐릭터의 죽음이 데이터(상속 아이템)로 연결되는가?
*   [ ] '이전 생애의 아이템'을 사용하는 것이 감정적 애착을 주는가?
*   [ ] 노화에 따른 페널티가 플레이어의 행동 패턴을 변화시키는가?
