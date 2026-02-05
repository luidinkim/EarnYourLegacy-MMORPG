# [Design Spec] 6.2 Data Schema (Hybrid Graph)
**Parent Module:** [06_Tech_Architecture](../06_Tech_Architecture/README.md)

## 1. Schema Overview
관계형 데이터(SQL)와 그래프 데이터(Graph)를 혼합하여 설계합니다.

## 2. SQL Tables (Entities)
```sql
TABLE Characters {
    id: u64,
    owner_identity: Identity,
    name: String,
    age: u8,
    legacy_score: u32,
    genome: JSON
}

TABLE Items {
    uuid: u128,
    template_id: u32,
    durability: u8,
    provenance_blob: Blob // History Log 압축 데이터
}

TABLE Laws {
    id: u64,
    region_id: u32,
    logic_code: String, // AST 형태의 로직
    enforcement_tier: Enum
}
```

## 3. Edge Tables (Relationships)
가문과 아이템의 이동 경로를 추적하기 위한 그래프 엣지 테이블입니다.

```sql
TABLE Lineage_Edge {
    from_node: u64 (CharacterID),
    to_node: u64 (CharacterID),
    relation_type: Enum (PARENT_OF, KILLED, MENTORED)
}

TABLE Item_History_Edge {
    item_uuid: u128,
    from_owner: u64,
    to_owner: u64,
    transfer_type: Enum (TRADE, LOOT, INHERIT)
}
```
*   **Query Example:** "나의 검(uuid:123)이 거쳐간 모든 주인의 이름을 시간순으로 나열하시오."
