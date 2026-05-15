
> **Must read SKILL.md before reading this file to understand the full task context.**

# News Media Processing Rules

News media is suitable for verifying events, announcements, interviews, and public statements, but most news is secondary sources. When evaluating news sources, first trace back to the original reporting media, then comprehensively assess that media's authority, stance, and article quality.

## I. First Determine Whether It Is a Repost/Aggregation

Upon encountering a news report, the first step is to confirm whether it is the original report. Many news websites are actually reposting or aggregating content from other media. Directly citing a reposting site loses traceability to the original media.

### Repost/Aggregation Identification Signals

```text
Article beginning or end marked with "Source: XXX," "Via: XXX," "Reprinted from: XXX"
Article states "According to XX report," "XX News Agency says" but does not link to the original text
Page domain is clearly not a news organization (e.g., SEO aggregator site, content farm)
Same article appears on multiple domains with nearly identical content
Article author is "Editor/Compiled," "Comprehensive Report" rather than a named reporter
Domain similar to well-known media but slightly different (counterfeit or mirror site)
```

### Trace-Back Processing

If determined to be a repost or aggregation, follow these steps:

```text
1. Extract original source clues from the text (media name, reporter name, original link)
2. Find the original publication page for that report via search engine or original link
3. Verify the original page actually exists and content is consistent
4. Switch the evaluation target to the original media, not the current reposting site
5. Mark the reposting/aggregation site with secondary tags secondary_report or aggregator_or_scraper

If the original source cannot be found:
  → Mark "original source untraceable"
  → Downgrade citation_usability one level
  → If multiple reposting sites exist but none traceable, do not consider as independent verification
```

## II. Evaluate Media Authority

After finding the original reporting media, assess the overall authority of that media. Note: The same media may have vastly different authority in different domains.

### 2.0 Media Authority Three-Tier Classification

Before domain-specific evaluation, first classify media into three tiers based on institutional nature and review mechanisms:

#### Tier 1: High Authority Media

Official news agencies and traditional print/broadcast/TV websites:
```text
- Official news agencies: Reuters, AP, AFP, TASS, etc.
- Traditional print media websites: NYT, Washington Post, WSJ, The Guardian, The Telegraph, etc.
- Traditional broadcast/TV websites: BBC, CNN, NHK, etc.

Characteristics: Have offline print or broadcast tradition, strict multi-layer editorial review mechanisms, public correction policies
Trust baseline: High
English traditional media (e.g., NYT, BBC, The Guardian, Reuters, AP, etc.) have long-developed editorial review systems with generally high credibility baselines — but this does not mean no verification is needed; still check for named reporters and original source citations.
```

#### Tier 2: Medium Authority Media

Smaller media and pure digital emerging media:
```text
- Pure digital-born media (no print tradition): TechCrunch, The Verge, BuzzFeed News, etc.
- Local/small media
- Industry vertical media (e.g., technology, automotive, gaming verticals)

Characteristics: No strict multi-layer review mechanisms of traditional print media; content publication speed often prioritized over accuracy; editorial processes relatively simplified
Trust baseline: Medium
Risk warning: The core difference between tier 2 and tier 1 media is the strictness of review processes. Their reports cannot automatically equate to high-authority sources; must be assessed in combination with article quality.
```

#### Tier 3: Low Authority Media / Quasi-Self-Media

Sources with the appearance of media but essentially close to self-media:
```text
- "Media accounts" on content aggregation platforms
- "New media" with traffic as primary goal and lacking editorial standards
- So-called "news websites" with no identifiable editorial team

Characteristics: Lacking verifiable editorial teams and review processes; content driven by traffic
Trust baseline: Low; evaluate per self_media or aggregator_or_scraper rules
```

#### Tier Usage Rules

```text
Tier 1 media + named reporter + citing original sources → Can independently serve as reliable citation; citation_usability can reach highly_usable
Tier 1 media + anonymous sources → citation_usability no higher than usable (see "Anonymous Source Special Rules")
Tier 2 media + named reporter + citing original sources → usable, but cross-verification recommended
Tier 2 media + unnamed/no original sources cited → use_with_caution
Tier 2 media agreeing with self-media/blog/forum but no tier 1 or official source corroboration → not considered valid multi-party verification (see 5.2.1)
Tier 3 media → evaluate per blog_forum or self_media rules
```

### 2.1 Domain-Specific Evaluation

Media authority is not absolute; it must be assessed in the context of the user's question domain:

```text
Technology/Internet:
  High authority: The Verge, Ars Technica, Wired, InfoQ
  Medium: TechCrunch
  Note: Tech media may have deviations in technical detail descriptions; not a substitute for official documentation

Finance/Business:
  High authority: Reuters, Bloomberg, Financial Times
  Medium: MarketWatch, CNBC
  Note: Financial media may have market influence motives in reporting on listed companies

Politics/International Relations:
  High authority: Reuters, AP, BBC
  Medium: Major national mainstream media
  Note: Political reporting is most affected by media stance; see section 2.2 below

Science/Medicine:
  High authority: Nature News, Science News, STAT News
  Medium: General tech media science sections
  Note: Science news often exaggerates paper conclusions; must cross-reference original paper
```

When evaluating, based on own knowledge or web research, determine whether the media is recognized as authoritative in the domain of the user's question. If a media is top-tier in domain A but average in domain B, adjust scores accordingly.

### 2.2 Political Stance and Media Bias

Different countries' media, and different media within the same country, have different political stances. Some reports may reflect bias in fact selection, wording, or article length.

#### Situations Requiring Special Attention to Stance

```text
User question involves international relations, territory, sovereignty, ethnicity, religion, etc. sensitive topics
User question involves policy comparison between different countries/regions
Reporting target is a government, political party, or political figure
Reporting involves ongoing geopolitical conflicts or controversial events
Reporting clearly contains praise/criticism or value judgments
```

#### Common Media Stance Reference

```text
Different countries' official/semi-official media naturally represent their respective national stances:
Examples:
  US: CNN, Fox News, MSNBC, NYT
  UK: BBC, The Guardian, The Telegraph
  Russia: RT, TASS
  Qatar: Al Jazeera

Different media within the same country have different leanings:
Examples:
  US left-leaning/liberal: NYT, CNN, MSNBC, Washington Post
  US right-leaning/conservative: Fox News, NY Post, Wall Street Journal (opinion pages)
  UK left-leaning: The Guardian
  UK right-leaning: The Telegraph, Daily Mail
```

#### Handling

```text
General case (no special user request):
  If the user question does not involve politically sensitive topics → serve only as background reference; do not affect main scoring
  If the user question involves politically sensitive topics → must note the media's stance leaning
    → Recommend supplementing with sources of different stances for cross-verification
    → Note in warnings: "This media has a specific political leaning"

When user explicitly requests stance check:
  → Check and output the media's political leaning, shareholder background, editorial policy to the extent possible
  → If a specific reporter is involved, check that reporter's reporting history for bias
  → Add media_stance field to the report
```

### 2.3 Media Credibility Assessment

Comprehensively assess the media's overall credibility, including but not limited to:

```text
Positive signals:
  Has public editorial standards and correction mechanisms
  Has clear distinction between news, opinion, and sponsored content
  Has bylined reporters and editor contact information
  Historically accurate reporting on major events
  Awarded journalism industry prizes or certifications
  Cited by other high-credibility media

Negative signals:
  History of false reporting being debunked or sued
  Serious clickbait issues
  Blurred boundaries between news and advertising (unlabeled advertorials/native ads)
  Obvious political or commercial interest-driven reporting
  History of spreading conspiracy theories or pseudo-science
  Retracting reports without public explanation
```

## III. Article-Level Quality Assessment

Even if a media's overall authority is high, individual article quality still needs independent assessment.

### Positive Signals

```text
Named reporter with verifiable reporting history
Clear publication and update dates
Cites and links to original sources (official announcements, papers, documents)
Named sources (not "informed sources")
Official response or multi-party interviews
Distinguishes news reporting from reporter commentary
Data has source attribution and methodology
```

### Negative Signals (Red Flags)

```text
"According to internet rumors," "sources say," "foreign media reports" without specific media name or link
"Informed sources reveal" without any context provided
No author byline
No publication date
Title severely mismatched with content
Large portions copied from other media without independent editorial work
Obvious marketing advertorial (product promotion disguised as news)
Anonymous sources as sole source with sensitive content
Emotional language, inflammatory headlines
```

### Anonymous Source Special Rules

When a report uses anonymous/vague source expressions, regardless of media tier, downgrade must be applied:

#### Anonymous Source Expressions

```text
"people familiar with the matter"
"sources say"
"industry sources"
"a person close to..."
"an official speaking on condition of anonymity"
"according to sources"
"it is understood that"
etc.
```

#### Downgrade Rules

```text
- Single anonymous source with no verifiable evidence → citation_usability downgrade one level
- Multiple anonymous sources but no named sources to corroborate → still must downgrade; note in warnings
- Even for tier 1 high-authority media, reports relying solely on anonymous sources cannot be equated to the credibility of that media's named reporting
- Anonymous source report + no other independent source corroboration → citation_usability no higher than use_with_caution
```

#### Note

```text
- Anonymous sources are a legitimate and necessary journalistic tool in investigative reporting; this rule does not否定 their journalistic value
- However, in source verification scenarios, anonymous sources cannot be traced or verified; evidence strength is inherently weaker
- Reports based on anonymous sources should not be treated as "confirmed facts" or "official positions"
- If multiple media all cite the same anonymous source (e.g., "according to informed sources" with the same content), this should not be considered multi-party independent verification — it is just multiple outlets relaying the same source
```

## IV. Author/Reporter Stance Check (On Demand)

Generally, reporter stance does not need to be checked. Only trigger in the following situations:

```text
User explicitly requests reporter stance check
Report content is highly controversial and the user cares about information credibility
Reporter is highly prominent and their personal stance clearly affects the reporting
```

Check content (if triggered):

```text
Reporter's work history and affiliated media
Topic leaning of reporter's past reports
Reporter's publicly expressed political or industry views
Reporter's social media statements (if related to the reporting topic)
Whether the reporter has a conflict of interest with the reporting subject
```

## V. Multi-Source Usage Rules

### 5.1 Breaking News

```text
Require at least 2-3 independent high-credibility media to corroborate each other
Prioritize sources with on-site reporters or official confirmation
Note: Multiple media under the same group (e.g., same parent company) cannot be considered independent sources
```

### 5.2 Multi-Source Repetition

```text
If multiple media have highly similar content but no original source links:
  → May just be互相 republishing or rewriting
  → Cannot be considered independent verification
  → Find the earliest published article with the most detailed original citations; trace back to the original media
```

### 5.2.1 Mixed Corroboration Across Authority Levels

When tier 2 media agrees with self-media, blogs/forums, and other lower-authority sources:

```text
Core principle: Tier 2 media review standards are already relatively loose and cannot provide authoritative endorsement for lower-authority sources.

Rules:
- Only tier 2 media + self-media/blog/forum agreeing ≠ valid multi-party verification
- This "agreement" does not increase overall credibility
- Must trace whether tier 1 media or official sources independently confirm the same claim
- If no tier 1 or official source corroboration → overall evidence level remains evidence_insufficient
- Note in warnings: "Only tier 2 media and self-media sources agree; not independently corroborated by high-authority sources"
- Be especially vigilant; do not relax judgment just because "it seems many outlets reported it"
```

### 5.3 What News Can and Cannot Be Used For

```text
Can be used for:
  Event time, location, participants
  Company public statements, financial data
  Direct quotes from interviewees
  News background, social reactions

Should not be used alone for:
  Technical feature details → prioritize official documentation
  Open source license judgments → prioritize LICENSE file in repository
  Medical conclusions → prioritize peer-reviewed papers or regulatory agencies
  Legal conclusions → prioritize original regulations
  Scientific consensus → prioritize review papers or academic institution statements
  Performance leadership claims → require independent evaluation
```

## VI. Output Recommendations

```json
{
  "source_type": "news",
  "article_type": "news | opinion | analysis | sponsored | press_release_repost | breaking",
  "is_repost": false,
  "original_media": {
    "name": "Reuters",
    "url": "https://www.reuters.com/...",
    "verified": true
  },
  "media_authority_by_field": {
    "relevant_field": "technology | finance | politics | science | general",
    "authority_level": "high | medium | low | unknown"
  },
  "media_stance": {
    "political_leaning": "left | center_left | center | center_right | right | varies | not_applicable",
    "country_of_origin": "CN | US | UK | ...",
    "note": "This media is based in the US and may have stance biases on US-China relations topics"
  },
  "media_credibility": "high | medium | low | disputed",
  "media_tier": "tier_1 | tier_2 | tier_3",
  "anonymous_sources_only": false,
  "links_to_primary_source": true,
  "multiple_independent_sources": false,
  "citation_usability": "highly_usable | usable | use_with_caution | not_recommended | do_not_use",
  "reasons": [
    "Reposted from Reuters original report",
    "Reuters has high authority in international finance",
    "Article cites original official announcement"
  ],
  "warnings": [
    "This media has a specific stance leaning on political topics",
    "Recommend supplementing with sources of different stances for cross-verification",
    "Technical details section does not provide original sources"
  ]
}
```

### New Field Descriptions

| Field | Description |
|-------|-------------|
| `is_repost` | Whether it is a repost/aggregation, not original reporting |
| `original_media` | Original media info (fill in when reposted) |
| `media_authority_by_field` | Media authority in the domain of the user's question |
| `media_stance` | Media political leaning and country of origin (required for sensitive topics; otherwise fill `not_applicable`) |
| `media_credibility` | Media overall credibility rating |
| `media_tier` | Media authority tier: `tier_1` (official media/traditional print), `tier_2` (smaller/emerging digital media), `tier_3` (low authority/quasi-self-media) |
| `anonymous_sources_only` | Whether report relies solely on anonymous sources |
| `multiple_independent_sources` | Whether multiple independent sources corroborate |
