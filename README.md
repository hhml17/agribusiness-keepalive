# agribusiness-keepalive

Pinger que mantiene despierta la API de livestock en Render (free tier se
duerme tras ~15 min sin tráfico, cold start ~30-50s).

**¿Por qué un repo público aparte?** En repos públicos los minutos de GitHub
Actions son gratis e ilimitados. El mismo workflow dentro del repo privado
agotó los 2.000 min/mes gratuitos en agosto 2026 y bloqueó todos los deploys.

- [keep-alive.yml](.github/workflows/keep-alive.yml): doble ping a
  `/api/ready` cada ~10 min (los crons de GitHub corren con retraso real de
  25-35 min; el doble ping con espera de 6 min achica la ventana).
- [keep-repo-active.yml](.github/workflows/keep-repo-active.yml): commit
  mensual trivial para que GitHub no deshabilite los crons por inactividad
  (regla de los 60 días).

Alternativa si algún día molesta: borrar este repo y usar un pinger externo
(cron-job.org / UptimeRobot) cada 5 min, o plan Starter de Render.
