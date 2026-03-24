# Cómo funcionan los prompts

Los prompts son las instrucciones que le das a la IA para que haga su trabajo en cada fase del pipeline. StartLab Scraper tiene prompts configurables desde la pantalla de Configuración.

---

## ¿Dónde están los prompts?

Ve a **Configuración → Prompts**. Verás los prompts agrupados en pestañas:

| Prompt | Fase | Qué controla |
|--------|------|-------------|
| Filtro de Cuentas | Fase 3 | Si una cuenta es relevante para el ICP |
| Filtro de Contenido | Fase 3 | Si el video es adaptable a StartLab |
| Adaptación | Fase 4 | Cómo reescribe el guion |
| Búsqueda | Fase 1 | Qué keywords usar para la búsqueda semántica |
| Golden Nuggets (YouTube) | Post-proceso | Cómo extrae los mejores fragmentos de videos largos |

---

## Variables disponibles en cada prompt

Los prompts usan variables entre llaves `{variable}` que la app reemplaza automáticamente antes de enviar a la IA.

### Filtro de Cuentas
```
{account}      → Handle de la cuenta (ej: @hormozi)
{followers}    → Número de seguidores
{bio}          → Biografía de la cuenta
{topics}       → Temas frecuentes del contenido
```

### Filtro de Contenido
```
{account}      → Handle de la cuenta
{views}        → Número de vistas del video
{caption}      → Caption/descripción del video
{transcript}   → Transcripción del audio (si está disponible)
```

### Adaptación
```
{transcript}   → Transcripción completa del video
{hook}         → Hook identificado por la IA en el análisis
{hook_tipo}    → Tipo de hook (pregunta, dato, contraste, etc.)
{estructura}   → Estructura narrativa del video
{estilo}       → Estilo de producción
{cta}          → CTA del video original
{formula_viral} → Fórmula viral identificada
```

---

## Cómo modificar un prompt

1. Ve a **Configuración → Prompts**
2. Selecciona el prompt que quieres editar
3. Modifica el texto
4. Haz clic en **Guardar**

El cambio aplica en el próximo run. No afecta los runs anteriores.

**Importante:** Mantén siempre las variables entre llaves `{variable}`. Si las eliminas, la IA no recibirá esa información.

---

## El prompt de Adaptación — el más importante

Este es el prompt que controla cómo la IA reescribe los guiones. Por defecto está optimizado para el tono y estructura de StartLab, pero puedes modificarlo para:

- Cambiar el tono (más formal, más casual, más agresivo)
- Cambiar los datos que menciona (si actualizan los números reales de clientes)
- Cambiar el CTA
- Adaptar la terminología si evoluciona la marca

### Reglas para modificar el prompt de Adaptación

**Qué puedes cambiar libremente:**
- El tono de voz
- Los datos y números específicos
- Los ejemplos de transformaciones de clientes
- El CTA final
- La terminología propia de la marca

**Qué NO debes eliminar:**
- Las variables `{transcript}`, `{hook}`, `{estructura}`, `{formula_viral}` — sin estas la IA no tiene el contexto del video original
- La instrucción de que la respuesta sea en JSON — la app parsea ese JSON para mostrar el resultado
- Los campos del JSON: `hook_adaptado`, `hook_variantes`, `guion_adaptado`, `formula_estructura`, `estilo_produccion`, `notas_grabacion`, `por_que_funciona`, `carrusel`

---

## Cómo estructurar un buen prompt de adaptación

Un buen prompt de adaptación tiene 4 partes:

### 1. Contexto de la marca
Quién es StartLab, a quién ayuda, qué hace. Esto da contexto a la IA para que entienda el universo al que debe adaptar el contenido.

```
Eres el estratega de contenido de [Empresa]. [Empresa] ayuda a [ICP]
a [transformación] con [método].
```

### 2. El ICP (cliente ideal)
Quién es el cliente ideal, qué dolores tiene, qué desea. Cuanto más específico, mejor.

```
ICP: [descripción del cliente ideal]
Dolores: [lista de dolores específicos]
Deseos: [lista de deseos concretos con números]
```

### 3. Reglas de adaptación
Qué debe hacer, qué está prohibido, qué terminología usar.

```
USAR: [terminología obligatoria]
PROHIBIDO: [lo que no debe mencionar]
Estructura: [cómo debe estructurar el guion]
```

### 4. Formato de salida
El JSON que la app espera recibir.

---

## ¿Puedo usar diferentes prompts para diferentes runs?

Sí. El campo **Instrucción personalizada** en la pantalla de Pipeline permite agregar instrucciones adicionales que se fusionan con el prompt de adaptación para ese run específico, sin modificar el prompt guardado en configuración.

Útil para: "Este run es solo para contenido de Instagram", "Adapta en un tono más urgente", etc.

---

## Resetear a los prompts por defecto

Si modificas un prompt y quieres volver al original, puedes:
1. Ir a **Configuración → Prompts**
2. Borrar todo el contenido del prompt
3. Guardar con el campo vacío — la app usará automáticamente el prompt por defecto
