<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · Deutsch · [Français](README.fr.md)

</div>

> **Dieses Repository ist ein Schaufenster, keine Quellcode-Veröffentlichung.** AffProof ist ein privates Projekt, deshalb gibt es hier keinen Code, nur was es kann, wie es gebaut ist und wie es aussieht. Wenn du darüber sprechen möchtest, melde dich über mein [GitHub-Profil](https://github.com/frommmmmg).

**Ein öffentliches, mehrsprachiges Verzeichnis, das Partnerprogramme prüft, damit man weiß, welche wirklich zahlen.** Jeder Eintrag enthält ein belegbasiertes Prüfprofil, Community-Bewertungen, Auszahlungsnachweise und eine Streitfall-Historie.

![AffProof-Architektur](assets/affproof-architecture.svg)

**Highlights**

- **Serverless am Edge.** Die ganze Seite läuft auf Cloudflare Workers mit D1-Datenbank (SQLite), statische Dateien kommen direkt vom Edge. Es gibt keinen dauerhaft laufenden Serverprozess, den man betreuen müsste.
- **Serverseitiges Rendering für die Suche.** Seiten werden im Worker gerendert, mit JSON-LD-Strukturdaten, `hreflang`-Tags und einer Sitemap pro Sprache.
- **8 Sprachen**, mit einem Übersetzungsablauf, der alle Sprachen mit dem englischen Original abgleicht.
- **Gestufte öffentliche API.** Schlüssel werden als SHA-256-Hashes gespeichert und in einer Middleware geprüft. Free, Pro und Enterprise steuern Paginierungslimits und zurückgegebene Felder.
- **Daten mit Belegpflicht.** Einträge durchlaufen vor dem Import eine Bewertung und eine Prüfschranke, und Datenbankschreibzugriffe sind so gestaltet, dass keine Daten unbemerkt verloren gehen.
- **Dynamische SVG-Badges**, die andere Seiten einbetten können.
- **Dokumentierte Entscheidungen.** Architekturentscheidungen und Fehler-Nachbetrachtungen liegen beim Code.

**Technik:** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

## Screenshots

![Öffentliche Startseite der Live-Seite](assets/affproof-home.png)
*Öffentliche Startseite der Live-Seite*

![Eine Prüfprofil-Seite der Live-Seite](assets/affproof-dossier.png)
*Eine Prüfprofil-Seite der Live-Seite*

## So funktioniert es

![Jeder Eintrag durchläuft eine Beleg-Schranke, bevor er importiert und übersetzt wird.](assets/affproof-evidence-pipeline.svg)
*Jeder Eintrag durchläuft eine Beleg-Schranke, bevor er importiert und übersetzt wird.*

![Die öffentliche API wird zuerst am Edge geschützt, dann im Worker per Schlüssel- und Tarifprüfung.](assets/affproof-api-flow.svg)
*Die öffentliche API wird zuerst am Edge geschützt, dann im Worker per Schlüssel- und Tarifprüfung.*

---

<div align="center">

<sub>Screenshots verwenden nur Beispiel- oder öffentliche Daten. © Alle Rechte vorbehalten. Beschreibungen dürfen mit Quellenangabe zitiert werden; die Software selbst darf nicht weitergegeben werden.</sub>

</div>
