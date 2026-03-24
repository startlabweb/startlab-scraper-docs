# API — Apify

Apify es una plataforma de scraping web que StartLab Scraper usa como proveedor alternativo para extraer videos de Instagram y TikTok. Es especialmente útil cuando ScrapeCreators no encuentra resultados o cuando quieres buscar por hashtags directamente.

---

## Para qué se usa en la app

Apify se usa en la **Fase 1 (Scraping)** dependiendo del modo de scraping configurado:

- **BD + Apify:** Bright Data encuentra las URLs, Apify obtiene los detalles de cada video
- **Solo Apify:** Apify hace todo — búsqueda y extracción de datos

Los actores (scrapers) que usa la app son:
- `clockworks/tiktok-scraper` — para búsqueda en TikTok por palabras clave
- `apify/instagram-scraper` — para búsqueda en Instagram por hashtags

---

## Cómo crear la cuenta y obtener la API key

### 1. Crear cuenta

Ve a [apify.com](https://apify.com) y regístrate. Puedes usar Google o email.

### 2. Obtener el API token

1. Una vez dentro, ve a **Settings → Integrations**
2. Copia el valor de **Personal API tokens**
3. Si no ves ninguno, haz clic en **Create new token**

### 3. Agregar la key en la app

Ve a **Configuración → API Keys → Apify** y pega el token.

---

## Planes y créditos

Apify funciona con un sistema de **créditos (compute units)**. Los actores de TikTok e Instagram son actores de pago.

| Plan | Precio | Créditos incluidos |
|------|--------|--------------------|
| Free | $0 | $5 USD de crédito inicial |
| Starter | $49/mes | $49 en créditos |
| Scale | $499/mes | $499 en créditos |

**Costo estimado por búsqueda:**
- TikTok (100 videos): ~$0.10-0.20
- Instagram (50 posts): ~$0.05-0.15

El plan Free alcanza para probar, pero para uso regular el Starter ($49/mes) es suficiente.

---

## Error: "no hay suficientes créditos"

Si ves el error `Apify sin créditos suficientes`, significa que tu balance llegó a $0.

Para recargar:
1. Ve a [console.apify.com/billing](https://console.apify.com/billing)
2. Agrega créditos (mínimo $10)
3. Reintenta el run

---

## Límites y errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `401` / token inválido | Token expirado o mal copiado | Regenera en Settings → Integrations |
| Sin resultados TikTok | La búsqueda no encontró videos | Prueba con otras keywords |
| Sin resultados Instagram | El hashtag tiene muy poco volumen | Usa keywords más populares |
| `not-enough-usage-to-run-paid-actor` | Sin créditos | Recarga en console.apify.com/billing |
| Timeout después de 2 min | El actor tardó demasiado | Normal en primeras búsquedas; reintenta |

---

## ¿Apify o ScrapeCreators?

| | Apify | ScrapeCreators |
|---|-------|---------------|
| TikTok | Búsqueda directa por keywords | Búsqueda por URL/perfil |
| Instagram | Búsqueda por hashtag | Búsqueda por hashtag/perfil |
| Setup | Más simple | Requiere más configuración |
| Costo | Por uso (créditos) | Por uso o suscripción |
| Velocidad | Moderada | Rápida |

Para la mayoría de casos, **ScrapeCreators es más rápido**. Usa Apify si SC falla o si quieres búsqueda directa por keywords en TikTok.
