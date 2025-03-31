## Requirements
Implement an API endpoint for deleting `[entity name]`.

## Business Model(mermaid)
```
classDiagram
direction TB

    class [EntityClass] {
        +String id
        +[OtherAttributeType] [otherAttributeName]
        +timestamp createdAt
        +timestamp updatedAt
    }
```

## Solution
1. API Design:
   - Create DELETE endpoint `/api/v1/[entityNamePlural]/{id}` for deleting existing [Entity Name]
   - [Support soft delete/hard delete, based on requirements]
   - Return appropriate HTTP status codes for success and error cases
   - [Special handling logic, if any]

## Structure

### Inheritance/Implementation Relationships
1. [EntityClass]Service interface defines [EntityClass] service methods
2. [EntityClass]ServiceImpl implements [EntityClass]Service interface
3. [EntityClass]Repository interface defines [EntityClass] repository methods
4. [EntityClass]RepositoryImpl implements [EntityClass]Repository interface

### Dependencies
1. [EntityClass]Controller calls [EntityClass]Service
2. [EntityClass]ServiceImpl calls [EntityClass]Repository
3. [EntityClass]RepositoryImpl calls [EntityClass]DAO

## Tasks

### Update [EntityClass]Controller class to implement delete API
  1. Endpoint: `/api/v1/[entityNamePlural]/{id}`
     1. Method: DELETE
     2. Path Variables:
        - id: String (required)
     3. Response Body: No content
     4. Logic:
        - Call [entityClassLowerCase]Service.delete[EntityClass](id)
        - Return 204 No Content status code
        - If id does not exist, return 404 Not Found
        - [Other error handling logic]

### Update [EntityClass]Service interface to add delete method
  1. Add method: delete[EntityClass](String id): void

### Update [EntityClass]ServiceImpl class to implement delete logic
  1. Implement delete[EntityClass] method:
     - Logic:
       - Call [entityClassLowerCase]Repository.findById(id) to retrieve existing entity
       - If entity does not exist, throw EntityNotFoundException
       - [If soft delete] Update entity status to deleted
       - [If soft delete] Update updatedAt timestamp
       - [If soft delete] Call [entityClassLowerCase]Repository.save(entity) to save the updated entity
       - [If hard delete] Call [entityClassLowerCase]Repository.delete(id) to delete the entity

### Update [EntityClass]Repository interface to add delete method
  1. [If hard delete] Add method: delete(String id): void

### Update [EntityClass]RepositoryImpl class to implement delete logic
  1. [If hard delete] Implement delete method:
     - Logic:
       - Call [entityClassLowerCase]DAO.deleteById(id) to delete the entity

## Common Tasks
1. All repository implementation classes should be annotated with @Repository
2. All Repository classes should implement JPA repository
3. All Service classes should be annotated with @Service
4. All Controller classes should be annotated with @RestController
5. All DTO and model classes should be annotated with @Data

## Constraints
- If id does not exist, return 404 Not Found
- After successful deletion, return 204 No Content status code
- [If soft delete] Must update updatedAt timestamp
- [If there are associated entities] Must handle associated entities
- [Other specific constraints] 