## Requirements
Implement an API endpoint for querying `[entity name]`.

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
- [RequestClass] "1" -- "*" [EntityName] : queries
```

## Solution
1. API Design:
   - Create GET endpoint `/api/v1/[entityNamePlural]` for retrieving [Entity Name] by criteria
   - [If retrieval by IDs is needed] Create GET endpoint `/api/v1/[entityNamePlural]/ids` for retrieving [Entity Name] by IDs
   - Implement pagination for large result sets
   - Support sorting by different fields
   - Return appropriate HTTP status codes for success and error cases

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

### Create [EntityClass]QueryParams class
  1. Attributes:
     - `[queryParamName]`: `[paramType]`
     - `[queryParamName]`: `[paramType]`
     - page: Integer
     - size: Integer
     - sortBy: String
     - sortDirection: String
  2. Constructor:
     - Use @AllArgsConstructor annotation
     - Default values:
       - page: 0
       - size: 10
       - sortBy: "createdAt"
       - sortDirection: "DESC"

### Create [EntityClass]Response class
  1. Attributes:
     - id: String
     - `[otherAttributeName]`: `[otherAttributeType]`
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Add static method: of(List<[EntityClass]> entities): List<[EntityClass]Response>
     - Logic:
       - Map List<[EntityClass]> to List<[EntityClass]Response>
       - Return the list of [EntityClass]Response

### Create Paged[EntityClass]Response class
  1. Attributes:
     - content: List<[EntityClass]Response>
     - totalPages: Integer
     - totalElements: Long
     - size: Integer
     - number: Integer
     - first: Boolean
     - last: Boolean
  2. Constructor:
     - Use @AllArgsConstructor annotation
  3. Add static method: of(Page<[EntityClass]> page): Paged[EntityClass]Response
     - Logic:
       - Map Page<[EntityClass]> to Paged[EntityClass]Response
         - Set content to [EntityClass]Response.of(page.getContent())
         - Set totalPages to page.getTotalPages()
         - Set totalElements to page.getTotalElements()
         - Set size to page.getSize()
         - Set number to page.getNumber()
         - Set first to page.isFirst()
         - Set last to page.isLast()
       - Return the Paged[EntityClass]Response

### Update [EntityClass]Controller class to implement retrieval API
  1. [If retrieval by IDs is needed] Endpoint: `/api/v1/[entityNamePlural]/ids`
     1. Method: GET
     2. Request Parameters:
        - ids: List<String> (required)
     3. Response Body: Returns data of type List<[EntityClass]Response>
     4. Logic:
        - Call [entityClassLowerCase]Service.get[EntityClass]sByIds(ids)
        - Map [EntityClass] entities to [EntityClass]Response DTOs
        - Return 200 OK status code and the list of [EntityClass]Response
        - If ids parameter is empty or invalid, return 400 Bad Request
  
  2. Endpoint: `/api/v1/[entityNamePlural]`
     1. Method: GET
     2. Request Parameters:
        - [queryParamName]: [paramType] (optional) - [paramDescription]
        - [queryParamName]: [paramType] (optional) - [paramDescription]
        - page: Integer (optional, default: 0)
        - size: Integer (optional, default: 10)
        - sortBy: String (optional, default: "createdAt")
        - sortDirection: String (optional, default: "DESC")
     3. Response Body: Returns data of type Paged[EntityClass]Response
     4. Logic:
        - Call [entityClassLowerCase]Service.get[EntityClass]sByCriteria(queryParams)
        - Map Page<[EntityClass]> to Paged[EntityClass]Response
        - Return 200 OK status code and the retrieved data
        - If query parameters are invalid, return 400 Bad Request
        - If no records match the criteria, return an empty list

### Update [EntityClass]Service interface to add retrieval methods
  1. [If retrieval by IDs is needed] Add method: get[EntityClass]sByIds(List<String> ids): List<[EntityClass]>
  2. Add method: get[EntityClass]sByCriteria([EntityClass]QueryParams queryParams): Page<[EntityClass]>

### Create [EntityClass]CriteriaBuilder class
  1. Add static method: buildPageableInfo([EntityClass]QueryParams queryParams): Pageable
     - Logic:
       - Validate page and size parameters
       - Create Sort object based on sortBy and sortDirection
       - Return PageRequest with page, size, and sort information
  2. Add static method: buildSpecification([EntityClass]QueryParams queryParams): Specification<[EntityClass]PO>
     - Logic:
       - Create Specification for each query parameter
       - Combine specifications with AND operator
       - Return the combined specification
       - If no criteria are provided, return a default specification
   
### Update [EntityClass]ServiceImpl class to implement retrieval logic
  1. [If retrieval by IDs is needed] Implement get[EntityClass]sByIds method:
     - Call [entityClassLowerCase]Repository.findAllByIdIn(ids) to retrieve entities
     - Return list of [EntityClass] objects
  2. Implement get[EntityClass]sByCriteria method:
     - Create pageable based on query parameters using [EntityClass]CriteriaBuilder
     - Call [entityClassLowerCase]Repository.findAll(queryParams, pageable) to retrieve paged entities
     - Return Page<[EntityClass]> object

### Update [EntityClass]Repository interface to add retrieval methods
  1. [If retrieval by IDs is needed] Add method: findAllByIdIn(List<String> ids): List<[EntityClass]>
  2. Add method: findAll([EntityClass]QueryParams queryParams, Pageable pageable): Page<[EntityClass]>

### Update [EntityClass]RepositoryImpl class to implement retrieval logic
  1. [If retrieval by IDs is needed] Implement findAllByIdIn method:
     - Call [entityClassLowerCase]DAO.findAllById(ids) to retrieve entities
     - Return list of [EntityClass] entities
  2. Implement findAll method with queryParams and pageable:
     - Create specification based on query parameters using [EntityClass]CriteriaBuilder
     - Call [entityClassLowerCase]DAO.findAll(specification, pageable) to retrieve paged entities
     - Map [EntityClass]PO entities to [EntityClass] domain objects
     - Return Page<[EntityClass]> object

### Update [EntityClass]DAO interface to add retrieval methods
  1. Extend JpaSpecificationExecutor<[EntityClass]PO>

## Common Tasks
1. All repository implementation classes should be annotated with @Repository
2. All Repository classes should implement JPA repository
3. All Service classes should be annotated with @Service
4. All Controller classes should be annotated with @RestController
5. All DTO and model classes should be annotated with @Data

## Constraints
- If query parameters are invalid (e.g., negative page or invalid sortBy/sortDirection values), return 400 Bad Request
- If no records match the criteria, return an empty list
- Default page is 0 if not specified
- Default page size is 10 if not specified
- Default sort is by createdAt in descending order if not specified
- Maximum page size is 100 to prevent performance issues
- Sorting is only supported for specific fields (such as name, createdAt, etc.)
- [Specific field] filtering supports partial matching (contains)
- [Specific field] filtering supports exact matching 