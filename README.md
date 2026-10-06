<div align="center">

# AffProof

English · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **This repository is a showcase, not a source release.** AffProof is a private project, so there is no code here, only what it does, how it is built and what it looks like. To talk about it, get in touch through my [GitHub profile](https://github.com/frommmmmg).

**A public, multilingual directory that vets affiliate programs, so people know which ones actually pay.** Each listing carries an evidence-backed due-diligence dossier, a reputation score, payout proofs and a dispute record.

![The architecture: edge filtering, a Hono Worker, and D1.](assets/affproof-architecture.svg)

**Highlights**

- **Serverless on the edge.** The whole site runs on Cloudflare Workers with a D1 (SQLite) database and static assets served from the edge. There is no long-running server process to maintain.
- **Two complete interface themes, switched live.** A dense black-and-gold layout and an 8-bit pixel-arcade skin, with optional sound effects. A width switch (1200, 768 and 390 px) previews the page at tablet and phone sizes.
- **Built for finding the right program fast.** Live search plus filters for platform, payout channel and time range, four sort orders (recommended, clicks, rank surge, proofs), and a gold-audited filter.
- **A strict channel grid instead of marketing claims.** Every card shows the same fixed slots for USDT, PayPal, Payoneer, Stripe and contact channels, lit when found and struck out when absent, so cards line up and nothing can be spun.
- **Reputation you can read.** A score out of 1000, verified payout records and a 48-hour public dispute window, instead of invented approval rates.
- **Server-side rendering built for search.** Pages are rendered inside the Worker, with JSON-LD structured data, `hreflang` tags and a sitemap per language.
- **8 languages**, with a translation workflow that keeps every language in step with the English source.
- **A public API with plans.** Keys are stored as SHA-256 hashes and checked in middleware. Free, Pro and Enterprise plans control pagination limits and which fields come back.
- **Evidence-gated data.** Every dossier goes through a scoring and quality gate before import, and database writes are designed so that nothing is silently lost.
- **Dynamic SVG badges** that other sites can embed, and **documented decisions**: architecture records and bug post-mortems live beside the code.

**Stack:** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

**In numbers (October 2026):** 380 programs indexed, 377 of them with a full audited dossier, in 8 languages.

## Screenshots

![The home page in the default black-and-gold theme.](assets/affproof-home.jpg)
*The home page in the default black-and-gold theme.*

![The program directory: filters, sort orders and the fixed channel grid.](assets/affproof-matrix.jpg)
*The program directory: filters, sort orders and the fixed channel grid.*

![The same pages in the 8-bit arcade theme.](assets/affproof-arcade-home.jpg)

![The same pages in the 8-bit arcade theme.](assets/affproof-arcade-matrix.jpg)
*The same pages in the 8-bit arcade theme.*

![A due-diligence dossier page, and its business terms and traffic section.](assets/affproof-dossier.jpg)

![A due-diligence dossier page, and its business terms and traffic section.](assets/affproof-dossier-seo.jpg)
*A due-diligence dossier page, and its business terms and traffic section.*

![The home page in Chinese and German.](assets/affproof-languages.jpg)
*The home page in Chinese and German.*

![On a phone: search and filters, and a program card.](assets/affproof-mobile.jpg)
*On a phone: search and filters, and a program card.*

## How it works

![Every entry passes an evidence gate before it is imported and translated.](assets/affproof-evidence-pipeline.svg)
*Every entry passes an evidence gate before it is imported and translated.*

![The public API is protected at the edge first, then by key and plan checks in the Worker.](assets/affproof-api-flow.svg)
*The public API is protected at the edge first, then by key and plan checks in the Worker.*

![One Worker renders every language.](assets/affproof-locale-render.svg)
*One Worker renders every language.*

---

<div align="center">

<sub>Screenshots use sample or public data only. © All rights reserved. Descriptions may be quoted with attribution; the software itself is not for redistribution.</sub>

</div>
