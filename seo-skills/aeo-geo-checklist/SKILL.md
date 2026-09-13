---
name: aeo-geo-checklist
description: AEO/GEO citation-readiness checklist for blog posts. Run this after drafting to verify a post can be extracted, trusted, and cited by AI answer engines (ChatGPT, Perplexity, Gemini, AI Overviews, Copilot). Works for any domain — adapt brand.yml per business, not this skill.
---

# AEO/GEO Citation-Readiness Checklist

## When to activate
After a draft is complete but before the final editorial pass. Run this if the user says "check AEO" or "geo optimize this post" or "make this AI-citation ready."

## What this does
Evaluates a blog draft against 9 criteria that answer engines use when deciding whether to extract, trust, and cite content. Returns a pass/fail report with specific fixes for any failed check.

## Checklist (9 gates)

### 1. Answer-First Opening
- [ ] The first 40-80 words after the H1 contain a self-contained, extractable answer to the primary query
- [ ] The answer does not require reading further paragraphs to be understood
- [ ] The answer would make sense as a standalone citation

**Why it matters:** Answer engines extract at the paragraph level. A well-structured opening is the most commonly cited block. (Source: HubSpot AEO guide, Similarweb FIFI framework)

### 2. Verified Statistics or Data Point
- [ ] At least one verified statistic, benchmark, or original data point is present in the draft
- [ ] The statistic has a traceable primary source (not a secondary re-quote)
- [ ] The statistic is not flagged as [FACT CHECK REQUIRED]

**Why it matters:** The GEO arXiv paper (KDD 2024) found Statistics Addition lifts AI visibility by 37-40% across all visibility metrics. It is the single highest-impact AEO tactic.

### 3. Primary-Source Inline Citations
- [ ] Every factual claim has an inline link to an authoritative primary source
- [ ] Sources include: GitHub repos, product documentation, standards bodies, papers, official releases
- [ ] No secondary Medium/LinkedIn blog cited as primary evidence

**Why it matters:** Cite Sources shows +26% baseline improvement, and the combination of citations + quoting + statistics produces compounding gains.

### 4. GitHub / Open-Source References for Technical Claims
- [ ] Where the draft discusses architecture, components, or implementation — relevant GitHub repos are linked
- [ ] Example: "uses a vector database" → links to Chroma, pgvector, or Weaviate repo
- [ ] Example: "built with LangChain" → links to langchain-ai/langchain

**Why it matters:** Primary-source repo links are trust signals that answer engines verify. GEO research recommends "authoritative primary-source links: product documentation, release notes, papers, standards, and GitHub repositories."

### 5. Author E-E-A-T Signals
- [ ] Author byline with name and credential (e.g., "Jane Doe, AI Engineer at Company")
- [ ] The credential is specific enough to establish topical authority
- [ ] If multiple authors: each has a byline

**Why it matters:** The GEO paper found +30% visibility improvement from "Authoritative" formatting. E-E-A-T signals are positively correlated with AI citation rates.

### 6. Content Freshness (Last-Updated)
- [ ] The YAML frontmatter has both `date` and `lastUpdated` fields
- [ ] `lastUpdated` is within 10 months of current date
- [ ] For technical content: API versions, deprecation notes, and package versions are current

**Why it matters:** AirOps data shows pages with a clear "last updated" timestamp receive 1.8x more AI citations. 95% of ChatGPT citations come from content updated within 10 months.

### 7. FAQ Section (If Present)
- [ ] FAQ section genuinely adds value not already covered in the body
- [ ] Each FAQ Q&A is a self-contained extractable answer
- [ ] FAQ schema would be appropriate (only if there are 2+ standalone Q&A pairs)

**Why it matters:** FAQ schema and FAQ content are among the most commonly extracted citation blocks. But redundant FAQ sections dilute authority.

### 8. Schema Metadata Readiness
- [ ] The content would accurately map to Article schema
- [ ] If FAQ present: would accurately map to FAQPage schema
- [ ] If tutorial with steps: would accurately map to HowTo schema
- [ ] Organization/Product schema matches the company entity in brand.yml

**Why it matters:** Structured data helps answer engines understand and trust content. Multiple sources (Semrush, Similarweb, Siteimprove) recommend schema as a foundation for AEO.

### 9. Anti-AI-Slop Editorial Pass
- [ ] No "seamless", "robust", "cutting-edge", "game-changer", or similar filler
- [ ] No generic AI industry rephrasing ("AI is revolutionizing X")
- [ ] No conclusion paragraph that merely re-states the opening
- [ ] Every heading adds distinct value (no "What Is X" if X is defined in the first paragraph)
- [ ] No unsupported claims presented as fact

**Why it matters:** AI-generated slop degrades trust for both human readers and answer engines. The ARC paper found content with high readability and fluency significantly outperforms keyword-stuffed alternatives.

## Output Format

```
## AEO/GEO Checklist Report

Status: [PASS | 1 FAIL | 2 FAILS | 3+ FAILS]

### Detailed Results

| # | Gate | Status | Fix |
|---|---|---|---|
| 1 | Answer-First Opening | ✅ PASS | — |
| 2 | Verified Statistics | ❌ FAIL | Add a verified stat from [suggested source] |
| 3 | Primary-Source Citations | ... | ... |
| ... | ... | ... | ... |

### Priority Fixes
1. [Highest impact failed gate — specific action]
2. [Next priority]
3. [Next priority]

### AEO Readiness Score
- 9/9: ✅ Ready for publish
- 7-8/9: ✅ Publish after fixing failed gates
- 5-6/9: ⚠️ Significant AEO gaps — recommended fix before publish
- <5/9: ❌ Do not publish in current state
```