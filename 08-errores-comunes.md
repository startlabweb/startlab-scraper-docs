# Errores Comunes y Soluciones

Esta guía cubre los errores más frecuentes que puedes encontrar al usar StartLab Scraper, con su causa exacta y cómo resolverlos.

---

## Fase 1 — Scraping {#fase-1}

### "Sin resultados" / "0 videos encontrados"

**Síntoma:** El run termina la Fase 1 con 0 videos o muy pocos.

**Causas posibles:**

1. **Las keywords son muy específicas** → Prueba con términos más amplios. En lugar de `"sistema predecible high ticket Colombia"`, usa `"sistema predecible ventas"`.

2. **Bright Data no encuentra resultados en Google** → Google puede no tener indexados videos recientes con esas keywords. Cambia al modo **Solo ScrapeCreators** o **Solo Apify** en Configuración → Umbrales.

3. **El hashtag de Instagram tiene poco volumen** → Usa keywords más populares en inglés o español.

4. **Apify sin créditos** → Error explícito: `Apify sin créditos suficientes`. Recarga en [console.apify.com/billing](https://console.apify.com/billing).

5. **ScrapeCreators API caída** → Temporal. Reintenta en unos minutos o cambia de modo de scraping.

**Solución rápida:** Cambia a **Solo ScrapeCreators** y usa keywords más amplias.

---

### TikTok siempre da 0 resultados

**Causa:** TikTok tiene mecanismos anti-scraping agresivos. Puede fallar por:
- La plataforma bloqueó temporalmente las IPs de Apify/SC
- Las keywords no tienen volumen en TikTok

**Solución:** Prueba con el modo **Solo Apify** y keywords en inglés. TikTok en inglés tiene más volumen que en español.

---

### Error de Apify: `not-enough-usage-to-run-paid-actor`

**Causa:** Tu cuenta de Apify no tiene suficientes créditos para ejecutar los actores de TikTok o Instagram (son actores de pago).

**Solución:** Ve a [console.apify.com/billing](https://console.apify.com/billing) y recarga créditos. Mínimo recomendado: $10.

---

## Fase 3 — Análisis IA {#fase-3}

### Error 401 de Anthropic

**Síntoma:** Los logs muestran `Anthropic error: 401`.

**Causa:** La API key de Anthropic es inválida, expirada, o fue mal copiada.

**Solución:**
1. Ve a [console.anthropic.com/api-keys](https://console.anthropic.com/api-keys)
2. Verifica que la key existe y está activa
3. Si expiró, crea una nueva
4. Actualiza la key en **Configuración → API Keys → Anthropic**

---

### Error 429 de Anthropic (Rate Limit)

**Síntoma:** Los logs muestran `Anthropic error: 429`.

**Causa:** Estás enviando demasiadas requests seguidas a la API de Claude.

**Solución:** La app tiene reintentos automáticos con backoff. Si el error persiste, espera 1-2 minutos y reintenta el run.

---

### Anthropic sin créditos

**Síntoma:** Error `{"error":{"type":"billing_error"}}` o similar.

**Solución:** Ve a [console.anthropic.com/settings/billing](https://console.anthropic.com/settings/billing) y recarga créditos.

---

## Fase 4 — Adaptación {#fase-4}

### "La respuesta no es JSON válido"

**Síntoma:** En los logs ves un error de parse o el video aparece sin adaptación.

**Causa:** Claude generó una respuesta que no puede parsearse como JSON. Suele pasar cuando:
- El prompt de adaptación fue modificado y rompió el formato de salida
- El transcript es muy corto o no tiene contenido relevante
- Claude respondió con un mensaje de disculpa en lugar de JSON

**Solución:**
1. Verifica que el prompt de adaptación termina con las instrucciones del JSON (`JSON estricto, sin markdown, sin texto extra`)
2. Si modificaste el prompt y rompió el formato, resetéalo vaciando el campo en Configuración → Prompts
3. Videos muy cortos (menos de 30 palabras de transcript) pueden no adaptarse bien — es normal

---

### Las adaptaciones salen genéricas / no suenan a StartLab

**Causa:** El prompt de adaptación no tiene suficiente contexto de la marca.

**Solución:** Enriquece el prompt de adaptación en Configuración → Prompts con:
- Más dolores específicos del ICP (con palabras exactas que usa el cliente)
- Más datos reales de transformaciones de clientes
- Frases prohibidas que sí se están colando
- Más ejemplos del tono que quieres

---

## Problemas de autenticación / acceso

### "No puedo entrar a la app"

**Causa:** El usuario no existe en Supabase o la sesión expiró.

**Solución:**
1. Ve a [supabase.com](https://supabase.com) → tu proyecto → **Authentication → Users**
2. Verifica que tu email está en la lista
3. Si no está, regístrate desde la pantalla de login de la app (el primer usuario se registra solo)
4. Si está pero no puedes entrar, ve a **Authentication → Users**, busca tu usuario y haz clic en **Send magic link**

---

### La app muestra datos de otro workspace

**Causa:** La Row Level Security (RLS) de Supabase no está bien configurada o las migraciones no se ejecutaron.

**Solución:** Verifica que ejecutaste todas las migraciones SQL en orden en el SQL Editor de Supabase.

---

## Problemas de Vercel / Deploy

### El run se corta a mitad sin error visible

**Causa:** La serverless function llegó al timeout de Vercel (10 segundos en Free, 60 en Pro).

**Solución:**
- Reduce el número de videos por run (usa **Max videos por keyword** en Configuración → Umbrales)
- Considera actualizar al plan Pro de Vercel ($20/mes)

---

### El auto-schedule no ejecuta

**Causa posibles:**
1. El `CRON_SECRET` no está configurado en Vercel → agrégalo en Settings → Environment Variables
2. El cron no está activado en la app → ve a **Configuración → Scheduler** y actívalo
3. Vercel Plan Free tiene límites en crons muy frecuentes

**Solución:** Verifica las variables de entorno en Vercel y que el scheduler esté activo.

---

## Notion

Ver [APIs — Notion](apis/notion.md) para errores específicos de la integración.

---

## ¿El error que tienes no está aquí?

1. Revisa los logs del run en la app (ícono de logs en el pipeline)
2. Revisa los logs de producción en [vercel.com](https://vercel.com) → tu proyecto → Functions
3. El mensaje de error suele indicar la causa exacta (API, timeout, JSON inválido, etc.)
