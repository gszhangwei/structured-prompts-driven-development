## 需求
实现一个`[实体名称]`API端点，允许用户查询`[实体名称]`。

## 业务模型
```
类图关系:

[实体类名] {
    +String id
    +[其他属性类型] [其他属性名]
    +timestamp createdAt
    +timestamp updatedAt
}

[查询请求类名] {
    +[查询条件类型] [查询条件名称]
    +Integer pageSize
    +Integer pageNumber
    +String sortBy
    +String sortDirection
}

[查询响应类名] {
    +List<[实体类名]> content
    +Integer pageSize
    +Integer pageNumber
    +Long totalElements
    +Integer totalPages
}

关系:
- [实体类名] "1" -- "*" [查询响应类名] : contains
- [查询请求类名] "1" -- "1" [查询响应类名] : produces
```

## 解决方案
1. API设计:
   - 创建GET端点 `/api/v1/[实体名称复数形式]` 用于查询`[实体名称]`列表
   - 创建GET端点 `/api/v1/[实体名称复数形式]/{id}` 用于查询单个`[实体名称]`
   - 支持分页、排序和过滤
   - 返回适当的HTTP状态码表示成功和错误情况
   - `[特殊处理逻辑，如有]`

## 结构

### 继承/实现关系
1. [实体类名]Service接口定义[实体类名]服务方法
2. [实体类名]ServiceImpl实现[实体类名]Service接口
3. [实体类名]Repository接口定义[实体类名]仓库方法
4. [实体类名]RepositoryImpl实现[实体类名]Repository接口

### 依赖关系
1. [实体类名]Controller调用[实体类名]Service
2. [实体类名]ServiceImpl调用[实体类名]Repository
3. [实体类名]RepositoryImpl调用[实体类名]DAO

## 任务

### 创建[实体类名]QueryParams类
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

### 创建[实体类名]Response类
  1. 属性:
     - id: String
     - `[其他属性名]`: `[其他属性类型]`
     - createdAt: LocalDateTime
     - updatedAt: LocalDateTime
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: of(List<[实体类名]> entities): List<[实体类名]Response>
     - 逻辑:
       - 将List<[实体类名]>映射为List<[实体类名]Response>
       - 返回[实体类名]Response列表

### 创建Paged[实体类名]Response类
  1. 属性:
     - content: List<[实体类名]Response>
     - totalPages: Integer
     - totalElements: Long
     - size: Integer
     - number: Integer
     - first: Boolean
     - last: Boolean
  2. 构造函数:
     - 使用@AllArgsConstructor注解
  3. 添加静态方法: of(Page<[实体类名]> page): Paged[实体类名]Response
     - 逻辑:
       - 将Page<[实体类名]>映射为Paged[实体类名]Response
         - 设置content为[实体类名]Response.of(page.getContent())
         - 设置totalPages为page.getTotalPages()
         - 设置totalElements为page.getTotalElements()
         - 设置size为page.getSize()
         - 设置number为page.getNumber()
         - 设置first为page.isFirst()
         - 设置last为page.isLast()
       - 返回Paged[实体类名]Response

### 更新[实体类名]Controller类实现检索API
  1. [如果需要按ID检索] 端点: `/api/v1/[实体名称复数形式]/ids`
     1. 方法: GET
     2. 请求参数:
        - ids: List<String> (必需)
     3. 响应体: 返回List<[实体类名]Response>类型的数据
     4. 逻辑:
        - 调用[实体类名小写]Service.get[实体类名]sByIds(ids)
        - 将[实体类名]实体映射为[实体类名]Response DTO
        - 返回200 OK状态码和[实体类名]Response列表
        - 如果ids参数为空或无效，返回400 Bad Request
  
  2. 端点: `/api/v1/[实体名称复数形式]`