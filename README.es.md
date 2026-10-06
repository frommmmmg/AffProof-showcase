<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · Español · [Deutsch](README.de.md) · [Français](README.fr.md)

</div>

> **Este repositorio es un escaparate, no una publicación de código.** AffProof es un proyecto privado, así que aquí no hay código: solo qué hace, cómo está construido y qué aspecto tiene. Si quieres hablar de él, escríbeme desde mi [perfil de GitHub](https://github.com/frommmmmg).

**Un directorio público y multilingüe que investiga los programas de afiliados para saber cuáles pagan de verdad.** Cada ficha incluye un expediente de diligencia debida con pruebas, una puntuación de reputación, comprobantes de pago y un historial de disputas.

![La arquitectura: filtrado en el borde, un Worker de Hono y D1.](assets/affproof-architecture.svg)

**Puntos clave**

- **Serverless en el borde.** Todo el sitio corre en Cloudflare Workers con base de datos D1 (SQLite) y archivos estáticos servidos desde el borde. No hay ningún proceso de servidor permanente que mantener.
- **Dos temas de interfaz completos, con cambio en vivo.** Un diseño denso en negro y dorado y otro de arcade de píxeles de 8 bits, con efectos de sonido opcionales. Un selector de ancho (1200, 768 y 390 px) previsualiza tamaños de tableta y móvil.
- **Pensado para encontrar rápido el programa adecuado.** Búsqueda en vivo con filtros por plataforma, canal de pago y rango de tiempo, cuatro órdenes (recomendado, clics, subida de ranking, pruebas) y un filtro de auditoría oro.
- **Una cuadrícula de canales estricta en vez de eslóganes.** Cada tarjeta muestra los mismos huecos fijos para USDT, PayPal, Payoneer, Stripe y canales de contacto, iluminados si existen y tachados si no, así las tarjetas se alinean y nada se puede maquillar.
- **Reputación legible.** Una puntuación sobre 1000, registros de pago verificados y una ventana pública de disputa de 48 horas, en lugar de tasas de aprobación inventadas.
- **Renderizado en servidor pensado para buscadores.** Las páginas se generan dentro del Worker, con datos estructurados JSON-LD, etiquetas `hreflang` y un sitemap por idioma.
- **8 idiomas**, con un flujo de traducción que mantiene todos los idiomas alineados con el original en inglés.
- **Una API pública con planes.** Las claves se guardan como hashes SHA-256 y se validan en un middleware. Los planes Free, Pro y Enterprise controlan los límites de paginación y los campos devueltos.
- **Datos con puertas de evidencia.** Cada expediente pasa una puntuación y un control de calidad antes de importarse, y las escrituras en la base de datos están diseñadas para no perder datos en silencio.
- **Insignias SVG dinámicas** que otros sitios pueden incrustar, y **decisiones documentadas**: los registros de arquitectura y los análisis de errores viven junto al código.

**Tecnología:** Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions

**En cifras (octubre de 2026):** 380 programas indexados, 377 de ellos con expediente auditado completo, en 8 idiomas.

## Capturas

![La página de inicio con el tema negro y dorado por defecto.](assets/affproof-home.jpg)
*La página de inicio con el tema negro y dorado por defecto.*

![El directorio de programas: filtros, órdenes y la cuadrícula fija de canales.](assets/affproof-matrix.jpg)
*El directorio de programas: filtros, órdenes y la cuadrícula fija de canales.*

![Las mismas páginas con el tema arcade de 8 bits.](assets/affproof-arcade-home.jpg)

![Las mismas páginas con el tema arcade de 8 bits.](assets/affproof-arcade-matrix.jpg)
*Las mismas páginas con el tema arcade de 8 bits.*

![Una ficha de diligencia debida, con su sección de condiciones comerciales y tráfico.](assets/affproof-dossier.jpg)

![Una ficha de diligencia debida, con su sección de condiciones comerciales y tráfico.](assets/affproof-dossier-seo.jpg)
*Una ficha de diligencia debida, con su sección de condiciones comerciales y tráfico.*

![La página de inicio en chino y alemán.](assets/affproof-languages.jpg)
*La página de inicio en chino y alemán.*

![En el móvil: búsqueda y filtros, y una tarjeta de programa.](assets/affproof-mobile.jpg)
*En el móvil: búsqueda y filtros, y una tarjeta de programa.*

## Cómo funciona

![Cada ficha pasa una puerta de evidencia antes de importarse y traducirse.](assets/affproof-evidence-pipeline.svg)
*Cada ficha pasa una puerta de evidencia antes de importarse y traducirse.*

![La API pública se protege primero en el borde y después con comprobaciones de clave y plan en el Worker.](assets/affproof-api-flow.svg)
*La API pública se protege primero en el borde y después con comprobaciones de clave y plan en el Worker.*

![Un solo Worker genera todos los idiomas.](assets/affproof-locale-render.svg)
*Un solo Worker genera todos los idiomas.*

---

<div align="center">

<sub>Las capturas usan solo datos de ejemplo o públicos. © Todos los derechos reservados. Las descripciones pueden citarse con atribución; el software no se puede redistribuir.</sub>

</div>
