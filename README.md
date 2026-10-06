<div align="center">

# AffProof

English · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **This repository is a showcase, not a source release.** AffProof is a private project, so there is no code here, only what it does, how it is built and what it looks like. To talk about it, get in touch through my [GitHub profile](https://github.com/frommmmmg).

**A public, multilingual directory that vets affiliate programs, so people know which ones actually pay.** Each listing carries an evidence-backed due-diligence profile, community reviews, payout proofs and a dispute record.

![AffProof architecture](assets/affproof-architecture.svg)

**Highlights**

- **Serverless on the edge.** The whole site runs on Cloudflare Workers with a D1 (SQLite) database and static assets served from the edge. There is no long-running server process to maintain.
- **Server-side rendering built for search.** Pages are rendered inside the Worker, with JSON-LD structured data, `hreflang` tags and a sitemap generated per language.
- **8 languages**, with a translation workflow that keeps every language in step with the English source.
- **A public API with tiers.** Keys are stored as SHA-256 hashes and checked in middleware. Free, Pro and Enterprise plans control pagination limits and which fields come back.
- **Evidence-gated data.** Due-diligence entries go through a scoring and gate step before import, and database changes are written to avoid silent data loss.
- **Dynamic SVG badges** that other sites can embed.
- **Documented decisions.** Architecture decision records and bug post-mortems live alongside the code.

**Stack:** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

## Screenshots

![Public home page of the live site](assets/affproof-home.png)
*Public home page of the live site*

![A due-diligence dossier page on the live site](assets/affproof-dossier.png)
*A due-diligence dossier page on the live site*

## How it works

![Every entry passes an evidence gate before it is imported and translated.](assets/affproof-evidence-pipeline.svg)
*Every entry passes an evidence gate before it is imported and translated.*

![The public API is protected at the edge first, then by key and plan checks in the Worker.](assets/affproof-api-flow.svg)
*The public API is protected at the edge first, then by key and plan checks in the Worker.*

---

<div align="center">

<sub>Screenshots use sample or public data only. © All rights reserved. Descriptions may be quoted with attribution; the software itself is not for redistribution.</sub>

</div>
