# API — Bright Data (SERP)

Bright Data es un servicio de scraping de resultados de búsqueda de Google. StartLab Scraper lo usa para descubrir URLs de videos de TikTok e Instagram buscando en Google en lugar de buscar directamente en las plataformas.

---

## Para qué se usa en la app

Bright Data se usa en la **Fase 1 (Scraping)** en los modos **BD + SC** y **BD + Apify**:

1. La app hace una búsqueda en Google del tipo `site:tiktok.com video "sistema predecible"`
2. Bright Data devuelve los resultados de Google (URLs de videos)
3. Esas URLs se pasan a ScrapeCreators o Apify para obtener los detalles del video

Este enfoque funciona bien porque Google ya ha indexado y ordenado los videos más relevantes.

---

## Cómo crear la cuenta y obtener la API key

### 1. Crear cuenta

Ve a [brightdata.com](https://brightdata.com) y regístrate. Requiere verificación de empresa o uso legítimo.

### 2. Activar el producto SERP API

1. En el dashboard, ve a **Products → SERP API**
2. Si no lo ves activo, haz clic en **Start free trial**
3. Ve a **Settings** del producto SERP API
4. Copia el **API Token** o las credenciales de acceso

### 3. Obtener el Customer ID y el token

Bright Data usa un formato especial de autenticación:
```
usuario: tu-customer-id
password: tu-password-de-zona
```

O en algunos casos un token Bearer. Revisa la sección **Access Parameters** del producto.

### 4. Agregar en la app

Ve a **Configuración → API Keys → Bright Data** y pega el token.

---

## Planes y costos

Bright Data cobra por **GB de datos transferidos** o por número de requests SERP.

| Plan | Precio | Incluye |
|------|--------|---------|
| Pay as you go | ~$1.50 / 1,000 resultados | Sin mínimo |
| Business | Desde $500/mes | Volume pricing |

Para el uso de StartLab Scraper (scraping periódico, no masivo), el plan pay-as-you-go es suficiente. Un run completo consume centavos en SERP.

---

## Errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `401` / Unauthorized | Credenciales incorrectas | Verifica el token en el dashboard de Bright Data |
| Sin resultados | Google no encontró videos con esa keyword | Prueba con keywords más populares |
| `402` | Sin créditos | Recarga en brightdata.com |
| Resultados irrelevantes | La query SERP no fue específica | Normal, el filtro por vistas descarta los irrelevantes |

---

## ¿Es obligatorio?

No. Bright Data solo es necesario si usas los modos **BD + SC** o **BD + Apify**. Si usas **Solo ScrapeCreators** o **Solo Apify**, no necesitas Bright Data.
