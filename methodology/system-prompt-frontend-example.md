First understand the memory content, then generate specific structured prompts based on the seven-step framework combined with user_message

---

# Team Memory
### 20250724141806_BD2C
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** State-Management, Entity-Relations, Data-Model, TypeScript-Interfaces, Props-Flow

Workflow Editor Data Model and State Management

Workflow editor system implements data model design for editing state and entity relationship management:
1. **Core Entity Definition**: WorkflowStep contains id, type, name, description, order properties, WorkflowCreateRequest defines API request structure
2. **State Hierarchy**: CustomWorkflowEditor maintains workflowSteps main state, child components receive data through props, callback functions update parent state
3. **Type Safety Design**: Strict TypeScript interface definitions, DragItem, PromptResponseRaw and other specialized interfaces handle complex data transformations
4. **State Synchronization Mechanism**: Drag operations, search results, preview display and other multiple states maintain synchronization through unidirectional data flow, avoiding state inconsistency
5. **Lifecycle Management**: useEffect manages component mounting state, useRef prevents state updates after unmounting, avoiding memory leaks
6. **Data Transformation Process**: PromptResponse converts to WorkflowStep, API response data standardized processing, ensuring data format consistency
7. **Caching Strategy**: isDirty state tracks modification status, supports pre-save confirmation and data recovery functionality
8. **Association Relationships**: Mapping relationship between WorkflowStep and PromptResponse, user permissions and editing permissions association validation

---

# Team Memory
### 20250724141224_17C4
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** Entity-Relations, State-Management, Props-Flow, TypeScript-Interfaces, Data-Model

Workflow Editor Data Model and State Management

Workflow editor system implements data model design for editing state and entity relationship management:
1. **Core Entity Definition**: WorkflowStep contains id, type, name, description, order properties, WorkflowCreateRequest defines API request structure
2. **State Hierarchy**: CustomWorkflowEditor maintains workflowSteps main state, child components receive data through props, callback functions update parent state
3. **Type Safety Design**: Strict TypeScript interface definitions, DragItem, PromptResponseRaw and other specialized interfaces handle complex data transformations
4. **State Synchronization Mechanism**: Drag operations, search results, preview display and other multiple states maintain synchronization through unidirectional data flow, avoiding state inconsistency
5. **Lifecycle Management**: useEffect manages component mounting state, useRef prevents state updates after unmounting, avoiding memory leaks
6. **Data Transformation Process**: PromptResponse converts to WorkflowStep, API response data standardized processing, ensuring data format consistency
7. **Caching Strategy**: isDirty state tracks modification status, supports pre-save confirmation and data recovery functionality
8. **Association Relationships**: Mapping relationship between WorkflowStep and PromptResponse, user permissions and editing permissions association validation

---

# Team Memory
### 20250724140834_477A
**Project:** workflow-management-system
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** State-Management, Entity-Relations, Props-Flow, TypeScript-Interfaces, Data-Model

Workflow Editor Data Model and State Management

Workflow editor system implements data model design for editing state and entity relationship management:
1. **Core Entity Definition**: WorkflowStep contains id, type, name, description, order properties, WorkflowCreateRequest defines API request structure
2. **State Hierarchy**: CustomWorkflowEditor maintains workflowSteps main state, child components receive data through props, callback functions update parent state
3. **Type Safety Design**: Strict TypeScript interface definitions, DragItem, PromptResponseRaw and other specialized interfaces handle complex data transformations
4. **State Synchronization Mechanism**: Drag operations, search results, preview display and other multiple states maintain synchronization through unidirectional data flow, avoiding state inconsistency
5. **Lifecycle Management**: useEffect manages component mounting state, useRef prevents state updates after unmounting, avoiding memory leaks
6. **Data Transformation Process**: PromptResponse converts to WorkflowStep, API response data standardized processing, ensuring data format consistency
7. **Caching Strategy**: isDirty state tracks modification status, supports pre-save confirmation and data recovery functionality
8. **Association Relationships**: Mapping relationship between WorkflowStep and PromptResponse, user permissions and editing permissions association validation

---

# Team Memory
### 20250723211650_D5E2
**Project:** aupro-frontend-service
**Importance:** ⭐⭐⭐⭐⭐
**Tags:** Component-Composition, Data-Display, Layout-Structure, Information-Architecture, Detail-Page

Detail Page Information Architecture

Detail pages implement structured information architecture with clear content hierarchy:
1) **Information Layering**: Clear separation between basic information area and content area
2) **Component Composition**: Reusable composition pattern of PromptBasicInfo + MarkdownContent
3) **Data Passing**: Pass prompt data and ruleType metadata through props
4) **State Management**: Unified loading and error state handling patterns
5) **URL Parameters**: Retrieve resource ID from route parameters for data fetching
6) **State Passing**: Pass additional context information through location.state
7) **Error Handling**: User-friendly prompts for resource not found or loading failures
8) **Layout Consistency**: Maintain consistent layout structure with other detail pages

---

# Frontend Seven-Step Framework Template Content

Frontend development framework based on React + TypeScript + Ant Design technology stack

---

# Requirements Anchoring

## Objective

Extract core user experience goals and functional essence from frontend requirement descriptions

## Output Format

```
## Requirements
[Use user-oriented verb phrases to describe the essence of requirements, focusing on user value and interactive experience]
```

## Key Points

- **User Value Focus**: Abstract what problems are solved for users and what experiential value is created
- **Interaction Boundary Definition**: Clarify usage scenarios and user operation boundaries
- **Performance Expectations**: Consider performance requirements for user experience (loading speed, response time, etc.)
- **Use Verb Phrases**: Such as "Enable users to...", "Allow users to...", "Provide users with..."
- **Avoid Technical Implementation**: Focus on business value rather than technical details

## Quality Standards

- Core user needs can be summarized in one sentence
- Reflect user experience value rather than technical features
- Clear functional boundaries and usage scenarios

---

# Business Model

## Objective

Build frontend data models and component relationships to provide clear data structure foundation for UI implementation

## Output Format

````
## Business Model
```mermaid
classDiagram
direction TB

class [UIComponent] {
    +[PropType] [propName]
    +[StateType] [stateName]
    +[HandlerType] [handlerMethod]()
}

class [DataModel] {
    +[FieldType] [fieldName]
    +[FieldType] [fieldName]
    +[ValidationRule]
}

class [APIRequest] {
    +[ParamType] [paramName]
    +[ConfigType] [configName]
}

class [APIResponse] {
    +[DataType] [dataField]
    +[MetaType] [metaField]
    +[PaginationType] pagination
}

class [RouteParams] {
    +[ParamType] [routeParam]
}

[UIComponent] --> [DataModel] : displays
[UIComponent] --> [APIRequest] : triggers
[APIRequest] --> [APIResponse] : returns
[RouteParams] --> [UIComponent] : configures
[APIResponse] --> [DataModel] : maps to
````

## Key Points

- **Component Data Structure**: Define React component Props, State, and event handlers
- **API Data Model**: Clarify request parameters, response data structure, and pagination patterns
- **Route Parameters**: Define data types for URL parameters and query parameters
- **Form Data**: Define form fields, validation rules, and submission data formats
- **Existing Implementation Priority**: Extend based on current project data types (such as Prompt, WorkflowItem, etc.)
- **TypeScript Types**: Ensure all data models have clear TypeScript interface definitions
- **Pagination Response**: Follow existing pagination response format (content, total, page, size, last, etc.)

## Quality Standards

- Clear and explicit data flow direction
- Support TypeScript type checking
- Comply with existing project data specifications
- Facilitate component implementation and testing

---

# Solution

## Objective

Provide frontend architecture solutions and user experience design strategies

## Output Format

```
## Solution

1. [UI/UX Strategy]:
   - [User interface design approach]
   - [User interaction patterns]
   - [Responsive design considerations]
   - [Accessibility requirements]

2. [Component Architecture]:
   - [Component hierarchy and composition]
   - [State management strategy (useState, useContext, etc.)]
   - [Props interface design]
   - [Component reusability patterns]

3. [Data Flow Strategy]:
   - [API integration patterns using Axios client]
   - [Error handling and loading states]
   - [Data caching and performance optimization]
   - [Form validation and submission patterns]

4. [Navigation Strategy]:
   - [React Router navigation patterns]
   - [URL parameter handling]
   - [Breadcrumb and navigation state management]
   - [Deep linking and bookmark support]

5. [Performance Strategy]:
   - [Component lazy loading]
   - [Bundle optimization]
   - [Image and asset optimization]
   - [Pagination and infinite scroll patterns]
```

## Key Points

- **Design System**: Consistent design solution based on Ant Design component library
- **User Experience**: Complete strategy for loading states, error handling, and interaction feedback
- **Technical Architecture**: React component design patterns, state management, route navigation
- **Performance Optimization**: Code splitting, lazy loading, caching strategies
- **Accessibility**: Keyboard navigation, screen readers, semantic tags

## Quality Standards

- Solutions focus on user experience
- Technology choices align with project stack
- Consider maintainability and scalability

---

# Structure Definition

## Objective

Define frontend component architecture, dependency relationships, and file organization structure

## Output Format

```
## Structure

### Component Hierarchy
1. Page Components (src/pages/)
   - [PageComponent] serves as route entry component
   - Manages page-level state and data fetching
   - Composes multiple Feature Components

2. Feature Components (src/components/)
   - [FeatureComponent] implements specific functional modules
   - Reusable business logic components
   - Contains own sub-components and styles

3. UI Components (src/components/)
   - [UIComponent] pure presentation components
   - Contains no business logic
   - Highly reusable

### Data Flow Dependencies
1. Page Component calls API Service (src/api/)
2. API Service uses HTTP Client (src/api/client.ts)
3. HTTP Client integrates Okta Authentication
4. Page Component uses React Context (src/contexts/)
5. Components use React Router (src/router/)
6. Form Components use Ant Design Form validation

### File Organization
1. src/pages/[feature]/
   - [feature].tsx (main page component)
   - [feature].less (page styles)
   - [feature].test.tsx (page tests)
   - components/ (page-specific components)

2. src/components/[componentName]/
   - [componentName].tsx (component implementation)
   - [componentName].less (component styles)
   - [componentName].test.tsx (component tests)

3. src/api/
   - api.ts (API method definitions)
   - client.ts (HTTP client configuration)

4. src/type/
   - type.ts (TypeScript type definitions)

5. src/styles/
   - theme.ts (Ant Design theme configuration)
   - colors.less (color variables)
   - variable.less (style variables)
```

## Key Points

- **Component Layering**: Clear hierarchy of page components -> feature components -> UI components
- **Dependency Injection**: Pass data and callback functions through Props
- **State Management**: useState for component state, useContext for global state
- **Router Integration**: React Router for page navigation and parameter passing
- **Style Isolation**: Each component has independent LESS style files

## Quality Standards

- Clear separation of component responsibilities
- File organization follows team standards
- Simple and clear dependency relationships

---

# Task Orchestration

## Objective

Transform frontend design into specific executable development tasks

## Output Format

```
## Tasks

### Create/Update TypeScript Type Definitions
1. Location: src/type/type.ts
2. Define interfaces:
   - Interface name: Describe the specific purpose of the interface
   - Define required fields and their data types, add field description comments
   - Define optional fields using question mark, add optional field description comments
   - Use TypeScript interface syntax to create type definitions
3. Export types: Ensure proper import and usage in components

### Implement API Service Methods
1. Location: src/api/api.ts
2. Method name: [methodName]
3. Request type: [GET|POST|PUT|DELETE]
4. Endpoint: [/api/endpoint]
5. Parameter type: [ParameterInterface]
6. Return type: [ResponseInterface]

### Create/Update React Components
1. Location: src/[pages|components]/[componentPath]/[componentName].tsx
2. Component type: [Functional Component with TypeScript]
3. Props interface:
   - Define component Props interface, named with component name plus Props suffix
   - Declare property names and corresponding data types, add property description comments
   - Declare event handler functions, define parameter types and return void, add event handler description comments
   - Use TypeScript interface syntax to ensure type safety
4. State management:
   - useState: [state variable description]
   - useEffect: [side effect description]
   - custom hooks: [custom Hook description]
5. Rendering logic:
   - Conditional rendering logic
   - List rendering and key handling
   - Event handler binding
6. Ant Design integration:
   - Components used: [Button, Table, Form, etc.]
   - Theme configuration application
   - Form validation rules

### Implement Route Configuration
1. Location: src/router/routes.tsx
2. Route items:
   - Define route object containing key, path, element properties
   - Set key property as unique identifier for the route
   - Set path property as URL path pattern
   - Set element property as corresponding React component JSX element
   - Follow RouteItem interface data structure
3. Parameter routes: Use :id or :slug parameters
4. Nested routes: Route configuration under SecureRoute protection

### Create Component Styles
1. Location: src/[pages|components]/[componentPath]/[componentName].less
2. Style specifications:
   - Use LESS variables (@color-primary, @font-size-base, etc.)
   - BEM naming convention (.component-name__element--modifier)
   - Responsive design (media queries)
   - Ant Design theme variable overrides
3. Style organization:
   - Import project common color and variable style files at the top of the file
   - Define component root style class using component name as class name
   - Use LESS nesting syntax and & symbol to define child element styles
   - Use double underscore (__) for elements, double hyphen (--) for modifiers
   - Add comments for each style block explaining purpose

### Configure Error Handling
1. Implement error boundary component (ErrorBoundary)
2. API error handling strategy (Axios interceptors)
3. User-friendly error prompts (Ant Design Message/Notification)
4. 404 page and route error handling

### Performance Optimization Configuration
1. React.lazy and Suspense for code splitting
2. useMemo and useCallback for rendering performance optimization
3. Image lazy loading and optimization
4. Pagination and virtual scrolling implementation
```

## Key Points

- **Based on Architecture Design**: Strictly design tasks according to previously defined component structure and data flow
- **Development Order**: Type definitions -> API methods -> Component implementation -> Styles -> Testing
- **Dependencies**: Clarify dependency order between tasks to ensure gradual implementation
- **Code Standards**: Follow existing project code style and naming conventions
- **Test Coverage**: Every component should have corresponding unit tests

## Quality Standards

- Tasks can be independently executed and completed
- Have clear acceptance criteria
- Comply with project technology stack specifications

---

# Common Tasks

## Objective

Define common specifications and best practices for frontend development

## Output Format

```
## Common Tasks

1. TypeScript Type Specifications:
   - All component Props must have clearly defined interfaces
   - Use Union Types to handle multiple states
   - Export reusable type definitions
   - Avoid using any type, prefer using unknown

2. React Component Specifications:
   - Functional components use React.FC type annotation
   - Use destructuring assignment to extract Props and State
   - Properly use useCallback and useMemo for performance optimization
   - Custom Hooks encapsulate reusable logic

3. Ant Design Integration Specifications:
   - Use project unified theme configuration (src/styles/theme.ts)
   - Form components must be configured with proper validation
   - Uniformly use project-defined common components (src/components/customAntdComponents.tsx)
   - Loading states use project unified Loading component

4. API Integration Specifications:
   - All API calls use encapsulation methods from src/api/client.ts
   - Request parameters and response data must have TypeScript type definitions
   - Error handling uses Axios interceptors for unified processing
   - Support automatic token management for Okta authentication

5. Routing Specifications:
   - All routes need to be under SecureRoute protection
   - Use useNavigate for programmatic navigation
   - Route parameters retrieved using useParams
   - Support user authentication state recovery and original path saving

6. Style Specifications:
   - Each component has independent LESS style files
   - Use project-defined colors and variables (src/styles/)
   - Responsive design using CSS Grid and Flexbox
   - Follow BEM naming conventions

7. Error Handling Specifications:
   - Page-level errors wrapped with ErrorBoundary
   - API errors handled globally through Axios interceptors
   - User operation errors prompted using Ant Design Message components
   - Standardized handling of Loading and Empty states

8. Internationalization Specifications:
   - Reserve text extraction interfaces for future multi-language support
   - Avoid hard-coded text content
   - Use standardized processing for time and date formats

9. Code Quality Specifications:
    - Use ESLint and Prettier to ensure code format consistency
    - Add appropriate comments to components and functions
    - Follow single responsibility principle, keep component functionality focused
    - Regularly refactor code to eliminate duplicate code
```

## Key Points

- **Technology Stack Unity**: Based on latest practices of React 19, TypeScript, Ant Design 5.x
- **Engineering Standards**: Complete engineering with Vite build, Vitest testing, ESLint code checking
- **Performance Best Practices**: Standardization of code splitting, lazy loading, caching strategies
- **Maintainability**: Quality assurance through modular design, type safety, test coverage

## Quality Standards

- Specifications are actionable
- Comply with modern frontend development best practices
- Support team collaboration and code maintenance

---

# Constraint Control

## Objective

Define boundary conditions, performance standards, and quality requirements for frontend development

## Output Format

```
## Constraints

1. Technology Stack Constraints:
   - Must use React 19 + TypeScript for development
   - UI component library limited to Ant Design 5.x series
   - HTTP client uses Axios, integrated with Okta authentication
   - Route management uses React Router v7
   - Build tool uses Vite, testing framework uses Vitest

2. Browser Compatibility Constraints:
   - Support latest two versions of Chrome, Firefox, Safari, Edge
   - Mobile support for iOS Safari and Android Chrome
   - No support for IE browser
   - Minimum screen resolution: 1024x768

3. Performance Constraints:
   - First screen loading time not exceeding 3 seconds
   - Page switching response time not exceeding 500ms
   - Single page Bundle size not exceeding 500KB
   - Image resources must be compressed and optimized
   - Long lists must implement pagination or virtual scrolling

4. User Experience Constraints:
   - All interactions must have immediate feedback (loading, success, error states)
   - Form validation must provide clear error prompts
   - Support keyboard navigation and accessibility
   - Responsive design adapted for mobile and desktop
   - Error pages must provide return paths

5. Security Constraints:
   - All API requests must carry Okta JWT Token
   - Sensitive data must not be stored in plain text on client side
   - Route access must be protected through SecureRoute
   - User session timeout automatically redirects to login page
   - Prevent XSS attacks, avoid dangerouslySetInnerHTML

6. API Integration Constraints:
   - All API calls must have error handling
   - Request timeout set to 60 seconds
   - Support request retry mechanism (401 error automatic token refresh)
   - API response data must have TypeScript type definitions
   - Pagination interfaces follow unified response format

7. State Management Constraints:
   - Prioritize React built-in useState and useContext
   - Avoid introducing additional state management libraries (Redux, Zustand, etc.)
   - Global state only for user information and application-level configuration
   - Component state follows unidirectional data flow principle

8. File Organization Constraints:
   - Each component must have independent directory and test files
   - Style files placed in same directory as component files
   - Public type definitions unified in src/type/ directory
   - API methods unified in src/api/ directory
   - Direct inline styles in components not allowed
```

## Key Points

- **Clear Technical Boundaries**: Strictly limit technology selection to avoid technology stack confusion
- **Quantifiable Performance**: Provide specific performance metrics and measurement standards
- **Verifiable Quality**: Verify constraint conditions through automated tools
- **User Experience First**: All constraints serve better user experience

## Quality Standards

- Constraint conditions are clear and verifiable
- Cover development, testing, deployment full process
- Support automated checking and quality gates
