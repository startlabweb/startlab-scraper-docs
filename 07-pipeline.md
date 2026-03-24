# El Pipeline — Fase a Fase

El pipeline de StartLab Scraper ejecuta 5 fases en secuencia. Cada fase toma el output de la anterior y lo procesa.

---

## Vista general

```
Fase 1: Scraping     → Encuentra videos en IG, TikTok, YouTube
    ↓
Fase 2: Filtro       → Descarta los que no alcanzan el mínimo de vistas
    ↓
Fase 3: Análisis IA  → Evalúa relevancia de cuenta y contenido
    ↓
Fase 4: Adaptación   → Reescribe guiones para StartLab
    ↓
Fase 5: Guardado     → Salva resultados y envía a Notion (si está configurado)
```

---

## Fase 1 — Scraping

**Qué hace:** Busca videos en las plataformas configuradas usando las keywords y perfiles definidos en Configuración.

**APIs que usa:**
- Instagram/TikTok: depende del modo de scraping (ver [Modos de scraping](04-modos-scraping.md))
- YouTube: YouTube Data API v3

**Configurable desde:**
- Configuración → Keywords (español e inglés)
- Configuración → Perfiles de IG/TikTok a monitorear
- Configuración → Umbrales → Máximo videos por keyword

**Parámetros importantes:**
- Videos de YouTube: máximo 30 días de antigüedad
- Videos de IG/TikTok: depende del filtro de Bright Data (últimos 6 días aprox.)

**Salida:** Lista de videos con URL, cuenta, vistas, caption, thumbnail

---

## Fase 2 — Filtro por Vistas

**Qué hace:** Descarta todos los videos que no alcanzan el mínimo de vistas configurado.

**APIs que usa:** Ninguna (lógica interna)

**Configurable desde:**
- Configuración → Umbrales → Vistas mínimas (por defecto: 50,000)

**Por qué existe:** No tiene sentido analizar con IA videos que nadie vio. Solo los videos virales probaron tener tracción.

**Salida:** Lista filtrada de videos (solo los que superaron el umbral)

---

## Fase 3 — Análisis con IA

**Qué hace:** Para cada video filtrado, ejecuta dos análisis:

1. **Filtro de cuentas:** ¿La cuenta que publicó el video es relevante para el ICP de StartLab? (coach, consultor, agencia, infoproductor que habla de escalar)

2. **Filtro de contenido:** ¿El video en sí es adaptable? ¿Toca dolores del ICP? ¿La estructura es replicable?

**APIs que usa:** Anthropic (Claude)

**Configurable desde:**
- Configuración → Prompts → Filtro de Cuentas
- Configuración → Prompts → Filtro de Contenido
- Configuración → Modelos → Fase 3

**Salida:** Lista de videos con análisis de relevancia (score 1-10, razón, categoría, temas)

---

## Fase 4 — Adaptación

**Qué hace:** Para cada video que pasó la Fase 3, Claude reescribe el guion completo adaptado a StartLab.

**El output por cada video incluye:**
- `hook_adaptado` — El gancho reescrito para el ICP de StartLab
- `hook_variantes` — 3 variantes del hook con diferentes ángulos
- `guion_adaptado` — Guion completo listo para grabar
- `formula_estructura` — Explicación de la fórmula narrativa usada
- `estilo_produccion` — Instrucciones de producción (plano, ritmo, música, paleta)
- `notas_grabacion` — 3 tips para grabar el video
- `por_que_funciona` — Por qué esta adaptación funcionará para el ICP
- `carrusel` — Slides listos para diseñar como carrusel

**APIs que usa:** Anthropic (Claude)

**Configurable desde:**
- Configuración → Prompts → Adaptación (el más importante)
- Configuración → Modelos → Fase 4
- Campo "Instrucción personalizada" al iniciar un run (agrega instrucciones extras para ese run específico)

**Salida:** Lista de videos con adaptación completa

---

## Fase 5 — Guardado

**Qué hace:** Guarda todos los resultados en Supabase y, si Notion está configurado, los envía también a la base de datos de Notion.

**APIs que usa:** Supabase (siempre) + Notion (si está configurado)

**Salida:** Run completado, resultados visibles en la app y en Notion

---

## Cuánto consume cada fase

| Fase | Costo principal | Estimación (50 videos, 10 adaptados) |
|------|----------------|--------------------------------------|
| Scraping | ScrapeCreators/Apify/BD | $0.10-0.50 |
| Filtro | - | Gratis |
| Análisis | Anthropic Claude | $0.15-0.30 |
| Adaptación | Anthropic Claude | $0.50-1.00 |
| Guardado | Supabase | Gratis (dentro del límite free) |
| **Total** | | **~$0.75-1.80 por run** |

---

## Errores por fase

| Fase | Error frecuente | Ver |
|------|----------------|-----|
| Fase 1 | Sin resultados / 0 videos | [Errores comunes](08-errores-comunes.md#fase-1) |
| Fase 3 | Error 401/429 de Anthropic | [Errores comunes](08-errores-comunes.md#fase-3) |
| Fase 4 | Respuesta no es JSON válido | [Errores comunes](08-errores-comunes.md#fase-4) |
| Fase 5 | Error de Notion `object not found` | [Notion](apis/notion.md) |
