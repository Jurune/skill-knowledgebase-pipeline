# knowledgebase-pipeline

一个可复用的知识库工程 Skill：把任意项目源码/文档整理为 `wiki` 知识库产物（结构化 + 可读版）。

## 1 分钟上手

1. 准备项目配置文件：`kb.config.project.json`
2. 触发 Skill 执行：

```text
请使用 knowledgebase-pipeline，基于 <项目路径>/kb.config.project.json 执行一轮完整知识库刷新。
```

3. 获取产物（默认在 `wiki/`）：
- `READING_TODO.md`：阅读清单与覆盖记录
- `功能拆解.md`：功能拆解（用户旅程/模块）
- `metadata.json`：结构化主数据（唯一事实源）
- `field_glossary.json`：字段术语标准（唯一命名源）
- `metadata.md`：人工阅读视图（由前两者生成）

## 设计原则

- `metadata.json` 只增量更新，不做重复条目
- `field_glossary.json` 保证字段中文名统一
- `metadata.md` 只生成，不手改
- `Field` 与 `Artifacts` 严格区分

## 配置示例

见：`assets/templates/kb.config.template.json`

核心字段：
- `project_root`
- `output_dir`
- `schema_version`
- `exclude_paths`
- `feature_taxonomy`
- `priority_rules`

## 适用场景

- 新项目快速搭建知识库
- 老项目做结构化沉淀
- 多项目统一知识管理规范

## 校验

校验规则见：`references/checklist.md`
元数据规范见：`references/schema.md`

## 版本管理

版本号遵循 `MAJOR.MINOR.PATCH` 语义化版本规范：

- **MAJOR**：工作流结构或产物格式的破坏性变更（如 schema 字段重命名、产物文件结构调整）
- **MINOR**：新增功能或规则，向后兼容（如新增 priority 规则、新增产物类型）
- **PATCH**：措辞修正、说明补充、示例更新等非功能性调整

变更历史见 [CHANGELOG.md](CHANGELOG.md)。

> 在 Anthropic Skills API 中部署时，建议生产环境固定版本号（epoch timestamp），开发环境使用 `”latest”`。

## 说明

本仓库提供的是”方法与模板”，不包含任何具体业务项目的私有知识数据。
