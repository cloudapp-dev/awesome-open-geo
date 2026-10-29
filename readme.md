# Awesome Open GEO [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Free and open-source tooling for Generative Engine Optimization — making your content findable, parsable, and citable by AI answer engines.

Generative Engine Optimization (GEO) is the practice of getting your content surfaced and cited by systems that answer instead of link: ChatGPT, Perplexity, Claude, Gemini, Google AI Overviews. The original GEO paper, listed under Research and Papers below, showed the levers differ from classic SEO: citations, statistics, and quotable structure move the needle where keyword density does not.

The tooling around it, however, is almost entirely paid SaaS. This list is the other half: **every entry is free to use and published under an OSI-approved license**, so you can read the source, self-host it, and audit what it measures. Hosted-only products, source-available licenses, and repositories without a license file are out of scope.

## Contents

- [Standards and Specifications](#standards-and-specifications)
- [Audit and Linting](#audit-and-linting)
- [Visibility and Citation Monitoring](#visibility-and-citation-monitoring)
- [llms.txt Tooling](#llmstxt-tooling)
- [Framework and CMS Integrations](#framework-and-cms-integrations)
- [Crawler Access and Log Analysis](#crawler-access-and-log-analysis)
- [Agent Skills and MCP Servers](#agent-skills-and-mcp-servers)
- [Research and Papers](#research-and-papers)
- [Directories and Datasets](#directories-and-datasets)

## Standards and Specifications

The contracts AI systems actually read. Everything else in this list implements one of these.

- [llms.txt](https://github.com/AnswerDotAI/llms-txt) - Proposal and reference tooling for `/llms.txt`, a curated markdown index that points language models at the pages you want them to read. The de facto standard the rest of this section builds on.
- [Schema.org](https://github.com/schemaorg/schemaorg) - The vocabulary behind JSON-LD structured data. Answer engines lean on it to resolve entities, so it remains the highest-leverage markup you can ship.
- [The Website Specification](https://github.com/jdevalk/specification.website) - Platform-agnostic, sourced checklist covering SEO, accessibility, security, and agent-readiness. Written by Yoast's founder and unusually rigorous about citing its claims.
- [ai.robots.txt](https://github.com/ai-robots-txt/ai.robots.txt) - Maintained registry of AI crawler user-agents with generated `robots.txt`, nginx, Caddy, HAProxy, and `.htaccess` configs. Useful in both directions: decide who to admit, not just who to block.

## Audit and Linting

Run these against your own site to find what stops an answer engine from quoting you.

- [geo-optimizer-skill](https://github.com/Auriti-Labs/geo-optimizer-skill) - Python CLI that scores a site 0–100 on AI-search readiness across eight categories and reports what to fix. Also ships as a library, an MCP server, and an Astro integration, so it drops into CI.
- [geo-lint](https://github.com/IJONIS/geo-lint) - Content linter with ~97 GEO rules that emits structured violations plus a suggested fix per rule, which makes it scriptable in an agent fix-loop rather than just a report.
- [seo-geo-audit](https://github.com/lireking/seo-geo-audit) - Dependency-free Node crawler combining classic SEO checks with AI-crawler readiness (llms.txt, structured data, bot access) and Core Web Vitals. No install step, no API key.
- [SEOCORE](https://github.com/codepurse/SEOCORE) - Multi-threaded TypeScript crawler with a rule engine and link-graph analyzer. The heavier option when you need internal-linking and site-architecture data, not just page checks.
- [seo-audit-skill](https://github.com/seo-skills/seo-audit-skill) - Command-line audit with 108 rules across 12 categories, including AI-search and structured-data checks.
- [laravel-seo-scanner](https://github.com/backstagephp/laravel-seo-scanner) - Scans Laravel routes from inside the app, so it audits pages that a public crawler cannot reach.

## Visibility and Citation Monitoring

Measuring whether AI engines actually mention you. This is where the paid-SaaS gap is widest, and where self-hosting matters most — these tools query models on your behalf, so you pay the inference cost either way.

- [Elmo](https://github.com/elmohq/elmo) - Self-hosted platform tracking how ChatGPT, Claude, Perplexity, Gemini, and AI Overviews mention, cite, and describe your brand. The most complete open alternative to the commercial visibility dashboards.
- [OneGlanse](https://github.com/aryamantodkar/oneglanse) - Drives the real product UIs in a browser instead of calling model APIs, capturing inline citations and recommended sources as users actually see them. API completions routinely differ from what the chat surface renders.
- [GEOrank](https://github.com/yaojingang/GEORank) - Self-hostable GEO workbench that turns a site diagnosis into prompts, action plans, and structured-data assets. Bring your own API key. Primary docs are Chinese, with an English readme.
- [Ansvisor](https://github.com/ansvisor/ansvisor) - AI visibility platform tracking citations, prompts, and competitors, developed in public with an open roadmap.
- [gego](https://github.com/AI2HU/gego) - Single Go binary that tracks brand visibility across LLMs. The lightest thing to drop on a server when you do not want a full platform.
- [searchstack-aeo](https://github.com/alexpospekhov/searchstack-aeo) - Python stack for monitoring visibility across generative engines, assembled for small teams rather than agencies.
- [goose-aeo](https://github.com/gooseworks-ai/goose-aeo) - AEO tracking CLI plus dashboard, designed to be driven by a coding agent.
- [potato](https://github.com/onism1767-creator/potato) - Narrow, fast check of how often a brand is mentioned and cited in web-search answers. Good for a quick read before committing to a full platform.

## llms.txt Tooling

Generating and validating the file, rather than hand-maintaining it.

- [llmstxt](https://github.com/dotenvx/llmstxt) - Converts an existing `sitemap.xml` into `llms.txt` in one npx command. The shortest path from a live site to a valid file.
- [llm-docs-builder](https://github.com/mensfeld/llm-docs-builder) - Transforms a markdown docs tree into LLM- and RAG-optimized output, generating `llms.txt` as part of the build.
- [llms-txt-php](https://github.com/raphaelstolt/llms-txt-php) - PHP library to write, read, and validate `llms.txt`, so generation can live in an existing PHP app instead of a separate toolchain.
- [actor-llmstxt-generator](https://github.com/apify/actor-llmstxt-generator) - Crawls a site and emits `llms.txt` as an Apify Actor, which is the practical option when the source is a site you do not control.
- [LLMTEXT-mcp](https://github.com/janwilmake/LLMTEXT-mcp) - Converts an `llms.txt` into an MCP server, letting agents query your documentation directly instead of scraping it.
- [mcpdoc](https://github.com/langchain-ai/mcpdoc) - Serves `llms.txt` sources to IDEs and agents over MCP, with the fetch surface deliberately constrained to the domains you list.

## Framework and CMS Integrations

Emit the right markup and machine-readable output from the stack you already run.

- [Nuxt SEO](https://github.com/harlan-zw/nuxt-seo) - Bundles structured data, meta, sitemaps, and robots handling for Nuxt, with explicit AEO coverage. The most mature framework-level implementation in this list.
- [nuxt-llms](https://github.com/nuxt-content/nuxt-llms) - Generates `/llms.txt` for a Nuxt app automatically from its content.
- [vitepress-plugin-llms](https://github.com/okineadev/vitepress-plugin-llms) - Produces `llms.txt` and per-page markdown from a VitePress docs site.
- [starlight-llms-txt](https://github.com/delucis/starlight-llms-txt) - Same for Astro Starlight documentation sites.
- [mkdocs-llmstxt](https://github.com/pawamoy/mkdocs-llmstxt) - MkDocs plugin that emits an `/llms.txt` on build.
- [sphinx-llms-txt](https://github.com/jdillard/sphinx-llms-txt) - `llms.txt` generation for Sphinx, covering the Python documentation ecosystem.
- [astro-llms-md](https://github.com/tfmurad/astro-llms-md) - Generates `llms.txt`, `llms-full.txt`, and per-page markdown for any Astro site.
- [ultralytics/mkdocs](https://github.com/ultralytics/mkdocs) - MkDocs plugin covering SEO metadata, JSON-LD, social cards, copy-for-LLM buttons, and `llms.txt` in one dependency.
- [dualmark](https://github.com/dodopayments/dualmark) - Serves a markdown twin of every page so agents get clean source while humans get HTML. Content negotiation instead of a separate index file.
- [site-md](https://github.com/yazinsai/site-md) - The same dual-serving idea for Next.js, as a drop-in middleware.
- [seo-graph](https://github.com/jdevalk/seo-graph) - Builds a connected Schema.org JSON-LD graph in JavaScript rather than emitting disconnected blobs, which is what entity resolution actually needs. Ships an Astro integration.
- [schema-dts](https://github.com/google/schema-dts) - TypeScript types for the Schema.org vocabulary, so invalid structured data fails at compile time.
- [RagRabbit](https://github.com/madarco/ragrabbit) - Self-hosted AI site search that also produces `llms.txt` from what it indexes, giving one crawl two uses.
- [aigeo](https://github.com/GitHiteshZope/aigeo) - Laravel package for surfacing products inside AI-generated answers.
- [GEO-AI-Woo](https://github.com/madeburo/GEO-AI-Woo) - WordPress and WooCommerce plugin generating `llms.txt`, AI crawler rules, and AI-oriented metadata.
- [NodeThemes SEO AI](https://github.com/nodethemes/nodethemes-seo-ai) - WordPress and WooCommerce SEO plugin (GPL-2.0) that serves `llms.txt`, outputs JSON-LD schema with FAQ data, logs AI crawler visits and scores every page for AI-answer readiness. AI writing features use your own OpenAI, Claude or Gemini key.

## Crawler Access and Log Analysis

You cannot be cited by a crawler you blocked, and you cannot tell whether you were crawled without reading logs. This section covers both directions honestly.

- [GoAccess](https://github.com/allinurl/goaccess) - Real-time terminal log analyzer. Filter access logs by user-agent and you have a free, exact answer to which AI crawlers hit which URLs — no sampling, no vendor.
- [ipranges](https://github.com/lord-alfred/ipranges) - Daily-updated IP ranges by provider, including OpenAI, Perplexity, Googlebot, and Bingbot. The only reliable way to confirm a claimed AI crawler is genuine rather than a spoofed user-agent.
- [Anubis](https://github.com/TecharoHQ/anubis) - Proof-of-work reverse proxy that stops scrapers. Listed because access control is a GEO decision: the tools here let you admit the crawlers you want cited by and shed the rest, instead of an all-or-nothing block.
- [the-great-gpt-firewall](https://github.com/samber/the-great-gpt-firewall) - Tracks which sites restrict AI crawlers. Useful competitive context on how a given sector is actually behaving.
- [device-detector](https://github.com/matomo-org/device-detector) - Battle-tested user-agent parser with bot definitions, for classifying crawler traffic inside your own analytics pipeline.

## Agent Skills and MCP Servers

GEO workflows packaged for coding agents. Fast to try, but treat their scoring as heuristic — none of these are calibrated against a benchmark.

- [claude-seo](https://github.com/AgriciDaniel/claude-seo) - Broad SEO skill suite for Claude Code with dedicated GEO, schema, and E-E-A-T workflows. The most widely used of these by a wide margin.
- [geo-seo-claude](https://github.com/zubair-trabzada/geo-seo-claude) - GEO-first counterpart focused on citability scoring rather than classic rankings.
- [orangeo-ai-visibility-skill](https://github.com/PixelOrange7/orangeo-ai-visibility-skill) - Narrow readiness check over robots.txt, llms.txt, schema, and citation signals. Small enough to read end to end before trusting it.
- [dev-gtm-claude-skills](https://github.com/Infrasity-Labs/dev-gtm-claude-skills) - GEO and AI-discoverability skills aimed specifically at developer-facing products.
- [ai-brand-monitor-mcp](https://github.com/khadinakbarlabs/ai-brand-monitor-mcp) - MCP server exposing brand-mention tracking across Perplexity, ChatGPT, Claude, and Gemini to any agent.

## Research and Papers

The evidence base. Worth reading before trusting any tool's score, since most scoring heuristics trace back to these findings.

- [GEO: Generative Engine Optimization](https://arxiv.org/abs/2311.09735) - The KDD 2024 paper that named the field, with the 10k-query GEO-bench. Established that citations, quotations, and statistics lift visibility up to ~40% while keyword density does almost nothing.
- [A Critical Survey of Generative Engine Optimization (2023–2026)](https://arxiv.org/abs/2607.14035) - Reviews 45 studies and reframes GEO as a multi-stage pipeline — activation, crawling, retrieval, reranking, citation, absorption — instead of a single ranking task. The best single starting point in 2026.
- [Structural Feature Engineering for GEO](https://arxiv.org/abs/2603.29979) - Isolates how content structure shapes citation behavior, reporting a 17.3% citation-rate improvement from structural changes alone.
- [AutoGEO](https://github.com/cxcscmu/AutoGEO) - ICLR 2026 framework that learns generative-engine preferences automatically instead of hand-tuning heuristics. Code included.
- [GEO reference implementation](https://github.com/GEO-optim/GEO) - Official code and benchmark harness accompanying the original paper, for reproducing its results on your own content.
- [AgenticGEO](https://github.com/AIcling/agentic_geo) - Self-evolving agentic system for GEO, with the experiment code published.
- [GEO Risks and Governance](https://arxiv.org/abs/2606.12439) - Position paper on concentration, disclosure, and blind spots. The counterweight to everything else here, and worth reading precisely because it is uncomfortable.

## Directories and Datasets

- [llms-txt-hub](https://github.com/thedaviddias/llms-txt-hub) - The largest directory of sites that publish `llms.txt`, useful both as adoption data and as a source of real-world examples.
- [Awesome llms.txt](https://github.com/SecretiveShell/Awesome-llms-txt) - Index of `llms.txt` files across the web, structured as seed data for crawling.
- [GEO research hub](https://github.com/Wu-beining/generative-engine-optimization-research-hub) - Running bibliography of GEO, AEO, and AIO papers, updated more often than any published survey.

## Related Lists

- [Awesome Generative Engine Optimization](https://github.com/amplifying-ai/awesome-generative-engine-optimization) - The broader GEO list, strongest on commercial platforms and case studies. Complements this one directly.
- [Awesome GEO](https://github.com/luka2chat/awesome-geo) - Another general GEO collection, lighter and more guide-oriented.
- [Awesome Agent Conventions](https://github.com/ItamarZand88/awesome-agent-conventions) - Convention files agents read and write, including `AGENTS.md` and `llms.txt`.

## Contributing

Contributions are welcome. Read [contributing.md](contributing.md) first — the licensing and quality bar is deliberately strict.
