# Seven-Step Framework Template Content


# Requirements Anchoring

## Objective
Extract the core problem essence and fundamental goals from requirement descriptions

## Output Format
```
## Requirements
[Use concise verb phrases to describe the essence of requirements, avoid feature enumeration]
```

## Construction Points
- **Essence Extraction**: Abstract what fundamental problem to solve and what value to create for whom
- **Boundary Definition**: Clarify the applicable scope and limitations of the solution
- **Value Focus**: Highlight business value and user benefits
- **Use Verb Phrases**: Such as "Implement...", "Create...", "Design..."
- **Avoid Feature Stacking**: Don't list specific functions, abstract the essential problems that need to be solved

## Quality Standards
- Core requirements can be summarized in one sentence
- Reflect business value rather than technical implementation
- Clear problem boundaries and constraints

---

# Business Model

## Objective
Build clear business entity relationship models to provide conceptual foundation for subsequent design

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

## Construction Points
- **Entity Identification**: Identify core business entities, supporting entities, DTO objects
- **Attribute Modeling**: Define key attributes for each entity using "type+name" format
- **Relationship Modeling**: Clarify relationship types (1:1, 1:N, N:M) and business semantics between entities
- **Existing Implementation Priority**: If current data structures can meet requirements, existing implementation must remain unchanged
- **Minimal Change Principle**: Only refactor when existing structures truly cannot support new requirements
- **Interface Design**: Include key methods and static factory methods
- **Data Flow**: Reflect complete data flow of request->processing->response
- **Consistency Assurance**: Ensure models can be accurately understood and implemented by AI
- **Simplicity > Feature Rich**: Avoid over-engineering, maintain system comprehensibility

## Conservative Constraints
- **Prohibit Unnecessary Refactoring**: If existing simple data types (like List<String>) can meet requirements, strictly prohibit creating complex entity wrappers
- **Function-Driven Changes**: Only consider structural adjustments when clear functional requirements cannot be implemented through existing structures
- **Gradual Improvement**: Prioritize extending based on existing structures rather than rebuilding from scratch
- **Backward Compatibility**: Any structural changes must ensure backward compatibility, avoiding breaking changes

## Quality Standards
- Focus on current task flows
- Clear and accurate entity relationships
- Support subsequent technical implementation
- Maintain simplicity of existing implementations
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

## Construction Points
- **Categorical Organization**: Organize by solution categories (such as API design, data processing, exception handling, etc.)
- **Architecture Decisions**: Provide key technical architecture choices and design patterns
- **Best Practices**: Combine industry standards and experience summaries
- **Decision Rationale**: Explain why specific solutions were chosen
- **Risk Assessment**: Identify potential risks and response strategies

## Quality Standards
- Solutions have operability
- Cover key technical decisions
- Reflect architectural thinking

---

# Structure Definition

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
5. [BusinessException] extends RuntimeException class (business exception base class)
6. [SpecificBusinessException] extends [BusinessException] class (specific business exception class)

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

## Construction Points
- **Inheritance System**: Clarify inheritance relationships of interfaces, abstract classes, and implementation classes
- **Dependency Chain**: Define call and dependency relationships between components
- **Layered Design**: Reflect clear layered architecture (Controller -> Service -> Repository -> DAO)
- **Responsibility Separation**: Responsibility boundaries and interaction interfaces of each layer
- **Extension Interfaces**: Interfaces and extension points reserved for future functionality expansion

## Quality Standards
- Clear architectural hierarchy
- Reasonable dependency relationships
- Support system extension

---

# Task Orchestration

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
2. Core Methods: [methodName]([parameters]): [ReturnType]
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
1. Responsibility: Define specific business scenario exception types, provide clear error information and error codes
2. Inheritance Relationship:
   - extends RuntimeException or extends BusinessException (if there is a base business exception class)
3. Attributes:
   - errorCode: String - Business error code (such as: USER_NOT_FOUND, INVALID_OPERATION, etc.)
   - errorMessage: String - Detailed error description
   - timestamp: LocalDateTime - Exception occurrence time
   - context: Map<String, Object> - Exception context information (optional)
4. Constructor Methods:
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
   - Data Exceptions: such as DataNotFoundException, DataConflictException
   - Permission Exceptions: such as UnauthorizedException, ForbiddenException
   - Business Rule Exceptions: such as BusinessRuleViolationException, InvalidStateException
   - External Dependency Exceptions: such as ExternalServiceException, IntegrationException
```

## Construction Points
- **Based on First Four Stages**: Strictly based on the complete context of requirements, models, solutions, and structures
- **Task Classification**: Group by functional modules or component types (entity classes, service classes, controllers, etc.)
- **Implementation Details**: Include specific code specifications, configuration requirements, business logic
- **Execution Order**: Organize task execution order based on dependency relationships
- **Single Responsibility**: Each task has clear responsibilities and boundaries
- **Verifiability**: Each task has clear completion criteria
- **Logical Rigor**: Ensure task orchestration is based on business models, solutions, and structured design, avoid logical loopholes, and ensure coherent contextual data flow

## Quality Standards
- Tasks can be executed directly
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
   - Custom exception type definitions and inheritance relationships
   - Business exception class creation standards:
     * Inherit RuntimeException or custom BusinessException base class
     * Must include errorCode (business error code) and errorMessage (error description)
     * Provide multiple constructor methods to support different scenarios
     * Classify by business domain (data exceptions, permission exceptions, business rule exceptions, external dependency exceptions)
   - Unified error response format (ErrorResponse DTO)
   - Standard implementation patterns for exception handler methods
   - Logging and exception tracking mechanisms
4. Data Validation: [Common validation patterns and rules]
5. Logging: [Logging standards and patterns]
6. Documentation Standards: [Documentation and comment standards]
```

## Construction Points
- **Standardization**: Define unified coding standards and configuration patterns
- **Reusability**: Extract reusable common implementation patterns
- **Consistency**: Ensure all components follow the same standards
- **Quality Assurance**: Built-in validation and verification mechanisms
- **Best Practices**: Reflect industry best practices and experience summaries

## Quality Standards
- Clear and specific standards
- Easy to execute and check
- Reflect best practices

---

# Constraint Control

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
   - All business exceptions must be uniformly handled by GlobalExceptionHandler
7. Technical Constraints: [Technical implementation restrictions and standards]
8. Data Constraints: [Data validation rules and format requirements]
9. API Constraints: [API design standards and interface contracts]
```

## Construction Points
- **Clear Boundaries**: Clearly define what can and cannot be done
- **Verifiability**: Constraint conditions should be verifiable
- **Completeness**: Cover all aspects including functionality, performance, security, integration, etc.
- **Practicality**: Constraints should help improve code quality and system stability
- **Quantified Standards**: Provide quantifiable standards and metrics whenever possible

## Quality Standards
- Clear constraint conditions
- Verifiable
- Complete coverage
