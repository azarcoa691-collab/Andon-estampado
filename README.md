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
1. 🔴 Críticos sin correr (menos horas primero).
2. ▶ En corrida.
3. **No cubre**: su inventario se acaba antes de su siguiente corrida de patrón (menos horas primero) → conviene adelantarlo.
4. Cubiertos, por orden de patrón (siguiente corrida según columna `Patron` y calendario de la prensa).
Las horas (y el hueco hasta la siguiente corrida) se miden en **horas productivas de turno**, no en horas de reloj: no bajan de noche entre turnos ni en días sin calendario.

## Botones
▶ ya está corriendo · ✔ terminó (pide piezas producidas, las suma al inventario y manda el número a su siguiente corrida de patrón) · ⛔ abortar (piezas + motivo, avisa a PC en ❌ ABORTADOS).

## Cumplimiento de patrón
% de sebangos de la prensa (con calendario) que están corriendo o cuyo inventario cubre hasta su siguiente corrida de patrón.

## Sonido
Pulsa **🔇 SONIDO** una vez (el navegador lo exige). Suena cada 20 s si algún sebango no corriendo tiene ≤ 1 h.

## Ajustes en `index.html`
`T` umbrales · `ALERT_H` horas de alarma · `SH` horarios de turno (T1 06:30–16:36, T2 17:20–02:24) · `CAL` calendarios (agregar mes nuevo = nueva clave `"2026-11"`).
