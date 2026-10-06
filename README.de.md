<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · Deutsch · [Français](README.fr.md)

</div>

> **Dieses Repository ist ein Schaufenster, keine Quellcode-Veröffentlichung.** AffProof ist ein privates Projekt, deshalb gibt es hier keinen Code, nur was es kann, wie es gebaut ist und wie es aussieht. Wenn du darüber sprechen möchtest, melde dich über mein [GitHub-Profil](https://github.com/frommmmmg).

**Ein öffentliches, mehrsprachiges Verzeichnis, das Partnerprogramme prüft, damit man weiß, welche wirklich zahlen.** Jeder Eintrag enthält ein belegbasiertes Prüfprofil, einen Reputationswert, Auszahlungsnachweise und eine Streitfall-Historie.

![Die Architektur: Edge-Filter, ein Hono-Worker und D1.](assets/affproof-architecture.svg)

**Highlights**

- **Serverless am Edge.** Die ganze Seite läuft auf Cloudflare Workers mit D1-Datenbank (SQLite), statische Dateien kommen direkt vom Edge. Es gibt keinen dauerhaft laufenden Serverprozess, den man betreuen müsste.
- **Zwei vollständige Oberflächen-Themes, live umschaltbar.** Ein dichtes Schwarz-Gold-Layout und ein 8-Bit-Pixel-Arcade-Skin, mit optionalen Soundeffekten. Ein Breitenschalter (1200, 768 und 390 px) zeigt Tablet- und Handy-Größen.
- **Gebaut, um schnell das passende Programm zu finden.** Live-Suche mit Filtern für Plattform, Auszahlungskanal und Zeitraum, vier Sortierungen (empfohlen, Klicks, Rang-Anstieg, Nachweise) und einem Gold-Audit-Filter.
- **Ein strenges Kanalraster statt Werbeversprechen.** Jede Karte zeigt dieselben festen Felder für USDT, PayPal, Payoneer, Stripe und Kontaktkanäle, hell wenn vorhanden und durchgestrichen wenn nicht, damit alles bündig bleibt und nichts beschönigt werden kann.
- **Lesbare Reputation.** Ein Wert von 1000, verifizierte Auszahlungsnachweise und ein öffentliches 48-Stunden-Streitfenster statt erfundener Annahmequoten.
- **Serverseitiges Rendering für die Suche.** Seiten werden im Worker gerendert, mit JSON-LD-Strukturdaten, `hreflang`-Tags und einer Sitemap pro Sprache.
- **8 Sprachen**, mit einem Übersetzungsablauf, der alle Sprachen mit dem englischen Original abgleicht.
- **Eine öffentliche API mit Tarifen.** Schlüssel werden als SHA-256-Hashes gespeichert und in einer Middleware geprüft. Free, Pro und Enterprise steuern Paginierungslimits und zurückgegebene Felder.
- **Daten mit Belegpflicht.** Jedes Prüfprofil durchläuft vor dem Import eine Bewertung und eine Qualitätsschranke, und Datenbankschreibzugriffe sind so gestaltet, dass keine Daten unbemerkt verloren gehen.
- **Dynamische SVG-Badges**, die andere Seiten einbetten können, und **dokumentierte Entscheidungen**: Architekturentscheidungen und Fehler-Nachbetrachtungen liegen beim Code.

**Technik:** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

**In Zahlen (Oktober 2026):** 380 Programme erfasst, davon 377 mit vollständigem geprüftem Profil, in 8 Sprachen.

## Screenshots

![Die Startseite im Standard-Theme Schwarz-Gold.](assets/affproof-home.jpg)
*Die Startseite im Standard-Theme Schwarz-Gold.*

![Das Programmverzeichnis: Filter, Sortierungen und das feste Kanalraster.](assets/affproof-matrix.jpg)
*Das Programmverzeichnis: Filter, Sortierungen und das feste Kanalraster.*

![Dieselben Seiten im 8-Bit-Arcade-Theme.](assets/affproof-arcade-home.jpg)

![Dieselben Seiten im 8-Bit-Arcade-Theme.](assets/affproof-arcade-matrix.jpg)
*Dieselben Seiten im 8-Bit-Arcade-Theme.*

![Eine Prüfprofil-Seite samt Abschnitt zu Geschäftsbedingungen und Traffic.](assets/affproof-dossier.jpg)

![Eine Prüfprofil-Seite samt Abschnitt zu Geschäftsbedingungen und Traffic.](assets/affproof-dossier-seo.jpg)
*Eine Prüfprofil-Seite samt Abschnitt zu Geschäftsbedingungen und Traffic.*

![Die Startseite auf Chinesisch und Deutsch.](assets/affproof-languages.jpg)
*Die Startseite auf Chinesisch und Deutsch.*

![Auf dem Handy: Suche und Filter sowie eine Programmkarte.](assets/affproof-mobile.jpg)
*Auf dem Handy: Suche und Filter sowie eine Programmkarte.*

## So funktioniert es

![Jeder Eintrag durchläuft eine Beleg-Schranke, bevor er importiert und übersetzt wird.](assets/affproof-evidence-pipeline.svg)
*Jeder Eintrag durchläuft eine Beleg-Schranke, bevor er importiert und übersetzt wird.*

![Die öffentliche API wird zuerst am Edge geschützt, dann im Worker per Schlüssel- und Tarifprüfung.](assets/affproof-api-flow.svg)
*Die öffentliche API wird zuerst am Edge geschützt, dann im Worker per Schlüssel- und Tarifprüfung.*

![Ein Worker rendert alle Sprachen.](assets/affproof-locale-render.svg)
*Ein Worker rendert alle Sprachen.*

---

<div align="center">

<sub>Screenshots verwenden nur Beispiel- oder öffentliche Daten. © Alle Rechte vorbehalten. Beschreibungen dürfen mit Quellenangabe zitiert werden; die Software selbst darf nicht weitergegeben werden.</sub>

</div>
