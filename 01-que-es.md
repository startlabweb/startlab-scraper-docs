# ¿Qué es StartLab Scraper?

StartLab Scraper es una herramienta de **inteligencia de contenido** diseñada para automatizar el proceso de encontrar, analizar y adaptar videos virales al universo de StartLab.

En lugar de pasar horas buscando manualmente en Instagram, TikTok o YouTube qué contenido está funcionando en tu nicho, la app hace ese trabajo automáticamente y te entrega guiones listos para grabar.

---

## ¿Qué hace exactamente?

La app ejecuta un **pipeline de 5 fases** en secuencia:

### Fase 1 — Scraping
Busca videos en Instagram, TikTok y YouTube usando las keywords que tú configuras. Puede buscar por hashtags, palabras clave, o directamente en perfiles específicos.

### Fase 2 — Filtro por vistas
Descarta automáticamente los videos que no alcanzaron el umbral mínimo de vistas que tú defines (por ejemplo: mínimo 50,000 vistas). Solo pasan los que probaron tener alcance.

### Fase 3 — Análisis con IA
Para cada video que pasó el filtro, la IA analiza:
- Si la cuenta que lo publicó es relevante para el ICP de StartLab
- Si el contenido del video es adaptable a StartLab
- El hook, la estructura narrativa, la fórmula viral que usa

### Fase 4 — Adaptación
Los videos que pasaron el análisis son reescritos por Claude adaptados al tono, terminología y estructura retórica de StartLab. Recibes:
- Hook adaptado (+ 3 variantes)
- Guion completo listo para grabar
- Notas de producción
- Carrusel listo para diseñar

### Fase 5 — Aprobación y guardado
Revisas los resultados y apruebas los que quieres guardar. Los aprobados quedan en la base de datos para usarlos cuando quieras.

---

## ¿Para quién es?

Para el equipo de contenido de StartLab que quiere:
- Encontrar referencias de contenido viral en el nicho
- No empezar guiones desde cero
- Tener un flujo sistemático y predecible de ideas adaptadas

---

## Flujo visual

```
Keywords/Plataformas
       ↓
  [Fase 1] Scraping de videos
       ↓
  [Fase 2] Filtro por vistas mínimas
       ↓
  [Fase 3] Análisis IA (cuenta + contenido)
       ↓
  [Fase 4] Adaptación a StartLab con Claude
       ↓
  [Fase 5] Revisión y aprobación manual
       ↓
  Videos aprobados listos para producción
```

---

## ¿Cuánto tarda un run completo?

Depende del número de videos y las APIs usadas, pero típicamente:

| Fase | Tiempo estimado |
|------|----------------|
| Scraping | 1-3 minutos |
| Filtro | Instantáneo |
| Análisis IA | 2-5 minutos (según volumen) |
| Adaptación | 3-8 minutos (según volumen) |
| **Total** | **5-15 minutos** |

---

## Siguiente paso

→ [Setup inicial — cómo configurar la app desde cero](02-setup.md)
