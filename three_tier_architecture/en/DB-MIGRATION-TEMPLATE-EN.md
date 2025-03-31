## Requirements
Create migration files based on the given business model.

## Business Model
```mermaid
classDiagram
direction TB

    class [EntityClass] {
        +[AttributeType] [attributeName]
        +[AttributeType] [attributeName]
        ...
    }

    [Relationship description]
```

## Tasks
- Create a migration file for the `[EntityClass]` entity.
  - File name: V[YearMonthDayHourMinuteSecond]__[description].sql
  - Table name: [tableName]
- ...

## Constraints
- Migration files should be placed in the `src/main/resources/db/migrations` directory.
- Migration files should be named following the format `V[YearMonthDayHourMinuteSecond]__[description].sql`.
- If there is an inheritance relationship, all inherited fields should be written in the child entity. 