# Research SEO/GEO Keywords

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that researches and delivers a prioritized keyword list for SEO and GEO — using web search and AI analysis instead of paid tools like Ahrefs or Semrush.

**No Ahrefs. No Semrush. No API keys.**

Uses web search, website crawling, and LLM analysis to find, cluster, and prioritize keywords — including a GEO dimension that traditional tools don't offer.

---

## Install

```bash
claude skill add --from https://github.com/onvoyage-ai/gtm-engineer-skills/research-keywords
```

Or manually copy `skill.md` into your project's `.claude/skills/` directory.

## Usage

```
/research-keywords
```

Or:
> "Research keywords for my product"
> "Find SEO and GEO keywords for [brand/URL]"
> "Run keyword research for my [product category]"

The skill is **interactive** — it asks you questions, researches, and delivers a structured keyword file.

---

## The 4-Phase Process

### Phase 1: Brand Intelligence
The skill asks about your product, audience, and competitors. It visits your website and competitor sites to extract language, positioning, and content gaps.

### Phase 2: Keyword Discovery
Researches keywords across 6 methods — no paid tools needed:

| Method | What It Finds |
|---|---|
| Google Autocomplete Mining | Real search suggestions and long-tail variants |
| People Also Ask (PAA) | Question-format keywords AI engines love to answer |
| Reddit & Community Mining | Real user language, pain points, and slang |
| Competitor Content Analysis | Topics competitors cover that you don't |
| Question & Problem Keywords | Problem-aware searches that lead to your product |
| AI Citation Keywords (GEO) | Queries where AI generates answers and cites sources |

### Phase 3: Keyword Analysis & Clustering
Groups keywords into topic clusters, scores each on 3 dimensions:
- **Relevance** to your product (1-5)
- **GEO Opportunity** — will AI answer this and cite sources? (1-5)
- **Business Value** — how close to conversion? (1-5)

Flags quick wins: existing pages to optimize, weak competitor content, AI citation gaps.

### Phase 4: Deliverable
Outputs a structured Markdown file with:
- Prioritized topic clusters with pillar + supporting keywords
- GEO-specific keyword table (highest AI citation potential)
- Quick wins and competitor gaps
- Full raw keyword list for reference
- Content recommendations per cluster

---

## What Makes This Different

| Traditional Keyword Research | This Skill |
|---|---|
| Requires Ahrefs/Semrush ($99-449/mo) | Free — uses web search |
| Focuses on search volume + difficulty | Adds GEO opportunity scoring |
| Outputs a spreadsheet of keywords | Outputs clustered, actionable content plan |
| Ignores AI citation potential | GEO is a first-class dimension |
| Marketer language | Real user language from Reddit/communities |

---

## Works With Other Skills

The keyword deliverable feeds directly into:
- **[write-seo-blog](../write-seo-blog/)** — write articles for top keyword clusters
- **[geo-content-research](../geo-content-research/)** — build full AI-ready content for high-GEO keywords
- **[create-geo-charts](../create-geo-charts/)** — create data visualizations for data-driven keywords

---

## Example Output

```
## Priority Keyword Clusters

### Cluster 1: Best AI Writing Tools — Priority: 14/15
Pillar Keyword: best AI writing tools 2026
Intent: Commercial Investigation
GEO Opportunity: 5/5 — AI Overviews appear, comparison format
Business Value: 5/5 — direct purchase intent
Relevance: 4/5

| Keyword | Intent | GEO Opp | Notes |
|---|---|---|---|
| best AI writing tools 2026 | Commercial | High | Pillar |
| AI writing tool comparison | Commercial | High | Comparison table content |
| is jasper AI worth it | Trust | High | PAA — address in FAQ |
| AI content writer for blogs | Commercial | Medium | Use-case variant |
```
