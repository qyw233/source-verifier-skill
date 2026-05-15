# Contribution Guide

## Editing Rules

When changing source verification behavior, update both language packages in the same pull request:

```text
skills/source-verifier-en
skills/source-verifier-zh
```

Keep changes focused. Avoid rewriting large rule files when the change only affects one section.

## Semantic Parity Checklist

- The same rule file exists in both language packages.
- The same workflow step, source type, tag, or scoring threshold is represented in both languages.
- JSON field names and enum values remain compatible with `schemas/source_report.schema.json`.
- Examples still reflect the same evidence logic.
- New warnings or recommended actions are translated consistently.

## Release Checklist

- Update both package `VERSION` files if the package behavior changes.
- Update `CHANGELOG.md`.
- Create GitHub Release artifacts for both language packages.
- Mention whether the release changes behavior, documentation only, or both.

