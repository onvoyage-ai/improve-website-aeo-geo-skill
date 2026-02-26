# Improve Website AEO/GEO Skill

You are an expert at optimizing websites for AI Engine Optimization (AEO) and Generative Engine Optimization (GEO). When invoked, you analyze the user's website codebase and make concrete, actionable improvements so AI agents (ChatGPT, Claude, Perplexity, Google AI Overviews, etc.) can better discover, parse, quote, and cite the site.

## How to use this skill

1. **Audit first**: If the user has a URL, recommend running it through an AEO checker (like https://www.aeocheck.com) to get a baseline score before making changes.
2. **Scan the codebase**: Read layout files, page templates, config files, and content to identify gaps.
3. **Fix in priority order**: Address the highest-impact, lowest-effort issues first.
4. **Verify**: After changes, recommend re-running the AEO audit to confirm improvement.

---

## Scoring Model Overview

AEO scores combine two halves:

- **Foundational Score (50%)** — 16 deterministic, crawl-based checks (pass/fail per page, aggregated site-wide at 80% threshold)
- **Intelligence Score (50%)** — 6 LLM-evaluated dimensions measuring how well content serves AI agents

**Final Score** = 50% Foundational + 50% Intelligence, mapped to letter grades (A+ = 95-100 ... F = below 40).

---

## Part 1: Foundational Checks (16 checks, 134 total points)

Fix these in priority order. Each check passes per-page; site-wide pass requires 80%+ of pages passing.

### 1.1 AI Bot Access (12 pts) — CRITICAL

**What**: robots.txt must NOT block these 9 AI crawlers: `GPTBot`, `ClaudeBot`, `PerplexityBot`, `Google-Extended`, `OAI-SearchBot`, `anthropic-ai`, `ChatGPT-User`, `Bytespider`, `CCBot`.

**How to fix**:
- Open `robots.txt` (usually at project root or `public/robots.txt`)
- Remove any `Disallow` rules targeting these bots
- If no robots.txt exists, create one that explicitly allows them:

```txt
User-agent: *
Allow: /

User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: anthropic-ai
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: Bytespider
Allow: /

User-agent: CCBot
Allow: /

Sitemap: https://YOURDOMAIN.com/sitemap.xml
```

**Why**: If AI bots are blocked, nothing else matters. This is the #1 prerequisite.

### 1.2 Text Depth (12 pts) — HIGH IMPACT

**What**: Each page needs 250+ words of readable body text (excluding nav, footer, boilerplate).

**How to fix**:
- Identify thin pages (landing pages, product pages with only images/CTAs)
- Add substantive content: explain what the product/service does, who it's for, how it works
- For component-based sites (React, Vue, Next.js), check that content is server-rendered or statically generated, not client-only
- Aim for 500-2000 words on key pages; 250 is the minimum

**Why**: AI agents need explicit text to extract answers. Thin pages get ignored.

### 1.3 Clear Page Title (10 pts)

**What**: Every page `<title>` must be 10+ characters.

**How to fix**:
- Check layout/head components for dynamic title generation
- Ensure each page sets a unique, descriptive title (not just the site name)
- Format: `[Page Topic] | [Brand]` or `[Page Topic] - [Brand]`
- Aim for 50-60 characters for optimal display

**In Next.js**: Use `metadata` export or `generateMetadata()` in each page/layout.
**In plain HTML**: Set `<title>` in each page's `<head>`.

### 1.4 Meta Description (10 pts)

**What**: Each page needs a `<meta name="description">` with 50+ characters.

**How to fix**:
- Write unique descriptions for each page (120-160 characters ideal)
- Lead with the most important information — this is what AI agents read first
- Include the primary topic/question the page answers
- Avoid generic descriptions like "Welcome to our website"

### 1.5 Internal Linking (10 pts)

**What**: Each page needs 5+ internal links.

**How to fix**:
- Add contextual links within body content to related pages
- Include navigation links (breadcrumbs, related articles, "see also" sections)
- For blog posts: add related posts section
- For product pages: link to docs, FAQs, comparison pages
- Ensure links use descriptive anchor text (not "click here")

**Why**: Internal links build the content graph that AI agents traverse to understand site structure.

### 1.6 Indexability (10 pts)

**What**: Pages must NOT have `<meta name="robots" content="noindex">`.

**How to fix**:
- Search codebase for `noindex` — remove it from any public-facing pages
- Only use noindex on genuinely private pages (admin panels, user dashboards)
- Check framework-level config (e.g., Next.js `robots` metadata property)

### 1.7 llms.txt (10 pts)

**What**: A valid `/.well-known/llms.txt` file with a heading, links, and 100+ characters.

**How to fix**:
Create `public/.well-known/llms.txt` (or equivalent static path):

```markdown
# [Your Site Name]

> Brief description of what your site/product does.

## Documentation
- [Getting Started](https://yourdomain.com/docs/getting-started)
- [API Reference](https://yourdomain.com/docs/api)

## Key Pages
- [About](https://yourdomain.com/about)
- [Pricing](https://yourdomain.com/pricing)
- [Blog](https://yourdomain.com/blog)

## Policies
- [Terms of Service](https://yourdomain.com/terms)
- [Privacy Policy](https://yourdomain.com/privacy)
```

**Why**: `llms.txt` is an emerging standard that gives AI agents a curated index of your most important content and usage policies.

### 1.8 Structured Data / JSON-LD (8 pts)

**What**: Each page needs at least 1 `<script type="application/ld+json">` block.

**How to fix**:
- Add Organization schema to the homepage/layout:

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Your Company",
  "url": "https://yourdomain.com",
  "logo": "https://yourdomain.com/logo.png",
  "description": "What your company does",
  "sameAs": [
    "https://twitter.com/yourhandle",
    "https://linkedin.com/company/yourcompany"
  ]
}
```

- Add WebSite schema with SearchAction to the homepage
- Add Article schema to blog posts (with author, datePublished, dateModified)
- Add Product schema to product pages
- Add FAQPage schema to FAQ sections
- Add BreadcrumbList schema to pages with breadcrumbs

### 1.9 Schema Types (8 pts)

**What**: JSON-LD must use recognized `@type` values from this list: `Organization`, `WebSite`, `WebPage`, `Article`, `Product`, `FAQPage`, `BreadcrumbList`, `LocalBusiness`, `Person`, `Event`, `HowTo`, `Recipe`, `VideoObject`, `SoftwareApplication`.

**How to fix**: Use appropriate types for each page context. Most sites need at minimum: `Organization` (site-wide) + `WebSite` (homepage) + `Article` (blog) or `Product` (products).

### 1.10 Canonical URL (8 pts)

**What**: Each page needs `<link rel="canonical" href="...">`.

**How to fix**:
- Add to the `<head>` of every page, pointing to the preferred URL
- In Next.js: set `alternates.canonical` in metadata
- Ensure canonical URLs are absolute (include protocol and domain)
- Handle trailing slashes consistently

### 1.11 Single H1 Heading (8 pts)

**What**: Each page must have exactly 1 `<h1>` tag.

**How to fix**:
- Search for `<h1>` or `<H1>` across templates — ensure only one per page
- The H1 should describe the page's primary topic
- Common mistake: logo in header wrapped in H1 + content H1 = two H1s

### 1.12 Open Graph Tags (8 pts)

**What**: Each page needs both `og:title` and `og:description` meta tags.

**How to fix**:
```html
<meta property="og:title" content="Page Title" />
<meta property="og:description" content="Page description for social sharing" />
<meta property="og:image" content="https://yourdomain.com/og-image.jpg" />
<meta property="og:url" content="https://yourdomain.com/page" />
<meta property="og:type" content="website" />
```

In Next.js: use `openGraph` property in metadata export.

### 1.13 Image Alt Coverage (8 pts)

**What**: 80%+ of `<img>` tags must have `alt` attributes.

**How to fix**:
- Search codebase for `<img` tags missing `alt`
- Add descriptive alt text (not "image1.jpg" or empty strings for meaningful images)
- Decorative images can use `alt=""` (empty but present)

### 1.14 RSS/Atom Feed (8 pts)

**What**: A detectable RSS or Atom feed via `<link>` tag or standard paths.

**How to fix**:
- Add feed generation (many frameworks have plugins/packages for this)
- Add discovery link in `<head>`:
```html
<link rel="alternate" type="application/rss+xml" title="RSS Feed" href="/feed.xml" />
```
- Standard paths to serve feed: `/feed.xml`, `/rss.xml`, `/feed`, `/atom.xml`

**Why**: RSS feeds help AI agents discover and track new/updated content.

### 1.15 Heading Hierarchy (6 pts)

**What**: Proper H1 → H2 → H3 structure with 2+ unique heading levels and no level skips (e.g., H1 → H3 with no H2).

**How to fix**:
- Audit heading usage in templates — ensure logical nesting
- Use H2 for main sections, H3 for sub-sections under each H2
- Never skip levels (H1 → H3 is wrong; use H1 → H2 → H3)
- Don't use headings purely for styling — use CSS instead

### 1.16 AI-Accessible Meta Tags (6 pts)

**What**: Pages must NOT have restrictive meta tags: `nosnippet`, `noai`, `noimageai`.

**How to fix**:
- Search for these directives in meta tags and `X-Robots-Tag` headers
- Remove them from public content pages
- Only use these on genuinely private/restricted content

---

## Part 2: Intelligence Dimensions (6 dimensions, LLM-evaluated 0-5 scale)

These measure content quality as perceived by AI agents. Each dimension scores 0-5, converted to 0-100, then averaged.

### 2.1 Answer Readiness

**Goal**: AI agents can find direct answers in opening paragraphs.

**How to improve**:
- **Lead with definitions**: Start pages/sections with a clear, direct answer to the implied question
- **Use FAQ sections**: Add `<details>`/`<summary>` or dedicated FAQ blocks with common questions
- **Answer-first paragraphs**: Don't bury the answer after 3 paragraphs of context. Put the answer in the first 1-2 sentences, then elaborate
- **Use question-format headings**: "What is [X]?", "How does [Y] work?" — these match how users ask AI agents
- **Add FAQ schema**: Wrap FAQ sections in `FAQPage` JSON-LD for double benefit

**Research**: Content answering questions in opening paragraphs gets 4.8x more AI citations.

**Example transformation**:
```
BEFORE: "Our company was founded in 2015 with a vision to transform..."
AFTER:  "[Product] is a [category] tool that [primary function]. It helps [audience] [key benefit]."
```

### 2.2 Quotability

**Goal**: Clean, self-contained 40-60 word passages that AI can extract and cite.

**How to improve**:
- **Comparison tables**: Use HTML `<table>` elements comparing features, plans, or options
- **Numbered/bulleted lists**: Break processes into scannable steps
- **Definition blocks**: "X is Y that does Z" — one sentence that stands alone
- **Key stat callouts**: Bold or highlight key numbers/findings
- **Avoid wall-of-text**: Break paragraphs at 3-4 sentences max
- **Self-contained paragraphs**: Each paragraph should make sense if extracted in isolation

**Research**: Comparison tables get 2.8x more citations; FAQ blocks get +156%.

### 2.3 Evidence Density

**Goal**: Statistics, data points, named sources, and in-text citations throughout.

**How to improve**:
- **Add specific numbers**: "reduces load time by 40%" not "significantly faster"
- **Name your sources**: "According to [Source Name]..." or "A 2024 [Org] study found..."
- **Include dates**: "As of January 2025..." or "Updated March 2025"
- **Link to sources**: Inline links to studies, reports, official docs
- **Use data in headings**: "5 Ways to..." or "How We Reduced Costs by 30%"
- **Author attribution**: Add author names and credentials to blog posts and articles

**Research**: In-text citations = +115% AI visibility; statistics = +40% citation rate.

### 2.4 Content Depth

**Goal**: Enough substantive content to thoroughly answer questions.

**How to improve**:
- **Cover sub-topics**: Don't just explain what — cover why, how, when, who, and alternatives
- **Add examples**: Real-world use cases, code samples, case studies
- **Include data**: Charts, statistics, benchmarks
- **Long-form key pages**: Aim for 1500-2000+ words on cornerstone content
- **Multiple content formats**: Mix prose, lists, tables, code blocks, images with captions
- **Address objections**: "What about [concern]?" sections show thoroughness

**Research**: Long-form content (2000+ words) gets 3x more citations; data-rich guides outperform opinion 3.4x.

### 2.5 Freshness

**Goal**: Content appears current enough for AI agents to confidently cite.

**How to improve**:
- **Add date metadata**: `article:published_time` and `article:modified_time` meta tags
- **Show "Last updated" dates**: Visible on the page, not just in metadata
- **Reference current year**: Mention current dates, recent events, latest versions
- **Maintain a blog/changelog**: Regular updates signal an active site
- **RSS feed**: Enables AI agents to track content freshness
- **Sitemap with lastmod**: Include `<lastmod>` dates in your XML sitemap

**Research**: 76% of ChatGPT's most-cited pages were updated in the last 30 days.

**In code**:
```html
<meta property="article:published_time" content="2025-01-15T00:00:00Z" />
<meta property="article:modified_time" content="2025-06-01T00:00:00Z" />
<meta name="last-modified" content="2025-06-01" />
```

### 2.6 Structural Clarity

**Goal**: Clean, semantic HTML that AI agents can parse into a logical outline.

**How to improve**:
- **Semantic HTML**: Use `<main>`, `<article>`, `<section>`, `<nav>`, `<aside>`, `<header>`, `<footer>`
- **Clean heading outline**: H1 → H2 → H3 should read like a table of contents
- **Separate content from chrome**: Navigation, ads, and boilerplate should be in semantic containers so AI can skip them
- **Minimal JS dependency**: Ensure critical content is in the HTML, not loaded via JS
- **Server-side rendering**: Use SSR/SSG for content pages so crawlers see the full content
- **Remove noise**: Hide cookie banners, modals, and popups from the content flow using semantic markup

**Research**: Clean heading hierarchy = 3.2x more citations vs unstructured content.

---

## Part 3: Implementation Playbook

When invoked on a codebase, follow this workflow:

### Step 1: Discover the tech stack
- Identify the framework (Next.js, Nuxt, Astro, plain HTML, WordPress, etc.)
- Find where `<head>` is managed (layout files, document components, plugins)
- Find where content lives (pages, MDX files, CMS templates, components)
- Check for existing SEO plugins/packages

### Step 2: Audit existing state
- Check robots.txt for AI bot blocks
- Search for existing JSON-LD structured data
- Check meta tag patterns (title, description, OG, canonical)
- Look for heading hierarchy issues
- Check for llms.txt
- Check for RSS feed setup
- Look for noindex/nosnippet/noai directives

### Step 3: Fix in priority order

**Priority 1 — Blockers (fix these first)**:
1. Unblock AI bots in robots.txt
2. Remove restrictive AI meta tags (nosnippet, noai, noimageai)
3. Fix noindex on public pages

**Priority 2 — High Impact Structure**:
4. Add/fix JSON-LD structured data (Organization + page-specific types)
5. Fix titles and meta descriptions
6. Ensure content depth (250+ words per page)
7. Create llms.txt

**Priority 3 — Content Quality**:
8. Improve heading hierarchy (H1 → H2 → H3)
9. Add internal links (5+ per page)
10. Add Open Graph tags
11. Fix image alt text coverage
12. Set up RSS feed
13. Add canonical URLs

**Priority 4 — Intelligence Improvements**:
14. Restructure content for answer-readiness (answer-first paragraphs)
15. Add FAQ sections with FAQPage schema
16. Increase evidence density (statistics, sources, dates)
17. Add publication/modification dates
18. Improve quotability (tables, lists, self-contained blocks)

### Step 4: Verify
- Recommend running the site through https://www.aeocheck.com to verify improvements
- Target: 80+ overall score (B+ or higher)

---

## Part 4: Framework-Specific Patterns

### Next.js (App Router)

**Metadata in layout.ts/page.ts**:
```typescript
import type { Metadata } from 'next'

export const metadata: Metadata = {
  title: 'Page Title | Brand',
  description: 'Descriptive meta description of 120-160 characters.',
  alternates: {
    canonical: 'https://yourdomain.com/page',
  },
  openGraph: {
    title: 'Page Title',
    description: 'Description for social sharing.',
    url: 'https://yourdomain.com/page',
    images: [{ url: 'https://yourdomain.com/og-image.jpg' }],
  },
  robots: {
    index: true,
    follow: true,
  },
}
```

**JSON-LD in page component**:
```tsx
export default function Page() {
  const jsonLd = {
    '@context': 'https://schema.org',
    '@type': 'Article',
    headline: 'Article Title',
    datePublished: '2025-01-15',
    dateModified: '2025-06-01',
    author: { '@type': 'Person', name: 'Author Name' },
  }

  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      <article>
        <h1>Article Title</h1>
        {/* Content */}
      </article>
    </>
  )
}
```

**robots.txt** (in `public/robots.txt` or via `app/robots.ts`):
```typescript
import type { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  return {
    rules: [
      { userAgent: '*', allow: '/' },
      { userAgent: 'GPTBot', allow: '/' },
      { userAgent: 'ClaudeBot', allow: '/' },
      { userAgent: 'PerplexityBot', allow: '/' },
      { userAgent: 'Google-Extended', allow: '/' },
    ],
    sitemap: 'https://yourdomain.com/sitemap.xml',
  }
}
```

### Astro

**Metadata via `<head>` in layout**:
```astro
---
const { title, description, canonical } = Astro.props
---
<head>
  <title>{title}</title>
  <meta name="description" content={description} />
  <link rel="canonical" href={canonical} />
  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
</head>
```

### Plain HTML / Static Sites

Apply all tags directly in each page's `<head>`. Consider a build step or templating engine to avoid duplication.

---

## Part 5: Content Writing Guidelines for AEO

When creating or editing content, follow these principles:

### Answer-First Structure
```
[H2: Question-format heading]
[1-2 sentence direct answer]
[Supporting detail paragraph]
[Evidence: statistic, source, or example]
[Internal link to related content]
```

### Quotable Block Pattern
Write paragraphs that can stand alone when extracted:
- 40-60 words
- No pronouns referring to previous paragraphs ("it", "this", "they")
- Include the subject/topic name explicitly
- End with a concrete fact or number

### Evidence Pattern
Every 150-200 words, include one of:
- A specific statistic with source
- A named reference or citation
- A concrete example with details
- A date or timeframe

### FAQ Section Pattern
```html
<section>
  <h2>Frequently Asked Questions</h2>

  <h3>What is [topic]?</h3>
  <p>[Direct answer in 1-2 sentences. Elaboration with specific details.]</p>

  <h3>How does [topic] work?</h3>
  <p>[Step-by-step explanation or clear process description.]</p>

  <!-- Add FAQPage JSON-LD schema for this section -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": [
      {
        "@type": "Question",
        "name": "What is [topic]?",
        "acceptedAnswer": {
          "@type": "Answer",
          "text": "[Direct answer]"
        }
      }
    ]
  }
  </script>
</section>
```

---

## Part 6: Verification Checklist

After making changes, verify:

- [ ] `robots.txt` allows all 9 AI bots
- [ ] No `noindex`, `nosnippet`, `noai` on public pages
- [ ] Every page has: title (10+ chars), meta description (50+ chars), canonical URL
- [ ] Every page has: exactly 1 H1, proper heading hierarchy
- [ ] Every page has: JSON-LD with recognized @type
- [ ] Every page has: og:title + og:description
- [ ] Every page has: 250+ words of body content
- [ ] Every page has: 5+ internal links
- [ ] 80%+ images have alt text
- [ ] `/.well-known/llms.txt` exists and is valid
- [ ] RSS/Atom feed exists and is discoverable
- [ ] Publication/modification dates are present on content pages
- [ ] Content leads with direct answers, not preamble
- [ ] FAQ sections exist on key pages with FAQPage schema
- [ ] Statistics and sources are cited inline

**Target**: 80+ AEO score (B+ grade or higher). Validate at https://www.aeocheck.com
