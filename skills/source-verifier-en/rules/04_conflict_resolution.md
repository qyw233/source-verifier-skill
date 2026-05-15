
> **Must read SKILL.md before reading this file to understand the full task context.**

# Multi-Source Conflict Resolution Rules

When different sources disagree, resolve by evidence strength, not by counting votes.

## I. Evidence Priority

Typically prioritize in the following order:

```text
1. Official primary source
2. Regulation, regulatory, court, standard原文
3. Peer-reviewed paper or formal technical report
4. Original data, code repository, release notes, model card
5. Named reporting by high-reputation news organization
6. Professional institution analysis
7. Ordinary blog, tech community
8. Social platform
9. Aggregator, republishing site, scraper site, suspicious site
```

## II. Conflict Resolution Rules

### Official Source vs. News Report

If an official source conflicts with a news report, the official source usually takes precedence. News reports can serve as supplementary background.

### New Source vs. Old Source

If a new version of official documentation conflicts with an old version, prioritize the new version.

### Multiple Secondary Sources Repeating the Same Claim

Multiple secondary sources repeating the same statement does not equal independent verification. If none of them have an original source, mark as evidence insufficient. For Chinese self-media and general non-authoritative media sources, this rule must be enforced even when there are many sources. See `source_self_media.md` for details on "Multiple self-media repetitions ≠ multi-party verification."

### Cross-Language Echo Chamber Detection

When multiple sources corroborate each other, check for the presence of an echo chamber:

```text
1. Is the topic's information origin in a different language (e.g., topic is English-origin, but all current sources are Chinese)
2. Are all these sources from the same language ecosystem
3. Does any source cite a primary source in the origin language

If conditions 1+2 are met and condition 3 is not:
  → Mark echo_chamber_detected = true
  → Do not consider as multi-party independent verification
  → Mark conflict status as evidence_insufficient
  → Must note: "Only repeated within a single language ecosystem; no origin language primary source found"
```

This detection depends on the topic origin language determination from `rules/05_cross_region_verification.md`.

### Academic Source Conflict

If paper conclusions conflict, distinguish between:

```text
Experimental conditions
Sample size
Whether peer-reviewed
Whether replicated
Whether a review or single study
```

### Legal/Policy Conflict

Must prioritize official effective texts; check:

```text
Jurisdiction
Effective date
Revision status
Whether just a draft,征求意见稿, or media interpretation
```

## III. Output Labels

```text
resolved_by_primary_source
resolved_by_newer_source
conflicting_evidence
evidence_insufficient
secondary_sources_only
```

## IV. Recommended Output

```json
{
  "conflict_status": "conflicting_evidence",
  "summary": "Official documentation has not stated that the feature is available, but multiple media report it is being tested.",
  "preferred_source": "official documentation",
  "final_note": "Currently, it can only be confirmed that the feature is in testing or reported stage; cannot confirm full availability."
}
```
