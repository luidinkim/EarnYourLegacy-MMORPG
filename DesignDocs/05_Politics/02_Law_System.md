# [Design Spec] 5.2 Law Editor & Enforcement
**Parent Module:** [05_Politics](../05_Politics/README.md)

## 1. Visual Logic Editor
유저는 Scratch나 Unreal Blueprint와 유사한 블록 코딩 인터페이스로 법을 작성합니다.

### 1.1 Logic Blocks
*   **Trigger (When):** `OnEnterZone`, `OnKill`, `OnGather`, `OnChat`, `OnTrade`.
*   **Condition (If):** `IsCitizen?`, `Level > 50`, `HoldingWeapon?`, `Wealth > 1000G`.
*   **Action (Then):** `BlockMove`, `TeleportJail`, `Fine(Amount)`, `AddBounty`, `Kill`.

## 2. Enforcement Tiers (집행 등급)

| Tier | Name | Cost | Reliability | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Tier 1** | **Sheriff (인력)** | Low | Low | 유저 보안관에게 체포 권한 부여. 보안관이 부패하거나 게으르면 법이 작동 안 함. |
| **Tier 2** | **AI Guard (NPC)** | Mid | Mid | NPC 경비병 순찰. 매수 가능성 존재. |
| **Tier 3** | **Divine Law (시스템)** | High | Absolute | 서버가 직접 개입. 위법 행위 시 즉시 번개(System Kill) 또는 투명벽으로 막힘. (SpacetimeDB Logic) |

## 3. Loophole Gameplay (법의 허점)
완벽한 법은 없습니다. 유저들은 법의 로직 허점을 찾아 범죄를 저지를 수 있습니다.
*   *예:* "무기를 들고 있으면 체포" -> "무기를 바닥에 놓고 발로 차서 이동시킨 뒤 살인 직전에 줍는다."
*   입법자는 이러한 창의적 범죄를 막기 위해 법 코드를 지속적으로 디버깅(개정)해야 합니다.
