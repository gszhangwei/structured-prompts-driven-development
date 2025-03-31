## Requirements
Implement an API endpoint for updating `[entity name]`.

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
- [RequestClass] "1" -- "1" [EntityName] : updates
```

## Solution
1. API Design:
   - Create PUT endpoint `/api/v1/[entityNamePlural]/{id}` for updating existing [Entity Name]
   - Implement optimistic locking to prevent concurrent update conflicts
   - Return appropriate HTTP status codes for success and error cases
   - [Special handling logic, if any]
   - [Data validation logic, if any]

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

### Create [UpdateRequestClass] class
  1. Attributes:
     - [attributeName]: [attributeType] (required/optional)
     - [attributeName]: [attributeType] (required/optional)
     - version: Integer (required, for optimistic locking)
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Validation:
     - version: @NotNull
     - [Other validation annotations]

### Update [EntityClass]Controller class to implement update API
  1. Endpoint: `/api/v1/[entityNamePlural]/{id}`
     1. Method: PUT
     2. Path Variables:
        - id: String (required)
     3. Request Body: [UpdateRequestClass]
     4. Response Body: Returns data of type [ResponseClass]
     5. Logic:
        - Call [entityClassLowerCase]Service.update[EntityClass](id, request)
        - Map updated [EntityClass] entity to [ResponseClass] DTO
        - Return 200 OK status code and the updated data
        - If id does not exist, return 404 Not Found
        - If version does not match, return 409 Conflict
        - If request body is invalid, return 400 Bad Request

### Update [EntityClass]Service interface to add update method
  1. Add method: update[EntityClass](String id, [UpdateRequestClass] request): [EntityClass]

### Update [EntityClass]ServiceImpl class to implement update logic
  1. Implement update[EntityClass] method:
     - Logic:
       - Call [entityClassLowerCase]Repository.findById(id) to retrieve existing entity
       - If entity does not exist, throw EntityNotFoundException
       - Check if version matches, if not, throw OptimisticLockException
       - Update entity attributes
       - Increment version number
       - Update updatedAt timestamp
       - Call [entityClassLowerCase]Repository.save(entity) to save the updated entity
       - Return the updated [EntityClass] object

### Update [EntityClass]Repository interface to add update method
  1. Add method: findById(String id): Optional<[EntityClass]>

### Update [EntityClass]RepositoryImpl class to implement update logic
  1. Implement findById method:
     - Logic:
       - Call [entityClassLowerCase]DAO.findById(id) to retrieve entity
       - If entity exists, convert [EntityClass]PO to [EntityClass]
       - Return Optional<[EntityClass]>

## Common Tasks
1. All repository implementation classes should be annotated with @Repository
2. All Repository classes should implement JPA repository
3. All Service classes should be annotated with @Service
4. All Controller classes should be annotated with @RestController
5. All DTO and model classes should be annotated with @Data

## Constraints
- If id does not exist, return 404 Not Found
- If version does not match, return 409 Conflict
- If request body is invalid, return 400 Bad Request
- After successful update, return 200 OK status code
- Must update updatedAt timestamp
- Must increment version number to support optimistic locking
- [Other specific constraints] 