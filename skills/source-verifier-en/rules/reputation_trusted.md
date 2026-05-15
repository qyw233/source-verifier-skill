
> **This file is maintained jointly by the user and the Agent, supporting custom extensions. Read before analyzing sources.**

# Trusted Sources List

Records known reliable websites, entities, or social media accounts. Sources matching this list default to a higher trust baseline, but still need to be assessed in combination with specific article quality and the user's question.

## Usage Rules

```text
- This list serves as the highest priority判定 basis; after a match, skip step 6 (detailed source type rule-by-rule checks)
- Before evaluating sources one by one, read this file along with reputation_unreliable.md and reputation_disputed.md
- If a source's domain/entity/URL matches this list → source_reliability_score directly set to 85-95
- citation_usability defaults to usable or highly_usable
- Note in reasons: "This source is on the trusted list; highest priority判定"
- Still need to check article quality (article_quality_score independently assessed) and timeliness (freshness)
- List priority: trusted list > disputed list > unreliable list (if matching multiple, highest priority prevails)
- If a source URL is inaccessible but matches this list → can give a higher preliminary assessment
```

## Format Description

```text
One entry per line, format: type | name | identifier | notes
Type: domain / url_pattern / social_account / entity
Name: Brief name of the source
Identifier: Domain, URL pattern, or social account identifier (platform:username)
Notes: Brief explanation of why it is trusted
```

## List
```text
domain | Reuters | reuters.com | International authoritative news agency
domain | Associated Press | apnews.com, ap.org | International authoritative news agency
domain | BBC News | bbc.com, bbc.co.uk | UK public broadcasting service
domain | World Health Organization | who.int | UN specialized health agency
domain | IEEE | ieee.org | Institute of Electrical and Electronics Engineers
domain | ACM | acm.org | Association for Computing Machinery
domain | Nature | nature.com | Top scientific journal
domain | Science | science.org | Top scientific journal
domain | GitHub | github.com | Code hosting platform (distinguish official repositories from personal repositories)
domain | Wikipedia | wikipedia.org | Encyclopedia (background reference only, not suitable as final evidence)
domain | PubMed | pubmed.ncbi.nlm.nih.gov | Biomedical literature database
domain | FDA | fda.gov | U.S. Food and Drug Administration

# === Below is the user custom expansion area; add or modify as needed ===
# Format: domain | name | identifier | notes
# Example: domain | Caixin | caixin.com | China's well-known financial media
```

Note: The Chinese government and official media entries from the original version have been removed for neutrality.
