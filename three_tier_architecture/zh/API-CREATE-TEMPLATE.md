## 需求
实现一个[实体名称]API端点，允许用户创建新的[实体名称]。

## 业务模型
```mermaid
classDiagram
direction TB

    class [实体类名] {
        +String id
        +[其他属性类型] [其他属性名]
        +timestamp createdAt
        +timestamp updatedAt
    }

    class [请求类名] {
        +[属性类型] [属性名]
        +[属性类型] [属性名]
        ...
    }

    class [响应类名] {
        +String id
        +[属性类型] [属性名]
        +timestamp createdAt
        +timestamp updatedAt
        ...
    }

    [实体类名] "1" -- "1" [响应类名] : maps to
    [请求类名] "1" -- "1" [实体类名] : creates
```

## 解决方案
1. API设计:
   - 创建POST端点 `/api/v1/[实体名称复数形式]` 用于创建新的[实体名称]
   - 返回适当的HTTP状态码表示成功和错误情况
   - [特殊处理逻辑，如有]

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

### 创建[实体类名]类（领域模型）
  1. 属性:
     - id: String
     - [其他属性名]: [其他属性类型]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: fromRequest([请求类名] request): [实体类名]
     - 逻辑:
       - 返回一个新的[实体类名]对象，设置id为新生成的UUID
       - 从请求中提取并设置其他属性
  4. 添加静态方法: fromPO([实体类名]PO po): [实体类名]
     - 逻辑:
       - 将持久化对象转换为领域模型对象

### 创建[实体类名]PO类（持久化模型）
  1. 属性:
     - id: String
     - [其他属性名]: [其他属性类型]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 添加唯一约束:
     - 使用@Table(uniqueConstraints = @UniqueConstraint(columnNames = {"[业务键字段1]", "[业务键字段2]"}))注解
  3. 添加静态方法: of([实体类名] entity): [实体类名]PO
     - 逻辑:
       - 将领域模型对象转换为持久化对象

### 创建[请求类名]类
  1. 属性:
     - [属性名]: [属性类型] (必需/可选)
     - [属性名]: [属性类型] (必需/可选)
     - [如果使用方式二] idempotencyKey: String (用于幂等性控制)
     - ...
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 验证:
     - [必需属性]: @NotBlank/@NotNull
     - [其他验证注解]

### 创建[响应类名]类
  1. 属性:
     - id: String
     - [其他属性名]: [其他属性类型]
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: of([实体类名] entity): [响应类名]
     - 逻辑:
       - 将领域模型对象映射为响应对象
       - 返回响应对象

### 创建[实体类名]Controller类实现创建API
  1. 端点: `/api/v1/[实体名称复数形式]`
     1. 方法: POST
     2. 请求体: [请求类名]
     3. 响应体: 返回[响应类名]类型的数据
     4. 逻辑:
        - 调用[实体类名小写]Service.create[实体类名](request)
        - 将[实体类名]实体映射为[响应类名]DTO
        - 返回201 Created状态码和创建的数据
        - 如果请求体缺少必需字段，返回400 Bad Request
        - 如果资源已存在（幂等性检查），返回200 OK和已存在的资源
        - [其他错误处理逻辑]

### 创建[实体类名]Service接口
  1. 添加方法: create[实体类名]([请求类名] request): [实体类名]

### 创建[实体类名]ServiceImpl类实现创建逻辑
  1. 实现create[实体类名]方法:
     - 逻辑:
       - [数据验证逻辑，如有]
       - [如果使用方式一] 根据业务键检查资源是否已存在，如果已存在则返回现有资源
       - [如果使用方式二] 检查idempotencyKey是否已处理，如果已处理则返回之前的结果
       - [如果使用方式三] 根据条件检查资源是否已存在，如果已存在则返回现有资源
       - 创建新的[实体类名]对象，使用[实体类名].fromRequest(request)
       - 设置必要的字段（id、createdAt、updatedAt等）
       - [空值检查逻辑，如有]
       - 调用[实体类名小写]Repository.save(entity)保存实体
       - [如果使用方式二] 记录已处理的idempotencyKey和对应的资源ID
       - 返回保存的[实体类名]对象

### 创建[实体类名]Repository接口
  1. 添加方法: save([实体类名] entity): [实体类名]
  2. [如果使用方式一或方式三] 添加方法: findBy[业务键]([业务键类型] [业务键]): Optional<[实体类名]>

### 创建[实体类名]RepositoryImpl类实现存储逻辑
  1. 实现save方法:
     - 逻辑:
       - 将[实体类名]实体转换为[实体类名]PO，使用[实体类名]PO.of(entity)
       - 调用[实体类名小写]DAO.save(po)保存实体
       - 将保存的[实体类名]PO转换回[实体类名]实体，使用[实体类名].fromPO(po)
       - 返回保存的[实体类名]对象
  2. [如果使用方式一或方式三] 实现findBy[业务键]方法:
     - 逻辑:
       - 调用[实体类名小写]DAO.findBy[业务键]([业务键])查找实体
       - 如果找到，将[实体类名]PO转换为[实体类名]
       - 返回Optional<[实体类名]>

### 创建[实体类名]DAO接口
  1. 继承JpaRepository<[实体类名]PO, String>
  2. [如果使用方式一或方式三] 添加方法: findBy[业务键]([业务键类型] [业务键]): Optional<[实体类名]PO>

### [如果使用方式二] 创建IdempotencyKeyRepository接口和实现类
  1. 用于存储和检查已处理的幂等性键
  2. 添加方法: save(String key, String resourceId): void
  3. 添加方法: findByKey(String key): Optional<String>

## 通用任务
1. 所有repository实现类都应使用@Repository注解
2. 所有Repository类都应实现JPA repository
3. 所有Service类都应使用@Service注解
4. 所有Controller类都应使用@RestController注解
5. 所有DTO和模型类都应使用@Data注解
6. 所有POJO类应使用@Data、@Entity、@Table、@AllArgsConstructor、@NoArgsConstructor注解

## 约束条件
- 如果请求体缺少必需字段，返回400 Bad Request
- 成功创建后返回201 Created状态码
- 如果资源已存在（幂等性检查），返回200 OK和已存在的资源
- 手动为实体生成唯一ID，不依赖数据库自动生成
- 初始化集合为空列表以防止空指针异常
- 在数据库层面添加唯一约束以确保幂等性
- [其他特定约束条件] 