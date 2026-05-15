> **Must read SKILL.md before reading this file to understand the full task context.**

# E-Commerce Platform Source Processing Rules

E-commerce platform sources include marketplace platforms, brand flagship stores, third-party merchant storefronts, product detail pages, user reviews, rankings, live commerce pages, discount pages, and price comparison pages. The core characteristic of this source type is that pages usually serve transaction conversion and have inherent commercial motivation, so a source should not be treated as reliable factual evidence merely because the platform is well-known or the sales volume is high.

**This rule is an overlay rule.** The current schema does not include an independent `commerce` source type, so do not output `source_type: commerce`. Choose the closest main source type based on the evidentiary nature of the page, and add secondary tags:

```text
Official brand flagship store / brand-operated page → source_type: official, add secondary_tags official_store, commercial_page
Third-party merchant product page → source_type: professional_analysis or unknown, add secondary_tags merchant_page, commercial_page
Platform ranking / recommendation / price comparison page → source_type: aggregator_or_scraper or professional_analysis, add secondary_tags ranking_page, commercial_page
User reviews / Q&A section → source_type: blog_forum, add secondary_tags user_reviews, commerce_platform
Live commerce / influencer recommendation page → source_type: self_media or social_media, continue with the corresponding rules
Counterfeit storefront, inducement redirects, abnormal low-price page → source_type: suspicious
```

## I. First Determine the Page Role

When evaluating an e-commerce platform source, first determine what role the page plays. Different roles have different evidentiary value:

```text
Platform itself: platform rules, transaction status, logistics, sales volume, ratings, recommendation ranking
Brand official store: the brand's commercial statement about product name, specifications, price, and sale status
Third-party merchant: that merchant's statement about product, inventory, price, and after-sales commitments
User reviews: a collection of individual consumer experiences
Platform rankings/recommendations: platform algorithm or commercial operation results
Commerce promotion content: marketing content or commercial promotion
```

## II. What Conclusions It Can Support

### Can Strongly Support

E-commerce platform pages can strongly support facts directly related to the transaction page itself:

```text
Whether a product is currently listed on that platform
The price, specifications, bundle, and inventory status shown on the page
The merchant's or store's description of the product
The sales volume, rating, and review count displayed by the platform
Whether a specific store exists on that platform
Whether some users expressed a certain experience in reviews
```

When using such information, explicitly state that these conclusions only represent **what the page or platform displays**. They do not automatically equal real product quality, all-channel sales, official facts, or long-term status.

### Can Only Cautiously Support

```text
Product quality
Real user satisfaction
Ranking among comparable products
Value-for-money conclusions
Long-term price trends
Whether out-of-stock, discontinuation, or price increases are representative across all channels
```

These conclusions require cross-checking with neutral reviews, brand official information, regulatory materials, third-party testing, price history tools, or multi-platform data.

### Cannot Independently Support

```text
Medical efficacy, treatment effects, health claims
Financial returns, investment gains, guaranteed profit claims
Absolute safety guarantees
Whether a product has official certification or regulatory approval
Actual brand market share
Ranking claims such as best-selling across the whole web or industry No. 1
Major quality issues or illegal conduct
```

## III. Brand Official Stores and Third-Party Merchants

### 3.1 Brand Official Stores

If the page clearly belongs to a brand official flagship store, brand-operated store, or platform-certified official store, it can serve as the brand's commercial statement on that platform.

```text
Can confirm: product name, specifications, official bundles, sale status, platform price, after-sales information
Cannot directly confirm: product effect superiority over competitors, real sales volume, user satisfaction, medical/legal/financial effects
```

Must check:

```text
Whether the store has platform official certification
Whether the store name matches the brand entity
Whether there is risk that an "authorized store," "specialty store," or "franchise store" is pretending to be an official flagship store
Whether the page is an advertising landing page or campaign page
Whether the product description contains exaggerated claims
```

If confirmed as an official store:

```text
source_type: official
secondary_tags: ["official_store", "commercial_page"]
citation_usability: usable or use_with_caution
```

Even for official stores, warnings should note: "This page has a commercial sales purpose; claims involving effects, superiority, rankings, or similar assertions require independent verification."

### 3.2 Third-Party Merchant Pages

Third-party merchant pages only represent that merchant's sales claims, and their evidence strength is lower than brand official sources.

```text
Default citation_usability: use_with_caution or not_recommended
source_reliability_score usually should not exceed 65
article_quality_score depends on page information completeness, qualification disclosure, and verifiability
```

Negative signals:

```text
Store entity is unclear
Product brand or authorization relationship is unclear
Title stacks keywords or uses exaggerated marketing language
Price is abnormally below market level
Images or detail page appear copied
Promises absolute effects or exaggerated guarantees
After-sales policy, qualifications, or test reports cannot be verified
```

If counterfeit goods, impersonation, inducement redirects, fake orders, or abnormally low prices are involved, reclassify as `suspicious`.

## IV. User Reviews and Q&A Sections

User reviews are a collection of individual experiences, not verified facts.

### Can Be Referenced

```text
Subjective user experiences
Clues about common issues
Clues about after-sales problems
Packaging, logistics, installation, and usage scenario feedback
```

### Cannot Serve As

```text
Proof of actual product efficacy
High-risk conclusions in medicine, law, finance, etc.
Statistically meaningful satisfaction conclusions
The sole basis for judging whether a product is compliant or safe
```

Must check for fake-review and abnormal-review signals:

```text
Large number of reviews concentrated in time
Highly similar review wording
Repeated images or videos
Large number of short reviews without details
Template-like follow-up reviews
Merchant replies to negative reviews without substantive response
Review area contains traffic diversion, cash-back incentives, or rewards for positive reviews
```

Handling:

```text
Ordinary review collection → citation_usability: use_with_caution, mark as user_experience
Suspected fake reviews → add secondary_tags: suspected_review_manipulation, citation_usability: not_recommended
Reviews conflict with official/testing/regulatory sources → defer to sources with higher evidence strength
```

## V. Platform Rankings, Recommendations, and Sales Volume

Platform rankings, recommendation slots, hot-sale lists, and search ranking usually mix sales volume, advertising, conversion rate, inventory, user profiling, and commercial placement. Do not directly equate them with objective rankings.

```text
Can state: the platform displayed a certain ranking or label at a certain time
Cannot state: the product is objectively No. 1, industry-leading, or most popular across the whole web
```

Must check:

```text
Whether ranking methodology is public
Whether advertising, sponsorship, or promotion is labeled
Whether it is personalized recommendation
Whether there is a time range
Whether it only covers platform-internal data
Whether raw data can be exported or reviewed
```

If the ranking lacks methodology:

```text
citation_usability: not_recommended
recommended_action: seek_independent_market_data
```

## VI. Price, Inventory, and Timeliness

E-commerce platform information is highly dynamic; prices, inventory, campaigns, coupons, and sales volume can change at any time.

```text
Must record access time or screenshot time
freshness requires a very high standard by default
Price and inventory information has high outdatedness risk
After a promotion ends, the page no longer supports historical price judgments unless a reliable archive exists
```

Freshness guidance:

```text
Same-day or real-time page → fresh
Price/inventory/promotion information older than 7 days → possibly_outdated
Price/inventory/promotion information older than 30 days → outdated
No access time or page time → freshness: unknown
```

## VII. Advertising, Commerce Promotion, and Interest Relationships

E-commerce pages usually have commercial purpose, but still distinguish public sales pages, platform ads, influencer commerce, and undisclosed promotion.

High-risk signals:

```text
"Must buy," "buy without thinking," "lowest price across the whole web," "No. 1" and similar unsupported language
Strong guidance to place orders, join private traffic channels, claim coupons, or receive cash-back
Merchant guidance appears in reviews or Q&A
Influencer content does not disclose commission, collaboration, or sponsorship
The page mainly consists of marketing language and lacks verifiable specifications
```

Handling:

```text
Clearly labeled advertising/sponsorship → add disclosed_advertisement, citation_usability: use_with_caution
Suspected undisclosed advertising → add undisclosed_advertisement, citation_usability: not_recommended or do_not_use
Influencer commerce content → switch to source_self_media.md or source_social.md for continued evaluation
```

## VIII. Special Rules for High-Risk Categories

### Healthcare, Supplements, Drugs, and Medical Devices

```text
Shopping pages cannot prove treatment effects or medical safety
Prioritize regulatory approval, instructions for use, clinical guidelines, papers, or official drug/device regulator information
User reviews cannot serve as efficacy evidence
Exaggerated efficacy claims or suggestions to replace treatment → citation_usability: do_not_use
```

### Finance, Insurance, and Investment Courses

```text
Product pages or course pages cannot prove profit capability
Must check qualifications, regulatory licenses, risk disclosures, and interest relationships
Promises of return, guaranteed profit, capital protection, or high returns → citation_usability: do_not_use
```

### Children's Products, Food, Cosmetics, and Safety Equipment

```text
Product pages can only show merchant statements
Safety, compliance, and certification status require regulator, testing report, or certification body originals
```

## IX. Output Recommendations

```json
{
  "source_type": "official | professional_analysis | blog_forum | self_media | social_media | aggregator_or_scraper | suspicious | unknown",
  "secondary_tags": [
    "commerce_platform",
    "commercial_page",
    "official_store",
    "merchant_page",
    "user_reviews",
    "ranking_page",
    "suspected_review_manipulation"
  ],
  "citation_usability": "usable | use_with_caution | not_recommended | do_not_use",
  "warnings": [
    "This page has a commercial sales purpose",
    "Price, inventory, and sales-volume information strongly depends on access time",
    "User reviews can only serve as experience clues, not high-risk factual evidence"
  ],
  "recommended_action": "cross_check_with_official_or_independent_sources"
}
```

