# Setup inicial

Esta guía cubre cómo poner en marcha StartLab Scraper desde cero, incluyendo Supabase, Vercel y las variables de entorno necesarias.

---

## Requisitos previos

Antes de empezar necesitas tener creadas las cuentas de:
- [Supabase](https://supabase.com) — base de datos y autenticación
- [Vercel](https://vercel.com) — hosting
- [GitHub](https://github.com) — para conectar el repositorio a Vercel

---

## Paso 1 — Clonar el repositorio

Clona el repositorio en tu máquina local:

```bash
git clone https://github.com/startlabweb/startlab-scraper-new-day.git
cd startlab-scraper-new-day
npm install
```

---

## Paso 2 — Crear el proyecto en Supabase

1. Entra a [supabase.com](https://supabase.com) y crea un nuevo proyecto
2. Elige una región cercana a tus usuarios (ej: `us-east-1`)
3. Guarda la contraseña de la base de datos en un lugar seguro
4. Una vez creado el proyecto, ve a **Settings → API**
5. Copia estos tres valores:
   - `Project URL` → será tu `NEXT_PUBLIC_SUPABASE_URL`
   - `anon public` key → será tu `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `service_role` key → será tu `SUPABASE_SERVICE_ROLE_KEY`

### Ejecutar las migraciones SQL

En Supabase, ve a **SQL Editor** y ejecuta en orden cada archivo de `supabase/migrations/`:

```
001_initial.sql
002_auto_schedule.sql
003_notion.sql
004_learning.sql
005_youtube.sql
006_youtube.sql
007_scraping_mode.sql
```

Puedes copiar el contenido de cada archivo y pegarlo en el SQL Editor. Ejecuta uno a la vez y verifica que no haya errores antes de continuar.

---

## Paso 3 — Variables de entorno

Crea un archivo `.env.local` en la raíz del proyecto con estas variables:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://tu-proyecto.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-anon-key
SUPABASE_SERVICE_ROLE_KEY=tu-service-role-key

# Cifrado de API keys (genera una cadena aleatoria de 32+ caracteres)
ENCRYPTION_SECRET=una-cadena-aleatoria-segura-de-32-caracteres

# Opcional — protege el endpoint de cron jobs de acceso externo
CRON_SECRET=otra-cadena-aleatoria
```

**Importante:** Las API keys de terceros (Anthropic, Apify, ScrapeCreators, etc.) NO van aquí. Se guardan cifradas en Supabase desde la pantalla de configuración de la app.

---

## Paso 4 — Deploy en Vercel

### Opción A — Desde la UI de Vercel (recomendado)

1. Ve a [vercel.com](https://vercel.com) y haz clic en **Add New Project**
2. Conecta tu cuenta de GitHub y selecciona el repositorio
3. Vercel detectará automáticamente que es un proyecto Next.js
4. Antes de hacer deploy, ve a **Environment Variables** y agrega las 4 variables del paso anterior
5. Haz clic en **Deploy**

### Opción B — Desde la CLI de Vercel

```bash
npm i -g vercel
vercel login
vercel --prod
```

### Deploy automático

Una vez conectado, **cada `git push` al branch `master` genera un deploy automático** en Vercel. No necesitas hacer nada más — el código llega a producción solo.

---

## Paso 5 — Configurar las API keys en la app

Una vez que la app esté desplegada:

1. Entra a la app con tu cuenta de Supabase (el primer usuario creado es el admin)
2. Ve a **Configuración → API Keys**
3. Agrega al menos:
   - **Anthropic** (obligatoria para análisis y adaptación)
   - **ScrapeCreators** o **Apify** (al menos una para scraping)
4. Haz clic en **Guardar** — las keys se cifran antes de guardarse en la base de datos

---

## Verificar que todo funciona

1. Ve a **Pipeline** en la app
2. Haz clic en **Iniciar Run**
3. Observa los logs en tiempo real
4. Si alguna fase falla con un error de API, revisa la sección [Errores comunes](08-errores-comunes.md)

---

## Siguiente paso

→ [APIs — cómo conseguir cada key](apis/anthropic.md)
