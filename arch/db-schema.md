---
description: Design a new database table or entity schema before writing migrations
---

Design the database schema for $ARGUMENTS (entity name, feature, or description) before any migration is written.

**Table Definition**
```
Table: TableName

Columns:
  Id            — PK, IDENTITY / SERIAL
  [column]      — type, nullable/not null, default, constraints
  CreatedAt     — datetime, not null, default GETUTCDATE() / NOW()
  UpdatedAt     — datetime, nullable (set on update)
  CreatedBy     — FK to Users or string, not null
  IsDeleted     — bit/bool, default false (if soft delete applies)

Foreign Keys:
  FK_TableName_ReferencedTable_Column

Indexes:
  IX_TableName_Column — reason for index
  UQ_TableName_Column — unique constraint if applicable
```

**Design Decisions**
- Why this table structure over alternatives
- Soft delete vs hard delete decision
- Audit columns included or not (and why)

**Relationships**
- One-to-many or many-to-many
- Cascade behavior on delete (Restrict / SetNull / Cascade)
- Navigation properties in EF Core entity

**EF Core Entity Sketch**
```csharp
public class EntityName
{
    public int Id { get; set; }
    // properties
}
```

**Fluent API Configuration Sketch**
```csharp
// Key index and relationship configs
```

**Data Volume & Performance**
- Expected row count (hundreds / millions)
- Most frequent query patterns against this table
- Indexes designed for those query patterns

**Open Questions**
- Decisions that need team input before the migration is written

Output the full schema design ready for review. Do not write the actual migration yet.
