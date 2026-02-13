# Validation Checklist

## Structural

- `metadata.json` is valid JSON
- `schema_version` exists
- every feature has unique `code`
- every feature has `feature.summary` and `feature.entry`

## Classification

- runtime states are under `field`
- files/configs/build outputs are under `artifacts`
- selector-like fields are marked in `field_kind_map` when applicable

## Terminology

- every `field` has Chinese term mapping in `field_glossary.json`
- same key maps to one standard term only
- deprecated aliases are documented (if used)

## Rendered View

- `metadata.md` regenerated from sources
- no placeholders like `待补充` / `待定义术语`
- feature order is deterministic (by `F{journey}-{index}`)

## Coverage

- `READING_TODO.md` checked for completed files
- unresolved files/issues explicitly listed
