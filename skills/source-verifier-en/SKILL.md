---
name: source-verifier-en
description: "Evaluates reliability of web information sources and answers user questions based on verified sources. Determines source type (official/academic/news/social_media/self_media/blog_forum), assesses domain authority, article quality, timeliness, and resolves source conflicts. Outputs structured citation usability reports and verified answers. USE FOR: source verification, check source reliability, verify web sources, fact-check sources, evaluate citation quality, source credibility assessment, inspect URL authority, cross-reference sources, answer questions with source verification. DO NOT USE FOR: general web search without source evaluation."
license: MIT
metadata:
  author: qyw233
  version: "0.1"
---

# Source Verifier Skill

## Objective

Verify whether provided web information sources are reliable, assess their authority, authenticity, and quality, and answer user questions based on trustworthy sources.

This Skill focuses on:

- Source collection and organization
- Source type identification
- Source reliability assessment
- Article quality evaluation
- Timeliness judgment
- Multi-source conflict resolution
- Generating source evaluation reports for LLM or user reference
- Answering the user's original question based on verified reliable sources

## ⚠️ Core Iron Law: Quantity ≠ Quality, Repetition ≠ Verification

**This is the most important principle of this Skill, runs through all evaluation steps, and must never be violated.**

```text
A claim unsupported by authoritative sources cannot be considered "multi-party independent verification" no matter how many sources repeat it.
No amount of quantity can increase the credibility level—

In particular:
  - General media (tier 2, tier 3)
  - Self-media (any type)
  - Ordinary users on social platforms
  - Blogs and forums
  - Content aggregators and scraper sites

The credibility of these sources can never be set to "high" (citation_usability at most use_with_caution),
no matter how many of them there are or how consistent their claims are.

"Multiple sources agree" can only be considered valid multi-party verification when ALL of the following conditions are met:
  1. At least one authoritative primary source (official/academic/high-reputation tier-1 media) independently confirms
  2. There is no mutual citation, content laundering, or republishing relationship between the sources
  3. Each source independently obtained the information, not from the same upstream source

Otherwise, "large quantity" is precisely a warning sign of content laundering/republishing/viral spread, not a credibility boost.
```

## Operation Modes

### Default Mode: Source Verification + Answer

After verifying all sources, directly answer the user's question based on verified reliable sources. The output contains two parts: source evaluation report + answer based on reliable sources. The model may determine how to organize the answer format.

### Mark-Only Mode

Only classify and mark source credibility, without providing answers. Enable this only when the user explicitly requests "mark only," "classify only," or "no answer needed."

## Trigger Conditions

This Skill should be invoked when the task involves:

- User requests verification of the reliability of web search result sources
- User requests judgment of whether a citation is reliable
- User requests checking whether a webpage can be used as a reference
- User requests comparison of credibility across multiple sources
- User requests source risk evaluation
- User question belongs to high-timeliness or high-risk fields such as news, healthcare, policy, finance, technology releases

## Overall Workflow

0. **Collect and Organize Sources**: Before verification, collate all available sources in the current conversation context:
   - Collect and organize sources from previous search tools, APIs, MCP tools, or results retrieved by loaded skills
   - Or sources manually submitted by the user via URLs or citations
   - Unify all sources into a to-be-verified list, without omitting any available source
1. Read the user's original question, URL list, or search results. Often comes from prior retrieval or links directly provided by the user. First normalize the input to ensure correct URL format, extract key information such as domain and path. When multiple URLs exist, process each URL independently to generate a corresponding source evaluation report.
1.5. **Use `rules/05_cross_region_verification.md` for cross-region/cross-language provenance analysis**: Determine the origin language of the information from the user's question (English-origin / Chinese-origin / Other), and set the cross-language baseline for subsequent evaluation. This step executes before evaluating each URL, and its output affects all cross-language penalty judgments in subsequent scoring rules, and provides echo chamber detection basis for the conflict resolution phase.
2. Normalize each URL:
   - Remove tracking parameters such as `utm_*`
   - Identify the main domain
   - Attempt to obtain title, body excerpt, author, publication time, update time
   - Check for redirects, mirrors, reposts, 404, etc.
3. **When the page cannot be fetched normally** (including but not limited to: network timeout, transfer error, 403/404, returning only minimal text such as just a title, requiring login, page relying on JS rendering where plain text scraping fails to obtain valid content): do NOT skip the URL. Based on available information (domain, URL path structure, known domain background), provide a **preliminary assessment** while outputting detailed `warnings` clearly noting missing information. Preliminary assessment rules:
   - `source_type` can still be determined based on domain (e.g., `shlab.org.cn` is known to be the Shanghai AI Lab official website; even if it cannot be fetched, it belongs to `official`)
   - `article_quality_score`: mark as unable to assess, give minimum usable score with explanation
   - `citation_usability`: default no higher than `use_with_caution`
   - `freshness`: mark as `unknown`
   - `warnings` must list each information item that could not be obtained (title, author, publication time, body excerpt, etc.) and the reason for inability to assess (e.g., "plain text fetch only returned title, unable to obtain body content," "target server connection timed out, no page content retrieved")
   - `reasons` must note "preliminary assessment based on domain, without page content verification"
3.5. **Reputation List Pre-check (Highest Priority)**: Before entering source classification and scoring, first read the following three reputation list files to check whether each URL's domain/entity/social account matches:
    - `rules/reputation_trusted.md` — Trusted sources list
    - `rules/reputation_unreliable.md` — Untrustworthy sources list
    - `rules/reputation_disputed.md` — Disputed sources list
    Sources that match a list directly follow the list rules for `source_reliability_score` and `citation_usability`, **skipping the detailed rule-by-rule checks in step 6** (article quality scoring and timeliness still need independent evaluation). List priority: trusted > disputed > unreliable (if matching multiple, highest priority prevails). All three files are maintained by the user and Agent together, supporting fine-grained custom extensions down to specific social accounts. Sources not matching any list proceed normally through the subsequent workflow.
4. Use `rules/00_source_taxonomy.md` to determine source type.
5. Use `rules/01_general_scoring.md` for general scoring.
6. For **sources not matching the reputation list**, load corresponding rules based on source type. Carefully check all rule files in the `rules/` directory — not just those listed below:
   - Official sources → `rules/source_official.md`
   - Academic sources → `rules/source_academic.md`
   - News media → `rules/source_news.md`
   - Social platforms (first determine if self-media; if so, terminate and switch) → `rules/source_social.md`
   - Self-media → `rules/source_self_media.md`
   - Blog/forum → `rules/source_blog_forum.md`
   - Suspicious sources → `rules/source_suspicious.md`
   - E-commerce platforms → `rules/source_commerce.md`
6.5. **Missed Entries Review**: After completing the evaluation of all sources, go back and check whether any sources should have matched the reputation list but were missed (e.g., domain matched but was not recognized, social account aliases not included). If omissions are found, add them to the corresponding list file to ensure they are not missed next time.
7. Read `rules/00_topic_registry.md`. Based on topics covered in the user's question (such as AI/tech, healthcare, law/policy), load the corresponding topic-specific rule files from the registry for overlay evaluation. The registry supports user custom extensions; see the registry file for details.
8. Use `rules/03_freshness.md` to determine whether the source is outdated.
9. Use `rules/04_conflict_resolution.md` to resolve source conflicts.
10. Output a report conforming to `schemas/source_report.schema.json`.
11. **(Default mode) Answer the user's question**: After completing source verification, generate a detailed report with the user's original question to provide an answer. By default, organize a detailed report evaluating and classifying sources. In this mode, complete tags for each source do not need to be displayed; certain issues requiring particular attention should be reflected in the report. However, all sources should be included, categorized by viewpoint or source type, and finally answer the user's question.

## Output Principles

Output must distinguish between:

```text
Whether the source entity (domain/institution) is reliable
The quality of the article itself (content/evidence)
Whether the page content is highly relevant to the user's question
Whether this source is suitable as the final citation for answering the question
```

Do not just output a single total score.

## Recommended Labels

### Source Type

```text
official
academic
news
professional_analysis
blog_forum
social_media
self_media
aggregator_or_scraper
suspicious
```

### Citation Usability

```text
highly_usable
usable
use_with_caution
not_recommended
do_not_use
```

## Final Answer Constraints

When source reliability is low or evidence is insufficient, do not output deterministic conclusions.

Use expressions such as:

```text
This source has average credibility.
This claim lacks support from authoritative primary sources.
Currently, assessment can only be based on available non-official sources.
Multiple secondary sources repeat this claim, but no official or primary evidence has been found yet.
```
