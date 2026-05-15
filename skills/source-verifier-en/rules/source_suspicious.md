
> **Must read SKILL.md before reading this file to understand the full task context.**

# Suspicious Source Processing Rules

When a source has serious risks, it should be marked as a suspicious source, and by default should not be used as final evidence.

## Suspicious Signals

```text
No author
No date
No institutional information
No contact information
Content appears copied
Heavy advertising or redirects
Title明显 exaggerated
Domain伪装成 official
Page filled with keyword stuffing
No outbound links
Broken citation chain
Content does not match title
Suspected AI-generated spam content
```

## Handling

Default:

```text
citation_usability: do_not_use
```

Exception:

This source can serve as a clue to find better original sources.

## Required Actions

When encountering a suspicious source:

1. Do not directly cite it as evidence.
2. Attempt to find the original source it copied or paraphrased.
3. Check if the content appears on more reliable websites.
4. If no more reliable source can be found, mark as evidence insufficient.

## Output Recommendations

```json
{
  "source_type": "suspicious",
  "citation_usability": "do_not_use",
  "warnings": [
    "No author and date",
    "Suspected scraper site",
    "Did not provide original sources"
  ],
  "recommended_action": "search_for_primary_source"
}
```
