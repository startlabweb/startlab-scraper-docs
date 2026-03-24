# API — ScrapeCreators

ScrapeCreators es el proveedor principal de scraping para Instagram y TikTok. Es más rápido que Apify para la mayoría de búsquedas y es el proveedor recomendado para uso regular.

---

## Para qué se usa en la app

ScrapeCreators se usa en la **Fase 1 (Scraping)** para:
- Buscar posts de Instagram por hashtags
- Buscar videos de TikTok por keywords
- Obtener detalles de videos a partir de URLs encontradas por Bright Data

---

## Cómo crear la cuenta y obtener la API key

### 1. Crear cuenta

Ve a [scrapecreators.com](https://scrapecreators.com) y regístrate con email.

### 2. Obtener el API key

1. Una vez dentro, ve a tu **Dashboard** o **Account**
2. Encuentra la sección **API Key**
3. Copia la key

### 3. Agregar la key en la app

Ve a **Configuración → API Keys → ScrapeCreators** y pega la key.

---

## Planes y límites

ScrapeCreators cobra por **número de requests** realizadas.

| Plan | Precio | Requests incluidas |
|------|--------|-------------------|
| Free | $0 | Limitado (prueba) |
| Basic | ~$29/mes | ~5,000 requests |
| Pro | ~$99/mes | ~25,000 requests |

**Estimación de uso por run:**
- Cada video scrapeado = 1 request aproximadamente
- Un run de 50 videos = ~50-100 requests

---

## Errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `401` / Unauthorized | API key inválida | Verifica que copiaste la key completa |
| `429` / Rate limit | Demasiadas requests en poco tiempo | La app maneja esto automáticamente con reintentos |
| Sin resultados | Hashtag con poco volumen o keyword muy específica | Usa keywords más amplias |
| `402` / Payment required | Plan expirado o sin créditos | Renueva el plan en scrapecreators.com |

---

## Comparación con Apify

Ver tabla comparativa en [APIs — Apify](apify.md#apify-o-scrapecreators).
