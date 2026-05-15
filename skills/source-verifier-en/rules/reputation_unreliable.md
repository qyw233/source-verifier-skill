
> **This file is maintained jointly by the user and the Agent, supporting custom extensions. Read before analyzing sources.**

# Untrustworthy Sources List

Records known unreliable websites, entities, or social media accounts. Sources matching this list should be significantly downgraded or directly discarded, unless there is strong corroboration from other independent sources.

## Usage Rules

```text
- This list serves as the highest priority判定 basis; after a match, skip step 6 (detailed source type rule-by-rule checks)
- Before evaluating sources one by one, read this file along with reputation_trusted.md and reputation_disputed.md
- If a source's domain/entity/URL matches this list → source_reliability_score directly set to 0-20
- citation_usability directly set to not_recommended or do_not_use (depending on severity)
- Note in warnings: "This source is on the unreliable list; highest priority unreliable判定"
- Even if a source matches this list, it should not be automatically ignored — still record and note the reason for the user to understand the full picture of information sources
- If a source URL is inaccessible and matches this list → citation_usability directly set to do_not_use
- List priority: trusted list > disputed list > unreliable list (if matching multiple, highest priority prevails)
```

## Format Description

```text
One entry per line, format: type | name | identifier | notes
Type: domain / url_pattern / social_account / entity
Name: Brief name of the source
Identifier: Domain, URL pattern, or social account identifier (platform:username)
Notes: Brief explanation of why it is unreliable
```

## List

```text
# Example entries (uncomment or add as needed):
# domain | Example Fake News Site | fake-news.example.com | Known for spreading false information
# social_account | Example Rumor Account | X:fake_user_123 | Repeatedly published unverified false news

# === User custom expansion area — add as needed ===
# Format: type | name | identifier | notes
# Example:
# domain | Example Content Farm | example-farm.com | Content laundering, SEO spam, no original content
# social_account | Example Marketing Account | weibo:1234567890 | Long-term publishing of fake marketing information
# entity | Example Known Pseudo-Science Organization | - | Spreads pseudo-science, warned by multiple authoritative institutions
```
