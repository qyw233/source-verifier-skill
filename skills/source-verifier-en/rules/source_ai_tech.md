
> **Must read SKILL.md before reading this file to understand the full task context.**

# AI and Technology Information Special Rules

AI, software, open source, model capabilities, API features, and other information change rapidly. Must prioritize original technical sources.

## Best Sources

```text
Official blog
Official documentation
API reference
Model card
Technical report
arXiv / Paper
GitHub repository
Hugging Face model page
Release notes
Changelog
Package registry
LICENSE file
Commit / PR / Issue
```

## Evidence Requirements by Technical Aspect

### Open Source Status

To confirm "open source," find the following evidence in official channels:

```text
Public code repository
Public model weights
LICENSE file
Official release page linking to code or weights
Official entry on package manager or model platform
```

Cannot be confirmed based on the following alone:

```text
Media says "open source"
Netizens say "open source"
Only demo, no code
Only API published, no code or weights
```

### Model Capability Evaluation

Refer to:

```text
Official documentation
Model card
Technical report
Paper
Reproducible experiments
Independent evaluation
```

Distinguish between:

```text
Officially claimed capabilities
Actually available capabilities
Demo capabilities
Stable API features
Beta features
```

### API Feature Evaluation

Prioritize reference:

```text
Official API documentation
SDK changelog
Release notes
Sample code
Developer announcements
```

Must check:

```text
Version number
Regional restrictions
Account permissions
Whether beta
Whether deprecated
```

### Model Release Date

Prioritize reference:

```text
Official announcement
Release notes
Model platform publication date
Paper submission date
GitHub release time
```

### Performance Evaluation (Benchmark)

For benchmark data queries, first determine the page's position in the classification system:

- The benchmark project's own official website (e.g., LiveBench, HELM, Open LLM Leaderboard, etc.) — for that benchmark's scores, it is "official" + "primary_source" — it is the original publisher of the benchmark data
- The benchmark paper (e.g., LiveBench paper on arXiv) — belongs to "academic"
- Aggregator sites republishing benchmark data (e.g.,某些 SEO sites copying rankings from official leaderboards) — belong to "aggregator_or_scraper"; should trace back to official leaderboard
- Media/blogs paraphrasing benchmark results — belong to secondary reports; cannot substitute for original source

Must check:

```text
Test set name
Evaluation methodology
Whether official self-evaluation
Whether independently reproduced
Whether overfitting or cherry-picking可能 exists
Whether compared with models of the same level and date
Whether the page is the benchmark project's own official entry point (rather than an aggregation republishing)
```

## Red Flag Signals

```text
Benchmark chart without methodology
Leaked screenshots
Social platform rumors
Model aggregator site copied lists
Unclear license status
"Strongest," "No. 1," "遥遥领先" without methodology
```

## Output Recommendations

```json
{
  "topic_rule": "ai_tech",
  "required_primary_evidence": ["official_docs", "release_notes", "github_repo", "model_card"],
  "warnings": ["Media reports alone cannot prove open source status"]
}
```
