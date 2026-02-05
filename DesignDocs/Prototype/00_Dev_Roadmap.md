# Development Roadmap: Prototype Alpha

**Goal:** "Life, Death, and Legacy" Core Loop Verification
**Timeline:** 1 Week (Estimated)

## Sprint 1: Foundation (Day 1-2)  
- [ ] **Project Setup:** Unity 6 + NetCode for GameObjects (or SpacetimeDB Local).
- [ ] **Data Managers:** Implement `CharacterManager`, `ItemManager`, `TimeManager`.
- [ ] **UI Base:** Setup MainMenu, GameHUD, InventoryUI.

## Sprint 2: The Core Loop (Day 3-4)
- [ ] **Feature: Aging:** Implement `TimeManager` tick system.
    - Verify HUD updates Age every minute.
    - Verify Traits are applied at specific ages.
- [ ] **Feature: Crafting:** Implement `Craft(Item)` function.
    - Verify `UUID` generation and `HistoryLog` creation.
- [ ] **Feature: Death:** Implement `KillCharacter()` logic.
    - Verify `JsonSaver` exports `LegacySnapshot.json`.

## Sprint 3: Inheritance & Polish (Day 5-6)
- [ ] **Feature: New Game+:** Implement `LoadSnapshot()` on character creation.
    - Verify new character starts with old item.
    - Verify item durability decay.
- [ ] **Polish:** Add simple visual cues (Grey hair for old age, Tombstone model).

## Sprint 4: Testing & Review (Day 7)
- [ ] **Playtest:** Complete full 10-minute life cycle loop.
- [ ] **Report:** Document feelings/feedback on the "Loss & Gain" mechanics.
