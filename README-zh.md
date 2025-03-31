# 架构开发结构化模板

本仓库包含用于开发不同架构模式应用程序的结构化模板。目前包含三层架构的模板，未来计划添加六边形架构的模板。

## 三层架构模板

三层架构部分提供了全面的模板，用于构建遵循传统三层架构模式（表示层、业务层和数据层）的应用程序。模板提供中英文两个版本。

### 目录结构

```
three_tier_architecture/
├── en/                     # 英文模板
│   ├── API-CREATE-TEMPLATE-EN.md
│   ├── API-DELETE-TEMPLATE-EN.md
│   ├── API-QUERY-TEMPLATE-EN.md
│   ├── API-UPDATE-TEMPLATE-EN.md
│   ├── DB-MIGRATION-TEMPLATE-EN.md
│   └── TEST-SCENARIOS-TEMPLATE-EN.md
│
└── zh/                     # 中文模板
    ├── API-CREATE-TEMPLATE.md
    ├── API-DELETE-TEMPLATE.md
    ├── API-QUERY-TEMPLATE.md
    ├── API-UPDATE-TEMPLATE.md
    ├── DB-MIGRATION-TEMPLATE.md
    └── TEST-SCENARIOS-TEMPLATE.md
```

### 可用模板

1. **API 模板**
   - 创建 API (`API-CREATE-TEMPLATE`)
   - 查询 API (`API-QUERY-TEMPLATE`)
   - 更新 API (`API-UPDATE-TEMPLATE`)
   - 删除 API (`API-DELETE-TEMPLATE`)

2. **数据库迁移模板** (`DB-MIGRATION-TEMPLATE`)
   - 数据库架构变更
   - 迁移流程

3. **测试场景模板** (`TEST-SCENARIOS-TEMPLATE`)
   - 测试用例规范
   - 测试策略和方法

### 使用方法

1. 根据需要选择适当的语言版本（en/ 或 zh/）
2. 复制相关的开发任务模板
3. 遵循模板中提供的结构化格式
4. 按照模板要求填写所有必需部分

### 即将推出

- 六边形架构模板和指南
- 其他架构模式和最佳实践

## 贡献

欢迎通过以下方式贡献：
- 对现有模板提出改进建议
- 提议新的模板
- 报告问题或不一致
- 添加新的架构模式模板

## 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详细信息。 