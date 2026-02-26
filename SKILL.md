---
name: knowledgebase-pipeline
description: Use when asked to build or refresh a project knowledge base from source code and documentation. Covers first-time setup, incremental updates, metadata normalization, and glossary management for any software project.
---

# Knowledgebase Pipeline

Execute a deterministic workflow to build or refresh wiki-style knowledge base artifacts for any software project.

## Enforce Data Ownership

Treat files as follows:
- `metadata.json`: single source of truth for structured knowledge
- `field_glossary.json`: single source of truth for field naming terminology
- `metadata.md`: generated readable view only
- `READING_TODO.md`: execution log and reading coverage tracker

Do not hand-edit `metadata.md` when `metadata.json` or glossary changes; always regenerate.

## Require Project Config

Use project-level config file (default name: `kb.config.project.json`) with these keys:

```json
{
  "project_root": "<absolute-or-relative-path>",
  "output_dir": "wiki",
  "schema_version": "1.0.0",
  "exclude_paths": ["node_modules", "dist", "skills"],
  "feature_taxonomy": "journey",
  "priority_rules": {
    "P0": ["app entry", "routing", "core runtime"],
    "P1": ["core hooks", "domain services"],
    "P2": ["support utilities", "test helpers"],
    "P3": ["docs", "configs", "assets"],
    "P4": ["build artifacts", "binary outputs"]
  }
}
```

If config is missing, create one from `assets/templates/kb.config.template.json` and fill values before processing.

## Run Pipeline

1. Inventory files under `project_root`, applying `exclude_paths`.
2. Build priority reading list and write `output_dir/READING_TODO.md`.
3. Decompose product functions by configured taxonomy and write `output_dir/功能拆解.md`.
4. Initialize or load `output_dir/metadata.json` using schema version.
5. Read files in priority order; after each file (or small batch), update affected feature entries in `metadata.json`.
6. Maintain field naming map in `output_dir/field_glossary.json`.
7. Generate `output_dir/metadata.md` from `metadata.json + field_glossary.json`.
8. Run validation checks and report unresolved items.

## Apply Metadata Rules

For each feature record, keep:
- `code`, `title`, `journey`
- `feature`: `summary`, `entry`, `details[]`
- `field[]`
- `rule[]`
- `requirement[]`
- `experience_note[]`
- `artifacts[]` (optional)
- `field_kind_map{}` (optional)

Classify correctly:
- `Field`: runtime state, mutable data, decision-driving values
- `Artifacts`: files/config/build outputs/resources; not runtime business state

When unsure, default to `Artifacts` and add a note for review.

## Keep Incremental Discipline

During long reads:
- Mark each completed file in `READING_TODO.md` immediately.
- Update impacted metadata entry immediately (do not defer to end).
- If newly read evidence contradicts previous entry, update existing feature instead of duplicating.

## Validate Before Finish

Use checks from `references/checklist.md`.

At minimum validate:
- no duplicate feature code
- all fields have glossary mapping
- `metadata.md` contains no unresolved placeholder labels
- every listed artifact path exists (or is clearly marked historical)

## Output Contract

Deliver:
- updated files list
- unresolved ambiguities/questions
- optional next actions for another iteration
