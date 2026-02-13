# knowledgebase-pipeline

A reusable knowledge-base engineering skill that turns source code and docs into structured `wiki` artifacts.

## 1-Minute Quickstart

1. Prepare a project config file: `kb.config.project.json`.
2. Trigger the skill:

```text
Please use knowledgebase-pipeline and run a full knowledge-base refresh based on <project-path>/kb.config.project.json.
```

3. Expected outputs (default under `wiki/`):
- `READING_TODO.md`: reading checklist and coverage log
- `功能拆解.md`: feature decomposition (journey/module based)
- `metadata.json`: structured source of truth
- `field_glossary.json`: naming standard for fields
- `metadata.md`: human-readable view generated from metadata + glossary

## Core Principles

- Update `metadata.json` incrementally, avoid duplicate feature records.
- Keep naming consistent via `field_glossary.json`.
- Treat `metadata.md` as generated output (do not hand-edit).
- Strictly separate `Field` vs `Artifacts`.

## Config Template

See: `assets/templates/kb.config.template.json`

Key config fields:
- `project_root`
- `output_dir`
- `schema_version`
- `exclude_paths`
- `feature_taxonomy`
- `priority_rules`

## Use Cases

- Bootstrap a knowledge base for a new project
- Structure and normalize an existing project
- Standardize KB workflows across multiple repositories

## Validation

- Validation checklist: `references/checklist.md`
- Metadata schema: `references/schema.md`

## Note

This repository provides process and templates only. It does not include private business project knowledge data.
