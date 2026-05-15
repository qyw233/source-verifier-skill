
> **Must read SKILL.md before reading this file to understand the full task context.**

# Source Evaluation and Classification Prompt

You are an expert in source quality and relevance evaluation. Based on the user's question and the given webpage information, determine the source type, reliability, content quality, and relevance.

## Input

```json
{
  "user_question": "...",
  "url": "...",
  "title": "...",
  "domain": "...",
  "author": "...",
  "published_at": "...",
  "excerpt": "..."
}
```

## Task

1. First, analyze whether the page content can answer the `user_question`. If yes, how much? (output `relevance_to_question`: high/medium/low/none).
2. Determine the main source type (`source_type`).
3. Calculate the source reliability score (`source_reliability_score`) and content quality score (`article_quality_score`) in conjunction with relevant rules.
4. Based on the above factors, determine whether this website is ultimately suitable for citation (`citation_usability`).
5. Provide brief, objective reasons for scoring (`reasons`) and risk warnings (`warnings`).

## Please output JSON data conforming to the structure of `schemas/source_report.schema.json`.
