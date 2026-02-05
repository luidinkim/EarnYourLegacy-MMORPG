# [Design Spec] 6.3 Security & RLS Mechanics
**Parent Module:** [06_Tech_Architecture](../06_Tech_Architecture/README.md)

## 1. Row Level Security (RLS)
SpacetimeDB의 RLS는 "누가 어떤 데이터를 볼 수 있는가?"를 정의합니다.

### 1.1 Default Policy (Private)
*   **Inventory:** 오직 소유자(Owner)만 `SELECT` 가능.
*   **Will (유언장):** 작성자와 공증인만 `SELECT` 가능.
*   **Status:** 기본 스탯은 공개, 히든 트성(Trait)은 본인만 확인 가능.

## 2. Information Warfare (Gameplay RLS)
게임 내 스킬이나 아이템을 통해 RLS 정책을 일시적으로 우회할 수 있습니다.

### 2.1 Spy Skill: Eavesdrop
*   **Logic:**
    ```rust
    fn eavesdrop(ctx: ReducerContext, target_id: Identity) {
        if roll_dice(ctx) > success_rate {
            // Grant temporary read access to target's ChatLogs table
            RLS::grant_access(ctx.sender, target_id, Table::ChatLogs, Duration::10min);
        }
    }
    ```
*   **Effect:** 대상의 귓속말 내역을 10분간 엿볼 수 있음.

### 2.2 Forensic Science (과학 수사)
*   시체 조사 스킬 사용 시, 사망 원인과 킬러의 흔적(Log)에 대한 `READ` 권한 획득.

## 3. Anti-Cheat
*   모든 중요한 로직은 서버(Reducer)에서 검증되므로 클라이언트 변조(Speed Hack 등)는 롤백 처리됨.
