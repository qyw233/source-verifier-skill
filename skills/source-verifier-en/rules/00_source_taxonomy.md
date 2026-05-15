
> **Must read SKILL.md before reading this file to understand the full task context.**

# Information Source Classification Rules

This file is used to determine which type a source belongs to. Each source must have one main type, and can have multiple secondary tags added.

## Main Types

### 1. official: Official Sources

Sources from the originating organization, company, government agency, project team, standards body, author, or product maintainer.

The core question for determining official is not "what type of entity is this," but **"who is the original publisher/maintainer of the information the user is looking up?"** As long as the entity itself is the original producer of the information and the user is visiting a page directly published by that entity, it is official.

Examples:

- Company official website announcement
- Government website
- Official documentation
- Official GitHub repository
- Official release notes
- Hugging Face official model page
- Standards body documents
- Original instructions published by project maintainers
- Benchmark project official website (e.g., a benchmark project's official site — for that benchmark score, it is official)
- Independent research institution's official data platform (e.g., Epoch AI's official benchmark database — for AI capability data, it is official)

Default trust level: A

Note: official only means "the data has an official original publisher and is traceable," not that the data conclusion itself is correct. Benchmarks may have methodological flaws or data contamination; vendor self-assessments may involve selective evaluation. official answers "where the information came from," not "whether the information is valid."

---

### 2. academic: Academic Sources

Papers, preprints, academic databases, university pages, publisher pages, or DOI landing pages.

Examples:

- arXiv
- IEEE
- ACM
- Springer
- Elsevier
- Nature / Science / Cell series
- University institutional repositories
- DOI landing page

Default trust level: A or B

Distinctions to make:

- Peer-reviewed papers: Stronger
- Preprints: Valuable, but may not have undergone peer review
- Conference posters, PPTs, lab blogs: Lower evidence strength

---

### 3. news: News Media

News agencies, tech media, financial media, professional reporting platforms.

Examples:

- Reuters
- AP
- BBC
- The Verge
- TechCrunch

Default trust level: B or C, depending on media reputation, article quality, and whether original sources are linked.

---

### 4. professional_analysis: Professional Analysis Sources

Professional institutions, industry reports, think tanks, consulting firms, technical team blogs, etc.

Examples:

- Gartner
- McKinsey
- Forrester
- Research institution reports
- Corporate engineering blogs
- Professional technical analysis articles

Default trust level: B or C.

---

### 5. blog_forum: Blogs, Forums, and Communities

Personal blogs, Q&A websites, tech communities, forum posts, user experience sharing.

Examples:

- Medium
- Reddit
- Stack Overflow
- Personal websites
- Forum posts

Default trust level: C or D.

Suitable as clues, experience references, and troubleshooting references; not suitable for directly supporting high-risk factual conclusions.

---

### 6. social_media: Social Platforms

Short posts, account updates, comments, screenshots, reposts, etc. The evidence strength of social platform sources is highly dependent on the identity of the account holder. Each account must be evaluated individually for its identity, verification quality, professional domain match, stance tendencies, and conflicts of interest.

Examples:

- X / Twitter
- LinkedIn posts
- YouTube comments
- Bilibili comments
- Telegram screenshots
- Xiaohongshu posts

Default trust level: D (ordinary users), but can be raised based on the account holder's identity.

Exception: If the account is a verified account of the original person, company, government agency, or project maintainer, add the secondary tag `official_social`.

Note: If determined to be self-media (personal IP运营 with commercial monetization behavior, content primarily based on personal opinions), reclassify as `self_media`, stop `source_social.md` rules, and switch to `source_self_media.md`.

Detailed evaluation rules in `rules/source_social.md`.

---

### 7. self_media: Self-Media

Accounts operated by individuals or small teams as independent creators on social/content platforms. The distinction from ordinary social platform users: clear personal IP attributes, continuous content output, and typically reliance on traffic or commercial monetization.

Identification features:

- Account name has personal IP characteristics (e.g., "XX says," "XX observes," "XX teacher," "XX bro/sis")
- Continuous content output as an individual, not occasional personal sharing
- Commercial monetization behavior (affiliate sales, courses, sponsorships, traffic sharing)
- Content primarily consisting of opinions, commentary, experience, tutorials
- Lack of institutional editorial review mechanism

Default trust level: D or E, depending on author qualifications and content quality.

Specific evaluation rules in `rules/source_self_media.md`.

---

### 8. aggregator_or_scraper: Aggregator or Scraper Sites

Republishing, scraping, mirror, SEO content farms, pages with no original information.

Default trust level: D.

Specific situation depends on the reliability of the original source and whether the original source is correctly cited.

---

### 9. suspicious: Suspicious Sources

Sources with serious reliability risks.

Typical signals:

- No author
- No date
- No institutional information
- Content appears copied
- Clickbait title
- Domain伪装成 official
- Heavy advertising and redirects
- No outbound citations
- Exaggerated, inflammatory, or marketing language
- Suspected AI-generated spam content

Default trust level: E.

## Secondary Tags

Can be added as needed:

```text
primary_source              Original source
secondary_report            Secondary report
opinion                     Commentary or opinion
sponsored                   Sponsored content
press_release               Press release
preprint                    Preprint
peer_reviewed               Peer-reviewed
outdated                    Possibly outdated
no_author                   No author
no_date                     No date
cites_original              Cites original source
does_not_cite_original      Does not cite original source
possible_scraper            Possible scraper site
  official_social              Official social account
  social_media_standalone_post Authoritative media independently published content on social platforms (not citing own reporting)
  undisclosed_advertisement    Undisclosed commercial promotion
  disclosed_advertisement      Disclosed commercial promotion/sponsorship
  potential_conflict_of_interest Potential conflict of interest
  political_bias_detected      Political stance bias
  commercial_bias_detected     Commercial stance bias
  preference_bias_detected     Preference/value stance bias
  brand_preference_detected    Brand preference (opinion leader)
  commercial_collaboration_detected Commercial collaboration (opinion leader)
  value_stance_detected        Value stance (opinion leader)
  industry_side_detected       Industry stance (opinion leader)
  opinion_leader               Opinion leader/KOL/influencer
  controversial_topic          Controversial topic
  high_stakes                  High-risk topic
  cross_language_report        Cross-language report (non-origin language source)
  echo_chamber_risk            Echo chamber risk (repetition within a single language ecosystem, no origin language primary source)
  origin_language_primary      Origin language primary source (cited original language official/authoritative source)
```

Other tags can be defined as needed.

## Classification Priority

If a source matches multiple categories, prioritize the category that best represents its evidentiary nature:

```text
Official original > Regulation/Standard/Paper > Original data/Code > News report > Professional analysis > Blog/Forum > Social platform (official account) > Self-media > Social platform (ordinary user) > Scraper site/Suspicious site
```

Examples:

- Blog article published on company official website: `official`, with optional `press_release` or `marketing` tag.
- Verified X account of company founder making announcement: `social_media` + `official_social`.
- Personal blogger consistently posting beauty reviews and affiliate sales on Weibo/Xiaohongshu: `self_media`.
- News media republishing company press release: `news` + `press_release` + `secondary_report`.
- Original project release on GitHub: `official` + `primary_source`.
