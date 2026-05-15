# Language Package Comparison

The English and Chinese packages are intended to be semantically aligned.

## Current Package Paths

```text
skills/source-verifier-en
skills/source-verifier-zh
```

## Alignment Rules

- Keep the same file and directory structure in both packages.
- Keep rule intent, scoring thresholds, output labels, and workflow steps semantically equivalent.
- Keep schema field names in English for programmatic readability.
- Localize human-facing descriptions, examples, warnings, and explanations.
- When adding a rule file to one language, add the matching file to the other language in the same change.

## Expected Differences

- `README.md`, rule prose, prompt text, examples, and schema descriptions may be localized.
- `VERSION` may include a language suffix, such as `0.1-en` or `0.1-zh`.
- Output field names and enum values should remain stable across languages.

