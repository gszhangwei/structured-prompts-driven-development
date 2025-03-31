## 需求
基于给定的业务模型创建迁移文件。

## 业务模型
```mermaid
classDiagram
direction TB

    class [实体类名] {
        +[属性类型] [属性名]
        +[属性类型] [属性名]
        ...
    }

    [关系描述]
```

## 任务
- 为`[实体类名]`实体创建迁移文件。
  - 文件名: V[年月日时分秒]__[描述].sql
  - 表名: [表名]
- ...

## 约束条件
- 迁移文件应放置在`src/main/resources/db/migrations`目录中。
- 迁移文件应按照`V[年月日时分秒]__[描述].sql`格式命名。
- 如果存在继承关系，所有继承的字段都应写在子实体中。

## 数据库迁移模板

### 创建表
```sql
CREATE TABLE `[表名]` (
    id VARCHAR(36) PRIMARY KEY,
    `[字段名]` `[字段类型]` `[字段约束]`,
    `[字段名]` `[字段类型]` `[字段约束]`,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    CONSTRAINT `[约束名称]` `[约束定义]`
);
```

### 修改表
```sql
-- 添加字段
ALTER TABLE `[表名]`
ADD COLUMN `[字段名]` `[字段类型]` `[字段约束]`;

-- 修改字段
ALTER TABLE `[表名]`
MODIFY COLUMN `[字段名]` `[新字段类型]` `[新字段约束]`;

-- 删除字段
ALTER TABLE `[表名]`
DROP COLUMN `[字段名]`;

-- 添加索引
CREATE INDEX `[索引名称]` ON `[表名]` (`[字段名]`);

-- 添加唯一约束
ALTER TABLE `[表名]`
ADD CONSTRAINT `[约束名称]` UNIQUE (`[字段名]`);

-- 添加外键约束
ALTER TABLE `[表名]`
ADD CONSTRAINT `[约束名称]` 
FOREIGN KEY (`[字段名]`) 
REFERENCES `[关联表名]`(`[关联字段名]`);
```

### 数据迁移
```sql
-- 插入数据
INSERT INTO `[表名]` (`[字段名]`, `[字段名]`)
VALUES (`[字段值]`, `[字段值]`);

-- 更新数据
UPDATE `[表名]`
SET `[字段名]` = `[新值]`
WHERE `[条件]`;

-- 删除数据
DELETE FROM `[表名]`
WHERE `[条件]`;
```

### 回滚脚本
```sql
-- 删除表
DROP TABLE IF EXISTS `[表名]`;

-- 删除索引
DROP INDEX `[索引名称]` ON `[表名]`;

-- 删除约束
ALTER TABLE `[表名]`
DROP CONSTRAINT `[约束名称]`;

-- 恢复数据
INSERT INTO `[表名]` (`[字段名]`, `[字段名]`)
SELECT `[字段名]`, `[字段名]`
FROM `[备份表名]`;
```

### 最佳实践
1. 每个迁移脚本都应该有对应的回滚脚本
2. 迁移脚本应该是幂等的
3. 在执行迁移前备份重要数据
4. 使用有意义的命名约定
5. `[其他最佳实践]` 