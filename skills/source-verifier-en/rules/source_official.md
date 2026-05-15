
> **Must read SKILL.md before reading this file to understand the full task context.**

# Official Source Processing Rules

Official sources are generally more reliable, but their information timeliness and specific context still need to be checked.

## Strong Official Sources

```text
Company official website
Government agency notice
Official documentation
Official API reference
Official GitHub repository
Release notes
Changelog
Standards body documents
Official model card
Official license file
```
## Possible Weak Official Sources

```text
Official blog (may contain marketing content)
Official social media account (may have promotional nature)
Official forum (may contain user-generated content)
```

## Check Steps

1. Confirm that the domain or account确实 belongs to the original organization, not a counterfeit phishing site or secondary republishing. Use tools to check SSL certificates, WHOIS information, social media verification, etc.
2. **Confirm whether the page content is published by the official team or submitted by platform users.** The domain belonging to an official organization does not mean the page content has official authority — many companies/institutions operate open-submission developer communities, blog platforms, or forums where users can自行 publish content. Must check:
   - Author identity: Is it signed by an official team member or a user nickname/anonymous? Does the author栏 have identifiers such as "Official Team," "Platform Administrator"?
   - URL path: Is it an official maintenance path like /docs/, /api/, /release-notes/, or an open submission path like /article/, /blog/, /community/, /user/?
   - Publication mechanism: Does the page have disclaimers such as "submission," "author's personal views, not representing the platform," "user publication," "community contribution"?
   - If determined to be UGC (user-generated content) on the platform, even if the domain belongs to an official entity, **terminate source_official rules and re-route to blog_forum or self_media rules for evaluation**.
3. Check whether the page is the current version, not an archive or old version documentation.
4. Distinguish the nature of the page:
   - Documentation
   - Release notes
   - Technical report
   - Marketing page
   - Blog announcement
   - Legal terms
   - Product introduction
   - Other
5. For features, API, license, open source status, prioritize using:
   - Documentation
   - Release notes
   - Changelog
   - GitHub repository
   - Model card
   - LICENSE file
6. When evaluating performance, effects, leadership claims, note the official promotional nature.

## Special Rules

### Open Source Status Assessment

To confirm "open source," find one of the following in official channels:

```text
Public code repository link
Public model weights page link
LICENSE file
Official release page clearly pointing to code or weights
Official entry on package manager or model platform
```

### Feature Support Assessment

Prioritize referencing:

```text
Official documentation
API reference
SDK changelog
Release notes
Sample code
```

### Product Availability Assessment

Need to check:

```text
Whether available to all users
Whether limited to beta
Whether limited to specific regions
Whether limited to enterprise edition
Whether permission application is required
```

## Risk Warnings

Official sources can represent "what the official claims," but maintain a critical eye for the following:

```text
Performance superior to all competitors (may involve selective evaluation)
User experience claims
Market share data
Absolute safety guarantees
Medical or legal effect descriptions
```

These typically require independent evaluation, regulatory documents, peer review, or third-party data support.
