
> **Must read SKILL.md before reading this file to understand the full task context.**

# Topic-Specific Rules Registry

This file records the mapping between all topics (domains) and their corresponding special rule files. The Agent loads corresponding rule files for叠加 evaluation based on topic keywords identified in the user's question.

## Registry

| Topic | Keywords / Trigger Conditions | Rule File |
|-------|-------------------------------|-----------|
| AI / Tech | AI, artificial intelligence, large model, LLM, GPT, open source, API, model capability, software release, deep learning, machine learning | `rules/source_ai_tech.md` |
| Healthcare | healthcare, health, disease, diagnosis, treatment, medication, vaccine, clinical trial, public health | `rules/source_medical.md` |
| Law / Policy | law, regulation, policy, compliance, legal precedent, judicial interpretation, legislation | `rules/source_law_policy.md` |

<!--
  The following are reserved expansion slots that users can add themselves:
  | Finance / Investment | stocks, funds, investment, financial products, securities, futures, cryptocurrency | `rules/source_finance.md` |
  | Education / Academia | education, exams, degrees, admissions, academic evaluation | `rules/source_education.md` |
  | Food Safety | food, additives, pesticide residues, food safety standards | `rules/source_food_safety.md` |
  ...
-->

## Agent Usage

1. Extract topic keywords from the user's question
2. Cross-reference this registry to match all hit topics
3. For each hit topic, load the corresponding rule file
4. Overlay topic rules on top of existing source type rules (topic rules are additional constraints, they do not replace source type rules)
5. If multiple topics are hit, load all corresponding rule files and evaluate comprehensively

## Matching Logic

```text
- User's question explicitly mentions a topic keyword → confirmed hit
- User's question does not directly mention keywords, but the substance falls within a topic's scope → should also be considered a hit
  (e.g., user asks "Can drug X treat disease Y" without mentioning "medical," but it is substantively a healthcare topic)
- User's question does not involve any registered topic → skip topic rule overlay step
- User's question spans multiple topics → load all relevant rules
```

## Custom Extensions

**Users can自行 extend this registry to suit their professional domain needs.**

### Manual Addition

Directly add a new row to the registry, following this format:

```text
| Topic Name | Trigger Keywords (comma-separated) | `rules/source_xxx.md` |
```

Then create the corresponding rule file in the `rules/` directory (following the format of existing topic rule files, including `source_reliability_score` adjustments, `citation_usability` constraints, domain-specific warnings, etc.).

### Let the Agent Do It

You can also directly tell the Agent your requirements, for example:

```
"Please add a finance/investment topic covering stocks, funds, cryptocurrency, etc."
"Please add an education/academia domain to the topic registry"
```

The Agent will automatically register the new topic in this registry and create the corresponding rule file.

### Notes

- The rule file for each topic should follow the naming convention `rules/source_<domain>.md`
- Rule files should follow the format of existing topic rule files: include sections such as "Best Sources," "Usability Constraints," "Domain-Specific Warnings," "Scenarios Not Usable as Evidence," etc.
- After modifying the registry, there is no need to modify SKILL.md — the Agent will automatically read the topic mappings from the registry.
