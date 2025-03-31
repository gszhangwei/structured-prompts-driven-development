# Structured Prompts for Architecture Development

This repository contains structured templates for developing applications using different architectural patterns. Currently, it includes templates for Three-Tier Architecture, with plans to add Hexagonal Architecture in the future.

## Three-Tier Architecture Templates

The three-tier architecture section provides comprehensive templates for building applications following the traditional three-tier architectural pattern (Presentation, Business, and Data layers). Templates are available in both English and Chinese.

### Directory Structure

```
three_tier_architecture/
├── en/                     # English templates
│   ├── API-CREATE-TEMPLATE-EN.md
│   ├── API-DELETE-TEMPLATE-EN.md
│   ├── API-QUERY-TEMPLATE-EN.md
│   ├── API-UPDATE-TEMPLATE-EN.md
│   ├── CONFIG-TEMPLATE-EN.md
│   ├── DB-MIGRATION-TEMPLATE-EN.md
│   └── TEST-SCENARIOS-TEMPLATE-EN.md
│
└── zh/                     # Chinese templates
    ├── API-CREATE-TEMPLATE.md
    ├── API-DELETE-TEMPLATE.md
    ├── API-QUERY-TEMPLATE.md
    ├── API-UPDATE-TEMPLATE.md
    ├── CONFIG-TEMPLATE.md
    ├── DB-MIGRATION-TEMPLATE.md
    └── TEST-SCENARIOS-TEMPLATE.md
```

### Available Templates

1. **API Templates**
   - Create API (`API-CREATE-TEMPLATE`)
   - Query API (`API-QUERY-TEMPLATE`)
   - Update API (`API-UPDATE-TEMPLATE`)
   - Delete API (`API-DELETE-TEMPLATE`)

2. **Configuration Template** (`CONFIG-TEMPLATE`)
   - Guidelines for configuring application settings
   - Environment-specific configurations

3. **Database Migration Template** (`DB-MIGRATION-TEMPLATE`)
   - Database schema changes
   - Migration procedures

4. **Test Scenarios Template** (`TEST-SCENARIOS-TEMPLATE`)
   - Test case specifications
   - Testing strategies and methodologies

### Usage

1. Choose the appropriate language version (en/ or zh/) based on your needs
2. Copy the relevant template for your development task
3. Follow the structured format provided in the template
4. Fill in all required sections as specified in the template

### Coming Soon

- Hexagonal Architecture templates and guidelines
- Additional architectural patterns and best practices

## Contributing

Feel free to contribute by:
- Suggesting improvements to existing templates
- Proposing new templates
- Reporting issues or inconsistencies
- Adding templates for new architectural patterns

## License

This project is licensed under the MIT License - see the [LICENSE](three_tier_architecture/LICENSE) file for details. 