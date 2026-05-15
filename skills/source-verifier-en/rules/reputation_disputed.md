
> **This file is maintained jointly by the user and the Agent, supporting custom extensions. Read before analyzing sources.**

# Disputed Sources List

Records websites, entities, or social media accounts whose credibility is disputed and require extra caution. The quality of these sources is unstable — they may have high-quality content or misleading information. Evaluation must be based on specific article content for independent judgment; do not outright reject or accept based solely on the list.

## Usage Rules

```text
- This list serves as the highest priority判定 basis; after a match, skip step 6 (detailed source type rule-by-rule checks)
- Before evaluating sources one by one, read this file along with reputation_trusted.md and reputation_unreliable.md
- If a source's domain/entity/URL matches this list → source_reliability_score directly set to 35-50
- citation_usability directly set to use_with_caution
- Note in warnings: "This source is on the disputed list; highest priority disputed判定"
- The disputed list sets a trust ceiling — content can be better than the ceiling but not worse
- Article quality score (article_quality_score) still needs independent evaluation per article
- List priority: trusted list > disputed list > unreliable list (if matching multiple, highest priority prevails)
```

## Format Description

```text
One entry per line, format: type | name | identifier | reason for dispute
Type: domain / url_pattern / social_account / entity
Name: Brief name of the source
Identifier: Domain, URL pattern, or social account identifier (platform:username)
Reason for dispute: Brief explanation of the point of contention
```

## List

```text
# Example entries (uncomment or add as needed):
# domain | Wikipedia | wikipedia.org | Open editing, unstable content quality, cannot be sole source
# entity | Example Disputed Media | - | Some reports alleged to contain factual bias; editorial review standards not transparent

# === User custom expansion area — add as needed ===
# Format: type | name | identifier | reason for dispute
# Example:
# domain | Example Disputed Tech Media | example-tech.com | Some reports contain exaggerations; editorial review process not rigorous enough
# social_account | Example Disputed KOL | weibo:9876543210 | Some statements alleged to be biased; previously caused controversy over unlabeled advertisements
```
