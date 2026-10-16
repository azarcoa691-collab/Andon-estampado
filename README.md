# 🚨 Andon de Estampado v2

Archivos: `index.html` (app) · `INVENTARIO_GENERAL.csv` (inventario que carga PC).

## Publicar (GitHub Pages)
1. Sube `index.html` y `INVENTARIO_GENERAL.csv` al repositorio (reemplaza los anteriores).
2. Settings → Pages → Branch `main` / `(root)`.

## Flujo diario de PC
Cuando PC toma el inventario: sube el nuevo `INVENTARIO_GENERAL.csv` al repo (mismo nombre) **o** abre el andon y usa **📂 CARGAR CSV**.
La hora de carga es la base: desde ahí las horas de alcance bajan en tiempo real.
Horas de alcance = `INVENTORY PIECES ÷ (Daily usage (pcs) ÷ 17)` (si faltan datos usa `SCOPE HOURS`).
Columnas requeridas: `SEBANGO`, `Process Name`, `Daily usage (pcs)`, `INVENTORY PIECES`, `Patron`.

## Orden de la lista
1. Críticos en rojo (sin correr) · 2. En corrida · 3. Resto por siguiente corrida según su **Patron** (col. S) y el calendario de la prensa. Empate → menos horas primero.

## Botones por sebango
▶ ya está corriendo · ✔ terminó · ⛔ abortar (pide piezas producidas y motivo y avisa a PC en la ventana **❌ ABORTADOS**).

## Sonido
Pulsa **🔇 SONIDO** una vez (el navegador lo exige). Suena cada 20 s si algún sebango no corriendo tiene ≤ 1 h.

## Ajustes en `index.html`
`T` umbrales · `ALERT_H` horas de alarma · `SH` horarios de turno (T1 06:30–16:36, T2 17:20–02:24) · `CAL` calendarios (agregar mes nuevo = nueva clave `"2026-11"`).
