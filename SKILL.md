---
name: knowledgebase-pipeline
description: Builds and maintains a reusable project knowledge-base pipeline that outputs structured wiki artifacts from source code and documents. Activates when the user asks to create, update, normalize, or operationalize project knowledge base assets (reading todo, feature breakdown, metadata schema records, glossary, and readable markdown views), including cross-project reuse with configurable inputs.
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

Copy this checklist and check off steps as you complete them:

```
Pipeline Progress:
- [ ] Step 1: Inventory files under project_root, apply exclude_paths
- [ ] Step 2: Build priority reading list → write output_dir/READING_TODO.md
- [ ] Step 3: Decompose product functions → write output_dir/功能拆解.md
- [ ] Step 4: Initialize or load output_dir/metadata.json
- [ ] Step 5: Read files in priority order; update metadata.json after each file/batch
- [ ] Step 6: Maintain field naming map in output_dir/field_glossary.json
- [ ] Step 7: Generate output_dir/metadata.md from metadata.json + field_glossary.json
- [ ] Step 8: Run validation checks and report unresolved items
```

## Apply Metadata Rules

See [references/schema.md](references/schema.md) for the complete feature record structure and JSON examples.

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
