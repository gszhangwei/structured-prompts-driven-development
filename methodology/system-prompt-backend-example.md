First understand the memory content, then generate specific structured prompts based on the seven-step framework combined with user_message

---

# Team Memory
### 3990836
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** Business-Process, Resource-Lifecycle, Multi-Type-Operations, Type-Routing, Change-Logging

Complete business process flow for managing Rule and Solution resources through unified PromptController:

1) **Resource Creation**: POST /prompts → validate request → extract user from UserContext → determine type from request.type → select service via PromptServiceSelector → generate prefixed ID → create resource → return PromptResponse with 201

2) **Resource Update**: PUT /prompts/{id} → extract type from ID prefix → validate permission (creator == current user) → update via specific service → record change log → return updated PromptResponse

3) **Resource Deletion**: DELETE /prompts/{id} → infer type from ID → check workflow references → validate permission → record deletion in change log → delete resource → return 204

4) **Batch Retrieval**: GET /prompts/ids → group IDs by type → parallel query multiple services → merge results maintaining order → return List<PromptResponse>

5) **Criteria Query**: GET /prompts?type=X → select service by type → apply filters/pagination → return PagedPromptResponse

All operations follow automatic type routing pattern with service selector delegation.

---

# Team Memory
### WF_API_001
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐
**Tags:** REST-API, CRUD-Operations, HTTP-Status-Codes, Service-Delegation, Error-Handling

WorkflowController implements comprehensive REST API pattern for workflow lifecycle management:

1) **Complete CRUD operations**: POST /workflows (create), GET /workflows (query with criteria), GET /workflows/ids (batch retrieval), GET /workflows/{name} (exact name lookup), POST /workflows/check-updates (update validation)
2) **Dual path mapping**: Supports both `/api/v1/workflows` and `/app/workflows` for API versioning and application routing
3) **Request validation**: @Valid annotation ensures WorkflowRequest integrity with proper error responses
4) **Response standardization**: All endpoints return consistent WorkflowResponse or PagedWorkflowResponse DTOs
5) **HTTP status codes**: 201 Created for creation, 200 OK for retrieval, 400 Bad Request for validation errors, 404 Not Found for missing resources
6) **Parameter validation**: IDs list limited to 100 items max, empty parameters trigger 400 errors
7) **Service delegation**: Controller focuses on HTTP concerns while delegating business logic to WorkflowService
8) **Error propagation**: Exceptions from service layer automatically handled by GlobalExceptionHandler

---

# Team Memory
### 3990827
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐
**Tags:** Unified-API, Multi-Type-Management, ID-Prefix-Strategy, Service-Selector, CRUD-Operations

PromptController implements a unified API pattern for managing heterogeneous resource types (Rule/Solution) through a single controller interface. Key components:

1) **PromptServiceSelector pattern** routes requests to appropriate service implementations based on ID prefix or type parameter
2) **Unified DTOs** (PromptResponse, PromptCreateRequest, PromptUpdateRequest) handle type-specific data with polymorphic factory methods
3) **ID prefix strategy** ("r_" for Rule, "s_" for Solution) enables automatic type inference
4) **Generic PromptService interface** with type-specific implementations (RuleService, SolutionService)
5) **Batch operations** group IDs by type for efficient processing
6) **UserContext integration** for permission validation and auto-filling creator fields
7) **Full CRUD operations** (POST /, PUT /{id}, DELETE /{id}, GET /ids, GET /) with consistent validation and error handling

---

# Team Memory
### WF_CREATE_001
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** Business-Process, Step-Validation, Cross-Type-Validation, Idempotency, User-Enrichment

WorkflowServiceImpl implements comprehensive workflow creation process with multi-type step validation:

1) **User enrichment**: enrichWithUserEmail() auto-fills owner from UserContext when not provided, maintaining backward compatibility
2) **Cross-type validation**: validateStepsExist() supports both Rule ("r_" prefix) and Solution ("s_" prefix) references via PromptServiceSelector
3) **Batch dependency checking**: Groups step IDs by type for efficient parallel validation across RuleService and SolutionService
4) **Idempotency protection**: findByNameAndOwner() prevents duplicate workflows with same name+owner combination
5) **Null safety**: orderedSteps defaults to empty ArrayList when not provided in request
6) **Error aggregation**: InvalidStepReferenceException includes all invalid step IDs with specific type information
7) **Atomic operations**: Either all validations pass and workflow is created, or transaction fails with detailed error
8) **Entity generation**: Workflow.fromRequest() creates domain object with UUID, timestamps, and validated steps

---

# Team Memory
### 3990867
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐
**Tags:** DTO-Pattern, Multi-Type-Response, Polymorphic-Factory, Type-Metadata, Auto-Population

PromptController uses unified DTO pattern to handle multiple resource types through single API interface:

1) **Base DTO classes**: PromptResponse, PagedPromptResponse, PromptCreateRequest include common fields plus type metadata
2) **Type information**: Each response includes both PromptType enum and typeDisplayName string for client flexibility
3) **Polymorphic factory methods**: PromptResponse.of(Entity, Type), of(Entity, String), of(Entity) with automatic type inference from ID prefix
4) **Type-specific fields**: Level for Rule resources, Solution.Type for Solution resources included conditionally
5) **Request conversion**: PromptCreateRequest.toPrompt(type, userEmail) creates appropriate entity based on type parameter
6) **Consistent pagination**: PagedPromptResponse wraps any Page<? extends Prompts> with type information
7) **Backward compatibility**: DTOs maintain type information for client-side routing and processing
8) **Auto-population support**: Creator field auto-filled from UserContext when not provided in requests

---

# Seven-Step Framework Template Content


# Requirements Anchoring (Requirements)

## Objective
Extract the core problem essence and fundamental goals from requirement descriptions

## Output Format
```
## Requirements
[Use concise verb phrases to describe the essence of requirements, avoid feature enumeration]
```

## Key Construction Points
- **Essence Extraction**: Abstract what fundamental problem is being solved and what value is created for whom
- **Boundary Definition**: Clarify the applicable scope and limitations of the solution
- **Value Focus**: Highlight business value and user benefits
- **Use Verb Phrases**: Such as "Implement...", "Create...", "Design..."
- **Avoid Feature Listing**: Don't enumerate specific features, but abstract the essential problems that need to be solved

## Quality Standards
- Core requirements can be summarized in one sentence
- Reflects business value rather than technical implementation
- Clear problem boundaries and constraints

---

# Business Model

## Objective
Build a clear business entity relationship model to provide conceptual foundation for subsequent design

## Output Format
```
## Business Model
```mermaid
classDiagram
direction TB

class [CoreEntity] {
    +[AttributeType] [attributeName]
    +[AttributeType] [attributeName]
    +[Method]()
}

class [RelatedEntity] {
    +[AttributeType] [attributeName]
    +[Method]()
}

class [RequestDTO] {
    +[AttributeType] [attributeName]
    +[ValidationRule]
}

class [ResponseDTO] {
    +[AttributeType] [attributeName]
    +[StaticMethod]()
}

[CoreEntity] "[cardinality]" -- "[cardinality]" [RelatedEntity] : [relationshipDesc]
[RequestDTO] --> [CoreEntity] : creates
[CoreEntity] --> [ResponseDTO] : maps to
```

## Key Construction Points
- **Entity Identification**: Identify core business entities, supporting entities, and DTO objects
- **Attribute Modeling**: Define key attributes for each entity using "Type + Name" format
- **Relationship Modeling**: Clarify relationship types (1:1, 1:N, N:M) and business semantics between entities
- **Existing Implementation Priority**: If current data structures can meet requirements, must keep existing implementation unchanged
- **Minimal Change Principle**: Only refactor when existing structures truly cannot support new requirements
- **Interface Design**: Include key methods and static factory methods
- **Data Flow**: Reflect complete data flow of request->processing->response
- **Consistency Assurance**: Ensure the model can be accurately understood and implemented by AI
- **Simplicity > Feature-rich**: Avoid over-engineering, maintain system understandability

## Conservative Constraints
- **Prohibit Unnecessary Refactoring**: If existing simple data types (like List<String>) can meet requirements, strictly forbid creating complex entity wrappers
- **Function-driven Changes**: Only consider structural adjustments when clear functional requirements cannot be implemented through existing structures
- **Progressive Improvement**: Prioritize extending based on existing structures rather than rebuilding from scratch
- **Backward Compatibility**: Any structural changes must ensure backward compatibility and avoid breaking changes

## Quality Standards
- Focus on current task flow
- Clear and accurate entity relationships
- Support subsequent technical implementation
- Maintain simplicity of existing implementation
- Avoid over-abstraction and unnecessary complexity

---

# Solution

## Objective
Provide high-level solution strategies and architectural approaches to guide specific implementation

## Output Format
```
## Solution
1. [Solution Category]:
   - [High-level strategy description]
   - [Architecture pattern or approach]
   - [Key design decisions and rationale]
   - [Alternative approaches consideration]

2. [Technical Implementation]:
   - [Framework or technology choice]
   - [Integration pattern]
   - [Performance and security considerations]
   - [Global exception handling strategy with GlobalExceptionHandler]

3. [Business Logic]:
   - [Core business rules]
   - [Validation and error handling strategy]
   - [Workflow and process design]
```

## Key Construction Points
- **Categorical Organization**: Organize by solution categories (such as API design, data processing, exception handling, etc.)
- **Architectural Decisions**: Provide key technical architecture choices and design patterns
- **Best Practices**: Combine industry standards and experience summaries
- **Decision Rationale**: Explain why specific solutions are chosen
- **Risk Assessment**: Identify potential risks and response strategies

## Quality Standards
- Solutions are actionable
- Cover key technical decisions
- Reflect architectural thinking

---

# Structure Definition (Structure)

## Objective
Define the technical architecture and component dependency relationships of the system

## Output Format
```
## Structure

### Inheritance Relationships
1. [Interface] interface defines [functionality description]
2. [Implementation] implements [Interface] interface
3. [DomainModel] extends [BaseModel] class
4. [Controller] extends [BaseController] class
5. [BusinessException] extends RuntimeException class (Business exception base class)
6. [SpecificBusinessException] extends [BusinessException] class (Specific business exception class)

### Dependencies
1. [ComponentA] calls [ComponentB]
2. [Service] depends on [Repository] and [ExternalService]
3. [Controller] injects [Service] and [ValidationService]

### Layered Architecture
1. Controller Layer: [ResponsibilityDescription]
2. Service Layer: [ResponsibilityDescription]
3. Repository Layer: [ResponsibilityDescription]
4. Data Access Layer: [ResponsibilityDescription]
5. Exception Handling Layer: [GlobalExceptionHandler for unified error handling]
```

## Key Construction Points
- **Inheritance System**: Clarify inheritance relationships between interfaces, abstract classes, and implementation classes
- **Dependency Chain**: Define call and dependency relationships between components
- **Layered Design**: Reflect clear layered architecture (Controller -> Service -> Repository -> DAO)
- **Responsibility Separation**: Responsibility boundaries and interaction interfaces of each layer
- **Extension Interfaces**: Interfaces and extension points reserved for future functionality expansion

## Quality Standards
- Clear architectural hierarchy
- Reasonable dependency relationships
- Support system expansion

---

# Task Orchestration (Tasks)

## Objective
Transform abstract solutions into specific executable implementation tasks

## Output Format
```
## Tasks

### Create/Update/Delete [ComponentType] - [ComponentName] Class
1. Responsibility: [Clear responsibility description]
2. Attributes:
   - [attributeName]: [Type] - [Description]
   - [attributeName]: [Type] - [Description with validation rules]
3. Methods:
   - [methodName]([parameters]): [ReturnType]
     - Logic:
       - [Step-by-step implementation logic]
       - [Conditional logic and edge cases]
       - [Error handling approach]
4. Annotations:
   - [RequiredAnnotations for framework integration]
5. Constraints:
   - [Validation rules and business constraints]

### Implement [ServiceType] - [ServiceName] Service
1. Interface Definition: [Interface methods and contracts]
2. Core Method: [methodName]([parameters]): [ReturnType]
   - Input Validation: [Input validation rules]
   - Business Logic: [Core business logic steps]
   - Exception Handling: [Exception handling strategy]
   - Return Value: [Return value construction]
3. Dependency Injection: [Required dependencies]
4. Transaction Management: [Transaction boundary definition]

### Configure [ConfigurationType] - [ConfigurationName]
1. Configuration Items: [Configuration parameters]
2. Default Values: [Default value settings]
3. Environment Variables: [Environment-specific settings]
4. Validation Rules: [Configuration validation]

### Create Exception Handler - GlobalExceptionHandler
1. Responsibility: Unified handling of global exceptions, providing standardized error responses
2. Exception Types:
   - BusinessException: [Business logic exceptions]
   - ValidationException: [Input validation exceptions]
   - SystemException: [System-level exceptions]
   - RuntimeException: [Unexpected runtime exceptions]
3. Methods:
   - handleBusinessException(BusinessException): ResponseEntity<ErrorResponse>
   - handleValidationException(ValidationException): ResponseEntity<ErrorResponse>
   - handleSystemException(SystemException): ResponseEntity<ErrorResponse>
   - handleGenericException(Exception): ResponseEntity<ErrorResponse>
4. Annotations:
   - @RestControllerAdvice
   - @ExceptionHandler for each exception type
5. Response Format:
   - Unified error response structure (error code, error message, timestamp, etc.)

### Create Business Exception Class - [BusinessExceptionName]
1. Responsibility: Define exception types for specific business scenarios, providing clear error information and error codes
2. Inheritance Relationship:
   - extends RuntimeException or extends BusinessException (if there's a base business exception class)
3. Attributes:
   - errorCode: String - Business error code (e.g., USER_NOT_FOUND, INVALID_OPERATION, etc.)
   - errorMessage: String - Detailed error description
   - timestamp: LocalDateTime - Exception occurrence time
   - context: Map<String, Object> - Exception context information (optional)
4. Constructors:
   - [ExceptionName](String errorCode, String errorMessage)
   - [ExceptionName](String errorCode, String errorMessage, Throwable cause)
   - [ExceptionName](String errorCode, String errorMessage, Map<String, Object> context)
5. Methods:
   - getErrorCode(): String - Get error code
   - getErrorMessage(): String - Get error message
   - getContext(): Map<String, Object> - Get context information
   - toString(): String - Format exception information
6. Usage Scenarios:
   - [Specific business scenarios where this exception should be thrown]
   - [Validation rules that trigger this exception]
   - [Business logic conditions that warrant this exception]
7. Exception Classification:
   - Data Exceptions: e.g., DataNotFoundException, DataConflictException
   - Permission Exceptions: e.g., UnauthorizedException, ForbiddenException
   - Business Rule Exceptions: e.g., BusinessRuleViolationException, InvalidStateException
   - External Dependency Exceptions: e.g., ExternalServiceException, IntegrationException
```

## Key Construction Points
- **Based on First Four Stages**: Strictly based on the complete context of requirements, model, solution, and structure
- **Task Classification**: Group by functional modules or component types (entity classes, service classes, controllers, etc.)
- **Implementation Details**: Include specific code specifications, configuration requirements, and business logic
- **Execution Order**: Organize task execution order according to dependency relationships
- **Single Responsibility**: Each task has clear responsibility and boundaries
- **Verifiability**: Each task has clear completion criteria
- **Logical Rigor**: Ensure task orchestration is based on business model, solution, and structured design, avoid logical loopholes, and ensure coherent context data flow

## Quality Standards
- Tasks are directly executable
- Cover complete implementation
- Accurate and specific details

---

# Common Tasks

## Objective
Define unified coding standards and common implementation patterns

## Output Format
```
## Common Tasks
1. Annotation Standards: [Specific annotation requirements for different component types]
2. Dependency Injection: [Dependency injection patterns and best practices]  
3. Exception Handling: [Unified exception handling approach via GlobalExceptionHandler]
   - Custom exception type definition and inheritance relationships
   - Business exception class creation standards:
     * Inherit from RuntimeException or custom BusinessException base class
     * Must include errorCode (business error code) and errorMessage (error description)
     * Provide multiple constructors to support different scenarios
     * Classify by business domain (data exceptions, permission exceptions, business rule exceptions, external dependency exceptions)
   - Unified error response format (ErrorResponse DTO)
   - Standard implementation patterns for exception handler methods
   - Logging and exception tracking mechanisms
4. Data Validation: [Common validation patterns and rules]
5. Logging: [Logging standards and patterns]
6. Documentation Standards: [Documentation and comment standards]
```

## Key Construction Points
- **Standardization**: Define unified coding standards and configuration patterns
- **Reusability**: Extract reusable common implementation patterns
- **Consistency**: Ensure all components follow the same standards
- **Quality Assurance**: Built-in validation and verification mechanisms
- **Best Practices**: Reflect industry best practices and experience summaries

## Quality Standards
- Standards are clear and specific
- Easy to execute and check
- Reflect best practices

---

# Constraint Control (Constraints)

## Objective
Define clear boundary conditions and quality standards

## Output Format
```
## Constraints
1. Functional Constraints: [Functional requirements and limitations with specific criteria]
2. Performance Constraints: [Performance requirements with measurable metrics]
3. Security Constraints: [Security requirements and compliance standards]
4. Integration Constraints: [Integration limitations and compatibility requirements]
5. Business Rule Constraints: [Business rule validation with specific conditions]
6. Exception Handling Constraints: [Exception handling standards and requirements]
   - Business exceptions must include clear error codes and error messages
   - Exception types must be classified and named by business domain
   - Exception information must not expose sensitive system internal information
   - All business exceptions must be handled uniformly by GlobalExceptionHandler
7. Technical Constraints: [Technical implementation restrictions and standards]
8. Data Constraints: [Data validation rules and format requirements]
9. API Constraints: [API design standards and interface contracts]
```

## Key Construction Points
- **Clear Boundaries**: Clearly define what can and cannot be done
- **Verifiability**: Constraint conditions should be verifiable
- **Completeness**: Cover all aspects including functionality, performance, security, integration, etc.
- **Practicality**: Constraints should help improve code quality and system stability
- **Quantified Standards**: Provide quantifiable standards and metrics whenever possible

## Quality Standards
- Clear constraint conditions
- Verifiable
- Complete coverage

---