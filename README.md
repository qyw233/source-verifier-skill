[![English README](https://img.shields.io/badge/README-English-blue)](README.md)
[![简体中文 README](https://img.shields.io/badge/README-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-red)](README.zh-CN.md)

Current language: English.

> This repository provides two aligned installable skill packages: [English](skills/source-verifier-en) and [Chinese](skills/source-verifier-zh). The Chinese package may work better for Chinese-language web sources, the Chinese internet information ecosystem, and Chinese models or model workflows.

# Source Verifier Skill

Large language models are becoming the primary gateway for information access, and the quality of sources directly affects the reliability of model outputs. However, an increasingly prominent issue is that a vast amount of content on the internet does not come from careful human or institutional writing, but rather from low-quality text generated in bulk by automated tools and widely disseminated through content distribution networks. These texts do not pursue accuracy; they pursue being crawled and cited by models.

A 2026 public survey demonstrated a typical case: using inexpensive software tools, a completely fictional product was packaged as "industry-leading," complete with forged technical specifications, user reviews, and ranking data, entering mainstream AI search recommendations within hours. This is not an isolated vulnerability exploit, but an industry chain called "Generative Engine Optimization" (GEO)—influencing the trust weights of large language models towards sources during retrieval-augmented generation by batch-deploying targeted text on the web.Third-party audits found that in AI search results within specific domains, nearly 30% of referenced links belonged to such targeted content. When these texts mutually corroborate semantically and dominate in quantity, they form a "false consensus": seemingly multi-party reporting, but in reality, circular citations of the same template.

The above phenomenon leads to a simple and urgent question: **How to judge whether a source is worth trusting?**

This Skill is designed for this purpose. It provides a systematic framework for evaluating web sources, determining the type, reliability, content quality, and citation value of a webpage information source. Its scope includes:

- Source collection and organization
- Source type identification (official / academic / news / social / self-media / blog/forum / aggregator / suspicious)
- Separate assessment of source entity reliability and individual article quality
- Timeliness assessment
- Multi-source conflict resolution
- Cross-region / cross-language information provenance verification
- Outputting source evaluation reports or source assessment results
- Answering user questions based on verified reliable sources

Therefore, this Skill prioritizes answering one question: **Is this source sufficient to support a specific conclusion for the current question?**

## Applicable Scenarios

- Checking the reliability of search results, web links, or citation lists
- As a source verification Skill in Agent environments that support Skills, such as Claude Code, Codex, OpenCode, OpenClaw  and its derivatives, and Hermes Agent, before searching, researching, or writing reports
- Adding a source checking node to workflows such as Dify, LangGraph, CrewAI
- Evaluating high-timeliness or high-risk information such as news, technology releases, papers, policy, healthcare

## Non-Applicable Scenarios

- Only want to do general search, not concerned about source quality
- Need final rulings for legal, medical, financial, or other professional opinions
- Have no URLs, source names, search results, or verifiable materials at all
- Need to judge factual truth but cannot access original evidence or context

## Quick Start

After installing or enabling this Skill, simply present the source verification task to the model. The user does not need to manually specify which rule files to read; the model automatically loads the corresponding rules based on the `SKILL.md` workflow.

### Basic Usage

```text
Please use source-verifier to evaluate whether the following sources are reliable and answer my question:

Question: Has a certain video generation model been open-sourced?

Sources:
1. https://official.example.com/blog/model-release
2. https://news.example.com/ai/model-open-source
```

The model will automatically identify source types, distinguish source entity reliability from article quality, check timeliness, reposting, secondary retelling, cross-language dissemination, and multi-source conflict risks, and then answer based on reliable sources.

### Evaluate Sources Only

If you only want to mark source quality and do not need the model to answer the original question, explicitly state:

```text
Please only evaluate the reliability of the following links; no need to answer the original question:

Question: Has a certain video generation model been open-sourced?

Sources:
1. https://official.example.com/blog/model-release
2. https://news.example.com/ai/model-open-source
```

### Using with Search Tools

A more common approach is to first let the model search or gather sources, then forcibly organize all the sources and invoke this Skill for verification, for example:

```text
Help me find out whether a certain video generation model has been open-sourced.

Please first use available search tools to collect sources; do not jump to conclusions.
Then organize all found source websites, use source-verifier to verify the reliability of each source.
Finally, answer the question based only on verified reliable sources.
```

If search results already exist, you can directly provide titles, URLs, and excerpts:

```text
Please verify the source quality of the following search results, filter out sources unsuitable for citation, and answer based on reliable sources:

Question: Has a certain video generation model been open-sourced?

Search Results:
1. Title: Model Release Announcement
   URL: https://official.example.com/blog/model-release
   Excerpt: We have released a new video generation model.

2. Title: Company Open-Sources Video Model
   URL: https://news.example.com/ai/model-open-source
   Excerpt: Media reports that the model has been open-sourced.
```

### Custom Reputation Lists and Domain Rules

If you have more nuanced judgments about certain media, institutions, accounts, or professional domains, you can have the model directly maintain this Skill's reputation lists and domain rules. Subsequent evaluations will automatically apply your local knowledge without repeating instructions in each prompt.

Reputation lists can record trusted, untrustworthy, and disputed sources. Entries support domains, URL patterns, social accounts, or entity names.

```text
Please add the following sources to source-verifier's reputation lists:

Trusted Sources:
- domain | Example Official Institution | example.gov | Official publishing channel for a certain domain

Untrustworthy Sources:
- domain | Example Scraper Site | scraper.example | Long-term repurposing, no author, no original source

Disputed Sources:
- domain | Example Disputed Media | disputed.example | Clear stance bias, fact-based reporting needs cross-verification
```

You can also extend specific domain rules:

```text
Please add a financial investment domain rule to source-verifier.

Requirements:
- Trigger when involving stocks, funds, cryptocurrency, financial products
- Prioritize regulatory announcements, exchange filings, listed company announcements, fund prospectuses
- Self-media, community screenshots, signal-following content can only serve as clues
- Automatically downgrade income promises, inside information, price predictions
```

Related files:

```text
rules/reputation_trusted.md      Trusted sources list
rules/reputation_unreliable.md   Untrustworthy sources list
rules/reputation_disputed.md     Disputed sources list
rules/00_topic_registry.md       Domain rules registry
rules/source_<domain>.md         Custom domain rules
```

Reputation lists only affect the trust baseline of the source entity; they do not mean the current page necessarily supports the user's question. Even if a source matches the trusted list, article quality, relevance, timeliness, and the evidence strength of specific claims still need independent evaluation.

## Output Methods

This Skill has two output methods, each with different format requirements:

1. **Default Mode: Source Evaluation Report + Answer**  
   Suitable for scenarios where the user wants to verify sources and get a final answer. The report format is not strictly constrained; the model may organize it based on the user's question, number of sources, and conflict situations. Output should include:
   - Reliability judgment and main risks for each source
   - Which sources can be cited, which can only serve as clues, and which are not recommended for use
   - Whether there are conflicts, reposting, content laundering, or common upstream between sources
   - Answer derived from reliable sources
   - Explanation of uncertainty when evidence is insufficient

2. **Evaluation-Only Mode: Output Only Assessment Results**  
   Enable this when the user explicitly requests "only evaluate sources," "only mark," or "no need to answer." This mode should output structured evaluation results for easy reading or reuse by subsequent workflows.

   The evaluation result for a single source should contain the core fields defined in `schemas/source_report.schema.json`:

   ```text
   user_question              User's question
   url                        Source URL
   domain                     Main domain
   title                      Page title
   source_type                Source type
   relevance_to_question      Relevance to the question
   source_reliability_score   Source entity reliability score
   article_quality_score      Current page quality score
   citation_usability         Citation usability
   freshness                  Timeliness
   reasons                    Reasons for scoring
   warnings                   Risk warnings
   recommended_action         Recommended action
   ```

   If the user's question is broken down into multiple claims or needs to aggregate support from multiple sources for the same question, output a question-level evidence pack. See `examples/example_evidence_pack.json` for structure.

## Core Principles

> **Quantity != Quality, Repetition != Verification.**

1. **Source entity reliability** and **individual article quality** must be assessed separately.
2. A claim unsupported by authoritative primary sources, even if repeated by many secondary sources, cannot be considered multi-party independent verification.
3. Official sources, papers, original regulations, standard documents, and project repositories typically have higher priority.
4. "Multiple sources agree" is only valid cross-verification when at least one authoritative primary source exists, there is no republishing or content laundering between sources, and each source independently obtained information.
5. Social platforms, forums, and self-media usually serve only as clues and cannot independently support high-risk conclusions.
6. Cross-language reports that do not cite primary sources in the origin language should be automatically downgraded.
7. Output results must explain the reasons, not just provide scores.

## Source Types

`source_type` currently supports:

```text
official                 Official sources
academic                 Academic sources
news                     News media
professional_analysis    Professional analysis, industry reports, think tanks or institutional research
blog_forum               Blogs, forums, community Q&A
social_media             Social platform content
self_media               Self-media, personal IP or small team content
aggregator_or_scraper    Aggregator, scraping, republishing sites
suspicious               Suspicious sources
unknown                  Unable to determine
```

Minimum rule routing:

```text
official              -> rules/source_official.md
academic              -> rules/source_academic.md
news                  -> rules/source_news.md
professional_analysis -> rules/01_general_scoring.md + topic rules
blog_forum            -> rules/source_blog_forum.md
social_media          -> rules/source_social.md
self_media            -> rules/source_self_media.md
aggregator_or_scraper -> rules/00_source_taxonomy.md + rules/source_suspicious.md
suspicious            -> rules/source_suspicious.md
```

Topic rules are loaded according to `rules/00_topic_registry.md`, for example:

```text
AI / Tech    -> rules/source_ai_tech.md
Healthcare   -> rules/source_medical.md
Law/Policy   -> rules/source_law_policy.md
```

## Workflow

Detailed workflow is in `SKILL.md`. Simplified workflow:

```text
1. Collect user question, URLs, search results, or citation lists
2. Normalize URLs, extract domain, title, author, publication time, body excerpt
3. Determine information origin language, identify cross-language secondary dissemination risks
4. Read reputation lists, set the initial trust baseline for source entities
5. Determine source type, load corresponding rules
6. Evaluate article quality, relevance, timeliness, and citation usability
7. Handle multi-source conflicts, prioritize evidence strength over source quantity
8. Output source evaluation report or source assessment results
9. Answer the user's question based on verified sources
```

## Directory Structure

```text
source-verifier-en/
├─ README.md                              # Project description
├─ SKILL.md                               # Skill definition and full execution workflow
├─ VERSION                                # Version number
├─ rules/
│  ├─ 00_source_taxonomy.md               # Source type classification rules
│  ├─ 00_topic_registry.md                # Topic-specific rules registry
│  ├─ 01_general_scoring.md               # General scoring rules
│  ├─ 03_freshness.md                     # Timeliness assessment rules
│  ├─ 04_conflict_resolution.md           # Multi-source conflict resolution rules
│  ├─ 05_cross_region_verification.md     # Cross-region / cross-language provenance verification rules
│  ├─ reputation_trusted.md               # Trusted sources reputation list
│  ├─ reputation_unreliable.md            # Untrustworthy sources reputation list
│  ├─ reputation_disputed.md              # Disputed sources reputation list
│  ├─ source_official.md                  # Official sources specific rules
│  ├─ source_academic.md                  # Academic sources specific rules
│  ├─ source_news.md                      # News media specific rules
│  ├─ source_social.md                    # Social platform specific rules
│  ├─ source_self_media.md                # Self-media specific rules
│  ├─ source_blog_forum.md                # Blog/forum specific rules
│  ├─ source_suspicious.md                # Suspicious sources specific rules
│  ├─ source_ai_tech.md                   # AI / Tech topic rules
│  ├─ source_medical.md                   # Healthcare topic rules
│  └─ source_law_policy.md                # Law/Policy topic rules
├─ prompts/
│  └─ evaluate_source.prompt.md           # Single source evaluation prompt template
├─ schemas/
│  └─ source_report.schema.json           # Single source result schema for evaluation-only mode
└─ examples/
   ├─ example_input.json                  # Structured input example (developer reference)
   └─ example_evidence_pack.json          # Question-level evidence pack example for evaluation-only mode
```

## Example: Filtering Contaminated Search Results

Below is a real usage scenario: for the same question and the same set of web search sources, the conclusions differ significantly without and with this Skill's source verification.

The original question asked in Chinese about Grok-2's parameter count:

```text
Grok-2 的参数量是多少？
```

DeepSeek web quick mode search results: [https://chat.deepseek.com/share/j7ou83xvm9ib30i7tt](https://chat.deepseek.com/share/j7ou83xvm9ib30i7tt)
Conclusion:
```text
Grok-2's total parameter count is approximately 905B (905 billion), with active parameters around 136B.
```

The problem with this conclusion: a relatively influential Chinese media outlet published the 905B claim without citing original sources. Subsequently, multiple Chinese media outlets, aggregators, and reposting sites further propagated it, creating the illusion that "many sources say so."

After using DeepSeek V4 Flash with OpenCode, extracting the same set of sources used by DeepSeek web, and invoking this Skill for verification, the generated report concluded:

```text
Grok-2's parameter count has no officially confirmed number.
Based on technical analysis of open-source weights, total parameters are approximately 269B, with active parameters around 115B.
The 905B figure reported by media has no official source support and is unreliable.
```

This Skill's role in this case:

- Identified that the 905B claim primarily originated from Chinese media republishing chains, not from official or technical primary sources.
- Determined that multiple republishing sources had highly overlapping content and cannot count as independent cross-verification.
- Found that xAI / Hugging Face official repositories have not published Grok-2's parameter count, so no official confirmation of any number can be asserted.
- Elevated the priority of stronger evidence sources: DataLearner, Unsloth, Ollama and other technical sources, based on open-source weights, model configurations, or metadata, pointing to approximately 269B-270B total parameters.

This example demonstrates this Skill's core value: based on mixed search results, identifying republishing contamination, distinguishing primary sources from secondary dissemination, and eliminating interference, transforming AI search from "it seems many sources say so" to "which sources truly support the conclusion."

## Known Limitations

- This Skill primarily guides the Agent in analyzing and verifying already obtained search results, web links, or candidate sources; it does not guide the Agent in designing more effective proactive search strategies.
- Effectiveness still depends on the quality of input sources. If the search tool returns poor sources with incomplete coverage or lacking primary sources, this Skill may still produce incorrect or incomplete conclusions. Therefore, for high-risk questions, prioritize better search tools and proactively supplement official, primary, regulatory, paper, standard, code repository, or original data sources.
- This Skill can only perform preliminary assessment based on source type, source entity, article quality, timeliness, evidence chain, and conflict situations. Even if a source is relatively authoritative, it does not guarantee that its specific claims are correct; final judgment and decisions remain the user's responsibility. This Skill will highlight notable risks for each source whenever possible.
- Professional domain rules for healthcare, legal, financial, education, e-commerce, etc., are currently primarily placeholders and general constraints. The author is not familiar with all specialized domains. Users should modify `rules/00_topic_registry.md` and corresponding `rules/source_<domain>.md` based on their own expertise.
- When pages cannot be fetched, only preliminary assessment based on domain and known information is possible, which cannot replace full-text verification.

## Version

Current version: `0.1`


