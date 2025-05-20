## Requirements
[Brief description of the data transformation requirements and goals]

## Data Model
```
classDiagram
direction TB
class [TableName1] {
+[DataType] field1
+[DataType] field2
...
}

class [TableName2] {
    +[DataType] field1
    +[DataType] field2
    ...
}
...
class [TableNameN] {
    +[DataType] field1
    +[DataType] field2
    ...
}
[TableName1] -- [TableName2] : "[Relationship]"
...
```
## Solution
1. Data Association Design:
   - [Describe how to associate/join data]
   - [Mention techniques like UNION ALL, JOIN types]
   - [Explain matching criteria and levels]

2. Data Processing Design:
   - Data Extension
     - [Explain expansion logic]
   - Data Enrichment
     - [Explain data filling strategy]
   - Field Standardization
     - [Explain normalization rules]

3. Data Aggregation Design:
   - [Explain aggregation methods]
   - [Mention grouping strategy]
   - [Describe deduplication approach]

## Structure
### Dependencies
1. [Describe data flow dependencies between tables]
2. [Explain hierarchical relationships]
3. [Note fallback data sources]

## Tasks

### Create `[IntermediateTable1]` CTE
1. Function: 
   - `[Describe the purpose of this intermediate table]`
2. Fields:
   - `[Field list with data types]`
   - `[Explain derived/calculated fields]`
3. Implementation Logic:
   - `[Detail the data selection criteria]`
   - `[Explain aggregation methods]`
   - `[Describe transformation rules]`

### Create `[IntermediateTableN]` CTE
1. Function:
    - `[Describe the purpose of this intermediate table]`
2. Fields:
    - `[Field list with data types]`
    - `[Explain derived/calculated fields]`
3. Implementation Logic:
    - `[Detail the data selection criteria]`
    - `[Explain aggregation methods]`
    - `[Describe transformation rules]`

`[Additional intermediate tables as needed...]`

### Create Final Output Table
1. Function:
   - [Describe the final consolidated output]
2. Fields:
   - [List final output fields]
3. Implementation Logic:
   - `[Explain final sorting order]`
   - `[Detail final transformations]`
   - `[Describe output structure]`

## Common Tasks
1. `[Field naming conventions]`
2. `[NULL handling approach]`
3. `[Date/time handling practices]`
4. `[Joining best practices]`
5. `[Table alias usage guidelines]`
6. `[Data merging techniques]`
7. `[Deduplication methods]`

## Constraints
- `[SQL syntax limitations]`
- `[Query structure restrictions]`
- `[Join limitations]`
- `[Subquery limitations]`
- `[Performance considerations]`
- `[Naming conventions]`

