<div align="center">

# AffProof

English · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [Français](README.fr.md)

🌐 **[affproof.com](https://affproof.com)** · [GitHub @frommmmmg](https://github.com/frommmmmg)

✍️ By **姜芊泽 (Jiang Qianze)** · WeChat Official Account: **Pin海引航**

</div>

> **This repository is a showcase, not a source release.** AffProof is closed-source, so there is no code here, only what it does, how it is built and what it looks like. To talk about it, get in touch through my [GitHub profile](https://github.com/frommmmmg).

**A public, multilingual directory that vets affiliate programs, so people know which ones actually pay.** Each listing carries an evidence-backed due-diligence dossier, a reputation score, payout proofs and a dispute record.

Affiliate marketing is full of programs that look generous on a landing page and quietly stop paying once you scale. Most directories simply copy the vendor's own claims. AffProof starts from the other end: it records what can be checked (the real programs page, the payout channels that are actually offered, the commission terms in writing) and lets the community add what only they can know, such as whether the money arrived. The motto is *Proof of payout. Zero fluff.*

![Architecture](assets/affproof-architecture.svg)

| | |
|---|---|
| **Website** | **[affproof.com](https://affproof.com)**, in 8 languages |
| **Role** | Designed, built and run by one person: product, data pipeline, front end, edge back end, operations |
| **Status** | Live in production |
| **Scale** | 380 programs indexed, 377 with a full audited dossier (October 2026) |
| **Stack** | Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions |

### What it does

**For webmasters**
- **Find the right program fast.** Live search, filters for platform, payout channel and time range, four sort orders (recommended, clicks, rank surge, proofs) and a gold-audited filter.
- **A strict channel grid instead of marketing claims.** Every card shows the same fixed slots for USDT, PayPal, Payoneer, Stripe and contact channels, lit when found and struck out when absent, so cards line up and nothing can be spun.
- **Reputation you can read.** A score out of 1000 built from the dossier, a rolling 30-day window of payout proofs and reviews, activity with decay, and penalties for disputes a vendor failed to answer within 48 hours. A vendor that resolves its disputes recovers automatically.
- **Two complete interface themes, switched live:** a dense black-and-gold layout and an 8-bit pixel-arcade skin with optional sound. A width switch (1200, 768 and 390 px) previews the page at tablet and phone sizes.

**For vendors**
- **Claim a listing in about ten seconds** and embed a dynamic *Verified by AffProof* SVG badge on your own site.

**For search and for developers**
- **Server-side rendering built for search.** Pages are rendered inside the Worker, with JSON-LD structured data, `hreflang` tags and a sitemap per language.
- **8 languages**, with a translation workflow that keeps every language in step with the English source.
- **A public API with plans.** Keys are stored as SHA-256 hashes and checked in middleware. Free, Pro and Enterprise plans control pagination limits and which fields come back.

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

<!--notes-->
## Engineering notes

- **Edge-native by decision, not by fashion.** There is no VPS, no container and no long-running process. The reasoning is written down as an architecture decision record: zero cold start, global scale, and a near-zero idle bill.
- **Two layers of API protection.** Rules at the edge stop scans and floods first; the Worker then checks the hashed key, applies the plan quota and projects only the fields that plan may see. Lists use cursor pagination, never deep `OFFSET`.
- **Operations behind Zero Trust.** The admin side and automation sit behind Cloudflare Access with service tokens, so unauthorised traffic is turned away at the edge before it reaches the Worker.
- **Self-healing reputation.** Dispute deadlines are evaluated lazily when a score is read, and the penalty is always recomputed from the current disputes. A program that ignores disputes is closed automatically and reopens once they are resolved.
- **A hard rule learned from an incident.** A bulk import once used a delete-and-reinsert write and silently wiped related data. Now imports update rows in place and are reconciled against the schema first. The post-mortem and the rule are written down next to the code.
- **Everything is documented.** Architecture decisions, bug records, a translation guide and a data-quality policy live in the repository, so the next change starts from the reasons, not from guesses.

<!--author-->
## About the author

<img src="assets/wechat-qr.png" alt="QR code of the WeChat Official Account Pin海引航" width="200" align="right">

**姜芊泽 (Jiang Qianze)** is a pen name. I am an independent developer who builds tools, data and automation for brands, merchants and creators going global. Every project in these showcases was designed, built and run end to end by me alone, from the product idea to the servers and the documentation.

I write about this work on my WeChat Official Account, **Pin海引航** (in Chinese). Scan the code to follow it, or find me on [GitHub](https://github.com/frommmmmg).

<br clear="right">
<!--/author-->

**Other showcases:** [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AutoPin-CS](https://github.com/frommmmmg/AutoPin-CS-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Screenshots use sample or public data only. © All rights reserved. Descriptions may be quoted with attribution; the software itself is not for redistribution.</sub>

</div>
