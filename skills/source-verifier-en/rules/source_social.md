
> **Must read SKILL.md before reading this file to understand the full task context.**

# Social Platform Source Processing Rules

The evidence strength of social platform sources is highly dependent on the **identity and credibility of the account holder**. Cannot simply judge by "social platform" as a medium alone; must evaluate each account's identity, verification quality, professional domain match, stance tendencies, and conflicts of interest.

## I. Core Principle: Account Holder Identity as the Core of Evaluation

The social platform is the medium, not the content producer. Different accounts on the same platform can have vastly different credibility. When evaluating a social platform source, the core questions are:

```text
Who operates this account?
What is the relationship between this person's identity and the domain of the user's question?
What is the nature of this person's verification?
What are this person's stance and potential conflicts of interest?
```

## II. Account Holder Identity Classification

First, classify social platform account holders into two major categories: **Influential Persons or Interested Parties** (A1 Public Figures / A2 Opinion Leaders / B Institutions) and **Ordinary Individuals**. The former includes persons with broad influence, as well as parties with direct interests in the topic of the user's question (even if their influence is limited).

### 2.1 Influential Persons or Interested Parties

Require more careful scrutiny and deliberation; their statements should not be fully accepted. Interested parties refer to entities with direct利害关系 to the topic of the user's question — even if their social influence is limited, because they are in the middle of the event, their statements have special evidentiary value or bias risk.

#### Class A: Natural Persons — Public Figures

Includes celebrities, famous personalities, politicians, well-known entrepreneurs, industry leaders, etc. who have broad social influence due to their identity or position.

```text
Typical subjects: Entertainers, sports stars, well-known entrepreneurs (e.g., Elon Musk, Lei Jun),
           Politicians (president/prime minister/minister/member of parliament, etc.), heads of international organizations,
           Recognized experts with industry influence
```

##### Evaluation Points

1. **Verification quality**: Does the account have high-quality verification?
2. **Relationship between statement and user question**: Is this public figure a direct party, authoritative spokesperson, or just giving a personal opinion on this topic?
3. **Stance analysis** (see section III)
4. **Conflict of interest detection** (see section IV)

##### Verification Quality Assessment

Not all verifications have the same reference value. Must distinguish:

**High-quality verification** (harder to obtain, has门槛):

```text
Government/institutional official verification (e.g., verified government accounts, institutional email-verified work identity on LinkedIn)
Professional qualification verification (e.g., verified "Doctor," "Lawyer" on platforms requiring professional license review)
Official identity verification (e.g., gray label for government officials on Twitter, institutional gold/gray badges)
Platform invitation-based authoritative identity verification (not open for application)
```

**Low-quality verification** (only requires payment or very low门槛):

```text
X (Twitter) Blue / Premium paid member verification — any paying user can obtain a blue checkmark
Platform "member verification" — pay to get it
Most platforms' "verified" marks that only require a phone number or simple information verification
```

**Correspondence between verification scope and statement domain**:

```text
Verification scope relevant to statement → verification provides some support for the statement
   Example: Finance professional verification + financial statement → has some professional reference value
   Example: Doctor verification + healthcare statement → has some professional reference value

Verification scope unrelated to statement → verification does not provide special support for the statement
   Example: Finance professional verification + healthcare statement → verification provides no additional authority
   Example: Entertainment celebrity verification + tech product technical review → verification provides no additional authority

No verification but past statements show professional background → opinion may still be reasonably considered
   Example: Unverified industry practitioner who has long published professional content in that domain recognized by peers
```

##### Public Figure Usability Assessment

```text
Public figure as a direct party/spokesperson of an event → can be considered a primary source
   Example: A company CEO personally announces a major company decision on social platform
   → citation_usability can reach highly_usable or usable (mark as "direct statement by the party concerned")

Public figure's personal opinion on a non-professional domain → only general reference
   Example: An entertainment celebrity's comment on a political event
   → citation_usability: use_with_caution

Public figure expressing opinion in their own professional domain with matching verification → can be used cautiously
   Example: Licensed attorney (verified) commenting on a legal event
   → citation_usability: usable (requires cross-verification)
```

#### Class A2: Opinion Leaders / KOLs / Influencers / Internet Celebrities [Key Focus]

**Opinion leaders are a category requiring special attention and careful consideration on social platforms.** Unlike Class A public figures, opinion leaders typically gain influence not through their identity or position, but through sustained expression on social platforms, accumulating large followings and gaining significant voice.

```text
Typical subjects: Major influencers on various platforms, famous bloggers,知名 creators, top streamers,
          High-follower-count vertical domain KOLs (tech/finance/beauty/automotive/gaming/education, etc.),
          Operators of self-media top accounts (even if their content is classified as self-media, as individuals they still fall under opinion leader category)
```

##### Core Characteristics of Opinion Leaders

```text
1. Significant follower count (typically 100K+), with strong voice and dissemination power
2. Attract followers through personal opinions, content output, or persona, not institutional identity
3. Have明显的 opinion guidance ability over their follower groups
4. May have multiple monetization methods and commercial partnerships
5. Typically have relatively clear and firm personal stances and preferences
```

##### Special Evaluation Dimensions for Opinion Leaders

Opinion leader evaluation cannot simply apply general standards for public figures; must着重 analyze from the following dimensions:

**(I) Voice and Influence Assessment**

```text
Follower count (tens of thousands / hundreds of thousands / millions / tens of millions)
  → More followers = greater dissemination influence of their statements = stricter evaluation responsibility
  → Note: Followers may include purchased fake followers; assess综合 with engagement rate (likes/comments/shares relative to followers)

Content dissemination power
  → Average engagement per content piece
  → Frequency of content being cited/reshared by other accounts
  → Whether they have agenda-setting ability on specific topics

Audience loyalty
  → Are comments meaningful discussion vs fans spamming likes/controlling comments
  → Level of trust and following by fans
```

**(II) Stance and Preference Identification [Must Highlight]**

Opinion leaders typically have relatively firm personal stances and preferences that may profoundly affect the objectivity and fairness of their statements:

```text
Brand/Product Preference:
  Example: A tech KOL长期 prefers a certain phone brand, consistently贬低 competitor products
  Example: A beauty blogger habitually recommends specific brands, never objectively reviews competitors
  → Must mark brand preference direction

Commercial Collaboration Tendency:
  Example: Long-term partnership with certain companies/brands
  Example: Invests in or holds shares in certain businesses, may be biased on related topics
  → Must mark potential commercial关联

Political/Value Stance:
  Example: Clear stance on national policy, international relations, etc.
  Example: Firm position on specific social issues (environment, feminism, privacy, open source, etc.)
  → Must mark political or value stance leaning

Liking/Disliking of Certain Things/Events:
  Example: A KOL has publicly expressed "faith" or "rejection" of certain technology
  Example: An influencer has personal preferences for certain product types (e.g., "only pushes domestic products," "will never recommend XX brand")
  → Must mark specific like/dislike target

Industry Alignment:
  Example: Clearly on one side in industry controversies
  Example: Long-term attacks on certain business models or technology approaches
  → Must mark industry stance
```

**(III) Commercial Interest and Monetization Detection [Must Carefully Consider]**

Opinion leaders typically depend on social platforms for commercial monetization; commercial motives in their statements must be strictly scrutinized:

```text
Advertising/Sponsorship Relationship:
  - Is the content labeled as advertising or sponsored?
  - Are there long-term brand partners?
  - Are purchase links/discount codes provided when recommending products?
  → If recommendation-type content, default to assuming commercial motive unless clear evidence of purely objective review

Financial Interest:
  - Does the person hold shares or financial interests in the recommended company/brand?
  - Is the person a producer/distributor of the recommended product?
  - Is the person in a competitive relationship with the criticized target?
  → Financial interest has more profound impact than general sponsorship; requires stricter downgrade

Platform Incentives:
  - Is the person driven by platform traffic incentive policies (e.g., jumping on trends, clickbait)?
  - Does the person participate in platform ad sharing or e-commerce sharing programs?
  → Platform incentives may drive opinion leaders to prioritize traffic over accuracy

Monetization Model Analysis:
  - Advertising revenue → tends to produce more attention-grabbing content
  - Affiliate sales/e-commerce → recommended products may not be the best but those with highest commission
  - Knowledge payment → may exaggerate problem severity to boost course sales
  - Fan tips → tends to cater to existing views of the fanbase
  → Different monetization models produce different types of bias
```

**(IV) Opinion Leader Statement Usability Assessment**

```text
Opinion leader as a direct party to an event → can be considered a primary source
  → citation_usability: usable (mark as "opinion leader direct statement")

Opinion leader expressing professional opinion in their深耕 vertical domain:
  → If: verifiable professional background + no commercial interest关联 + cites original sources
    → citation_usability: usable (requires cross-verification)
  → If: lacks verifiable background or has commercial interest关联
    → citation_usability: use_with_caution (note interest relationship)

Opinion leader expressing opinion on non-professional domain:
  → citation_usability: use_with_caution or not_recommended

Opinion leader making statements with明显的 brand preference/commercial bias:
  → Must mark specific bias direction
  → Downgrade citation_usability one level
  → If unlabeled commercial promotion → not_recommended or do_not_use

Opinion leader making inflammatory, emotional, or obviously traffic-driven statements:
  → citation_usability: not_recommended or do_not_use
  → Note in warnings: "Statements have明显的 emotional煽动/traffic-driven characteristics"
```

**(V) Special Handling for Multiple Opinion Leaders Agreeing**

```text
Must be especially vigilant about multiple opinion leaders agreeing on the same topic:

1. Check if these opinion leaders share a common commercial关联 (same MCN, same brand partnership, etc.)
2. Check if the claim originates from the same information source (may just be互相 sharing/citing)
3. Check if publication times are highly concentrated (may be organized marketing campaigns or opinion manipulation)
4. Analyze whether someone spoke first and others followed ("herd effect")

Conclusion:
  - If common commercial关联 or same source exists → not considered multi-party independent verification
  - Even without obvious关联, multiple opinion leaders agreeing should only be regarded as "public opinion倾向," not "fact confirmation"
  - Must trace back to official or authoritative primary sources for final verification
```

##### Opinion Leader Output Marking Requirements

For opinion leader sources, the output must include the following marks:

```text
secondary_tags must include:
  opinion_leader  — identifies the subject as an opinion leader
  + specific bias tags (as applicable):
    - brand_preference_detected (brand preference)
    - commercial_collaboration_detected (commercial collaboration)
    - value_stance_detected (value stance)
    - industry_side_detected (industry alignment)

warnings must include:
  - "This source is an opinion leader with X00K followers, having strong voice and dissemination influence"
  - "This opinion leader has [specific stance/preference/interest] on [related topic/brand/domain]"
  - "Their statements may be influenced by [commercial collaboration/personal preference/platform incentives]"

recommended_action:
  - "Recommend finding independent sources without conflicts of interest for cross-verification"
  - "Recommend confirming whether the statement is advertising/sponsored content"
```

##### Distinguishing Opinion Leaders from Public Figures and Self-Media

```text
Public Figure (A1) vs Opinion Leader (A2):
  Public figure: Influence derived from their identity/position (celebrities, politicians, entrepreneurs)
  Opinion leader: Influence derived from their sustained content output and follower accumulation on social platforms
  The two may overlap (if a celebrity is also an active content creator)

Opinion Leader (A2) vs Self-Media (self_media):
  → From account operation nature: if the account is self-media (commercial monetization + personal IP运营),
     route source type to self_media, evaluate per rules/source_self_media.md
  → From individual identity: if the individual is posting on social platforms (not through their self-media channel)
     and has显著的 opinion leader characteristics, evaluate here as A2 opinion leader
  → Simple判断: see if the specific source URL is their self-media content or their social account post
```

#### Class B: Institution/Organization Accounts

Includes official accounts of companies, government agencies, non-profit organizations, schools, media organizations, etc. on social platforms. Institutional accounts are typically interested parties — their statements on their own affairs have primary evidence value, but may also have self-serving motives on issues involving their own interests.

##### B-1: Company/Enterprise Official Accounts

```text
For confirming official information (e.g., product releases, announcements, responses) → high usability
For discussing industry trends → note their commercial stance and potential self-serving motives
```

##### B-2: Government/Regulatory Official Accounts

```text
For confirming policies, regulations, official statements → high usability
Note: Even official accounts, political statements still need political stance analysis
```

##### B-3: Authoritative Media Organization Accounts on Social Platforms

**This is a sub-type requiring special handling.** When authoritative media (such as Reuters, BBC, NYT, etc.) publish content on social platforms, handle differently based on whether they cite their own media sources:

```text
Case 1: The post/tweet cites the media's own full report (with link)
  → The social platform content is consistent with the media's own source
  → Reference rules/source_news.md evaluation rules for that media
  → The social platform post is merely an "entry point" to the media report
  → citation_usability consistent with the original report

Case 2: The post/tweet does not cite the media's own report; independently edited content
  → Treat it as the media account operating similarly to self-media
  → Lacks full editorial review process (fast-paced social platform publishing, review standards lower than formal reporting)
  → Evaluate per rules/source_self_media.md rules
  → Default citation_usability no higher than use_with_caution
  → Must add secondary_tags: ["social_media_standalone_post"]

Case 3: The post/tweet cites/shares other sources (not its own)
  → Should trace back to the original source
  → The post itself serves only as a dissemination node, with no independent evidentiary value
```

##### B-4: Personal Accounts of Key Institutional Figures

Includes personal or work accounts of company executives, government officials, institutional spokespersons, etc. on social platforms.

```text
These key figures typically have high-quality verification (harder to obtain, has门槛)

Usable scenarios:
  - As informal statements or supplementary information from the institution
  - Understanding the institution's stance direction or internal perspective
  - Direct confirmation or denial of an event by the party concerned

Notes:
  - Personal account statements do not equal official institutional stance (unless explicitly speaking in institutional capacity)
  - Even key figures may include personal biases in their personal accounts
  - Should mark as "personal statement by key institutional figure"
  - Default citation_usability no higher than usable
  - If multiple key figures agree → credibility can be appropriately raised but still needs official confirmation
```

##### B-5: Unknown Employee Accounts

Some employees may not be verified, but their past statements show they work in relevant industries with professional backgrounds.

```text
Identification signals:
  - Account bio mentions company/institution
  - Historical content围绕 specific industry
  - Has posted verifiable professional information (internal screenshots should be treated cautiously)
  - Interacted with or recognized by colleagues or peers

Evaluation points:
  - Is the employee's statement within their normal job scope?
    → If within scope (e.g., engineer discussing company technology) → has some reference value
    → If clearly beyond scope (e.g., junior employee discussing company strategy) → lower reference value
  - Does it involve internal confidential or non-public information?
    → If yes → treat cautiously; may violate confidentiality agreements, and cannot be verified
  - Default citation_usability no higher than use_with_caution
```

### 2.2 Ordinary Individuals

General personal social accounts with no significant influence, no professional verification, and no institutional affiliation.

```text
Evaluation principles:
  - Generally serve as reference opinions; not suitable as key evidence
  - Can be used to understand public reactions, user experiences, grassroots opinions
  - Multiple ordinary users saying the same thing may reflect某种 opinion倾向, but cannot be considered fact confirmation

Usable scenarios:
  - Product/service user experience cases
  - Public opinion analysis, public reaction research
  -线索 discovery (requires further verification)

Cannot serve as:
  - Sole source for fact confirmation
  - Basis for scientific/medical/legal conclusions
  - Substitute for company/institutional official positions

Default citation_usability: use_with_caution or not_recommended
```

## III. Stance Tendency Analysis

Active public figures and institutions on social platforms typically have relatively firm stance tendencies. These stances may significantly affect the objectivity of their statements and are factors that must be considered during evaluation.

### 3.1 Types of Stances to Identify

```text
Political stance:
  Example: Political figures' partisan stance, support/opposition to national policies
  Example: National stance倾向 on international relations topics
  → Mark political_leaning

Commercial stance:
  Example: An investor/entrepreneur's preference or排斥 toward certain industries
  Example: A company executive's evaluation of competitors
  → Mark commercial_leaning

Preference/Value stance:
  Example: Preference for specific technical approaches (e.g., an AI researcher strongly advocating for certain architecture)
  Example: Specific stance on social issues (environment, privacy, open source, etc.)
  → Mark preference_leaning
```

### 3.2 Stance Analysis Process

```text
1. Identify the account's historical statements on topics related to the user's question
2. Determine if the stance is publicly firm or vague and changeable
3. Evaluate whether this stance affects the objectivity of their current statement:
   - Direct interested party → high bias risk
   - Long-term public alignment with某方 → medium bias risk
   - No明显 historical stance → low bias risk (still need to关注 other signals)
4. Output stance标签 and impact assessment in the report
```

### 3.3 Output Recommendations

```text
For sources with clear stances, add stance标签 in secondary_tags:
  political_bias_detected
  commercial_bias_detected
  preference_bias_detected

Note in warnings:
  "This account has a clear [political/commercial/preference] stance on this topic, which may affect statement objectivity"
```

## IV. Conflict of Interest and Advertising Suspicion Detection

Statements by influential public figures and institutions on social platforms may contain hidden commercial interests. Should reference the relevant practices in self-media rules (`rules/source_self_media.md`) for detection.

### 4.1 Detection Signals

```text
Clear advertising/sponsorship signals:
  - Post labeled #ad #sponsored #partnership or similar tags
  - Explicit mention of brand/product with purchase link/discount code
  - Content is product promotion and style明显 different from other content

Suspected advertising/promotion signals:
  - Consistent positive reviews of certain product/brand/company, never mentioning flaws
  - Abnormal posting frequency, concentrated promotion in specific periods
  - Frequent互动 with commercial partners, mutual promotion
  - Content偏离 from the account's usual topic domain, unusually recommending specific products
  - Marketing language ("personally tested and effective," "must buy," "strongly recommend" — claims without objective support)

Interest-associated signals (not advertising but interest relationship):
  - Discussion target is a company in which the account holder has invested/holds shares
  - Discussion target is the account holder's own company or direct competitor
  - Discussion target is the account holder's partner or commercial关联 party
  - Account holder has direct financial利害关系 in the related topic
```

### 4.2 Handling

```text
Confirmed advertising/sponsorship but not labeled → serious issue
  → secondary_tags: ["undisclosed_advertisement"]
  → citation_usability: not_recommended or do_not_use
  → warnings add: "Content appears to be unlabeled commercial promotion; objectivity questionable"

Clearly labeled advertising/sponsorship → transparency acceptable but credibility limited
  → secondary_tags: ["disclosed_advertisement"]
  → citation_usability: use_with_caution (mark as "declared sponsored content")

Interest relationship exists but not direct advertising → must mark
  → secondary_tags: ["potential_conflict_of_interest"]
  → Downgrade citation_usability one level
  → warnings add: "Account holder has potential conflict of interest with this topic"

No obvious interest relationship → does not affect scoring
```

### 4.3 Interest Relationship Severity Assessment

Not all interest relationships severely affect credibility. Need to assess the **directness** and **impact strength** of the interest relationship:

```text
Core interest relationship (severely affects objectivity):
  Example: A CEO evaluating their own company's product
  Example: An investor evaluating a company in their portfolio
  → Default treat as stance statement, not objective analysis

Indirect interest relationship (may affect but not decisive):
  Example: An industry practitioner evaluating peers
  Example: A company employee evaluating industry trends in their sector
  → Must note but not完全否定

No interest relationship:
  Example: Consumer evaluating a product with no commercial关联 to them
  → Normal evaluation
```

## V. Social Platform Source Usability Overview

### Situations Where It Can Be Used More Strongly

```text
Account belongs to original company/government agency/project team → add tag official_social
Account belongs to event party/direct spokesperson → add tag primary_source
Account with high-quality verification and statements within professional domain
Authoritative media account citing its own media's full report (with link)
Post contains original documents, announcements, code, images, or videos that are verifiable
Post links to official source and content is consistent
Clear publication time,完整 context
```

Such sources can be marked as:

```text
social_media + official_social (or other corresponding secondary tags)
citation_usability: highly_usable or usable
```

### Situations Requiring Caution

```text
Influential public figure's statements outside their professional domain
High-quality verification but does not match the domain of the statement
Low-quality verification (paid verification)
Personal account statements of key institutional figures (non-official channel)
Unknown employee but historical content shows industry background
Unverified but verifiable professional background account
Authoritative media account's independent social platform content not citing its own report
```

```text
Default citation_usability no higher than use_with_caution
Must assess综合 with stance analysis and conflict of interest detection
```

### Situations Not Recommended as Final Evidence

```text
Anonymous accounts
Unverified and untraceable background accounts
Ordinary individual's single statement on professional domain topic
Screenshots (see Section VI screenshot handling)
Reposts/redistributions (should trace back to original source)
Rumor chains/comment section content
No timestamp/no context/no original link
Only expresses personal speculation or emotion
Contains unlabeled commercial promotions
Clearly undeclared conflicts of interest
```

## VI. Self-Media Identification and Routing

Self-media refers to accounts operated by individuals or small teams as independent creators on social/content platforms, typically relying on platform traffic sharing, advertising, affiliate sales, or knowledge payment for monetization. The core difference from traditional media and official accounts: lacks institutional editorial review mechanisms; content quality depends entirely on individual ability and motivation.

### Self-Media Identification Signals

When most of the following signals are present, classify as self-media:

```text
Account name has personal IP characteristics (e.g., "XX says," "XX observes," "XX diary," "XX teacher," "XX bro/sis")
Account bio emphasizes personal identity rather than institutional affiliation (e.g., "former XX company employee," "independent researcher")
Content primarily consists of opinions, commentary, interpretation, rather than first-hand news reporting or official announcements
Homepage or content includes commercial promotions, affiliate sales links, course promotions, paid community引流
Content更新 frequency is extremely high (multiple posts daily), titles追求 click-through rates
Account has not passed institutional verification; only personal verification or unverified
Profile picture is a personal photo or cartoon image, not an institutional logo
Content style is personalized; frequent use of "I," "I think," "I believe"
Comment section has大量 fan互动 rather than factual discussion
Cross-platform same-name account matrix operations
```

### Routing Rules

If identified as self-media, **immediately terminate** current `source_social.md` rule processing, reclassify the source as `self_media` main type, and switch to `rules/source_self_media.md`:

```text
source_type: social_media  →  Determined as self-media  →  STOP source_social.md
                                                         →  source_type = self_media
                                                         →  Load rules/source_self_media.md
```

Self-media sources default no higher than `use_with_caution`.

### Distinguishing Self-Media from Official Accounts / Influential Persons and Interested Parties

```text
Verified institutional account → official_social → process per Class B institutional account rules
Verified individual expert (e.g., real-name verified scholar, doctor, lawyer with institutional backing) → process per Class A1 influential person rules
Influential public figures (celebrities/celebrities/politicians) → process per Class A1 influential person rules
Opinion leaders / KOLs / influencers (high follower count, strong voice content creators) → process per Class A2 opinion leader rules
Unverified/personal verification + personal IP operations + commercial monetization → self_media → load source_self_media.md
```

## VII. Screenshot Handling

Screenshots default to low credibility; should check:

```text
Whether the original post link can be found
Whether the screenshot is完整
Whether the account is real
Whether the timestamp is clear
Whether it may have been edited
Whether any other source corroborates
```

If the original post cannot be found, mark:

```text
citation_usability: not_recommended
article_quality_score: < 30
```

## VIII. Output Recommendations

### 8.1 Full Output Format

```json
{
  "source_type": "social_media",
  "account_holder": {
    "category": "public_figure | opinion_leader | institution | employee | general_public",
    "sub_category": "celebrity | politician | executive | industry_expert | kol_vertical | kol_general | influencer | live_streamer | corporate_official | government_account | media_organization | key_personnel | unknown_employee | ordinary_user | ...",
    "identity_verifiable": true,
    "verification_quality": "high_quality | low_quality | unverified",
    "verification_relevance_to_claim": "matched | unrelated | partial",
    "follower_count_tier": "mega | macro | mid | micro | nano | unknown",
    "professional_domain": "technology | finance | healthcare | law | entertainment | politics | general | unknown"
  },
  "post_type": "original_post | repost | screenshot | comment",
  "is_official_account": false,
  "stance_analysis": {
    "political_leaning_detected": false,
    "commercial_leaning_detected": false,
    "preference_leaning_detected": false,
    "brand_preference_detected": false,
    "commercial_collaboration_detected": false,
    "value_stance_detected": false,
    "industry_side_detected": false,
    "stance_note": "This account has a clear commercial stance on this topic, which may affect statement objectivity"
  },
  "conflict_of_interest": {
    "detected": false,
    "type": "advertisement | sponsorship | financial_interest | undisclosed_ad | none",
    "severity": "high | medium | low | none",
    "note": "Account holder has an investment relationship with the discussed target"
  },
  "citation_usability": "highly_usable | usable | use_with_caution | not_recommended | do_not_use",
  "reasons": [
    "This source is a verified account of the CEO of the company in question, constituting a primary statement",
    "Account has high-quality institutional verification matching the domain of the statement",
    "Content is personal opinion, not an official statement"
  ],
  "warnings": [
    "Social platform source; not suitable as sole evidence",
    "Account holder has a clear commercial stance on this topic",
    "Suspected unlabeled commercial promotion"
  ],
  "recommended_action": "cross_check_with_official_source"
}
```

### 8.2 Concise Output Format (General User Scenario)

When the source is an ordinary individual or simple social platform content, use a精简 format:

```json
{
  "source_type": "social_media",
  "is_official_account": false,
  "post_type": "original_post | repost | screenshot | comment",
  "citation_usability": "use_with_caution",
  "warnings": ["Social platform source; not suitable as final evidence"]
}
```

### 8.3 Field Descriptions

| Field | Description |
|-------|-------------|
| `account_holder.category` | Account holder main category: `public_figure` (A1 public figure), `opinion_leader` (A2 opinion leader/KOL/influencer), `institution` (B institution), `employee` (employee), `general_public` (ordinary individual) |
| `account_holder.sub_category` | Account holder subcategory |
| `account_holder.identity_verifiable` | Whether identity can be independently verified (not just relying on platform verification) |
| `account_holder.verification_quality` | `high_quality` (high-barrier verification), `low_quality` (low-barrier/paid verification), `unverified` (not verified) |
| `account_holder.verification_relevance_to_claim` | Match between verification scope and current statement domain |
| `account_holder.follower_count_tier` | Follower count level: `mega` (million+), `macro` (hundreds of thousands), `mid` (tens of thousands), `micro` (thousands), `nano` (hundreds or below) |
| `account_holder.professional_domain` | Verifiable professional domain |
| `stance_analysis` | Stance tendency analysis result |
| `conflict_of_interest` | Conflict of interest detection result |

If determined to be self-media, terminate this rule, change `source_type` to `self_media`, and use the output format from `source_self_media.md`.
