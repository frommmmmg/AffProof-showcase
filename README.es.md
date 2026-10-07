<div align="center">

# AffProof

[English](README.md) · [中文](README.zh.md) · Español · [Deutsch](README.de.md) · [Français](README.fr.md)

🌐 **[affproof.com](https://affproof.com)** · [GitHub @frommmmmg](https://github.com/frommmmmg)

✍️ Por **姜芊泽 (Jiang Qianze)** · cuenta oficial de WeChat: **Pin海引航**

</div>

> **Este repositorio es un escaparate, no una publicación de código.** AffProof no es de código abierto, así que aquí no hay código: solo qué hace, cómo está construido y qué aspecto tiene. Si quieres hablar de él, escríbeme desde mi [perfil de GitHub](https://github.com/frommmmmg).

**Un directorio público y multilingüe que investiga los programas de afiliados para saber cuáles pagan de verdad.** Cada ficha incluye un expediente de diligencia debida con pruebas, una puntuación de reputación, comprobantes de pago y un historial de disputas.

El marketing de afiliación está lleno de programas que parecen generosos en su página de aterrizaje y dejan de pagar discretamente cuando creces. La mayoría de los directorios copia lo que dice el propio proveedor. AffProof parte del otro extremo: registra lo que se puede comprobar (la página real del programa, los canales de pago que de verdad se ofrecen, las condiciones de comisión por escrito) y deja que la comunidad aporte lo que solo ella sabe, como si el dinero llegó. El lema es *Proof of payout. Zero fluff.*

![Arquitectura](assets/affproof-architecture.svg)

| | |
|---|---|
| **Sitio web** | **[affproof.com](https://affproof.com)**, en 8 idiomas |
| **Mi papel** | Diseñado, construido y operado por una sola persona: producto, canalización de datos, front end, back end en el borde y operaciones |
| **Estado** | En producción |
| **Escala** | 380 programas indexados, 377 con expediente auditado completo (octubre de 2026) |
| **Tecnología** | Cloudflare Workers · Hono · D1 · Workers Assets · GitHub Actions |

### Qué hace

**Para webmasters**
- **Encontrar rápido el programa adecuado.** Búsqueda en vivo con filtros por plataforma, canal de pago y rango de tiempo, cuatro órdenes (recomendado, clics, subida de ranking, pruebas) y un filtro de auditoría oro.
- **Una cuadrícula de canales estricta en vez de eslóganes.** Cada tarjeta muestra los mismos huecos fijos para USDT, PayPal, Payoneer, Stripe y canales de contacto, iluminados si existen y tachados si no, así las tarjetas se alinean y nada se puede maquillar.
- **Reputación legible.** Una puntuación sobre 1000 que sale del expediente, de una ventana móvil de 30 días de pruebas de pago y reseñas, de la actividad con decaimiento y de penalizaciones por disputas que el proveedor no respondió en 48 horas. Un proveedor que resuelve sus disputas se recupera solo.
- **Dos temas de interfaz completos, con cambio en vivo:** un diseño denso en negro y dorado y otro de arcade de píxeles de 8 bits con sonido opcional. Un selector de ancho (1200, 768 y 390 px) previsualiza tamaños de tableta y móvil.

**Para proveedores**
- **Reclamar una ficha en unos diez segundos** e incrustar en su sitio una insignia SVG dinámica *Verified by AffProof*.

**Para buscadores y desarrolladores**
- **Renderizado en servidor pensado para buscadores.** Las páginas se generan dentro del Worker, con datos estructurados JSON-LD, etiquetas `hreflang` y un sitemap por idioma.
- **8 idiomas**, con un flujo de traducción que mantiene todos los idiomas alineados con el original en inglés.
- **Una API pública con planes.** Las claves se guardan como hashes SHA-256 y se validan en un middleware. Los planes Free, Pro y Enterprise controlan los límites de paginación y los campos devueltos.

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

<!--notes-->
## Notas de ingeniería

- **Nativo del borde por decisión, no por moda.** No hay VPS, ni contenedores, ni procesos permanentes. El razonamiento está escrito como registro de decisión de arquitectura: cero arranque en frío, escala global y un coste en reposo casi nulo.
- **Dos capas de protección de la API.** Las reglas del borde frenan primero los escaneos y las avalanchas; después el Worker comprueba la clave con hash, aplica la cuota del plan y devuelve solo los campos que ese plan puede ver. Las listas usan paginación por cursor, nunca `OFFSET` profundo.
- **Operaciones tras Zero Trust.** La administración y la automatización están tras Cloudflare Access con tokens de servicio, de modo que el tráfico no autorizado se rechaza en el borde antes de llegar al Worker.
- **Reputación que se recupera sola.** Los plazos de las disputas se evalúan de forma perezosa al leer la puntuación y la penalización se recalcula siempre con las disputas actuales. Un programa que ignora las disputas se cierra automáticamente y se reabre cuando se resuelven.
- **Una regla dura aprendida de un incidente.** Una importación masiva usó una escritura de borrar y reinsertar y eliminó datos relacionados sin avisar. Ahora las importaciones actualizan las filas en su sitio y se concilian antes con el esquema. El análisis y la regla están escritos junto al código.
- **Todo está documentado.** Decisiones de arquitectura, registros de errores, una guía de traducción y una política de calidad de datos viven en el repositorio, para que el siguiente cambio parta de las razones y no de suposiciones.

<!--author-->
## Sobre el autor

<img src="assets/wechat-qr.png" alt="Código QR de la cuenta oficial de WeChat Pin海引航" width="200" align="right">

**姜芊泽 (Jiang Qianze)** es un seudónimo. Soy un desarrollador independiente que crea herramientas, datos y automatización para marcas, comerciantes y creadores que salen al mercado global. Cada proyecto de estas muestras lo he diseñado, construido y operado yo solo, desde la idea de producto hasta los servidores y la documentación.

Escribo sobre este trabajo en mi cuenta oficial de WeChat, **Pin海引航** (en chino). Escanea el código para seguirla, o encuéntrame en [GitHub](https://github.com/frommmmmg).

<br clear="right">
<!--/author-->

**Otras muestras:** [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AutoPin-CS](https://github.com/frommmmmg/AutoPin-CS-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Las capturas usan solo datos de ejemplo o públicos. © Todos los derechos reservados. Las descripciones pueden citarse con atribución; el software no se puede redistribuir.</sub>

</div>
