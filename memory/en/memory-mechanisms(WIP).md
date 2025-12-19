# Memory Generation Strategy Framework

## Overview

This document describes a systematic memory generation strategy for decomposing complex software systems into understandable, reusable, and maintainable knowledge units. Through three-dimensional classification standards and structured descriptions, it builds the team's technical knowledge assets.

---

##  1. Holistic Analysis Phase

### Code Deep Exploration

#### Static Analysis
- **Target File Parsing**: Read class structures, method signatures, annotation information
- **Interface Identification**: Understand externally exposed APIs and internal interfaces
- **Data Flow Analysis**: Trace complete path from request entry to response

#### Dependency Tracking
```
Target File → codebase_search → Related Component Discovery
↓
Dependency Graph Construction → Design Pattern Recognition → Architecture Pattern Extraction
```

- **Upward Tracking**: Callers, users, integration points
- **Downward Tracking**: Dependent services, data layer, external systems
- **Horizontal Association**: Same-layer components, collaborative relationships, data transfer

#### Association Mining
- **Design Pattern Discovery**: Strategy, Factory, Observer, etc.
- **Architecture Pattern Recognition**: MVC, layered architecture, microservice patterns
- **Integration Pattern Analysis**: API Gateway, event-driven, message queues

### Architecture Pattern Recognition Matrix

| Pattern Type | Identification Markers | Example |
|--------------|------------------------|---------|
| **Unified Interface Pattern** | Single controller handling multiple resource types | PromptController |
| **Service Selector Pattern** | Type/condition-based specific implementation selection | PromptServiceSelector |
| **Factory Pattern** | Parameter-based different object creation | PromptCreateRequest.toPrompt() |
| **Dependency Injection** | @Autowired annotations and constructor injection | Various Service components |
| **Audit Pattern** | Change records and log tracking | ChangeLog system |

---

## 2. 4D Classification Mapping (Extended Cognitive Dimension)

### Memory Type Judgment Logic

```mermaid
graph TD
A[Analyze Content] --> B{Description Type?}
B -->|Architecture Design/Design Patterns/Technical Conventions| C[ImplementationRule]
B -->|Business Process/API Call Chain/Sequence Diagram| D[ProcessFlow]
B -->|Entity Relationships/Data Models/Architecture Diagrams| E[BusinessModel]

C --> F[Technical Implementation Rules]
D --> G[Business Process Rules]
E --> H[Business Modeling Rules]

F --> I{Cognitive Type?}
G --> J{Cognitive Type?}
H --> K{Cognitive Type?}

I -->|Concepts/Principles| L[Declarative]
I -->|Methods/Practices| M[Procedural]
I -->|Cases/Experiences| N[Episodic]

J -->|Concepts/Principles| O[Declarative]
J -->|Methods/Practices| P[Procedural]
J -->|Cases/Experiences| Q[Episodic]

K -->|Concepts/Principles| R[Declarative]
K -->|Methods/Practices| S[Procedural]
K -->|Cases/Experiences| T[Episodic]
```

### Cognitive Memory Classification

#### Declarative Memory - "What" Knowledge
- **Definition**: Stores conceptual definitions, technical principles, and architectural design concepts
- **Identification Markers**: Concept explanations, principle elaborations, architectural thoughts, design philosophies
- **Typical Content**:
    - Technical concept definitions: "The core idea of microservices architecture is service autonomy and loose coupling"
    - Design principles: "Single Responsibility Principle requires each class to have only one reason to change"
    - Architectural concepts: "DDD emphasizes driving software design through domain models"
- **Application Scenarios**: Technical training, concept dissemination, architecture understanding

#### Procedural Memory - "How-to" Knowledge
- **Definition**: Stores operational processes, development methods, and best practices
- **Identification Markers**: Step descriptions, flowcharts, methodologies, operational guides
- **Typical Content**:
    - Development processes: "Standard API design process: Requirements analysis → Interface design → Implementation → Testing"
    - Operational methods: "Git branch management strategy: Feature branch development → PR review → Merge to main"
    - Best practices: "Code review checklist: Functional correctness → Code standards → Performance considerations → Security checks"
- **Application Scenarios**: Operational guidance, process standards, method inheritance

#### Episodic Memory - "When and Where" Knowledge
- **Definition**: Stores specific project experiences, problem-solving cases, and historical decisions
- **Identification Markers**: Time and location, specific projects, problem scenarios, solutions
- **Typical Content**:
    - Project experience: "In Q3 2024 user system project, we adopted JWT+Redis solution to solve distributed session problems"
    - Problem cases: "Production database connection pool exhaustion resolved by adjusting pool parameters and optimizing slow queries"
    - Decision records: "Technical decision to choose Kubernetes over Docker Swarm with background and considerations"
- **Application Scenarios**: Experience sharing, problem troubleshooting, decision reference

### Resource Type Recognition Strategy

#### Entity
- **Identification Markers**: Core business objects, domain models, data entities
- **Examples**: Rule, Solution, Workflow, User
- **Characteristics**: Clear business meaning and lifecycle

#### Process
- **Identification Markers**: Business operations, workflows, state transitions
- **Examples**: Creation process, update process, approval process
- **Characteristics**: Describes business behavior and operation sequences

#### Integration
- **Identification Markers**: External interfaces, API design, inter-system interactions
- **Examples**: REST API, message queues, third-party integrations
- **Characteristics**: Involves system boundaries and external communication

#### Configuration
- **Identification Markers**: System configuration, rule definitions, policy settings
- **Examples**: ID prefix strategy, routing rules, permission configuration
- **Characteristics**: Parameters and rules affecting system behavior

#### Infrastructure
- **Identification Markers**: Technical foundation components, platform services, operational tools
- **Examples**: Database connections, caching, monitoring
- **Characteristics**: Technical facilities supporting business operations

### Operation Type Classification Standards

#### ProcessFlow Operations
- **Create**: Resource creation process
- **Update**: Resource update process
- **Query**: Query and retrieval operations
- **Delete**: Delete and cleanup operations
- **Batch**: Batch processing operations
- **Search**: Search and filtering operations

#### ImplementationRule Patterns
- **UnifiedManagement**: Unified management pattern
- **Performance**: Performance optimization pattern
- **Security**: Security control pattern
- **Pattern**: General design patterns

#### BusinessModel Modeling
- **EntityRelation**: Entity relationship modeling
- **DataModel**: Data model design
- **Architecture**: Architecture design modeling
- **Integration**: Integration pattern modeling

### Cognitive Memory Type Mapping

#### Correspondence with Traditional Classification
```markdown
Traditional Classification → Cognitive Type Mapping:

ImplementationRule + Pattern → Primarily Declarative (concepts and principles)
ImplementationRule + UnifiedManagement → Potentially Procedural (management methods)

ProcessFlow + Create/Update/Query/Delete → Primarily Procedural (operational processes)
ProcessFlow + Specific business scenarios → Potentially Episodic (project experience)

BusinessModel + EntityRelation → Primarily Declarative (model concepts)
BusinessModel + Architecture → Primarily Declarative (architectural thoughts)
```

---

## 3. Granularity Control Strategy

### Single Responsibility Principle

#### Good Memory Item Examples
```markdown
Title: Service Selector Pattern for Multi-Type Resource Management
Content: Focus on service selection and routing mechanisms
Scope: Complete implementation of a single design pattern
```

#### Memory Item Examples to Avoid
```markdown
Title: All Functions of PromptController
Problem: Scope too broad, lacks focus
Suggestion: Split into multiple specific patterns and processes
```

### Memory Size Control Standards

| Dimension | Standard | Description |
|-----------|----------|-------------|
| **Minimum Unit** | One complete technical pattern or business process | Ensure memory completeness |
| **Maximum Scope** | No more than one subsystem's core responsibilities | Avoid information overload |
| **Target Length** | 150-300 words, containing 8-10 key points | Balance detail and readability |
| **Complexity** | Understandable by medium technical background | Ensure team members can apply |

### Split Decision Tree

```mermaid
graph TD
A[Content to Record] --> B{Exceeds 300 words?}
B -->|Yes| C[Find Natural Split Points]
B -->|No| D[Check Single Responsibility]

C --> E[Split by Pattern]
C --> F[Split by Process Stage]
C --> G[Split by Component]

D --> H{Single Responsibility?}
H -->|Yes| I[Form Memory Item]
H -->|No| J[Re-analyze Responsibility Boundaries]
```

---

## 4. Metadata Field Generation Strategy

### Project Field Generation Rules

#### Naming Conventions
- **Format**: Use lowercase letters and hyphens in kebab-case format
- **Structure**: [domain]-[system/module]-[type]
- **Examples**: `workflow-management-system`, `user-authentication-service`

#### Project Identification Strategy
```markdown
Technical Domain Classification:
- workflow-management-system: Workflow management related
- prompt-management-system: Prompt management related
- user-authentication-service: User authentication related
- api-gateway-service: API gateway related
- data-processing-pipeline: Data processing pipeline related
```

### Tag Field Generation Strategy

#### Tag Quantity Standards
- **Fixed Quantity**: Each memory item must contain 5 tags
- **Priority**: Sorted by importance and relevance
- **Uniqueness**: Avoid duplicate or overly similar tags

#### Tag Classification System
```markdown
1. **Technical Pattern Tags**
    - REST-API, Service-Selector, DTO-Pattern, Query-Builder
    - Multi-Type-Management, Unified-API, ID-Prefix-Strategy

2. **Functional Feature Tags**
    - CRUD-Operations, Batch-Processing, Step-Validation
    - User-Context, Auto-Fill, Permission-Management

3. **Quality Attribute Tags**
    - Performance-Optimization, Security-Enforcement, Thread-Safe
    - Error-Handling, Exception-Handling, Input-Validation

4. **Business Domain Tags**
    - Business-Process, Workflow-Integration, Resource-Lifecycle
    - Cross-Type-Validation, Dependency-Validation, Change-Logging

5. **Technical Implementation Tags**
    - Parallel-Processing, Type-Abstraction, Factory-Methods
    - HTTP-Status-Codes, Service-Delegation, Referential-Integrity
```

#### Tag Selection Algorithm
```mermaid
graph TD
A[Analyze Memory Content] --> B[Identify Main Technical Patterns]
B --> C[Determine Core Functional Features]
C --> D[Evaluate Quality Attributes]
D --> E[Categorize Business Domain]
E --> F[Extract Technical Implementation Details]
F --> G[Sort Top 5 by Importance]
G --> H[Verify Tag Uniqueness]
```

### Importance Field Scoring Strategy

#### Scoring Standard System
```markdown
10 points (Extremely High Importance) - Critical
- Core business processes, essential system functions
- Architectural decisions affecting overall system design
- Security-critical components or data integrity mechanisms

9 points (High Importance) - High
- Important architectural patterns affecting overall system design
- Key security mechanisms and user management functions
- Core API design and unified management patterns

8 points (Medium-High Importance) - Medium-High
- Important technical implementations affecting system performance and maintainability
- Key integration patterns and service coordination mechanisms
- Important exception handling and error recovery strategies

7 points (Medium Importance) - Medium
- Standard technical practices contributing to code quality and development efficiency
- Performance optimization and query building support functions
- Data transformation and DTO design patterns

6 points (Medium-Low Importance) - Medium-Low
- Auxiliary functions providing convenience but not core necessities
- Specific scenario lookup and retrieval functions
- Standardized response formats and data mapping

5 points and below (Low Importance) - Low
- Utility functions, replaceable or optional implementations
- Edge case handling and compatibility functions
- Configuration functions and customizable options
```

#### Importance Assessment Matrix

| Dimension | Weight | Assessment Criteria |
|-----------|--------|-------------------|
| **Business Criticality** | 40% | Impact on core business processes |
| **Technical Complexity** | 25% | Implementation complexity and technical difficulty |
| **Reuse Value** | 20% | Application potential in other projects |
| **Maintenance Cost** | 10% | Long-term maintenance and update difficulty |
| **Innovation Level** | 5% | Innovation and advancement of technical solutions |

#### Scoring Decision Process
```mermaid
graph LR
A[Content Analysis] --> B[Business Criticality Assessment]
B --> C[Technical Complexity Assessment]
C --> D[Reuse Value Assessment]
D --> E[Maintenance Cost Assessment]
E --> F[Innovation Level Assessment]
F --> G[Weighted Total Calculation]
G --> H[Adjust to 1-10 Scale]
```

---

## 5. Content Structuring Strategy

### Standard Description Template

**CRITICAL FORMAT REQUIREMENTS**:
- Each memory item MUST start with ### (H3 heading)
- Each memory item MUST include #### Summary section
- All metadata fields are REQUIRED: Classification, Scope, Project, Tags, Importance
- NEW OPTIONAL FIELD: CognitiveType (Declarative/Procedural/Episodic)
- Tags MUST be exactly 5 items, comma-separated
- Importance MUST be in X/10 format (e.g., 9/10)

**COMMON FORMAT ERRORS TO AVOID**:
- Missing #### Summary section
- Incorrect metadata field names
- Tags not comma-separated
- Importance not in X/10 format
- Using wrong heading levels (must be ### for title, #### for Summary)

```markdown
### [Memory Item Title]
**Classification**: [MemoryType] - [ResourceType] - [OperationType]
**CognitiveType**: [Declarative/Procedural/Episodic]
**Scope**: [Global/Project/Team]
**Project**: [project-identifier]
**Tags**: [Tag1], [Tag2], [Tag3], [Tag4], [Tag5]
**Importance**: [1-10]/10

#### Summary
[System/Component] implements [Pattern Name] for [Target Purpose]:
1) **Core Mechanism**: Describe main working principles and key components
2) **Implementation Method**: Explain specific technical implementation approaches
3) **Workflow**: Overview main operation steps and data flow
4) **Error Handling**: Describe exception handling strategies
5) **Integration Interface**: Explain collaboration with other components
6) **Extensibility**: Describe system extensibility design
7) **Performance Considerations**: Related performance optimizations and limitations
8) **Security Control**: Related security mechanisms and permission control

# Cognitive Type Extension Guide
When using the CognitiveType field, refer to the following description focus:

## Declarative - "What" Knowledge
- Focus on describing concept definitions, technical principles, architectural design thoughts
- Example: "The core idea of microservices architecture is service autonomy and loose coupling"

## Procedural - "How-to" Knowledge  
- Focus on describing operational processes, development methods, best practices
- Example: "Standard API design process: Requirements analysis → Interface design → Implementation → Testing"

## Episodic - "When and Where" Knowledge
- Focus on describing specific project experiences, problem-solving cases, historical decisions
- Example: "In Q3 2024 user system project, we adopted JWT+Redis solution to solve distributed session problems"
```

### Association Modeling Strategy

#### Vertical Association (Abstraction Levels)
```
Interface Layer (Controller)
↓
Business Layer (Service)
↓
Data Layer (Repository)
↓
Entity Layer (Entity)
```

#### Horizontal Association (Same-Layer Components)
```
Controller ←→ Filter ←→ Exception Handler
Service ←→ Validator ←→ Event Publisher
Repository ←→ Cache ←→ Message Queue
```

#### Sequential Association (Business Process)
```
Request Validation → Permission Check → Business Processing → Data Persistence → Response Return
```

### Content Quality Standards

| Quality Dimension | Assessment Criteria | Checkpoints |
|-------------------|-------------------|-------------|
| **Accuracy** | Accurate technical descriptions, correct code references | Code verification, technical review |
| **Completeness** | Covers key processes and components | Process check, component checklist |
| **Clarity** | Clear logic, easy to understand | Readability test, terminology consistency |
| **Practicality** | Can guide actual development work | Use cases, example code |

---

## 6. Scope Assessment Algorithm

### Scope Assessment Matrix

```mermaid
graph LR
A[Analyze Content] --> B{Technical Universality}
B -->|High Universality| C[Global Scope]
B -->|Medium Universality| D[Domain Scope]
B -->|Specific Business| E[Project Scope]
B -->|Team Convention| F[Team Scope]

C --> G[Design Patterns, Architecture Patterns]
D --> H[Business Domain Patterns]
E --> I[Specific Business Implementation]
F --> J[Development Standard Conventions]
```

### Global Level Assessment Criteria
- **Technical Patterns**: Design patterns reusable across multiple projects
- **Architecture Components**: Universal architectural design and implementation methods
- **Utility Methods**: Independent utility classes and helper methods
- **Standard Protocols**: Universal interface and protocol definitions

#### Examples
```markdown
Global: Service Selector Pattern
- Applicable to any scenario requiring type routing

Global: Unified DTO Pattern  
- Suitable for multi-type resource API design

Global: ID Prefix Strategy
- Universal resource identification and classification method
```

### Project Level Assessment Criteria
- **Business Logic**: Project-specific business rules and processes
- **Data Models**: Project-specific entity relationships and constraints
- **Integration Implementation**: Specific external system integration methods
- **Permission Models**: Project-specific permission design

#### Examples
```markdown
Project: PromptController Business Process
- Specific to current project's Rule/Solution management

Project: User Permission Integration
- UserContext-based permission implementation

Project: Workflow Dependency Validation
- Specific business rules and constraint checking
```

---

## 7. Quality Assurance Mechanism

### Completeness Check List

#### Technical Coverage Dimensions
- [ ] **Architecture Level**: Overall design concepts and patterns
- [ ] **Design Patterns**: Specific technical implementation patterns
- [ ] **Integration Interfaces**: Component collaboration methods
- [ ] **Data Flow**: Information flow within the system

#### Business Coverage Dimensions
- [ ] **CRUD Operations**: Create, Read, Update, Delete processes
- [ ] **Permission Control**: Authentication, authorization, permission validation
- [ ] **Data Integrity**: Constraint checking, dependency validation
- [ ] **Audit Trail**: Operation records, change logs

#### Layer Coverage Dimensions
- [ ] **Presentation Layer**: Controller, API interface design
- [ ] **Business Layer**: Service, business logic implementation
- [ ] **Data Layer**: Repository, data access patterns
- [ ] **Model Layer**: Entity, DTO, data structures

### Consistency Validation Standards

#### Naming Consistency
```markdown
Unified Terminology Usage
- "PromptController" vs "Prompt Controller"
- Choose one and maintain consistency

Consistent Concept Definitions
- "Service Selector" definition consistent across all memories
- Avoid different expressions of the same concept
```

#### Classification Consistency
```markdown
Similar Patterns Use Same Classification
- All "XXX Selector Pattern" classified as ImplementationRule-Configuration-Pattern
- All "XXX Business Process" classified as ProcessFlow-Process-ProcessFlow
```

#### Granularity Consistency
```markdown
Similar Complexity Memories Maintain Similar Length
- Design pattern memories: 200-250 words
- Business process memories: 250-300 words
- Simple configuration memories: 150-200 words
```

#### Metadata Consistency
```markdown
Project Field Consistency
- Memories from same system use same project identifier
- Follow kebab-case naming convention
- Project identifier matches actual system name

Tag Standardization
- Each memory item has exactly 5 tags
- Use tags from standard tag classification system
- Tags sorted by importance and relevance
- Avoid semantically duplicate tags

Importance Score Consistency
- Similar functional complexity memories use similar scores
- Core business processes score 8-10 points
- Supporting functions score 6-7 points
- Utility functions score 5 points or below
```

---

## 8. Practical Application Case Analysis

### Complete PromptController Case Breakdown

#### Discovery Process
```mermaid
graph TD
A[PromptController.java] --> B[Code Analysis]
B --> C[Dependency Tracking]
C --> D[Pattern Recognition]
D --> E[6 Core Memory Items]

C --> F[PromptServiceSelector]
C --> G[UserContext Integration]
C --> H[DTO Design Pattern]
C --> I[Permission Validation Process]
C --> J[Dependency Relationship Validation]
```

#### Memory Item Mapping

| Memory Item | Classification | CognitiveType | Scope | Project | Importance | Tag Examples |
|-------------|----------------|---------------|--------|---------|------------|--------------|
| **Unified Management Pattern** | ImplementationRule-Entity-UnifiedManagement | Declarative | Project | workflow-management-system | 9/10 | Unified-API, Multi-Type-Management, CRUD-Operations, Service-Selector, ID-Prefix-Strategy |
| **Business Process** | ProcessFlow-Process-ProcessFlow | Procedural | Project | workflow-management-system | 10/10 | Business-Process, Resource-Lifecycle, Multi-Type-Operations, Type-Routing, Change-Logging |
| **Service Selector** | ImplementationRule-Configuration-Pattern | Declarative | Global | workflow-management-system | 9/10 | Service-Selector, Type-Routing, Batch-Processing, ID-Prefix-Inference, Pattern-Extensibility |
| **User Context** | ImplementationRule-Process-Security | Procedural | Project | workflow-management-system | 9/10 | User-Context, Permission-Management, Auto-Population, Thread-Safe, Security-Validation |
| **DTO Design** | ImplementationRule-Integration-Pattern | Declarative | Global | workflow-management-system | 8/10 | DTO-Pattern, Multi-Type-Response, Polymorphic-Factory, Type-Metadata, Auto-Population |
| **Dependency Validation** | ProcessFlow-Process-ProcessFlow | Procedural | Project | workflow-management-system | 10/10 | Dependency-Validation, Cross-Type-Validation, Referential-Integrity, Workflow-Integration, Pre-Deletion-Check |

#### Cognitive Type Application Examples

**Declarative Memory Examples**:
- Service Selector Pattern: Describes what the service selector pattern is, its core concepts and design philosophy
- DTO Design Pattern: Explains the conceptual definition and design principles of data transfer objects

**Procedural Memory Examples**:
- Business Process: Details the specific workflow and steps of business operations
- User Context Integration: Explains how to integrate user context operational methods

**Episodic Memory Examples**:
- Can add specific problem-solving cases from projects, such as: "In the 2024 project refactoring, how we solved the complexity of multi-type resource management"

#### Granularity Control Example

**Good Granularity Control**
```markdown
Memory: Service Selector Pattern
Content: Focus on type routing mechanism
- Type mapping logic
- ID prefix inference
- Batch processing optimization
- Error handling strategy
Length: 238 words, 8 key points
```

**Granularity Needing Optimization**
```markdown
Original Idea: Complete PromptController functionality
Problem: Content too broad
Optimization: Split into 6 independent memory items
Result: Each memory focuses on single responsibility
```

#### Complete Format Example

**Perfect Format Example (Extended Cognitive Types)**
```markdown
### Service Selector Pattern for Multi-Type Resource Management
**Classification**: ImplementationRule - Configuration - Pattern
**CognitiveType**: Declarative
**Scope**: Global
**Project**: workflow-management-system
**Tags**: Service-Selector, Type-Routing, Batch-Processing, ID-Prefix-Inference, Pattern-Extensibility
**Importance**: 9/10

#### Summary
System implements Service Selector Pattern for dynamic type-based service routing and management:
1) **Core Mechanism**: Type detection through ID prefix analysis and service mapping registry
2) **Implementation Method**: Factory pattern with type-specific service implementations and routing logic
3) **Workflow**: Request analysis → Type detection → Service selection → Delegation → Response handling
4) **Error Handling**: Fallback mechanisms for unknown types and graceful degradation strategies
5) **Integration Interface**: Unified interface for all service types with consistent method signatures
6) **Extensibility**: Plugin architecture allowing new service types without code modification
7) **Performance Considerations**: Caching of service instances and optimized type detection algorithms
8) **Security Control**: Type validation and access control based on service capabilities
```

**Procedural Memory Example**
```markdown
### Standard API Design Process
**Classification**: ProcessFlow - Process - ProcessFlow
**CognitiveType**: Procedural
**Scope**: Global
**Project**: api-design-standards
**Tags**: API-Design, Development-Process, Best-Practice, Quality-Assurance, Documentation
**Importance**: 8/10

#### Summary
Standard API design process ensures interface consistency and maintainability:
1) **Requirements Analysis**: Define API functional requirements, performance requirements and security constraints
2) **Interface Design**: Define resource models, HTTP methods, URL structure and data formats
3) **Documentation**: Create detailed API documentation including request/response examples
4) **Prototype Implementation**: Develop API prototype and conduct internal testing validation
5) **Review and Optimization**: Team review of interface design, collect feedback and optimize
6) **Formal Implementation**: Implement complete functionality according to design documentation
7) **Testing Validation**: Execute unit tests, integration tests and performance tests
8) **Release and Maintenance**: Version release, monitor operational status and continuous optimization
```

**Episodic Memory Example**
```markdown
### Q3 2024 User System Distributed Session Solution
**Classification**: ProcessFlow - Integration - ProblemSolution
**CognitiveType**: Episodic
**Scope**: Project
**Project**: user-management-system
**Tags**: Distributed-Session, JWT-Redis, Problem-Solution, Production-Issue, Architecture-Decision
**Importance**: 9/10

#### Summary
Successfully resolved distributed session management issues in Q3 2024 user system project:
1) **Problem Background**: User session state cannot be shared across multiple services in microservices architecture
2) **Technical Challenge**: Traditional session storage solutions cannot meet distributed deployment requirements
3) **Solution Selection**: After technical research, chose JWT+Redis hybrid solution
4) **Implementation Process**: JWT stores basic user information, Redis caches session state and permission data
5) **Key Decisions**: Set JWT expiration time to 2 hours, Redis session cache to 24 hours
6) **Effect Evaluation**: Resolved session sharing issues, system response time improved by 30%
7) **Lessons Learned**: JWT is suitable for storing non-sensitive user information, sensitive data still requires server-side validation
8) **Applicable Scenarios**: Suitable for medium-scale distributed systems, large-scale systems need to consider Redis clustering
```

---

## 9. Continuous Optimization Strategy

### Iterative Improvement Process

```mermaid
graph LR
A[Memory Creation] --> B[Usage Feedback]
B --> C[Effect Evaluation]
C --> D[Optimization Adjustment]
D --> A

B --> E[Usage Frequency Statistics]
B --> F[Understanding Difficulty Assessment]
B --> G[Application Success Rate]

C --> H[Granularity Adjustment]
C --> I[Classification Optimization]
C --> J[Content Supplementation]
```

### Feedback Collection Mechanism

#### Usage Effect Indicators
- **Search Efficiency**: Ability to quickly find relevant memories
- **Understanding Speed**: Learning time for new team members
- **Application Success Rate**: Success rate of implementing functions based on memories
- **Reuse Rate**: Memory reuse in different scenarios

#### Optimization Triggers
- Memory usage frequency below expectations
- Team member feedback on understanding difficulties
- Discovery of better classification methods
- Technology stack upgrades requiring updates

### Pattern Extraction and Upgrade

#### Project → Global Upgrade Standards
```markdown
Condition Check:
1. Similar implementations appear in multiple projects
2. Technical patterns have universality
3. Team considers promotion valuable
4. Validated through practice

Upgrade Process:
1. Abstract universal patterns
2. Remove project-specific details
3. Add applicable scenario descriptions
4. Update classification and scope
```

### Tool-Assisted Strategy

#### Automated Detection
- **Code Similarity Analysis**: Discover duplicate implementation patterns
- **Dependency Relationship Tracking**: Update inter-component associations
- **Change Impact Analysis**: Impact of code changes on memories

#### Memory Management Tools
- **Classification Statistics**: Memory quantity distribution by dimensions
- **Association Graph**: Reference relationships between memories
- **Usage Heat Map**: Memory access frequency analysis

---

## Core Philosophy and Value

### Design Philosophy
> **Decompose complex software systems into understandable, reusable, and maintainable knowledge units**

### Value Manifestation
1. **Knowledge Assetization**: Make tacit knowledge explicit, accumulate team wisdom
2. **Learning Acceleration**: New members quickly understand system architecture and design concepts
3. **Decision Support**: Provide references for technology selection and architecture design
4. **Quality Assurance**: Improve code quality and consistency through pattern reuse
5. **Innovation Promotion**: Improve and innovate based on existing patterns

### Implementation Recommendations
1. **Gradual Progress**: Start with core modules, gradually cover the entire system
2. **Team Collaboration**: Encourage team members to contribute and improve memory items
3. **Continuous Maintenance**: Regularly review and update memory content
4. **Tool Support**: Develop or select appropriate memory management tools
5. **Culture Building**: Foster a team culture of knowledge sharing and learning
6. **Format Validation**: Always validate memory format before submission to prevent parsing errors

---

**Document Version**: v2.1
**Last Updated**: 2025-12-19
**Applicable Scope**: Software development team knowledge management
**Maintenance Team**: Technical Architecture Group
**Major Updates**:
- v2.0: Added metadata field generation strategy (project, tags, importance)
- v2.1: Extended with Cognitive Memory Types (Declarative, Procedural, Episodic) as optional CognitiveType field
