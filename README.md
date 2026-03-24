# StartLab Scraper — Documentación

Bienvenido a la documentación completa de **StartLab Scraper**, la herramienta de inteligencia de contenido que extrae, filtra y adapta videos virales de Instagram, TikTok y YouTube al universo de StartLab.

---

## Índice

| # | Documento | Qué cubre |
|---|-----------|-----------|
| 1 | [¿Qué es StartLab Scraper?](01-que-es.md) | Qué hace la app, el pipeline completo, para qué sirve |
| 2 | [Setup inicial](02-setup.md) | Cómo configurar la app desde cero (Supabase, Vercel, variables de entorno) |
| 3 | [APIs — Anthropic](apis/anthropic.md) | Claude API: cómo crear cuenta, obtener key, planes |
| 4 | [APIs — Apify](apis/apify.md) | Apify: cuenta, token, actores que usa la app, créditos |
| 5 | [APIs — ScrapeCreators](apis/scrapecreators.md) | ScrapeCreators: cuenta, token, planes, límites |
| 6 | [APIs — Bright Data](apis/brightdata.md) | Bright Data SERP: cuenta, API key, créditos |
| 7 | [APIs — YouTube](apis/youtube.md) | YouTube Data API v3: Google Cloud, cuotas diarias |
| 8 | [APIs — Notion](apis/notion.md) | Cómo conectar Notion con la app |
| 9 | [Modos de scraping](04-modos-scraping.md) | Los 4 modos: cuándo usar cuál, qué APIs necesitas |
| 10 | [Cómo funcionan los prompts](05-prompts.md) | Fases, variables, cómo modificar, ejemplos |
| 11 | [Vercel — Free vs Pro](06-vercel.md) | Límites, qué necesitas pagar, cómo funciona el deploy |
| 12 | [El Pipeline — fase a fase](07-pipeline.md) | Qué hace cada fase, qué consume, cuánto tarda |
| 13 | [Errores comunes](08-errores-comunes.md) | Troubleshooting: síntomas, causas, soluciones |

---

## Antes de empezar

StartLab Scraper requiere:

- Una cuenta en **Supabase** (base de datos + autenticación)
- Un deploy en **Vercel** (hosting del frontend y backend)
- Al menos una API de scraping activa (**ScrapeCreators** o **Apify**)
- La API de **Anthropic** (Claude) para las fases de análisis y adaptación

Las APIs opcionales (Bright Data, YouTube, Notion) amplían las capacidades pero no son obligatorias para que la app funcione.

---

## ¿Tienes un problema?

Ve directamente a [Errores comunes](08-errores-comunes.md) — ahí están los errores más frecuentes con su causa y solución.
