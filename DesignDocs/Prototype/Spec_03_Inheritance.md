# Tech Spec: Prototype Inheritance System

## 1. The Will (LegacySnapshot)

사망 시점의 데이터를 다음 캐릭터에게 전달하기 위한 중간 데이터 포맷입니다.

```csharp
[System.Serializable]
public class LegacySnapshot {
    public string ancestor_name;
    public int ancestor_legacy_score;
    public ItemInstance inherited_item; // Only 1 item allowed for prototype
}
```

## 2. Inheritance Flow

### Step 1: On Death
1.  Check `Inventory`.
2.  If `Inventory.Count > 0`:
    *   Select the item with the highest `rarity` or `provenance_count`.
    *   Save this item to `LegacySnapshot.json`.
3.  Delete current `CharacterSave.json`.

### Step 2: New Game (Character Creation)
1.  Load `LegacySnapshot.json`.
2.  **IF Exists:**
    *   Show Message: "Inheriting Will from [AncestorName]".
    *   Add `inherited_item` to new character's inventory directly.
    *   Add `provenance_log`: `{ event: "INHERITED", from: AncestorName, to: NewName }`.
3.  **ELSE:**
    *   Start with empty inventory (Wooden Club).

## 3. Decay Logic (Entropy)
*   When loading `inherited_item`:
    *   `item.max_durability *= 0.8f;` // 20% decay penalty
    *   If `max_durability < 10`: Item crumbles to dust (Delete item).
