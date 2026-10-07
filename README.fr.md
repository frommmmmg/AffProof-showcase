<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · Français

🌐 **[affproof.com](https://affproof.com)** · [GitHub @frommmmmg](https://github.com/frommmmmg)

✍️ Par **姜芊泽 (Jiang Qianze)** · compte officiel WeChat: **Pin海引航**

</div>

> **Ce dépôt est une vitrine, pas une publication de code source.** AffProof n'est pas open source : il n'y a donc pas de code ici, seulement ce qu'il fait, comment il est construit et à quoi il ressemble. Pour en discuter, contactez-moi via mon [profil GitHub](https://github.com/frommmmmg).

**Un annuaire public et multilingue qui examine les programmes d'affiliation pour savoir lesquels paient vraiment.** Chaque fiche comporte un dossier de diligence raisonnée appuyé sur des preuves, un score de réputation, des preuves de paiement et un historique des litiges.

Le marketing d'affiliation regorge de programmes qui semblent généreux sur leur page d'accueil et cessent discrètement de payer dès que l'on monte en volume. La plupart des annuaires recopient simplement les affirmations de l'éditeur. AffProof part de l'autre bout : il consigne ce qui peut être vérifié (la vraie page du programme, les canaux de paiement réellement proposés, les conditions de commission par écrit) et laisse la communauté ajouter ce qu'elle seule peut savoir, par exemple si l'argent est bien arrivé. La devise : *Proof of payout. Zero fluff.*

![Architecture](assets/affproof-architecture.svg)

| | |
|---|---|
| **Site web** | **[affproof.com](https://affproof.com)**, en 8 langues |
| **Mon rôle** | Conçu, construit et exploité par une seule personne : produit, pipeline de données, front end, back end en périphérie, exploitation |
| **Statut** | En production |
| **Échelle** | 380 programmes référencés, 377 avec un dossier audité complet (octobre 2026) |
| **Technologies** | Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions |

### Ce qu'il fait

**Pour les webmasters**
- **Trouver vite le bon programme.** Recherche en direct avec filtres par plateforme, canal de paiement et période, quatre tris (recommandé, clics, hausse de rang, preuves) et un filtre d'audit or.
- **Une grille de canaux stricte plutôt que des slogans.** Chaque carte affiche les mêmes emplacements fixes pour USDT, PayPal, Payoneer, Stripe et les canaux de contact, allumés s'ils existent et barrés sinon : les cartes restent alignées et rien ne peut être embelli.
- **Une réputation lisible.** Un score sur 1000 construit à partir du dossier, d'une fenêtre glissante de 30 jours de preuves de paiement et d'avis, d'une activité avec décroissance, et de pénalités pour les litiges restés sans réponse au-delà de 48 heures. Un éditeur qui règle ses litiges remonte automatiquement.
- **Deux thèmes d'interface complets, commutables en direct :** une mise en page dense noir et or et un thème arcade pixel 8 bits avec son en option. Un sélecteur de largeur (1200, 768 et 390 px) prévisualise les tailles tablette et mobile.

**Pour les éditeurs**
- **Revendiquer une fiche en une dizaine de secondes** et intégrer sur son site un badge SVG dynamique *Verified by AffProof*.

**Pour le référencement et les développeurs**
- **Rendu côté serveur pensé pour le référencement.** Les pages sont générées dans le Worker, avec données structurées JSON-LD, balises `hreflang` et un sitemap par langue.
- **8 langues**, avec un flux de traduction qui garde chaque langue alignée sur l'original anglais.
- **Une API publique avec des offres.** Les clés sont stockées sous forme de hachages SHA-256 et vérifiées dans un middleware. Les offres Free, Pro et Enterprise règlent les limites de pagination et les champs renvoyés.

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

<!--notes-->
## Notes d'ingénierie

- **Natif en périphérie par décision, pas par mode.** Pas de VPS, pas de conteneur, pas de processus permanent. Le raisonnement est consigné dans un enregistrement de décision d'architecture : zéro démarrage à froid, passage à l'échelle mondial et coût au repos quasi nul.
- **Deux couches de protection pour l'API.** Des règles en périphérie arrêtent d'abord les scans et les rafales ; le Worker vérifie ensuite la clé hachée, applique le quota de l'offre et ne renvoie que les champs autorisés pour cette offre. Les listes utilisent la pagination par curseur, jamais un `OFFSET` profond.
- **Exploitation derrière le Zero Trust.** L'administration et l'automatisation sont derrière Cloudflare Access avec des jetons de service : le trafic non autorisé est refusé en périphérie avant d'atteindre le Worker.
- **Une réputation qui se rétablit toute seule.** Les échéances de litige sont évaluées paresseusement à la lecture du score et la pénalité est toujours recalculée à partir des litiges en cours. Un programme qui ignore les litiges est fermé automatiquement et rouvre dès qu'ils sont réglés.
- **Une règle stricte tirée d'un incident.** Un import en masse a un jour utilisé une écriture de suppression puis réinsertion et effacé des données liées sans bruit. Désormais, les imports mettent les lignes à jour sur place et sont d'abord rapprochés du schéma. L'analyse et la règle sont écrites à côté du code.
- **Tout est documenté.** Décisions d'architecture, journaux de bogues, guide de traduction et politique de qualité des données vivent dans le dépôt, pour que le changement suivant parte des raisons et non de suppositions.

<!--author-->
## À propos de l'auteur

<img src="assets/wechat-qr.png" alt="QR code du compte officiel WeChat Pin海引航" width="200" align="right">

**姜芊泽 (Jiang Qianze)** est un pseudonyme. Je suis un développeur indépendant qui crée des outils, des données et de l'automatisation pour les marques, marchands et créateurs qui visent l'international. Chaque projet de ces vitrines a été conçu, construit et exploité par moi seul, de l'idée du produit jusqu'aux serveurs et à la documentation.

J'écris sur ce travail sur mon compte officiel WeChat, **Pin海引航** (en chinois). Scannez le code pour le suivre, ou retrouvez-moi sur [GitHub](https://github.com/frommmmmg).

<br clear="right">
<!--/author-->

**Autres vitrines:** [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AutoPin-CS](https://github.com/frommmmmg/AutoPin-CS-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Les captures n'utilisent que des données d'exemple ou publiques. © Tous droits réservés. Les descriptions peuvent être citées avec attribution ; le logiciel lui-même ne peut pas être redistribué.</sub>

</div>
