# API — Notion

La integración con Notion permite exportar automáticamente los videos adaptados a una base de datos en Notion, listo para que el equipo de contenido los gestione desde ahí.

---

## Para qué se usa en la app

Cuando la integración está configurada, cada video que pasa la **Fase 4 (Adaptación)** puede enviarse automáticamente a una base de datos de Notion con:
- Hook adaptado y variantes
- Guion completo
- Información del video original (cuenta, plataforma, vistas)
- Estado (pendiente de grabar, en producción, publicado)

---

## Cómo configurar Notion

### 1. Crear una integración en Notion

1. Ve a [notion.com/my-integrations](https://www.notion.so/my-integrations)
2. Haz clic en **+ New integration**
3. Dale un nombre (ej: `StartLab Scraper`)
4. Selecciona el workspace donde quieres que funcione
5. En **Capabilities**, deja marcados: **Read content**, **Update content**, **Insert content**
6. Haz clic en **Save**
7. Copia el **Internal Integration Token** — empieza con `secret_...`

### 2. Crear la base de datos en Notion

La base de datos puede tenerla ya creada o crearla nueva. Necesita estas columnas (properties):

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `Nombre` | Title | Título del video / hook adaptado |
| `Plataforma` | Select | Instagram, TikTok, YouTube |
| `Cuenta` | Text | Handle de la cuenta original |
| `Vistas` | Number | Vistas del video original |
| `Hook` | Text | Hook adaptado a StartLab |
| `Guion` | Text | Guion completo |
| `Estado` | Select | Pendiente, En producción, Publicado |
| `URL Original` | URL | Link al video original |
| `Fecha` | Date | Fecha de extracción |

### 3. Conectar la integración a la base de datos

1. Abre la base de datos en Notion
2. Haz clic en los tres puntos `...` (arriba a la derecha)
3. Ve a **Connections → Add connections**
4. Busca el nombre de tu integración (`StartLab Scraper`) y selecciónala

### 4. Obtener el Database ID

El Database ID está en la URL de la base de datos:
```
https://notion.so/startlab/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx?v=...
                           ↑ esto es el database ID (32 caracteres)
```

Cópialo (sin el `?v=...` y sin guiones, aunque Notion los acepta con guiones también).

### 5. Configurar en la app

Ve a **Configuración → Notion** y agrega:
- **Integration Token**: el token `secret_...` del paso 1
- **Database ID**: el ID del paso 4

---

## Errores comunes

| Error | Causa | Solución |
|-------|-------|----------|
| `object not found` | La integración no tiene acceso a la DB | Conecta la integración a la base de datos (paso 3) |
| `unauthorized` | Token inválido o expirado | Regenera el token en notion.com/my-integrations |
| `validation_error` | Columnas faltantes o mal nombradas | Verifica que la DB tiene todas las columnas del paso 2 |
| Los datos no aparecen | Database ID incorrecto | Revisa la URL de la base de datos y copia solo el ID |

---

## ¿Es obligatorio?

No. Notion es completamente opcional. Los videos adaptados siempre se guardan en Supabase (la base de datos de la app) independientemente de si Notion está configurado o no.
