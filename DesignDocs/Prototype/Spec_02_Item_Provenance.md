# Tech Spec: Prototype Item System (Provenance)

## 1. Item Data Structure

```csharp
[System.Serializable]
public class ItemInstance {
    public string item_uuid; // Unique ID
    public string template_id; // e.g. "iron_sword"
    public ItemStats dynamic_stats;
    public List<ProvenanceLog> history_log;
}

[System.Serializable]
public class ProvenanceLog {
    public long timestamp;
    public string event_type; // CRAFTED, KILLED, INHERITED
    public string actor_name;
    public string description;
}
```

## 2. Crafting Logic (CraftingSystem.cs)

*   **Input:** 2 x Iron Ore, 1 x Wood.
*   **Process:**
    *   Generate new `UUID`.
    *   **Randomize Stats:** 
        *   `Attack = BaseAttack + Random.Range(-5, 5)`
        *   `Durability = BaseDurability + (PlayerAge > 50 ? 20 : 0)` // Older smiths make durable weapons.
    *   **Create Log:**
        *   `event_type: "CRAFTED"`
        *   `actor_name: Player.Name`
        *   `description: "Forged during the [WeatherType]"`

## 3. History Viewer UI

*   **Inspector:** Upon right-click, iterate through `history_log` list.
*   **Display:** Instantiate `LogEntryPrefab` for each record.
    *   Text: "[Date] [Event] by [Actor]"
