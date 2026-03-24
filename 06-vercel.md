# Vercel — Cómo funciona el deploy

Vercel es la plataforma donde está desplegada StartLab Scraper. Maneja el frontend, las API routes (backend), y los cron jobs automáticos.

---

## ¿Qué hace Vercel exactamente?

Vercel convierte el proyecto Next.js en una aplicación web accesible desde internet:

- **Frontend:** Sirve las páginas de la app (React)
- **Backend (API Routes):** Ejecuta las funciones del servidor (`/app/api/**`) en serverless functions
- **Cron Jobs:** Ejecuta automáticamente el pipeline según el schedule configurado

---

## Cómo funciona el deploy automático

Cada vez que haces `git push` al branch `master` en GitHub:

1. GitHub notifica a Vercel que hay cambios
2. Vercel clona el repositorio y ejecuta `npm run build`
3. Si el build pasa, el deploy se activa en ~30-60 segundos
4. La URL de producción queda actualizada automáticamente

**No necesitas hacer nada manual** para que los cambios lleguen a producción.

---

## Plan Free vs Pro

| Característica | Free | Pro ($20/mes) |
|---------------|------|--------------|
| Proyectos | Ilimitados | Ilimitados |
| Ancho de banda | 100 GB/mes | 1 TB/mes |
| Tiempo de ejecución (serverless) | **10 segundos** | **60 segundos** |
| Cron jobs | 2 por proyecto | Ilimitados |
| Dominio personalizado | Sí (CNAME) | Sí |
| Logs en tiempo real | 1 hora | 7 días |
| Soporte | Community | Email |

### El límite más importante: tiempo de ejecución

En el **plan Free**, las serverless functions tienen un límite de **10 segundos**. StartLab Scraper ejecuta runs que pueden tardar varios minutos, por lo que **el plan Free no es suficiente para runs completos**.

Con el **plan Pro (60 segundos)**, los runs más pequeños funcionan bien. Para runs grandes (muchos videos, muchas fases), puede seguir siendo insuficiente.

**Solución:** La app está diseñada para dividir el trabajo — cada fase se ejecuta como una llamada separada desde el frontend, evitando el límite de tiempo por llamada.

### Cron jobs

Los cron jobs de Vercel ejecutan el pipeline automáticamente según el schedule que configures en la app.

- **Plan Free:** máximo 2 cron jobs por proyecto. La app usa 1 (el auto-schedule).
- **Plan Pro:** ilimitados

---

## Variables de entorno en Vercel

Las variables de entorno se configuran en **Vercel → Project → Settings → Environment Variables**.

Deben coincidir exactamente con las del archivo `.env.local` que usaste localmente:

```
NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY
SUPABASE_SERVICE_ROLE_KEY
ENCRYPTION_SECRET
CRON_SECRET (opcional)
```

**Importante:** Si cambias una variable en Vercel, necesitas hacer un nuevo deploy para que surta efecto. Puedes forzarlo desde **Deployments → Redeploy**.

---

## Ver los logs de producción

Para ver qué está pasando en producción cuando ejecutas un run:

1. Ve a [vercel.com](https://vercel.com) y entra a tu proyecto
2. Ve a **Functions** o **Logs**
3. Filtra por la función `/api/run/start`
4. Verás los `console.log` que genera el pipeline

---

## Errores comunes relacionados con Vercel

| Error | Causa | Solución |
|-------|-------|----------|
| `FUNCTION_INVOCATION_TIMEOUT` | La función tardó más de 10s (Free) o 60s (Pro) | Reduce el número de videos por run |
| `Build failed` | Error de TypeScript o dependencias | Revisa los logs del deploy en Vercel |
| Variables de entorno no disponibles | Faltó configurarlas en Vercel | Agrégalas en Settings → Environment Variables |
| El cron no ejecuta | CRON_SECRET no configurado o mal configurado | Verifica la variable y el archivo `vercel.json` |

---

## ¿Necesito el plan Pro?

Depende del uso:

- **Solo quieres probar la app:** Free es suficiente para runs pequeños
- **Uso regular con 20-50 videos por run:** Pro es recomendable
- **Auto-schedule diario:** Pro asegura que el cron no falle por timeouts

El plan Pro son **$20 USD/mes** por el workspace de Vercel (incluye todos tus proyectos).
