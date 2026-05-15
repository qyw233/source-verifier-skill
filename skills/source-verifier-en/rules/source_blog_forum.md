
> **Must read SKILL.md before reading this file to understand the full task context.**

# Blog, Forum, and Community Source Processing Rules

The quality of blogs and forums varies greatly. First distinguish the form of the source, then assess综合 based on author identity, content type, and verifiability.

## I. First Distinguish Blog from Forum

Before evaluation, must first determine whether the source is a blog or a forum. The evidentiary nature and evaluation dimensions differ:

### Blog Characteristics

```text
Centered on the author (individual or team); articles published around specific topics
Content typically long-form; author has full control over content
Page usually has clear author introduction and publication date
Reader interaction exists in the form of comments, not affecting the main text
Common platforms: Independent blogs, Medium, Stack Overflow Blog, personal websites
```

### Forum Characteristics

```text
Based on topics or posts as basic units; multi-party participation in discussion
Content consists of OP post + replies; information distributed across multiple responses
Author identity may be diverse (OP, replier, passing netizen)
Answer or conclusion may not be in the first post; may require reviewing replies
Common platforms: Stack Overflow, GitHub Issue, Reddit, community forums
```

### Post-Determination Routing

```text
Determined as blog → jump to "Section III: Blog"
Determined as forum → jump to "Section II: Forum"
```

## II. Forum

The core characteristic of forums is multi-person participation in discussion, so the evaluation focus is not a single author, but the **credibility of the discussion content and conclusions**.

### 2.1 First Determine Forum Discussion Type

Upon receiving a forum source, first determine which type of discussion it belongs to:

```text
Technical/Problem-Solving: Question-answer mode; has clear question and expected answer
                  Examples: Stack Overflow Q&A, GitHub Issue, technical support forums

Opinion Discussion: Everyone expresses their views; no standard answer; discussing subjective feelings or value judgments
                  Examples: Reddit热门 posts, "What do you think" type questions

Product/Item Discussion: Discussion围绕 a specific product, service, or brand
                  Examples: Product review posts, hardware discussions
```

### 2.2 Technical/Problem-Solving Forums

Credibility in such forums depends on **whether the problem was resolved** and **whether the solution is reproducible**.

#### Check Steps

```text
1. Does the question have a clear answer or resolution mark (e.g., Stack Overflow Accepted Answer, GitHub Issue Closed status)
2. Does the solution include reproducible steps (code, commands, configuration)
3. Is the responder's identity verifiable (maintainer, project member, high-reputation user)
4. Is the solution applicable to the current version (check timestamp)
5. Have multiple independent responders provided similar solutions
```

#### Credibility Classification

```text
Official Accepted/Closed mark + contains code + multiple people verified → relatively high credibility; citation_usability can reach usable
Has solution but not marked + only single response → medium credibility; citation_usability: use_with_caution
Question posted but no valid answer → only as线索; citation_usability: not_recommended
Only speculative answers, no code, no verification → low credibility; citation_usability: not_recommended
```

### 2.3 Opinion Discussion Forums

In scenarios where everyone expresses their views (Reddit, forums, "What do you think" type), forum content itself cannot serve as factual evidence; it can only reflect **the distribution of certain groups' opinions**.

```text
Referenceable: Public reactions, user sentiment, diversity of experience sharing
Cannot be used as: Fact confirmation, data source, official position, scientific conclusion
Default citation_usability: use_with_caution or not_recommended
```

If the discussion cites original sources (official announcements, papers, regulations), the original source takes precedence; forum content is only supplementary.

### 2.4 Product/Item Discussion — Suspected Advertising Detection

When forum discussion围绕 a **specific product, brand, service, course, APP**, must detect hidden advertising or advertorials.

#### Suspected Advertising Signals

```text
Poster or high-vote responder's account is newly registered or has only posted similar content
Content lavishly praises, almost no mention of flaws or risks
Contains promotional links, discount codes, invitation codes, "DM me" etc. traffic-driving behavior
Multiple floor posts highly similar; reply times concentrated
Content uses明显的 marketing language ("personally tested and effective," "must buy," "amazing," "GOAT")
Poster跨-platform publishes similar content
Account avatar or signature contains commercial information
```

#### Handling

```text
Confirmed or highly suspected advertising → add secondary tag suspected_advertisement
                    → citation_usability: not_recommended or do_not_use
                    → warnings note: "Suspected commercial promotion content"
                    → Recommend finding neutral reviews or official information

Cannot determine but个别 signals present → add secondary tag possible_advertisement
                                → citation_usability: use_with_caution
```

## III. Blog

Blogs are centered on the author; the evaluation focus is on **author identity and content quality**.

### 3.1 Technical Blogs

Technical blogs refer to personal or team blogs围绕 software development, AI, engineering, operations, etc.

#### High-Quality Technical Blog Signals

```text
Author identity clear; technical background verifiable (e.g., GitHub profile, LinkedIn, personal projects)
Article contains runnable code, logs, configurations, or reproduction steps
Links to official documentation, papers, GitHub issues, or source code
Marks writing date and update history
Conclusions have boundaries; clearly states applicable scope and limitations
Has valuable reader discussion or author follow-up responses
Historical article quality consistent; no frequent credibility issues
```

#### Low-Quality Technical Blog Signals

```text
Author anonymous or untraceable
Only gives conclusions without methods; no code, no steps
Excessive SEO optimization, keyword stuffing
Content clearly copied or translated from others, or AI-generated
Exaggerated titles ("one article to master all," "the most comprehensive on the web"), shallow content
Advertising or course promotion占 large proportion
Generalizing individual cases in specific environments as universal conclusions
```

#### Credibility Reference

```text
Well-known project maintainer/core contributor's technical blog → relatively high credibility
Real name + verifiable background + cites original sources → above average credibility
Anonymous + no citations + no code → only as线索
```

### 3.2 Non-Technical Blogs

The credibility of non-technical blogs highly depends on the **relationship between author identity and user question**.

#### Core Judgment: Who Is the Author?

If the user's question involves "whether someone said something" or "what someone's view is":

```text
Blog author is the person the user is asking about:
  → This blog has the highest evidentiary authority for that person's views (primary source)
  → source_type can upgrade to official with tag primary_source
  → citation_usability: highly_usable

Blog author is a third party quoting or commenting on that person's words:
  → Only represents the blog author's understanding; cannot be equated to the quoted person's original meaning
  → Should尽可能 find the quoted person's original statement
  → If original source cannot be found, mark "citation chain incomplete"
  → citation_usability: use_with_caution or not_recommended
```

#### Personal Opinion Blog

```text
Blog only expresses author's personal views, commentary, reflections → does not represent facts
If author is a domain expert (verifiable qualifications), views have some reference value
If author identity unclear, those views cannot serve as argument basis
Must mark "This content is personal opinion,未经 independent verification"
```

### 3.3 Blog Quality General Check

Whether technical or non-technical, check:

```text
Has clear author?         → No author: deduct points
Has publication date?     → No date: deduct points
Has original source links? → No citations: deduct points
Has unlabeled commercial promotion? → If unlabeled, add suspected_advertisement
Content matches title?    → Mismatch: deduct points
Distinguishes facts from opinions? → If not, lower article_quality_score
```

## IV. Suitable and Unsuitable Usage Scenarios

### Suitable as Reference

```text
Software troubleshooting, environment configuration, development experience
Technical tutorials, implementation examples
Genuine user experience feedback (must mark as personal experience)
Personal observations on tech trends (must mark as personal opinion)
Public expression by the person themselves (blog is the author themselves)
```

### Not Suitable as Final Evidence

```text
Legal/policy basis
Medical diagnosis or treatment recommendations
Financial investment advice
Sole source for scientific consensus
Sole confirmation of company official publication status
Open source license judgment
Sole reporting of major news events
```

## V. Output Recommendations

```json
{
  "source_type": "blog_forum",
  "content_form": "blog | forum",
  "author_expertise": "clear | unclear | unknown",
  "forum_subtype": "tech_qa | general_discussion | product_discussion",
  "problem_resolved": true,
  "solution_has_code_or_steps": true,
  "advertisement_suspected": false,
  "evidence_type": ["code", "logs", "screenshots", "personal_experience", "opinion_only"],
  "citation_usability": "usable | use_with_caution | not_recommended | do_not_use",
  "reasons": ["..."],
  "warnings": [
    "This source is a forum discussion; lacks authoritative review",
    "Question does not yet have a clear solution",
    "Suspected commercial promotion content"
  ]
}
```

### New Field Descriptions

| Field | Description |
|-------|-------------|
| `content_form` | `blog` or `forum` |
| `forum_subtype` | Forum sub-type: `tech_qa` (technical Q&A), `general_discussion` (general discussion), `product_discussion` (product discussion) |
| `problem_resolved` | Only valid for forum tech Q&A: whether the problem is resolved |
| `solution_has_code_or_steps` | Whether the solution contains actionable steps |
| `advertisement_suspected` | Whether advertising is suspected |
