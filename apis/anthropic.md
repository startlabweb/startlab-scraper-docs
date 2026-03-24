# API — Anthropic (Claude)

Anthropic es la empresa que hace Claude, el modelo de IA que usa StartLab Scraper para analizar y adaptar el contenido. Es la única API **obligatoria** para que funcionen las fases 3 y 4.

---

## Para qué se usa en la app

- **Fase 3:** Claude analiza si una cuenta es relevante para el ICP de StartLab y si el contenido del video es adaptable
- **Fase 4:** Claude reescribe el guion del video adaptado al tono y estructura de StartLab

---

## Cómo crear la cuenta y obtener la API key

### 1. Crear cuenta

Ve a [console.anthropic.com](https://console.anthropic.com) y regístrate. Puedes usar Google o email.

### 2. Activar billing

Anthropic requiere que actives un método de pago antes de usar la API (incluso en el plan de prueba).

1. Ve a **Settings → Billing**
2. Agrega una tarjeta de crédito
3. Anthropic te da **$5 USD de crédito gratuito** cuando activas billing por primera vez

### 3. Crear la API key

1. Ve a **API Keys** en el menú lateral
2. Haz clic en **Create Key**
3. Dale un nombre descriptivo (ej: `startlab-scraper`)
4. Copia la key — **solo se muestra una vez**. Si la pierdes, tendrás que crear una nueva

### 4. Agregar la key en la app

Ve a **Configuración → API Keys → Anthropic** y pega la key.

---

## Planes y costos

Anthropic cobra por **tokens usados** (entrada + salida). No hay plan mensual fijo.

| Modelo | Input | Output | Uso en la app |
|--------|-------|--------|---------------|
| Claude Sonnet 4.6 | $3 / MTok | $15 / MTok | Análisis y adaptación (default) |
| Claude Haiku 4.5 | $0.80 / MTok | $4 / MTok | Opción más barata para filtros |

**Estimación de costo por run completo** (50 videos analizados, 10 adaptados):
- Análisis: ~$0.15-0.30
- Adaptación: ~$0.50-1.00
- **Total estimado: $0.65-1.30 por run**

---

## Límites y errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `401 Unauthorized` | API key inválida o expirada | Regenera la key en console.anthropic.com |
| `429 Too Many Requests` | Rate limit alcanzado | Espera unos segundos y reintenta |
| `529 Overloaded` | Servidores de Anthropic saturados | Reintenta en unos minutos |
| Sin créditos | Balance en $0 | Recarga en Settings → Billing |

---

## ¿Qué pasa si me quedo sin créditos?

Las fases 3 y 4 fallarán. La app mostrará un error de API. Los videos no serán analizados ni adaptados, pero los de fases anteriores (scraping y filtro) seguirán guardados.

Puedes recargar desde [console.anthropic.com/settings/billing](https://console.anthropic.com/settings/billing).
