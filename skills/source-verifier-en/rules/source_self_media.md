
> **Must read SKILL.md before reading this file to understand the full task context.**

# Self-Media Source Processing Rules

Self-media refers to accounts operated by individuals or small teams as independent creators on social/content platforms, typically relying on platform traffic sharing, advertising, affiliate sales, or knowledge payment for monetization. The core difference from official accounts and traditional media: lacks institutional editorial review mechanisms; content quality depends entirely on individual ability and motivation.

**Default credibility assumption: self-media sources generally have low overall credibility; default no higher than `use_with_caution`.** Even professional self-media must undergo strict content quality verification before limited citation. Do not relax judgment because of quantity or consistent claims — quite the opposite:大量 self-media repeating the same claim often indicates that the claim has been virally disseminated through content laundering/republishing chains, not经过 multi-party independent verification. In such cases, be especially vigilant.

**Self-media cannot serve as sole evidence; generally requires cross-verification from other independent sources.**

### Exception: When the User Query Directly Targets the Self-Media Itself

If the user's question is about the self-media's own situation, opinions, statements, or status (e.g., "How did certain self-media evaluate XX event," "What does a certain blogger think about XX product," "What content has certain self-media published"), then the self-media's content constitutes a **primary original source** for answering that question:

```text
Trigger conditions (any one met):
  - User explicitly asks about the self-media's views, attitudes, statements
  - User asks about the self-media's own situation (e.g., operating status, commercial partnerships, controversial events)
  - User asks whether the self-media has published certain types of content
  - User treats the self-media as research subject or information target

Handling in this case:
  → source_type upgrades to official; add secondary tag primary_source
  → This self-media has the highest evidentiary authority for "what it said" and "what its views are" — treated as official primary source
  → citation_usability can be raised to highly_usable
  → Note in reasons: "User query directly targets this self-media; its own content constitutes an official primary source"

Important boundary:
  - The self-media is a primary source for its own statements/views, but external facts mentioned in its statements still require independent verification
  - Example: User asks "How did certain self-media evaluate XX event" → the self-media content is a primary source, usable
  - Example: User asks "Is XX event true," citing a self-media's claim → the self-media is merely a secondary source; cannot be used as sole evidence
  - Determining criterion: Is the answer to the user's question primarily about the self-media itself, or about external facts discussed by the self-media
```

## I. Self-Media Type细分

### 1. Professional Self-Media

Operated by individuals with domain professional backgrounds (e.g., licensed physicians, practicing attorneys, university faculty, industry engineers with real-name verification); content primarily focused on professional knowledge普及.

```text
Characteristics: Real name, verifiable professional qualifications, rigorous content, has citation sources
Trust level: C;个别 can reach B
```

### 2. Experiential Self-Media

Operated by practitioners or eyewitnesses; content primarily focused on industry experience, operational tips, pitfall records.

```text
Characteristics: First-person experience description, reproducible, has specific scenarios
Trust level: C or D
```

### 3. Marketing Self-Media

Primarily aimed at commercial monetization; content围绕 affiliate sales, course promotions, brand partnerships, traffic monetization.

```text
Characteristics: Dense commercial links, exaggerated titles, shallow content, frequent sales pitches
Trust level: D or E
```

### 4. Repurposing/Content Laundering Self-Media

大量 copying, splicing, translating others' content; lacking original information.

```text
Characteristics: Content highly similar to others; no first-hand information; no author's views
Trust level: E
```

### 5. Emotional/Traffic-Driven Self-Media

Primarily uses emotional煽动, controversy creation, and trend-hopping to obtain traffic.

```text
Characteristics: Clickbait, binary opposition narratives, lacks data support, emotional comment section
Trust level: E
```

## II. Quality Assessment Signals

### Positive Signals

```text
Author identity verifiable, with relevant domain qualifications or professional background
Content cites official sources, papers, original regulations, and provides traceable links
Data has attribution, methods have explanation, conclusions have boundaries
Distinguishes factual陈述 from personal opinion
Content长期 consistent; historical record shows no repeated contradictions
Comment section contains meaningful discussion and author supplements
Author has record of correcting errors
No hidden commercial interests (or sponsorship/partnership clearly labeled)
```

### Negative Signals

```text
Author identity vague or untraceable
Frequent use of "reportedly," "internet says," "informed sources," "inside information" without giving sources
Historical content repeatedly debunked or contradictory to facts
Title severely mismatched with body
Content driven by emotion rather than facts
Commercial promotions not labeled
Cross-platform发布大量 homogenized content
Comment section comment controlled, deleted, or only fan likes
Using anxiety or fear to drive conversions (e.g., "if not now, it'll be too late")
```

## III. Usage Rules by Scenario

**Default premise: In all scenarios, self-media sources default to citation_usability no higher than `use_with_caution`. The following "can be used cautiously" scenarios are exceptions under this default ceiling, not upgrades of self-media to reliable sources.**

### Can Be Used Cautiously

```text
Author is real-name with verifiable professional background doing domain knowledge科普
Specific reproducible operation tutorials, configuration methods, troubleshooting experience
Genuine user experience with specific products (must mark as personal experience)
Industry practitioner trend observations (must clarify as personal opinion)
```

When used, must:
- Mark as "personal opinion/experience,未经 independent verification"
- If more authoritative sources exist, prioritize them
- Do not use this source as sole evidence

### Cannot Be Used as Evidence

```text
Medical diagnosis, treatment recommendations
Legal opinions, policy interpretations as sole basis
Financial investment advice
Sole source for scientific conclusions or statistical data
Sole confirmation of company operating status, product releases
Sole basis for open source license judgments
Sole reporting of major news events
```

### Multiple Self-Media Repetition ≠ Multi-Party Verification

**Core principle: The quantity of self-media sources cannot substitute for quality. Multiple self-media repeating the same claim does not mean the claim has been多方 verified.**

When evaluating multiple sources and finding multiple Chinese self-media accounts repeating the same claim, the following rules must be applied:

```text
1. First determine whether the claim is corroborated by an official source or authoritative primary source:
   - Has official/primary source → rely on official/primary source; self-media only supplementary
   - No official/primary source → proceed to step 2

2. Determine whether a high-credibility news media has independently reported:
   - Has high-credibility media with named reporting and citing original sources → can partially参考 media judgment
   - Only average quality media or unnamed reporting → equivalent to no independent verification; proceed to step 3
   - No independent media reporting → proceed to step 3

3. Only self-media互相 repeating:
   → Not considered multi-party independent verification
   → Overall evidence level: evidence_insufficient
   → Conclusion: The claim lacks support from reliable sources; cannot be used as any factual basis
```

#### Typical Danger Signals

```text
- Same topic intensively published by大量 Chinese self-media accounts, but content highly similar
- These self-media none provide traceable original source links
- The earliest traceable source is still another self-media account
- No English/origin language primary source corroboration
- No official announcement, no paper, no original regulation, no data source
- Vague citation chains like "foreign media reports," "according to sources," "informed sources say"
```

#### Special Note on Chinese Ecosystem

The Chinese self-media ecosystem contains大量 traffic-driven content production:

```text
- An unverified claim can be rewritten and disseminated by dozens of self-media accounts within hours
- This "large quantity" is the result of content laundering/repurposing, not multi-party independent investigation
- Even if the number of sources reaches dozens, the evidence strength remains zero
- Be especially vigilant about such situations; never increase credibility assessment simply because "multiple sources agree"
- In such cases, proactively search for official or authoritative sources in the origin language for re-verification
```

#### Judgment Output

```text
- Individual self-media source citation_usability unchanged (still evaluated per existing rules)
- But at the conflict resolution level, multiple self-media "agreeing" does not count as independent verification
- Conflict status: evidence_insufficient
- Must output warning: "Multiple Chinese self-media repeat the same claim, but none trace back to an official or authoritative primary source; not considered valid corroboration"
- Recommended action: search_for_origin_language_primary_source
```

## IV. Domain-Specific Rules

### Healthcare

Medical content published by self-media:

```text
Licensed physician real-name verified + citing guidelines/papers → use_with_caution (still mark as non-diagnostic advice)
No qualifications or untraceable → do_not_use
Even if the author is a doctor, individual advice ≠ medical standard
```

### Law/Policy

```text
Licensed attorney real-name + citing original legal text → use_with_caution (mark as non-legal advice)
No qualifications → do_not_use
Self-media interpretation should not be equated to the regulation itself
```

### Finance/Investment

```text
Regardless of author qualifications, self-media financial advice defaults to not_recommended
Data provided by the author may be referenced, but not relied upon alone for investment decisions
Must check for conflicts of interest (e.g., position disclosure)
```

### AI / Tech

```text
Industry practitioner experience, technical tutorials → can be referenced
Open source status, API features, model capabilities → must cross-verify with official sources
Product reviews, performance comparisons → must check for commercial partnerships
```

## V. Cross-Platform Matrix Evaluation

If the same self-media operates on multiple platforms (e.g., WeChat Official Account, Bilibili, Douyin, Xiaohongshu, etc.), should:

```text
1. Check if content is consistent across platforms
2. Different platforms may have different content strategies (e.g., in-depth content on WeChat, traffic content on Douyin)
3. Focus on the platform with the highest content quality as the primary reference
4. Matrix operation itself is not a negative signal, but注意 whether there is organized marketing behavior
```

## VI. Output Requirements

```json
{
  "source_type": "self_media",
  "self_media_type": "professional | experiential | marketing | content_farm | clickbait",
  "author_identity": {
    "is_verified": false,
    "is_real_name": false,
    "claimed_expertise": "...",
    "verifiable_credentials": "..."
  },
  "commercial_interest": {
    "detected": false,
    "type": "sponsorship | affiliate | course_sales | none"
  },
  "content_originality": "original | partially_original | derivative | likely_copied",
  "sources_cited": false,
  "citation_usability": "use_with_caution | not_recommended | do_not_use",
  "reasons": ["..."],
  "warnings": [
    "Self-media source; lacks institutional editorial review",
    "Author's professional qualifications未经 independent verification",
    "Content contains unlabeled commercial promotion"
  ],
  "recommended_action": "cross_check_with_official_source"
}
```

## VII. Quick Judgment Flowchart

```text
Social platform account
  │
  ├─ Is it an institution/organization verified account? → Yes → official_social → process per source_social.md official rules
  │
  └─ No → Operated as individual?
          │
          ├─ Has verifiable professional qualifications + no commercial monetization + cites original sources?
          │   └─ Yes → Professional self-media → can be cautiously cited; ceiling use_with_caution
          │
          ├─ Has any of: commercial monetization, clickbait, emotional, shallow content?
          │   └─ Yes → Based on severity, set to not_recommended or do_not_use
          │
          └─ Is it repurposing/content laundering/no original content?
              └─ Yes → do_not_use; recommend finding original source

Note: Regardless of evaluation result, self-media sources default to not being usable as the sole basis for facts.
Multiple self-media sources agreeing ≠ multi-party verification; instead, treat as a warning signal of a content laundering/republishing chain.
```
