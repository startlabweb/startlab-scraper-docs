# API — YouTube Data API v3

La YouTube Data API permite a StartLab Scraper buscar videos directamente en YouTube, incluyendo Shorts y videos largos, filtrando por fecha de publicación y ordenando por vistas.

---

## Para qué se usa en la app

La YouTube Data API se usa en la **Fase 1 (Scraping)** para:
- Buscar Shorts virales publicados en los últimos 30 días
- Buscar videos largos publicados en los últimos 30 días
- Filtrar por idioma (español, inglés, portugués)
- Ordenar por número de vistas

---

## Cómo crear la cuenta y obtener la API key

### 1. Acceder a Google Cloud Console

Ve a [console.cloud.google.com](https://console.cloud.google.com). Necesitas una cuenta de Google.

### 2. Crear un proyecto

1. Haz clic en el selector de proyecto (arriba a la izquierda)
2. Clic en **Nuevo proyecto**
3. Dale un nombre (ej: `startlab-scraper`)
4. Haz clic en **Crear**

### 3. Activar la YouTube Data API v3

1. En el menú, ve a **APIs y servicios → Biblioteca**
2. Busca `YouTube Data API v3`
3. Haz clic en el resultado y luego en **Habilitar**

### 4. Crear las credenciales (API Key)

1. Ve a **APIs y servicios → Credenciales**
2. Haz clic en **Crear credenciales → Clave de API**
3. Se creará la key automáticamente
4. Cópiala (puedes verla después en la lista de credenciales)

### 5. Agregar en la app

Ve a **Configuración → API Keys → YouTube** y pega la key.

---

## Cuotas diarias

La YouTube Data API tiene un límite de **10,000 unidades por día** en el plan gratuito. Cada tipo de request consume unidades:

| Operación | Costo en unidades |
|-----------|------------------|
| Búsqueda (`search.list`) | 100 unidades |
| Detalles de video (`videos.list`) | 1 unidad |

**Estimación por run:**
- 3 keywords × 20 resultados = ~300-600 unidades de búsqueda
- Un run completo consume ~500-1,000 unidades

Con el límite gratuito de 10,000 unidades puedes hacer ~10-20 runs diarios sin costo.

### ¿Qué pasa si te quedas sin cuota?

La API devuelve el error `quotaExceeded`. La app lo mostrará en los logs. La cuota se resetea automáticamente a medianoche (hora del Pacífico).

Si necesitas más cuota, puedes solicitarla en Google Cloud → Quotas, pero para la mayoría de usos el límite gratuito es más que suficiente.

---

## Errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `API key not valid` | Key mal copiada o API no habilitada | Verifica en Google Cloud Console que la API está habilitada |
| `quotaExceeded` | Se agotaron las 10,000 unidades diarias | Espera hasta mañana o solicita más cuota |
| Sin resultados | Keywords muy específicas en el período de 30 días | Prueba con otras keywords |
| Videos en idioma incorrecto | Keywords en inglés atrajeron resultados en hindi/bengalí | Normal, el filtro de idioma de la app lo maneja |

---

## ¿Es obligatorio?

No. Si no configuras la API de YouTube, la app simplemente no scrapeará YouTube. Las fases de IG y TikTok funcionan independientemente.
