# 🚨 Andon de Estampado

Sistema andon HTML5 que muestra el alcance (SCOPE HOURS) de cada sebango por prensa, con estatus por colores.

## Archivos
- `index.html` – la aplicación (un solo archivo, sin dependencias)
- `INVENTARIO_GENERAL.csv` – base de datos (se relee automáticamente cada 60 s)

## Publicar en GitHub Pages
1. Crea un repositorio nuevo en GitHub (ej. `Andon`).
2. Sube `index.html`, `INVENTARIO_GENERAL.csv` y este `README.md` (Add file → Upload files).
3. Ve a **Settings → Pages**. En *Branch* elige `main` y carpeta `/ (root)`. Guarda.
4. En 1–2 minutos estará en `https://TU-USUARIO.github.io/Andon/`.

## Actualizar el inventario
Sube una nueva versión de `INVENTARIO_GENERAL.csv` con **el mismo nombre** (Add file → Upload files → Commit).
Las pantallas la toman solas en el siguiente ciclo (GitHub Pages puede tardar 1–2 min en publicar el cambio).
El CSV debe conservar las columnas `SEBANGO`, `Process Name` y `SCOPE HOURS`.

## Ajustes (en `index.html`)
- Umbrales de estatus: `const T={C:2,A:8,X:24}` (horas)
- Frecuencia de actualización: `REFRESH_MS` (milisegundos)
- Archivo de datos: `CSV_URL`

| Estatus | Rango (h) |
|---|---|
| 🚨 Crítico | < 2 |
| ⚠️ Atención | 2 – 8 |
| ⚙️ Acción | 8 – 24 |
| ✅ Calma | ≥ 24 |

> Nota: el repo en GitHub Pages gratuito es público; no subas datos confidenciales.
