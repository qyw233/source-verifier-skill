
> **Must read SKILL.md before reading this file to understand the full task context.**

# Timeliness Assessment Rules

Certain information changes rapidly, so whether a source is "new" directly affects reliability.

## I. Topics That Require Attention to Timeliness

The following topics should prioritize the latest sources:

```text
News events
Political figures and positions
Company CEO, product status, pricing, features
AI models, APIs, open source status, licenses
Software versions, dependencies, system requirements
Laws, regulations, policies, regulatory rules
Medical guidelines, drug information, safety warnings
Financial prices, exchange rates, stocks, funds
Sports scores, schedules, rankings
Travel visas, flights, attraction opening status
```

## II. Timeliness Levels

### fresh

The source's publication time is suitable for the current question, with no obvious risk of being outdated.

### possibly_outdated

The source may be outdated; need to seek newer sources for confirmation.

### outdated

The source is clearly outdated and should not be used as final evidence for current facts.

### timeless

Basic concepts, mathematical formulas, historical facts, classic papers, etc., typically do not require the latest sources, but version differences should still be noted.

## III. Rough Guidelines by Domain

```text
AI / Software features: Prioritize sources within 30–90 days; official documentation based on current version.
News events: Prioritize sources from the last few days to weeks.
Policies and regulations: Prioritize currently effective texts; check effective dates and revision dates.
Medical advice: Prioritize recent guidelines, systematic reviews, regulatory agency updates.
Academic foundational theory: Classic sources are usable, but前沿 conclusions require recent literature.
```

## IV. Processing Rules

1. If a source has no date, add a `no_date` warning.
2. If the source date is earlier than known key change points, evaluate whether its conclusions are still valid.
3. If a newer version of official documentation exists, prioritize the updated version.
4. For questions about "latest," "recent," "currently supported," must find current sources.
5. If only old sources are available, output "uncertain" or "may be outdated."

## V. Output Field Recommendations

```json
{
  "freshness": "fresh | possibly_outdated | outdated | timeless",
  "published_at": "2026-04-12",
  "updated_at": "2026-04-20",
  "freshness_note": "This source is an official release note, published very recently."
}
```
