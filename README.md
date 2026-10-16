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

## Horario considerado
Lunes a viernes. T1 06:30–16:36 · T2 17:20–02:24 (el T2 del viernes termina el sábado 02:24). Sábados y domingos sin producción.
PC carga el inventario al inicio de cada turno; si no se ha cargado 30 min después del inicio, el pie de pantalla avisa en rojo.

## Orden de la lista
1. 🔴 Críticos sin correr (menos horas primero).
2. ▶ En corrida.
3. **SE AGOTA ANTES**: el inventario no alcanza hasta la siguiente corrida de su patrón (menos horas primero) → conviene adelantarlo.
4. **ALCANZA**: cubierto hasta su corrida; ordenados por patrón.
Alcanza = horas de inventario ≥ horas productivas que faltan para su siguiente corrida; "sobran/faltan X h" es la diferencia.

## Botones
▶ ya está corriendo · ✔ terminó (piezas producidas → inventario; el número pasa a su siguiente corrida) · ⛔ abortar (piezas, motivo, nota y casilla 🛑 *sospecha de defecto*).
**❌ ABORTADOS** (PC): piezas producidas con su alcance en horas, alcance actual del número, estado de calidad y atención de PC.
Piezas con 🛑 NO suman inventario hasta que se **✔ Liberen** (certificadas); **✖ Scrap** las descarta. Mientras tanto aparece un aviso morado en todas las pantallas.

## Sonido
Pulsa **🔇 SONIDO** una vez (el navegador lo exige). Suena una **sirena** (3 s) cada 12 s, con borde rojo parpadeante, si algún sebango no corriendo tiene ≤ 1 h.

## Ajustes en `index.html`
`T` umbrales · `ALERT_H` horas de alarma · `SH` horarios de turno (T1 06:30–16:36, T2 17:20–02:24) · `CAL` calendarios (agregar mes nuevo = nueva clave `"2026-11"`).
