## 需求
实现一个`[实体名称]`API端点，允许用户创建新的`[实体名称]`。

## 业务模型
```
类图关系:

[实体类名] {
    +String id
    +[其他属性类型] [其他属性名]
    +timestamp createdAt
    +timestamp updatedAt
}

[请求类名] {
    +[属性类型] [属性名]
    +[属性类型] [属性名]
    ...
}

[响应类名] {
    +String id
    +[属性类型] [属性名]
    +timestamp createdAt
    +timestamp updatedAt
    ...
}

关系:
- [实体类名] "1" -- "1" [响应类名] : maps to
- [请求类名] "1" -- "1" [实体类名] : creates
```

## 解决方案
1. API设计:
   - 创建POST端点 `/api/v1/[实体名称复数形式]` 用于创建新的`[实体名称]`
   - 返回适当的HTTP状态码表示成功和错误情况
   - `[特殊处理逻辑，如有]`

2. 幂等性实现:
   - 为请求添加唯一标识符（如客户端生成的UUID或业务唯一键）
   - 在数据库中添加唯一约束（如name+owner组合或其他业务唯一键）
   - 在服务层实现检查逻辑，避免重复创建
   - 对于重复请求，返回已存在的资源而不是创建新资源
   - 实现方式：
     - 方式一：使用自然业务键（如在[实体类名]DAO中添加findBy[业务键]方法）
     - 方式二：使用请求ID（如添加idempotencyKey参数并存储已处理的请求ID）
     - 方式三：使用条件检查（如在创建前检查资源是否已存在）
   
   - 幂等性实现方式选择建议：
     - 对于简单业务：优先使用方式一（自然业务键）或方式三（条件检查），实现简单直接
     - 对于有性能要求的复杂业务：优先使用方式二（请求ID），可以避免重复的业务逻辑处理，提高性能
     - 在实际应用中，可以根据具体需求组合使用多种方式，以提供更强的幂等性保证

## 结构

### 继承关系
1. [实体类名]Service接口定义[实体类名]服务方法
2. [实体类名]ServiceImpl实现[实体类名]Service接口
3. [实体类名]Repository接口定义[实体类名]仓库方法
4. [实体类名]RepositoryImpl实现[实体类名]Repository接口

### 依赖关系
1. [实体类名]Controller调用[实体类名]Service
2. [实体类名]ServiceImpl调用[实体类名]Repository
3. [实体类名]RepositoryImpl调用[实体类名]DAO

## 任务

### 创建`[实体类名]`类（领域模型）
  1. 属性:
     - id: String
     - `[其他属性名]`: `[其他属性类型]`
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: fromRequest(`[请求类名]` request): `[实体类名]`
     - 逻辑:
       - 返回一个新的`[实体类名]`对象，设置id为新生成的UUID
       - 从请求中提取并设置其他属性
  4. 添加静态方法: fromPO(`[实体类名]`PO po): `[实体类名]`
     - 逻辑:
       - 将持久化对象转换为领域模型对象

### 创建`[实体类名]`PO类（持久化模型）
  1. 属性:
     - id: String
     - `[其他属性名]`: `[其他属性类型]`
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 添加唯一约束:
     - 使用@Table(uniqueConstraints = @UniqueConstraint(columnNames = {"[业务键字段1]", "[业务键字段2]"}))注解
  3. 添加静态方法: of([实体类名] entity): [实体类名]PO
     - 逻辑:
       - 将领域模型对象转换为持久化对象

### 创建`[请求类名]`类
  1. 属性:
     - `[属性名]`: `[属性类型]` (必需/可选)
     - `[属性名]`: `[属性类型]` (必需/可选)
     - `[如果使用方式二]` idempotencyKey: String (用于幂等性控制)
     - ...
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 验证:
     - `[必需属性]`: @NotBlank/@NotNull
     - `[其他验证注解]`

### 创建`[响应类名]`类
  1. 属性:
     - id: String
     - `[其他属性名]`: `[其他属性类型]`