## Requirements
Implement an API endpoint for creating new `[entity name]`.

## Business Model
```
Class Diagram:

[EntityName] {
    +String id
    +[OtherPropertyType] [otherPropertyName]
    +timestamp createdAt
    +timestamp updatedAt
}

[RequestClass] {
    +[PropertyType] [propertyName]
    +[PropertyType] [propertyName]
    ...
}

[ResponseClass] {
    +String id
    +[PropertyType] [propertyName]
    +timestamp createdAt
    +timestamp updatedAt
    ...
}

Relationships:
- [EntityName] "1" -- "1" [ResponseClass] : maps to
- [RequestClass] "1" -- "1" [EntityName] : creates
```

## Solution
1. API Design:
   - Create POST endpoint `/api/v1/[entityNamePlural]` for creating new [Entity Name]
   - Return appropriate HTTP status codes for success and error cases
   - [Special handling logic, if any]

2. Idempotency Implementation:
   - Add unique identifiers to requests (such as client-generated UUID or business unique keys)
   - Add unique constraints in the database (such as name+owner combination or other business unique keys)
   - Implement checking logic in the service layer to avoid duplicate creation
   - For duplicate requests, return the existing resource instead of creating a new one
   - Implementation approaches:
     - Approach 1: Use natural business keys (e.g., add findBy[BusinessKey] method in [EntityClass]DAO)
     - Approach 2: Use request ID (e.g., add idempotencyKey parameter and store processed request IDs)
     - Approach 3: Use conditional checks (e.g., check if resource already exists before creation)
   
   - Idempotency implementation approach recommendations:
     - For simple business cases: Prefer Approach 1 (natural business keys) or Approach 3 (conditional checks), as they are straightforward to implement
     - For complex business cases with performance requirements: Prefer Approach 2 (request ID), as it can avoid duplicate business logic processing and improve performance
     - In practice, multiple approaches can be combined based on specific requirements to provide stronger idempotency guarantees

## Structure

### Inheritance
1. [EntityClass]Service interface defines [EntityClass] service methods
2. [EntityClass]ServiceImpl implements [EntityClass]Service interface
3. [EntityClass]Repository interface defines [EntityClass] repository methods
4. [EntityClass]RepositoryImpl implements [EntityClass]Repository interface

### Dependencies
1. [EntityClass]Controller calls [EntityClass]Service
2. [EntityClass]ServiceImpl calls [EntityClass]Repository
3. [EntityClass]RepositoryImpl calls [EntityClass]DAO

## Tasks

### Create [EntityClass] class (Domain Model)
  1. Attributes:
     - id: String
     - [otherAttributeName]: [otherAttributeType]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Add static method: fromRequest([RequestClass] request): [EntityClass]
     - Logic:
       - Return a new [EntityClass] object with id set to a newly generated UUID
       - Extract and set other attributes from the request
  4. Add static method: fromPO([EntityClass]PO po): [EntityClass]
     - Logic:
       - Convert persistence object to domain model object

### Create [EntityClass]PO class (Persistence Model)
  1. Attributes:
     - id: String
     - [otherAttributeName]: [otherAttributeType]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. Add unique constraint:
     - Use @Table(uniqueConstraints = @UniqueConstraint(columnNames = {"[businessKeyField1]", "[businessKeyField2]"})) annotation
  3. Add static method: of([EntityClass] entity): [EntityClass]PO
     - Logic:
       - Convert domain model object to persistence object

### Create [RequestClass] class
  1. Attributes:
     - [attributeName]: [attributeType] (required/optional)
     - [attributeName]: [attributeType] (required/optional)
     - [If using Approach 2] idempotencyKey: String (for idempotency control)
     - ...
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Validation:
     - [requiredAttribute]: @NotBlank/@NotNull
     - [Other validation annotations]

### Create [ResponseClass] class
  1. Attributes:
     - id: String
     - [otherAttributeName]: [otherAttributeType]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Add static method: of([EntityClass] entity): [ResponseClass]
     - Logic:
       - Map domain model object to response object
       - Return response object

### Create [EntityClass]Controller class to implement creation API
  1. Endpoint: `/api/v1/[entityNamePlural]`
     1. Method: POST
     2. Request Body: [RequestClass]
     3. Response Body: Returns data of type [ResponseClass]
     4. Logic:
        - Call [entityClassLowerCase]Service.create[EntityClass](request)
        - Map [EntityClass] entity to [ResponseClass] DTO
        - Return 201 Created status code and the created data
        - If request body is missing required fields, return 400 Bad Request
        - If resource already exists (idempotency check), return 200 OK and the existing resource
        - [Other error handling logic]

### Create [EntityClass]Service interface
  1. Add method: create[EntityClass]([RequestClass] request): [EntityClass]

### Create [EntityClass]ServiceImpl class to implement creation logic
  1. Implement create[EntityClass] method:
     - Logic:
       - [Data validation logic, if any]
       - [If using Approach 1] Check if resource already exists by business key, if it does, return existing resource
       - [If using Approach 2] Check if idempotencyKey has been processed, if it has, return previous result
       - [If using Approach 3] Check if resource already exists based on conditions, if it does, return existing resource
       - Create new [EntityClass] object using [EntityClass].fromRequest(request)
       - Set necessary fields (id, createdAt, updatedAt, etc.)
       - [Null check logic, if any]
       - Call [entityClassLowerCase]Repository.save(entity) to save the entity
       - [If using Approach 2] Record the processed idempotencyKey and corresponding resource ID
       - Return the saved [EntityClass] object

### Create [EntityClass]Repository interface
  1. Add method: save([EntityClass] entity): [EntityClass]
  2. [If using Approach 1 or 3] Add method: findBy[BusinessKey]([BusinessKeyType] [businessKey]): Optional<[EntityClass]>

### Create [EntityClass]RepositoryImpl class to implement storage logic
  1. Implement save method:
     - Logic:
       - Convert [EntityClass] entity to [EntityClass]PO using [EntityClass]PO.of(entity)
       - Call [entityClassLowerCase]DAO.save(po) to save the entity
       - Convert saved [EntityClass]PO back to [EntityClass] entity using [EntityClass].fromPO(po)
       - Return the saved [EntityClass] object
  2. [If using Approach 1 or 3] Implement findBy[BusinessKey] method:
     - Logic:
       - Call [entityClassLowerCase]DAO.findBy[BusinessKey]([businessKey]) to find the entity
       - If found, convert [EntityClass]PO to [EntityClass]
       - Return Optional<[EntityClass]>

### Create [EntityClass]DAO interface
  1. Extend JpaRepository<[EntityClass]PO, String>
  2. [If using Approach 1 or 3] Add method: findBy[BusinessKey]([BusinessKeyType] [businessKey]): Optional<[EntityClass]PO>

### [If using Approach 2] Create IdempotencyKeyRepository interface and implementation class
  1. For storing and checking processed idempotency keys
  2. Add method: save(String key, String resourceId): void
  3. Add method: findByKey(String key): Optional<String>

## Common Tasks
1. All repository implementation classes should be annotated with @Repository
2. All Repository classes should implement JPA repository
3. All Service classes should be annotated with @Service
4. All Controller classes should be annotated with @RestController
5. All DTO and model classes should be annotated with @Data
6. All POJO classes should be annotated with @Data, @Entity, @Table, @AllArgsConstructor, @NoArgsConstructor

## Constraints
- If request body is missing required fields, return 400 Bad Request
- After successful creation, return 201 Created status code
- If resource already exists (idempotency check), return 200 OK and the existing resource
- Manually generate a unique ID for the entity, do not rely on database auto-generation
- Initialize collections as empty lists to prevent null pointer exceptions
- Add unique constraints at the database level to ensure idempotency
- [Other specific constraints] 