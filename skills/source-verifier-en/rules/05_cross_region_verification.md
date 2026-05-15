
> **Must read SKILL.md before reading this file to understand the full task context.**

# Cross-Region / Cross-Language Provenance Verification Rules

This rule executes at the earliest stage of the workflow — after obtaining the user's question, first determine the information origin language and set the cross-language evaluation baseline.

## I. Core Principles

1. **Information Origin Principle**: The primary source of information about a topic is typically in the language environment where the topic originated. US company → English official; China policy → Chinese official; Japanese product → Japanese official.
2. **Language Mismatch Downgrade Principle**: Reports about the same topic in a non-origin language are automatically downgraded unless they cite a primary source in the origin language.
3. **Chinese Self-Media and General Media Ecosystem Warning**: The Chinese information ecosystem contains a large number of content-laundering/repurposing content farms. "Multiple Chinese sources agree" alone cannot be considered multi-party independent verification.

## II. Topic Origin Determination

Analyze from the user's question where the information source should be in terms of language/region:

### Determination Dimensions

| Dimension | English-origin | Chinese-origin | Other |
|-----------|---------------|----------------|-------|
| Company/Product | US/UK/CA/AU etc. English-speaking company | Chinese company/product | JP/KR/EU etc. |
| Policy/Regulation | FDA, EU AI Act, SEC etc. | Chinese policy, regulation | Local regulations |
| Academic/Technical | Major international journals, conferences | Chinese academic institutions dominant | Local institutions |
| Event | Event occurring in US/UK etc. | Event occurring in China | Local event |

### Determination Method

```text
1. Extract key entities from the user's question (company name, product name, regulation name, person, institution)
2. Determine the country/region those entities belong to
3. Determine the information origin language:
   - US/UK/Canada/Australia/International general → English (English-origin)
   - China → Chinese (Chinese-origin)
   - Japan → Japanese
   - Other → Local language
4. If cannot determine → mark as unknown, do not apply cross-language downgrade
```

### Examples

```text
User asks: "What features does OpenAI's latest GPT-5 support?"
  → Entities: OpenAI (US company), GPT-5 (US product)
  → Information origin language: English-origin

User asks: "What requirements does the EU AI Act have for foundation models?"
  → Entity: EU AI Act (EU regulation)
  → Information origin language: English-origin (EU official texts are primarily in English)

User asks: "What are the latest updates to Baidu's ERNIE Bot?"
  → Entities: Baidu (Chinese company), ERNIE Bot (Chinese product)
  → Information origin language: Chinese-origin
```

## III. Source Language vs. Topic Origin Matching Rules

### 3.1 Direct Match (Source Language = Topic Origin Language)

Normal evaluation, no cross-language downgrade.

### 3.2 Language Mismatch (Source Language ≠ Topic Origin Language)

If a source reports in a non-origin language (e.g., Chinese article reporting on a US company product), apply the following rules:

#### Has Original Source Citation

If the source **explicitly cites and links** to a primary source in the origin language (official announcement, paper, original regulation, etc.):
```text
- Add secondary tag: cross_language_report
- Normal evaluation, no additional downgrade
- Note in reasons: "Has cited primary source in original language"
```

#### No Original Source Citation

If the source **does not cite** a primary source in the origin language:
```text
- Add secondary tag: cross_language_report
- source_reliability_score: additional -15
- citation_usability: downgrade at least one level (usable → use_with_caution → not_recommended → do_not_use)
- Note in warnings: "This source reports in a non-origin language and does not cite a primary source in the original language"
```

## IV. Language Ecosystem Baseline Credibility Adjustment

Different language information ecosystems have structural differences. The following adjustments are applied in addition when evaluating **non-origin language sources**.

### 4.1 English Sources (for Chinese-origin topics)

```text
- English mainstream news/academic sources: Generally have完善的 editorial review mechanisms, typically higher credibility → normal evaluation
- English self-media/blogs/forums: Treated equally to Chinese counterparts, no special bonus
- English tabloids/content farms: Treated as suspicious
```

### 4.2 Chinese Sources (for English-origin or other non-Chinese topics)

In the Chinese information ecosystem, non-official sources (self-media, general media, blogs/forums) have structural credibility risks:

```text
- Large number of content-laundering/repurposing self-media互相抄袭, forming false "multi-party corroboration"
- Marketing accounts prioritize traffic over content accuracy
- Some platforms (such as Baijiahao, Toutiao, etc.) have content review focused on compliance rather than factual accuracy

Adjustment rules (only effective for non-Chinese-origin topics):
- Chinese self_media: additional -10 (叠加 on existing score from source_self_media.md)
- Chinese blog_forum (excluding international platforms like Stack Overflow, GitHub): additional -8
- Chinese news (unnamed reporter or no original source link): additional -5
- Chinese official media/official sources: normal evaluation, no additional penalty
```

Note: The above downgrades are additional adjustments for **non-Chinese-origin topics**. If the topic itself is Chinese-origin (e.g., Chinese company product, Chinese policy), Chinese sources are not subject to this downgrade rule.

### 4.3 Chinese Low-Quality Content Platform Identification

The following platforms in the Chinese information ecosystem are dominated by low-quality content. When evaluating, default to a negative预设 (unless the page cites verifiable primary sources):

```text
- Baidu Baijiahao (baijiahao.baidu.com): Content farm,大量 content laundering and SEO spam
- Sohu Hao (mp.sohu.com, sohu.com/a/...): Content repurposing platform
- NetEase Hao (dy.163.com, 163.com/dy/...): Content distribution platform
- Toutiao Hao (self-media articles on toutiao.com): Traffic-driven content
- Other content distribution platforms: Dayu Hao, Qiehao, Yidian Hao, Dafeng Hao, etc.

Identification features:
- URL path contains /a/, /dy/, /mp/ etc. content distribution paths
- Page has obvious platform self-media标识 like "xx Hao," "xx Creator"
- Article title exaggerated, body shallow, no real-name author or author无法查证
- Page has大量 recommended links or advertisements

Processing:
- Articles from these platforms classify as self_media or aggregator_or_scraper
- Unless the article explicitly cites and links to verifiable primary sources, citation_usability no higher than use_with_caution
- Note platform low-quality risk in warnings
```

## V. Echo Chamber Detection

When processing multiple sources, check for the following pattern:

### Detection Conditions
```text
1. Topic is English-origin or other non-Chinese origin
2. All currently available sources are Chinese
3. These Chinese sources have similar content but do not cite a common original source
4. No primary or authoritative source in the origin language has been found
```

### Determination
```text
If all conditions are met → echo_chamber_detected = true
  → Do not consider as multi-party independent verification
  → Even with many sources, overall credibility cannot be increased
  → Mark echo_chamber_risk in the conflict resolution report
  → Recommendation: Search for origin language sources before evaluating
```

## VI. Output Format

### Global Assessment (shared by all sources in a single evaluation)

```json
{
  "topic_origin_language": "english | chinese | japanese | other | mixed | unknown",
  "topic_origin_region": "US | CN | JP | EU | ...",
  "echo_chamber_detected": false,
  "origin_language_sources_found": true,
  "cross_language_notes": "The information source for this topic should be in English. Current Chinese sources have not cited any English primary sources; downgrade applied."
}
```

### Per-Source Judgment

```json
{
  "cross_language_report": true,
  "language_matched_with_origin": false,
  "cites_primary_source_in_origin_language": false,
  "cross_language_penalty": -15
}
```

## VII. Collaboration with Other Rules

- This rule executes at **step 1.5** of the workflow, after URL normalization and before source type classification
- This rule's output affects scoring adjustments in subsequent `01_general_scoring.md`
- This rule's echo chamber detection results are used by `04_conflict_resolution.md`
- This rule's identification of Chinese low-quality platforms affects type determination in `00_source_taxonomy.md`
