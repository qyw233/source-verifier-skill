
> **Must read SKILL.md before reading this file to understand the full task context.**

# Academic Source Processing Rules

Academic sources are suitable for supporting technical, scientific, methodological, and experimental conclusions, but evidence strength needs to be distinguished.

## Source Strength

### High Strength

```text
Peer-reviewed journal paper
Peer-reviewed conference paper
Formal publisher page
DOI record
Systematic review or meta-analysis
Standard textbook or classic monograph
```

### Medium Strength

```text
arXiv preprint
University institutional repository
Workshop paper
Technical report
Lab page
```

### Lower Strength

```text
PPT
Poster
Unpublished manuscript
Blog post without peer review
Conclusions only posted on social platforms
```

## Check Steps

1. Extract title, authors, year, publication venue, DOI or arXiv ID.
2. Determine whether peer-reviewed.
3. Check whether relevant claims (such as experimental results, conclusions) are fully elaborated in the paper.
4. Distinguish between the authors' own conclusions and cited background descriptions from others.
5. Distinguish between experimental results, hypotheses, future work, and speculation.
6. Check for updated versions, errata, or retraction information.

## Common Risks

Limitations when presenting research conclusions:

For example:

```text
Paper only verified in simulation ≠ Proven effective in real systems
Small sample experiment effective ≠ Universally effective
Author proposed method ≠ The method has become mainstream
Mentioned in related work ≠ This paper proved the conclusion
Preprint results ≠ Already confirmed by peer review
```

## AI / Control / Engineering Papers Special Considerations

Check:

```text
Whether real experiments or only simulations
Whether datasets or code are publicly available
Whether comparison baselines are sufficient
Whether limitations are stated
Whether evaluation metrics are sufficient
Whether there is parameter tuning bias
```

## Output Recommendations

```json
{
  "source_type": "academic",
  "peer_review_status": "preprint | peer_reviewed | unknown",
  "bibliographic_info": {
    "title": "...",
    "authors": ["..."],
    "year": 2026,
    "venue": "...",
    "doi_or_arxiv": "..."
  },
  "warnings": ["This paper is a preprint", "Experiments are only simulations"]
}
```
