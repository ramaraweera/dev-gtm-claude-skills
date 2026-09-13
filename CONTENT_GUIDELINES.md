# Blog Content Guidelines — Multi-Domain Workflow

This file lives in the forked `dev-gtm-claude-skills` repo root. It defines the end-to-end content creation contract that all agent stages (Researcher, Strategist, Writer, Tech Reviewer, SEO/GEO Reviewer, Editor) must follow. It is domain-agnostic — adapt `brand.yml` per business, not this file.

## 1. Content Philosophy

Every article must be **genuinely useful to a qualified buyer**. Not "more content for SEO." The test: would a practitioner, engineer, or decision-maker save this link, share it with a colleague, or act on it?

### Hard Rules

- **No padding.** Do not add sections, sentences, or paragraphs to hit a word-count target. If the topic is fully covered in 450 words, stop at 450.
- **No generic AI news summaries.** Do not rewrite this week's AI industry headlines unless you have original analysis or data that changes the reader's decision.
- **No tool roundups without original testing.** Listing 10 tools with descriptions from their landing pages is not a useful article. Testing three tools and reporting measured results is.
- **No invented proof.** No fabricated client stories, case studies, statistics, or quotes.
- **Every claim needs a source.** Primary documentation, official release notes, papers, standards bodies, or your own original measurement. Not a Medium blog that references another Medium blog.

## 2. Content Brief Requirements

Before any draft begins, the Strategist agent produces a brief containing:

```
target_query:    "the primary search query this post targets"
search_intent:   informational | commercial | comparison | implementation
unique_angle:    "what makes this post different from the top 5 existing results"
primary_sources:
  - "link to authoritative doc or repo"
  - "link to standards body or paper"
original_input:  "company telemetry, benchmark, experiment, or real example"
internal_links:
  - "related service page"
  - "related pillar page or blog post"
audience:        (from brand.yml)
word_count:      400-700 | 800-1300 | 1200-1800
draft: true      # MUST remain true until human approval
```

## 3. Article Structure

### Opening (40-80 words)
Directly answer the primary query. This is the extractable block answer engines will cite.

**Pattern:**
> "[Answer to query]. [1-sentence elaboration]. [Context or limitation, if needed]."

**Example (RAG vs Fine-Tuning):**
> "Use RAG when your main problem is keeping an LLM grounded in changing private or external knowledge. Use fine-tuning when you need a durable change in behavior, style, or task performance. Many production systems use both: fine-tuning for behavior and RAG for current facts."

### Body
- One H1 (the title)
- 3-6 meaningful H2 headings (each answers a sub-question or covers a subtopic)
- H3 only for genuinely complex sections requiring sub-structure
- Each H2 section starts with the answer, then provides evidence and depth

### Closing CTA
Low-pressure, specific. Avoid: "Contact us today," "Don't wait," "Transform your business."

**Pattern:**
> "If you're assessing [specific problem], we can help scope a practical approach around your [data/requirements/budget/security needs]."

### No Standard "Conclusion" Filler
Do not add a "Conclusion" heading that summarises what was already said. End with the CTA or a forward-looking observation.

## 4. Technical Accuracy Requirements

| What | Requirement |
|---|---|
| Code snippets | Must be runnable or trivially adaptable. Include prerequisites and version info. |
| API claims | Must reference the documented version and be current within 6 months. |
| Benchmark numbers | Must state methodology: hardware, model version, dataset, date. |
| Deployment claims | Must specify environment: self-hosted, API, cloud tenancy, containerised. |
| Cost figures | Must specify currency, region, and date sourced. |

## 5. Internal Link Rules

- Link to the relevant service page at most once in the body.
- Link to related blog posts where they genuinely complement the current topic.
- Link to product documentation or GitHub repos when a technical claim is made.
- Do not force links into every section. Natural relevance only.

## 6. Quality Gates (Applied in Order)

### Gate 1: ai-content-quality (via Hermes skill or Editor agent)
Apply the `ai-content-quality` editorial gate. This checks:
- No AI slop phrasing
- Clear sentence-level prose
- Fact-check flags formatted as `[FACT CHECK REQUIRED: claim — evidence needed]`
- Preserved YAML frontmatter, source URLs, and core argument

### Gate 2: AEO/GEO Citation-Readiness
Checklist:
- [ ] Opening 40-80 words contains a self-contained, extractable answer
- [ ] ≥1 verified statistic or original data point present
- [ ] All factual claims have inline primary-source citations
- [ ] GitHub or documentation repository links present where technical architecture is discussed
- [ ] Author E-E-A-T byline present (name + 1-line credential)
- [ ] FAQ schema genuinely adds value not covered in body
- [ ] Article schema metadata would be accurate for this content

### Gate 3: Domain Authority Signals
- External brand mentions across authoritative platforms (Wikipedia, GitHub, news, docs) are consistent
- Entity facts (company name, product names, founder names) match external sources
- Content recency: last-updated timestamp on every page

## 7. Multi-Agent Pipeline Definition

When the forked repo is configured with multi-agent support, the pipeline runs sequentially:

```
1. Researcher ──→ 2. Strategist ──→ 3. Writer ──→ 4. Tech Reviewer ──→ 5. SEO/GEO Reviewer ──→ 6. Editor
```

**Role definitions for AGENTS.md:**

```yaml
agents:
  researcher:
    tools: [web_search, web_extract]
    output: source list with URLs, claims extracted, competitor gap analysis
  strategist:
    tools: [file]  # reads brand.yml + research output
    output: content brief (YAML) with angle, intent, audience, sources
  writer:
    tools: [file]  # reads brand.yml + brief
    output: full markdown draft with YAML frontmatter
  tech_reviewer:
    tools: [web_search, terminal]
    output: validation report for code, API versions, citations
  seo_geo_reviewer:
    tools: [file]  # runs AEO/GEO checklist
    output: quality report with pass/fail per gate
  editor:
    tools: [file]  # applies anti-slop pass + final polish
    output: production-ready draft
```

## 8. Publishing Boundary

**This workflow NEVER publishes.** The output is always a review package delivered to the human approver. A separate, human-authorized publish workflow takes over after approval.