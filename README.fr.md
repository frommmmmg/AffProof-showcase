<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · Français

</div>

> **Ce dépôt est une vitrine, pas une publication de code source.** AffProof est un projet privé : il n'y a donc pas de code ici, seulement ce qu'il fait, comment il est construit et à quoi il ressemble. Pour en discuter, contactez-moi via mon [profil GitHub](https://github.com/frommmmmg).

**Un annuaire public et multilingue qui examine les programmes d'affiliation pour savoir lesquels paient vraiment.** Chaque fiche comporte un profil de diligence raisonnée appuyé sur des preuves, des avis de la communauté, des preuves de paiement et un historique des litiges.

![Architecture d'AffProof](assets/affproof-architecture.svg)

**Points forts**

- **Serverless en périphérie.** Tout le site tourne sur Cloudflare Workers avec une base D1 (SQLite) et des fichiers statiques servis depuis la périphérie. Aucun processus serveur permanent à maintenir.
- **Rendu côté serveur pensé pour le référencement.** Les pages sont générées dans le Worker, avec données structurées JSON-LD, balises `hreflang` et un sitemap par langue.
- **8 langues**, avec un flux de traduction qui garde chaque langue alignée sur l'original anglais.
- **Une API publique par paliers.** Les clés sont stockées sous forme de hachages SHA-256 et vérifiées dans un middleware. Les offres Free, Pro et Enterprise règlent les limites de pagination et les champs renvoyés.
- **Des données soumises à des preuves.** Les fiches passent par une notation et un contrôle avant import, et les écritures en base sont conçues pour ne pas perdre de données en silence.
- **Badges SVG dynamiques** que d'autres sites peuvent intégrer.
- **Décisions documentées.** Les décisions d'architecture et les analyses d'incidents vivent à côté du code.

**Technologies :** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

## Captures d'écran

![Page d'accueil publique du site en production](assets/affproof-home.png)
*Page d'accueil publique du site en production*

![Une fiche de diligence raisonnée sur le site en production](assets/affproof-dossier.png)
*Une fiche de diligence raisonnée sur le site en production*

## Comment ça marche

![Chaque fiche franchit un contrôle de preuves avant d'être importée et traduite.](assets/affproof-evidence-pipeline.svg)
*Chaque fiche franchit un contrôle de preuves avant d'être importée et traduite.*

![L'API publique est protégée d'abord en périphérie, puis par des contrôles de clé et d'offre dans le Worker.](assets/affproof-api-flow.svg)
*L'API publique est protégée d'abord en périphérie, puis par des contrôles de clé et d'offre dans le Worker.*

---

<div align="center">

<sub>Les captures n'utilisent que des données d'exemple ou publiques. © Tous droits réservés. Les descriptions peuvent être citées avec attribution ; le logiciel lui-même ne peut pas être redistribué.</sub>

</div>
