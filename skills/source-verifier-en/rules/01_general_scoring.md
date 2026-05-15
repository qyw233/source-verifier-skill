
> **Must read SKILL.md before reading this file to understand the full task context.**

# General Scoring Rules

Each source needs four types of results:

1. `source_reliability_score`: Overall source reliability
2. `article_quality_score`: Current article or page quality
3. `citation_usability`: Whether suitable as final citation

## I. Source Reliability Score source_reliability_score

Start from 50.

### Bonus Points

```text
Official source: +35
Government, legal, regulatory agency source: +35
Official documentation, release notes, project repository: +30
Peer-reviewed academic paper: +30
Preprint or university institution page: +20
High-reputation news organization: +20
Professional or research institution: +15
Author and institution clearly identified: +8
Has correction mechanism or editorial standards: +5
Page links to original source: +8
```

### Deductions

```text
Ordinary social platform content: -20
Anonymous blog: -15
No author: -8
No date: -8
Does not link to original source: -10
Scraper site, mirror site, SEO content farm: -35
Title明显 exaggerated or misleading: -20
Matches known low-credibility source list: -40
Only cites other secondary sources: -10
Suspected advertisement or sponsorship but not labeled: -20
```

Score capped between 0 and 100.

## II. Article Quality Score article_quality_score

Evaluate the specific page, not just the domain.

### Positive Signals

```text
Has clear author
Has publication or update date
Has original source links
Has data, code, papers, announcements, or original regulations
Has direct citations or traceable evidence
Clearly distinguishes news, commentary, advertising, sponsored content
Title matches body content
```

### Negative Signals

```text
No author
No date
No original source links
Clickbait title
Heavy use of "reportedly," "internet says," "foreign media says," "sources say"
Title and body内容不一致
Suspected copying from other sites
Excessive SEO optimization
Too much advertising or marketing content
```

## III. Citation Usability citation_usability

Citation usability is not equivalent to source reliability. It must be assessed in combination with "article content quality" and "relevance to the user's question."

### highly_usable

Meets:

```text
Source is primary source or high-quality authoritative source
Fully and directly answers the user's question
Article quality is extremely high, with sufficient evidence
No obvious timeliness or context issues
Traceable, accessible, verifiable
```

### usable

Meets:

```text
Source is generally reliable
Can partially or indirectly answer the user's question
Article quality is good
Content is logically consistent, has reference value
May be a secondary source, but links or cites the original source
```

### use_with_caution

Meets any:

```text
Content is incomplete or has bias
Barely relevant to the user's question, but not directly
Source is a secondary report
Has timeliness risk
Lacks author or original links
Suitable as supplementary material, not as sole evidence
```

### not_recommended

Meets any:

```text
Source quality is low
Key factual descriptions are vague
Though source is reliable, content is irrelevant or unhelpful to the user's question
Lacks key context
Only rumors or retellings
Better sources already available
```

### do_not_use

Meets any:

```text
Scraper site, spam site, fake official site
Content is seriously misleading
Source inaccessible or content incomplete
Contradicts high-credibility sources
Used for high-risk topics but evidence insufficient
```

## IV. Output Requirements

Do not output only scores; reasons must be provided.

Recommended format:

```json
{
  "source_reliability_score": 82,
  "article_quality_score": 76,
  "citation_usability": "usable",
  "reasons": [
    "This source is official documentation",
    "Page includes publication date and clear functional description",
    "Content is detailed and logically consistent"
  ],
  "warnings": [
    "No independent third-party verification of performance claims"
  ]
}
```
