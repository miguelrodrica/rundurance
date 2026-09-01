# Limpieza de archivos — Rundurance v1-inicio (Agosto 2026)

Este documento registra los cambios de limpieza y depuración realizados en la rama `v1-inicio`, alineados con el documento `V1_SUMMARY.md` y el nuevo alcance del proyecto.

---

## 🚮 Archivos/Carpetas eliminados (ya no forman parte de la versión 1)

### Frontend (landing y vistas atleta)
- public/index.html
- public/pages/atletas.html
- public/pages/progreso.html
- public/pages/sesiones.html
- public/pages/configuracion.html
- public/pages/dashboard.html
- public/pages/finance.html
- public/assets/js/atletas.js
- public/assets/js/progreso.js
- public/assets/js/sesiones.js
- public/assets/js/configuracion.js
- public/assets/js/dashboard.js
- public/assets/js/finance.js
- public/assets/js/api.js
- public/assets/images/hero_readme.png
- public/assets/images/favicon_rundurance.png
- public/assets/images/logo_rundurance.png

### Backend (APIs/módulos fuera del alcance de V1)
- src/controllers/athleteController.js
- src/controllers/planController.js
- src/controllers/workoutController.js
- src/models/athleteModel.js
- src/models/workoutModel.js
- src/models/planModel.js
- src/routes/athletes.js
- src/routes/plans.js
- src/routes/workouts.js
- src/services/fitParser.js
- src/services/zwoParser.js
- src/services/n8n.js
- src/services/s3.js
- src/middleware/admin.js

### Readme, documentales y data legada (no relevante a V1)
- src/controllers/_README.md
- src/models/_README.md
- src/middleware/_README.md
- src/services/_README.md
- src/routes/_README.md
- src/_README.md
- src/db/_README.md
- public/_README.md
- public/pages/_README.md
- docs/fit/ (carpeta completa)
- docs/ux/ (carpeta completa)
- docs/project/ (carpeta completa)
- docs/instrucciones.md
- docs/MVC.md

---

## 📦 ¿Qué se conserva?
- Toda la lógica, modelos, controladores y rutas mínimos para owner, gestión de clientes y pagos.
- Autenticación del owner.
- Infraestructura básica del backend (Node/Express), configuraciones y documentación relevante (`V1_SUMMARY.md`, `README.md`).
- Estructura base para ampliaciones futuras.

---

**Motivo:**
La limpieza responde al enfoque de la versión 1, optimizando el código solo para lo que el cliente realmente necesita y asegurando un entorno confiable y mantenible. Todo el contenido original se conserva en la rama `legacy-mvp`.

---

Realizado y documentado: Agosto 2026.
