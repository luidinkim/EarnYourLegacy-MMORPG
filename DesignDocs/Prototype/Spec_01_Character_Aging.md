# Tech Spec: Prototype Character System (Identity & Aging)

## 1. Data Schema (C# Serializable Class)

```csharp
[System.Serializable]
public class CharacterData {
    public string uuid;
    public string name;
    public int age_tickets; // 1 tick = 1 in-game year (or day)
    public GeneticTrait[] traits;
    public float current_hp;
    public float max_hp;
    public bool is_dead;
    public long created_timestamp;
    public long death_timestamp;
}

[System.Serializable]
public class GeneticTrait {
    public string id; // e.g., "heavy_bones"
    public string display_name;
    public StatModifier[] modifiers;
}
```

## 2. Aging Logic (AgingManager.cs)

*   **Tick Rate:** 60 seconds (Realtime) = 1 Year (Game Time).
*   **Logic:**
    *   `Update()` loop checks `Time.deltaTime`.
    *   Every 60s -> `age_tickets++`.
    *   **Phase Check:**
        *   `IF age > 20`: Apply `Prime` buff.
        *   `IF age > 50`: Apply `MiddleAge` debuff (Str -1).
        *   `IF age > 75`: Apply `Elder` debuff (HP Max -30%).
        *   `IF age > 90`: Trigger `DeathEvent(Natural)`.

## 3. Death Handler

*   **Method:** `public void KillCharacter(DeathType type)`
*   **Process:**
    1.  Set `is_dead = true`.
    2.  Capture `death_timestamp`.
    3.  Calculate `LegacyScore` based on (`age_tickets` * 10) + (`monster_kills` * 5).
    4.  Save entire `CharacterData` to `LegacyHistory.json`.
    5.  Trigger UI: "You Died. Your Legacy Score: [XXX]".
