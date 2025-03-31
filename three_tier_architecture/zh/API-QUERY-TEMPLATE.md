## 需求
实现一个`[实体名称]`API端点，允许用户通过各种条件检索`[实体名称]`。

## 业务模型（Mermaid）
```
classDiagram
direction TB

    class `[实体类名]` {
        +String id
        +`[其他属性类型]` `[其他属性名]`
        +timestamp createdAt
        +timestamp updatedAt
    }

    class Paged`[实体类名]`Response {
        +List~`[实体类名]`Response~ content
        +int totalPages
        +long totalElements
        +int size
        +int number
        +boolean first
        +boolean last
    }

    class `[实体类名]`Response {
        +String id
        +`[其他属性类型]` `[其他属性名]`
        +timestamp createdAt
        +timestamp updatedAt
    }

    `[实体类名]` "n" -- "1" Paged`[实体类名]`Response : contains
```

## 解决方案
1. API设计:
   - 创建GET端点 `/api/v1/[实体名称复数形式]` 用于按条件检索`[实体名称]`
   - `[如果需要按ID检索]` 创建GET端点 `/api/v1/[实体名称复数形式]/ids` 用于按ID检索`[实体名称]`
   - 为大型结果集实现分页
   - 支持按不同字段排序
   - 返回适当的HTTP状态码表示成功和错误情况

## 结构

### 继承关系
1. `[实体类名]`Service接口定义`[实体类名]`服务方法
2. `[实体类名]`ServiceImpl实现`[实体类名]`Service接口
3. `[实体类名]`Repository接口定义`[实体类名]`仓储方法
4. `[实体类名]`RepositoryImpl实现`[实体类名]`Repository接口

### 依赖关系
1. `[实体类名]`Controller调用`[实体类名]`Service
2. `[实体类名]`ServiceImpl调用`[实体类名]`Repository
3. `[实体类名]`RepositoryImpl调用`[实体类名]`DAO

## 任务

### 创建`[实体类名]`QueryParams类
  1. 属性:
     - `[查询参数名]`: `[参数类型]`
     - `[查询参数名]`: `[参数类型]`
     - page: Integer
     - size: Integer
     - sortBy: String
     - sortDirection: String
  2. 构造函数:
     - 使用@AllArgsConstructor注解
     - 默认值:
       - page: 0
       - size: 10
       - sortBy: "createdAt"
       - sortDirection: "DESC"

### 创建`[实体类名]`Response类
  1. 属性:
     - id: String
     - `[其他属性名]`: `[其他属性类型]`
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: of(List<`[实体类名]`> entities): List<`[实体类名]`Response>
     - 逻辑:
       - 将List<`[实体类名]`>映射为List<`[实体类名]`Response>
       - 返回`[实体类名]`Response列表

### 创建Paged`[实体类名]`Response类
  1. 属性:
     - content: List<`[实体类名]`Response>
     - totalPages: Integer
     - totalElements: Long
     - size: Integer
     - number: Integer
     - first: Boolean
     - last: Boolean
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: of(Page<`[实体类名]`> page): Paged`[实体类名]`Response
     - 逻辑:
       - 将Page<`[实体类名]`>映射为Paged`[实体类名]`Response
         - 设置content为`[实体类名]`Response.of(page.getContent())
         - 设置totalPages为page.getTotalPages()
         - 设置totalElements为page.getTotalElements()
         - 设置size为page.getSize()
         - 设置number为page.getNumber()
         - 设置first为page.isFirst()
         - 设置last为page.isLast()
       - 返回Paged`[实体类名]`Response

### 更新`[实体类名]`Controller类实现检索API
  1. `[如果需要按ID检索]` 端点: `/api/v1/`[实体名称复数形式]`/ids`
     1. 方法: GET
     2. 请求参数:
        - ids: List<String> (必需)
     3. 响应体: 返回List<`[实体类名]`Response>类型的数据
     4. 逻辑:
        - 调用`[实体类名小写]`Service.get`[实体类名]`sByIds(ids)
        - 将`[实体类名]`实体映射为`[实体类名]`Response DTO
        - 返回200 OK状态码和`[实体类名]`Response列表
        - 如果ids参数为空或无效，返回400 Bad Request
  
  2. 端点: `/api/v1/[实体名称复数形式]`
     1. 方法: GET
     2. 请求参数:
        - `[查询参数名]`: `[参数类型]` (可选) - `[参数描述]`
        - `[查询参数名]`: `[参数类型]` (可选) - `[参数描述]`
        - page: Integer (可选, 默认: 0)
        - size: Integer (可选, 默认: 10)
        - sortBy: String (可选, 默认: "createdAt")
        - sortDirection: String (可选, 默认: "DESC")
     3. 响应体: 返回Paged`[实体类名]`Response类型的数据
     4. 逻辑:
        - 调用`[实体类名小写]`Service.get`[实体类名]`sByCriteria(queryParams)
        - 将Page<`[实体类名]`>映射为Paged`[实体类名]`Response
        - 返回200 OK状态码和检索到的数据
        - 如果查询参数无效，返回400 Bad Request
        - 如果没有匹配条件的记录，返回空列表

### 更新`[实体类名]`Service接口添加检索方法
  1. `[如果需要按ID检索]` 添加方法: get`[实体类名]`sByIds(List<String> ids): List<`[实体类名]`>
  2. 添加方法: get`[实体类名]`sByCriteria(`[实体类名]`QueryParams queryParams): Page<`[实体类名]`>

### 创建`[实体类名]`CriteriaBuilder类
  1. 添加静态方法: buildPageableInfo(`[实体类名]`QueryParams queryParams): Pageable
     - 逻辑:
       - 验证page和size参数
       - 基于sortBy和sortDirection创建Sort对象
       - 返回带有page、size和排序信息的PageRequest
  2. 添加静态方法: buildSpecification(`[实体类名]`QueryParams queryParams): Specification<`[实体类名]`PO>
     - 逻辑:
       - 为每个查询参数创建Specification
       - 使用AND运算符组合Specification
       - 返回组合的Specification
       - 如果没有提供条件，返回默认Specification
   
### 更新`[实体类名]`ServiceImpl类实现检索逻辑
  1. `[如果需要按ID检索]` 实现get`[实体类名]`sByIds方法:
     - 调用`[实体类名小写]`Repository.findAllByIdIn(ids)检索实体
     - 返回`[实体类名]`对象列表
  2. 实现get`[实体类名]`sByCriteria方法:
     - 使用`[实体类名]`CriteriaBuilder基于查询参数创建pageable
     - 调用`[实体类名小写]`Repository.findAll(queryParams, pageable)检索分页实体
     - 返回Page<`[实体类名]`>对象

### 更新`[实体类名]`Repository接口添加检索方法
  1. `[如果需要按ID检索]` 添加方法: findAllByIdIn(List<String> ids): List<`[实体类名]`>
  2. 添加方法: findAll(`[实体类名]`QueryParams queryParams, Pageable pageable): Page<`[实体类名]`>

### 更新`[实体类名]`RepositoryImpl类实现检索逻辑
  1. `[如果需要按ID检索]` 实现findAllByIdIn方法:
     - 调用`[实体类名小写]`DAO.findAllById(ids)检索实体
     - 返回`[实体类名]`实体列表
  2. 实现带有queryParams和pageable的findAll方法:
     - 使用`[实体类名]`CriteriaBuilder基于查询参数创建specification
     - 调用`[实体类名小写]`DAO.findAll(specification, pageable)检索分页实体
     - 将`[实体类名]`PO实体映射为`[实体类名]`领域对象
     - 返回Page<`[实体类名]`>对象

### 更新`[实体类名]`DAO接口添加检索方法
  1. 继承JpaSpecificationExecutor<`[实体类名]`PO>

## 通用任务
1. 所有repository实现类都应使用@Repository注解
2. 所有Repository类都应实现JPA repository
3. 所有Service类都应使用@Service注解
4. 所有Controller类都应使用@RestController注解
5. 所有DTO和模型类都应使用@Data注解

## 约束条件
- 如果查询参数无效（例如，负数页码或无效的sortBy/sortDirection值），返回400 Bad Request
- 如果没有匹配条件的记录，返回空列表
- 如果未指定，默认页码为0
- 如果未指定，默认页面大小为10
- 如果未指定，默认按createdAt降序排序
- 最大页面大小为100，以防止性能问题
- 排序仅支持特定字段（如name、createdAt等）
- `[特定字段]`过滤支持部分匹配（contains）
- `[特定字段]`过滤支持精确匹配 