# Modos de Scraping

StartLab Scraper tiene 4 modos de scraping para Instagram y TikTok. Cada modo combina diferentes APIs y tiene sus propias ventajas. El modo se configura en **Configuración → Umbrales → Modo de scraping**.

> YouTube siempre usa su propia API directamente, independientemente del modo elegido.

---

## Los 4 modos

### Modo 1: BD + ScrapeCreators (recomendado)

**Qué hace:** Bright Data busca las URLs en Google, ScrapeCreators obtiene los detalles.

**Flujo:**
1. Bright Data hace búsquedas en Google (`site:tiktok.com video "keyword"`)
2. Google devuelve las URLs más relevantes de TikTok/Instagram
3. ScrapeCreators obtiene los datos de cada video (vistas, caption, etc.)

**Cuándo usarlo:** Es el modo por defecto. Funciona bien cuando tienes ambas APIs activas y quieres resultados rápidos y relevantes.

**APIs necesarias:** Bright Data + ScrapeCreators

**Pros:**
- Google filtra el contenido más relevante antes de que lo procese la app
- ScrapeCreators es rápido para obtener detalles
- Menor consumo de créditos que Solo ScrapeCreators

**Contras:**
- Requiere 2 APIs activas
- Puede fallar si Google no indexó bien los videos recientes

---

### Modo 2: BD + Apify

**Qué hace:** Bright Data busca las URLs en Google, Apify obtiene los detalles.

**Flujo:**
1. Bright Data hace búsquedas en Google
2. Google devuelve las URLs de TikTok/Instagram
3. Apify obtiene los datos de cada video usando sus actores especializados

**Cuándo usarlo:** Cuando tienes Apify activo pero no ScrapeCreators, o cuando SC está fallando.

**APIs necesarias:** Bright Data + Apify

**Pros:** Similar a BD + SC pero usa Apify como extractor

**Contras:** Apify puede ser más lento en algunos casos

---

### Modo 3: Solo Apify

**Qué hace:** Apify hace todo — búsqueda directa por keywords en TikTok e Instagram.

**Flujo:**
1. La app pasa las keywords a Apify directamente
2. Apify busca en TikTok usando el actor `clockworks/tiktok-scraper`
3. Apify busca en Instagram usando hashtags con `apify/instagram-scraper`

**Cuándo usarlo:**
- Cuando no tienes Bright Data
- Cuando quieres buscar directamente en las plataformas sin pasar por Google
- Cuando los modos BD no encuentran suficientes resultados

**APIs necesarias:** Solo Apify

**Pros:**
- Un solo proveedor
- Búsqueda directa en las plataformas
- No depende de la indexación de Google

**Contras:**
- Apify cobra por cada búsqueda (más caro para muchas keywords)
- Los resultados pueden incluir contenido menos relevante

---

### Modo 4: Solo ScrapeCreators

**Qué hace:** ScrapeCreators hace todo — busca y extrae directamente.

**Flujo:**
1. ScrapeCreators busca por hashtags en Instagram y TikTok
2. Retorna los posts con sus datos

**Cuándo usarlo:** Cuando no tienes Bright Data ni Apify y solo quieres usar SC.

**APIs necesarias:** Solo ScrapeCreators

---

## Tabla comparativa

| Modo | APIs necesarias | Velocidad | Costo | Calidad de resultados |
|------|----------------|-----------|-------|----------------------|
| BD + SC | Bright Data + SC | Rápido | Bajo | Alta (Google filtra) |
| BD + Apify | Bright Data + Apify | Moderado | Bajo | Alta (Google filtra) |
| Solo Apify | Apify | Moderado | Medio | Moderada |
| Solo SC | ScrapeCreators | Rápido | Bajo | Moderada |

---

## ¿Cuál elijo?

**Si tienes todas las APIs:** usa **BD + SC**

**Si solo tienes Apify:** usa **Solo Apify**

**Si solo tienes SC:** usa **Solo SC**

**Si los resultados son pocos:** prueba cambiar de modo y compara

---

## Cómo cambiar el modo

1. Ve a **Configuración**
2. Pestaña **Umbrales**
3. En **Modo de scraping**, selecciona el modo
4. Haz clic en **Guardar**

El cambio aplica en el próximo run.
