# 七步框架模板内容


# 需求锚定（Requirements）

## 目标
从需求描述中提取核心问题本质和根本目标

## 输出格式
```
## Requirements
[使用简洁的动词短语描述需求的本质，避免功能特性列举]
```

## 构建要点
- **本质提炼**：抽象出解决什么根本问题、为谁创造什么价值
- **边界定义**：明确解决方案的适用范围和限制条件
- **价值聚焦**：突出业务价值和用户获益
- **使用动词短语**：如"Implement..."、"Create..."、"Design..."
- **避免特征堆砌**：不要列举具体功能，要抽象出需要解决的本质问题

## 质量标准
- 一句话能概括核心需求
- 体现业务价值而非技术实现
- 明确问题边界和约束 

---

# 业务模型（Business Model）

## 目标
构建清晰的业务实体关系模型，为后续设计提供概念基础

## 输出格式
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

## 构建要点
- **实体识别**：识别核心业务实体、支撑实体、DTO对象
- **属性建模**：为每个实体定义关键属性，使用"类型+名称"格式
- **关系建模**：明确实体间的关系类型（1:1, 1:N, N:M）和业务语义
- **现有实现优先**：如果当前数据结构能够满足需求，必须保持现有实现不变
- **最小变更原则**：仅在现有结构确实无法支持新需求时才进行重构
- **接口设计**：包含关键的方法和静态工厂方法
- **数据流向**：体现请求->处理->响应的完整数据流
- **一致性保障**：确保模型能被AI准确理解和实现
- **简洁 > 功能丰富**：避免过度工程化，保持系统可理解性

## 保守性约束
- **禁止不必要重构**：如果现有简单数据类型（如List<String>）能满足需求，严禁创建复杂实体包装
- **功能驱动变更**：只有在明确的功能需求无法通过现有结构实现时，才考虑结构调整
- **渐进式改进**：优先考虑在现有结构基础上扩展，而非推倒重建
- **向后兼容**：任何结构变更必须保证向后兼容，避免破坏性变更

## 质量标准
- 关注当前任务流程
- 实体关系清晰准确
- 支持后续技术实现
- 保持现有实现的简洁性
- 避免过度抽象和不必要的复杂性 

---

# 解决方案（Solution）

## 目标
提供高层次的解决策略和架构方案，指导具体实现

## 输出格式
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

## 构建要点
- **分类组织**：按解决方案类别组织（如API设计、数据处理、异常处理等）
- **架构决策**：提供关键的技术架构选择和设计模式
- **最佳实践**：结合行业标准和经验总结
- **决策依据**：说明为什么选择特定方案的原因
- **风险评估**：识别潜在风险和应对策略

## 质量标准
- 方案具有可操作性
- 涵盖关键技术决策
- 体现架构思维 

---

# 结构定义（Structure）

## 目标
定义系统的技术架构和组件依赖关系

## 输出格式
```
## Structure

### 继承关系（Inheritance Relationships）
1. [Interface] interface定义[functionality description]
2. [Implementation] implements [Interface] interface
3. [DomainModel] extends [BaseModel] class
4. [Controller] extends [BaseController] class
5. [BusinessException] extends RuntimeException class（业务异常基类）
6. [SpecificBusinessException] extends [BusinessException] class（具体业务异常类）

### 依赖关系（Dependencies）
1. [ComponentA] 调用 [ComponentB]
2. [Service] 依赖 [Repository] 和 [ExternalService]
3. [Controller] 注入 [Service] 和 [ValidationService]

### 分层架构（Layered Architecture）
1. Controller Layer: [ResponsibilityDescription]
2. Service Layer: [ResponsibilityDescription]
3. Repository Layer: [ResponsibilityDescription]
4. Data Access Layer: [ResponsibilityDescription]
5. Exception Handling Layer: [GlobalExceptionHandler for unified error handling]
```

## 构建要点
- **继承体系**：明确接口、抽象类、实现类的继承关系
- **依赖链路**：定义组件间的调用和依赖关系
- **分层设计**：体现清晰的分层架构（Controller -> Service -> Repository -> DAO）
- **职责分离**：每层的职责边界和交互接口
- **扩展接口**：为未来功能扩展预留的接口和扩展点

## 质量标准
- 架构层次清晰
- 依赖关系合理
- 支持系统扩展 

---

# 任务编排（Tasks）

## 目标
将抽象方案转化为具体可执行的实现任务

## 输出格式
```
## Tasks

### 创建/更新/删除[ComponentType] - [ComponentName]类
1. 职责：[Clear responsibility description]
2. 属性：
   - [attributeName]: [Type] - [Description]
   - [attributeName]: [Type] - [Description with validation rules]
3. 方法：
   - [methodName]([parameters]): [ReturnType]
     - 逻辑：
       - [Step-by-step implementation logic]
       - [Conditional logic and edge cases]
       - [Error handling approach]
4. 注解：
   - [RequiredAnnotations for framework integration]
5. 约束：
   - [Validation rules and business constraints]

### 实现[ServiceType] - [ServiceName]服务
1. 接口定义：[Interface methods and contracts]
2. 核心方法：[methodName]([parameters]): [ReturnType]
   - 输入验证：[Input validation rules]
   - 业务逻辑：[Core business logic steps]
   - 异常处理：[Exception handling strategy]
   - 返回值：[Return value construction]
3. 依赖注入：[Required dependencies]
4. 事务管理：[Transaction boundary definition]

### 配置[ConfigurationType] - [ConfigurationName]
1. 配置项：[Configuration parameters]
2. 默认值：[Default value settings]
3. 环境变量：[Environment-specific settings]
4. 验证规则：[Configuration validation]

### 创建异常处理器 - GlobalExceptionHandler
1. 职责：统一处理全局异常，提供标准化错误响应
2. 异常类型：
   - BusinessException: [Business logic exceptions]
   - ValidationException: [Input validation exceptions]
   - SystemException: [System-level exceptions]
   - RuntimeException: [Unexpected runtime exceptions]
3. 方法：
   - handleBusinessException(BusinessException): ResponseEntity<ErrorResponse>
   - handleValidationException(ValidationException): ResponseEntity<ErrorResponse>
   - handleSystemException(SystemException): ResponseEntity<ErrorResponse>
   - handleGenericException(Exception): ResponseEntity<ErrorResponse>
4. 注解：
   - @RestControllerAdvice
   - @ExceptionHandler for each exception type
5. 响应格式：
   - 统一的错误响应结构（错误码、错误消息、时间戳等）

### 创建业务异常类 - [BusinessExceptionName]
1. 职责：定义特定业务场景的异常类型，提供清晰的错误信息和错误码
2. 继承关系：
   - extends RuntimeException 或 extends BusinessException（如果有基础业务异常类）
3. 属性：
   - errorCode: String - 业务错误码（如：USER_NOT_FOUND, INVALID_OPERATION等）
   - errorMessage: String - 详细错误描述
   - timestamp: LocalDateTime - 异常发生时间
   - context: Map<String, Object> - 异常上下文信息（可选）
4. 构造方法：
   - [ExceptionName](String errorCode, String errorMessage)
   - [ExceptionName](String errorCode, String errorMessage, Throwable cause)
   - [ExceptionName](String errorCode, String errorMessage, Map<String, Object> context)
5. 方法：
   - getErrorCode(): String - 获取错误码
   - getErrorMessage(): String - 获取错误消息
   - getContext(): Map<String, Object> - 获取上下文信息
   - toString(): String - 格式化异常信息
6. 使用场景：
   - [Specific business scenarios where this exception should be thrown]
   - [Validation rules that trigger this exception]
   - [Business logic conditions that warrant this exception]
7. 异常分类：
   - 数据异常：如 DataNotFoundException, DataConflictException
   - 权限异常：如 UnauthorizedException, ForbiddenException
   - 业务规则异常：如 BusinessRuleViolationException, InvalidStateException
   - 外部依赖异常：如 ExternalServiceException, IntegrationException
```

## 构建要点
- **基于前四阶段**：严格基于需求、模型、方案、结构的完整上下文
- **任务分类**：按功能模块或组件类型分组（实体类、服务类、控制器等）
- **实现细节**：包含具体的代码规范、配置要求、业务逻辑
- **执行顺序**：按依赖关系组织任务执行顺序
- **职责单一**：每个任务职责明确且边界清晰
- **可验证性**：每个任务都有明确的完成标准
- **逻辑严谨性**：确保任务编排基于业务模型、解决方案、结构化设计，避免出现逻辑漏洞，保证上下文数据流的连贯性

## 质量标准
- 任务可直接执行
- 覆盖完整实现
- 细节准确具体 

---

# 通用任务（Common Tasks）

## 目标
定义统一的编码规范和通用实现模式

## 输出格式
```
## Common Tasks
1. 注解规范：[Specific annotation requirements for different component types]
2. 依赖注入：[Dependency injection patterns and best practices]  
3. 异常处理：[Unified exception handling approach via GlobalExceptionHandler]
   - 自定义异常类型定义和继承关系
   - 业务异常类创建标准：
     * 继承RuntimeException或自定义BusinessException基类
     * 必须包含errorCode（业务错误码）和errorMessage（错误描述）
     * 提供多种构造方法支持不同场景
     * 按业务领域分类（数据异常、权限异常、业务规则异常、外部依赖异常）
   - 统一错误响应格式（ErrorResponse DTO）
   - 异常处理器方法的标准实现模式
   - 日志记录和异常跟踪机制
4. 数据验证：[Common validation patterns and rules]
5. 日志记录：[Logging standards and patterns]
6. 文档规范：[Documentation and comment standards]
```

## 构建要点
- **标准化**：定义统一的编码规范和配置模式
- **复用性**：提取可复用的通用实现模式
- **一致性**：确保所有组件遵循相同的标准
- **质量保障**：内置验证和校验机制
- **最佳实践**：体现行业最佳实践和经验总结

## 质量标准
- 规范明确具体
- 易于执行检查
- 体现最佳实践 

---

# 约束控制（Constraints）

## 目标
定义明确的边界条件和质量标准

## 输出格式
```
## Constraints
1. 功能约束：[Functional requirements and limitations with specific criteria]
2. 性能约束：[Performance requirements with measurable metrics]
3. 安全约束：[Security requirements and compliance standards]
4. 集成约束：[Integration limitations and compatibility requirements]
5. 业务规则约束：[Business rule validation with specific conditions]
6. 异常处理约束：[Exception handling standards and requirements]
   - 业务异常必须包含明确的错误码和错误消息
   - 异常类型必须按业务领域分类和命名
   - 异常信息不得暴露敏感的系统内部信息
   - 所有业务异常必须被GlobalExceptionHandler统一处理
7. 技术约束：[Technical implementation restrictions and standards]
8. 数据约束：[Data validation rules and format requirements]
9. API约束：[API design standards and interface contracts]
```

## 构建要点
- **边界明确**：清晰定义可以做什么和不能做什么
- **可验证性**：约束条件应该可以验证
- **完整性**：覆盖功能、性能、安全、集成等各个方面
- **实用性**：约束应该有助于提高代码质量和系统稳定性
- **量化标准**：尽可能提供可量化的标准和指标

## 质量标准
- 约束条件明确
- 可验证
- 覆盖面完整 