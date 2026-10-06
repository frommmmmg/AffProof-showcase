<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · Français

</div>

> **Ce dépôt est une vitrine, pas une publication de code source.** AffProof est un projet privé : il n'y a donc pas de code ici, seulement ce qu'il fait, comment il est construit et à quoi il ressemble. Pour en discuter, contactez-moi via mon [profil GitHub](https://github.com/frommmmmg).

**Un annuaire public et multilingue qui examine les programmes d'affiliation pour savoir lesquels paient vraiment.** Chaque fiche comporte un dossier de diligence raisonnée appuyé sur des preuves, un score de réputation, des preuves de paiement et un historique des litiges.

![L'architecture : filtrage en périphérie, un Worker Hono et D1.](assets/affproof-architecture.svg)

**Points forts**

- **Serverless en périphérie.** Tout le site tourne sur Cloudflare Workers avec une base D1 (SQLite) et des fichiers statiques servis depuis la périphérie. Aucun processus serveur permanent à maintenir.
- **Deux thèmes d'interface complets, commutables en direct.** Une mise en page dense noir et or et un thème arcade pixel 8 bits, avec effets sonores en option. Un sélecteur de largeur (1200, 768 et 390 px) prévisualise les tailles tablette et mobile.
- **Conçu pour trouver vite le bon programme.** Recherche en direct avec filtres par plateforme, canal de paiement et période, quatre tris (recommandé, clics, hausse de rang, preuves) et un filtre d'audit or.
- **Une grille de canaux stricte plutôt que des slogans.** Chaque carte affiche les mêmes emplacements fixes pour USDT, PayPal, Payoneer, Stripe et les canaux de contact, allumés s'ils existent et barrés sinon : les cartes restent alignées et rien ne peut être embelli.
- **Une réputation lisible.** Un score sur 1000, des paiements vérifiés et une fenêtre publique de litige de 48 heures, au lieu de taux d'approbation inventés.
- **Rendu côté serveur pensé pour le référencement.** Les pages sont générées dans le Worker, avec données structurées JSON-LD, balises `hreflang` et un sitemap par langue.
- **8 langues**, avec un flux de traduction qui garde chaque langue alignée sur l'original anglais.
- **Une API publique avec des offres.** Les clés sont stockées sous forme de hachages SHA-256 et vérifiées dans un middleware. Les offres Free, Pro et Enterprise règlent les limites de pagination et les champs renvoyés.
- **Des données soumises à des preuves.** Chaque dossier passe par une notation et un contrôle qualité avant import, et les écritures en base sont conçues pour ne pas perdre de données en silence.
- **Badges SVG dynamiques** que d'autres sites peuvent intégrer, et **décisions documentées** : les décisions d'architecture et les analyses d'incidents vivent à côté du code.

**Technologies :** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

**En chiffres (octobre 2026) :** 380 programmes référencés, dont 377 avec un dossier audité complet, en 8 langues.

## Captures d'écran

![La page d'accueil avec le thème noir et or par défaut.](assets/affproof-home.jpg)
*La page d'accueil avec le thème noir et or par défaut.*

![L'annuaire des programmes : filtres, tris et la grille fixe des canaux.](assets/affproof-matrix.jpg)
*L'annuaire des programmes : filtres, tris et la grille fixe des canaux.*

![Les mêmes pages avec le thème arcade 8 bits.](assets/affproof-arcade-home.jpg)

![Les mêmes pages avec le thème arcade 8 bits.](assets/affproof-arcade-matrix.jpg)
*Les mêmes pages avec le thème arcade 8 bits.*

![Une fiche de diligence raisonnée, avec sa section sur les conditions commerciales et le trafic.](assets/affproof-dossier.jpg)

![Une fiche de diligence raisonnée, avec sa section sur les conditions commerciales et le trafic.](assets/affproof-dossier-seo.jpg)
*Une fiche de diligence raisonnée, avec sa section sur les conditions commerciales et le trafic.*

![La page d'accueil en chinois et en allemand.](assets/affproof-languages.jpg)
*La page d'accueil en chinois et en allemand.*

![Sur mobile : recherche et filtres, et une carte de programme.](assets/affproof-mobile.jpg)
*Sur mobile : recherche et filtres, et une carte de programme.*

## Comment ça marche

![Chaque fiche franchit un contrôle de preuves avant d'être importée et traduite.](assets/affproof-evidence-pipeline.svg)
*Chaque fiche franchit un contrôle de preuves avant d'être importée et traduite.*

![L'API publique est protégée d'abord en périphérie, puis par des contrôles de clé et d'offre dans le Worker.](assets/affproof-api-flow.svg)
*L'API publique est protégée d'abord en périphérie, puis par des contrôles de clé et d'offre dans le Worker.*

![Un seul Worker génère toutes les langues.](assets/affproof-locale-render.svg)
*Un seul Worker génère toutes les langues.*

---

<div align="center">

<sub>Les captures n'utilisent que des données d'exemple ou publiques. © Tous droits réservés. Les descriptions peuvent être citées avec attribution ; le logiciel lui-même ne peut pas être redistribué.</sub>

</div>
