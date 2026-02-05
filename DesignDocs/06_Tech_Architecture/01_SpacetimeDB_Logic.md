# [Design Spec] 6.1 SpacetimeDB & Logic-in-Database
**Parent Module:** [06_Tech_Architecture](../06_Tech_Architecture/README.md)

## 1. Architecture Philosophy
전통적인 [Client - Server - DB] 3티어 구조를 탈피하고, [Client - SpacetimeDB] 2티어 구조를 사용합니다.

## 2. Why SpacetimeDB?
*   **Zero Latency Logic:** 이동, 전투, 법률 체크 등 빈번한 로직이 DB 내부 메모리에서 즉시 연산됩니다. Round-trip이 없습니다.
*   **Relational State:** 게임의 모든 상태(위치, HP, 인벤토리)가 SQL 테이블로 존재하므로 복잡한 쿼리("반경 100m 내의 모든 빨간 옷을 입은 전사")가 가능합니다.

## 3. Rust Modules (Server-Side Logic)

### 3.1 Reducers (Action Handlers)
```rust
#[spacetimedb(reducer)]
pub fn move_player(ctx: ReducerContext, new_pos: Vector3) {
    // 1. Fetch current statutes (Laws) for the region
    let laws = LawTable::filter_by_region(new_pos);
    
    // 2. Validate move against laws (Atomic Check)
    for law in laws {
        if !law.evaluate(ctx.sender, new_pos) {
            return; // Move blocked by law
        }
    }
    
    // 3. Update Position
    let mut player = Player::filter_by_identity(ctx.sender).unwrap();
    player.position = new_pos;
    Player::update_by_identity(ctx.sender, player);
}
```

## 4. Client Synchronization
*   **Subscription:** 클라이언트는 SQL 쿼리 형태로 필요한 데이터만 구독합니다.
*   **Prediction:** 클라이언트에서 선행 예측(Prediction) 후, DB의 Reducer 결과와 다를 경우 롤백(Reconciliation)합니다.
