## 需求
实现一个`[实体名称]`API端点，允许用户删除现有的`[实体名称]`。

## 业务模型
```
类图关系:

[实体类名] {
    +String id
    +[其他属性类型] [其他属性名]
    +timestamp createdAt
    +timestamp updatedAt
}
```

## 解决方案
1. API设计:
   - 创建DELETE端点 `/api/v1/`[实体名称复数形式]`/{id}` 用于删除现有的`[实体名称]`
   - `[支持软删除/硬删除，根据需求]`
   - 返回适当的HTTP状态码表示成功和错误情况
   - `[特殊处理逻辑，如有]`

## 结构

### 继承关系
1. `[实体类名]`Service接口定义`[实体类名]`服务方法
2. `[实体类名]`ServiceImpl实现`[实体类名]`Service接口
3. `[实体类名]`Repository接口定义`[实体类名]`仓库方法
4. `[实体类名]`RepositoryImpl实现`[实体类名]`Repository接口

### 依赖关系
1. `[实体类名]`Controller调用`[实体类名]`Service
2. `[实体类名]`ServiceImpl调用`[实体类名]`Repository
3. `[实体类名]`RepositoryImpl调用`[实体类名]`DAO

## 任务

### 更新`[实体类名]`Controller类实现删除API
  1. 端点: `/api/v1/`[实体名称复数形式]`/{id}`
     1. 方法: DELETE
     2. 路径变量:
        - id: String (必需)
     3. 响应体: 无内容
     4. 逻辑:
        - 调用`[实体类名]Service.delete[实体类名](id)`
        - 返回204 No Content状态码
        - 如果id不存在，返回404 Not Found
        - `[其他错误处理逻辑]`

### 更新`[实体类名]`Service接口添加删除方法
  1. 添加方法: delete`[实体类名]`(String id): void

### 更新`[实体类名]`ServiceImpl类实现删除逻辑
  1. 实现delete`[实体类名]`方法:
     - 逻辑:
       - 调用`[实体类名]Repository.findById(id)`检索现有实体
       - 如果实体不存在，抛出EntityNotFoundException
       - `[如果是软删除]` 更新实体状态为已删除
       - `[如果是软删除]` 更新updatedAt时间戳
       - `[如果是软删除]` 调用`[实体类名]Repository.save(entity)`保存更新后的实体
       - `[如果是硬删除]` 调用`[实体类名]Repository.delete(id)`删除实体

### 更新`[实体类名]`Repository接口添加删除方法
  1. `[如果是硬删除]` 添加方法: delete(String id): void

### 更新`[实体类名]`RepositoryImpl类实现删除逻辑
  1. `[如果是硬删除]` 实现delete方法:
     - 逻辑:
       - 调用`[实体类名]DAO.deleteById(id)`删除实体

## 通用任务
1. 所有repository实现类都应使用@Repository注解
2. 所有Repository类都应实现JPA repository
3. 所有Service类都应使用@Service注解
4. 所有Controller类都应使用@RestController注解
5. 所有DTO和模型类都应使用@Data注解

## 约束条件
- 如果id不存在，返回404 Not Found
- 删除成功后返回204 No Content状态码
- `[如果是软删除]` 必须更新updatedAt时间戳
- `[如果有关联关系]` 必须处理关联实体
- `[其他特定约束条件]` 