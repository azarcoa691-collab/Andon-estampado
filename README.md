# 🚨 Andon de Estampado

## Archivos
| Archivo | Dónde va |
|---|---|
| `index.html`, `PATRONES.csv`, `CALENDARIOS.json`, `PARES.csv` | GitHub (reemplaza los anteriores) |
| `andon_servidor.gs` | Google Apps Script — **solo para el correo de aborto** (opcional). No va a GitHub |

El inventario ya **no** va en GitHub: PC lo sube y queda en Firebase (proyecto `andon-estampado`).

## Cada turno (PC)
1. Abre el andon → **📂 CARGAR INVENTARIO** → elige el Excel o CSV.
2. Escribe el **correo y la contraseña de PC** (los creados en Firebase → Authentication → Usuarios). Se piden una vez por hora.
3. Aparece "✅ Inventario compartido". Las pantallas de prensa lo reciben **solas, al instante** (si la red bloquea la conexión en vivo, se actualizan en máximo 1 minuto o al recargar).
El inventario se toma como el del inicio de turno (06:30 / 17:20).

## Reglas de Firebase (Realtime Database → Reglas)
```
{
  "rules": {
    ".read": true,
    "inv": { ".write": "auth != null && auth.token.email != null" },
    "abt": {
      ".write": "auth != null && auth.token.email != null",
      "$id": { ".write": "newData.exists() || (auth != null && auth.token.email != null)" }
    }
  }
}
```
**Hay que volver a pegar estas reglas** (reemplazan a las anteriores): todos pueden leer; subir el inventario exige sesión; crear o actualizar un aborto NO exige sesión (para que cualquier operador lo registre de inmediato); **borrar** el historial de abortados sí exige sesión.

## Historial de abortados compartido
❌ ABORTADOS ahora se sincroniza por Firebase, igual que el inventario: lo que se aborta, se marca "Atendido" o se libera/descarta en un equipo aparece en todos los demás, solos o al refrescar.
**🗑️ BORRAR HISTORIAL** pide confirmar y luego pide el correo y la contraseña de PC (las mismas de cargar el inventario). Borra el historial de **todos** los dispositivos y no se puede deshacer; úsalo para limpiar las pruebas antes de usarlo en planta.

## Correo de aborto (opcional, Google Apps Script)
1. script.google.com → Nuevo proyecto → pega `andon_servidor.gs` → cambia `MAIL_TO` (**tu correo para pruebas**).
2. **Implementar → Nueva implementación → Aplicación web** · Ejecutar como *Yo* · Acceso *Cualquier usuario* → autoriza → copia la URL.
3. En GitHub, en `index.html`, pega la URL en `MAIL_API=""` → Commit → Ctrl+F5.
4. Prueba: **❌ ABORTADOS → ✉️ PROBAR AVISO**.
**Correo definitivo**: cambia `MAIL_TO` → Implementar → Administrar implementaciones → ✏️ → Nueva versión → Implementar (la URL no cambia).

## Pares espejo (izquierdo/derecho)
`PARES.csv` lista los números que salen del mismo troquel (columnas `SEBANGO_A,SEBANGO_B`). Cada par se muestra como **una sola casilla** `K507 / K517`:
- las horas son las del lado con **menos inventario** (la casilla dice "limita K517" si difieren 1 h o más);
- ▶ / ✔ / ⛔ aplican a los dos lados, y las piezas producidas se suman a **cada** número;
- para agregar o quitar un par, edita `PARES.csv` en GitHub (una fila por par).

## Calendarios
`CALENDARIOS.json`: octubre oficial y **nov-2026 a mar-2027 proyectados** con el ciclo de cada prensa (festivos: 16-nov, 1-feb, 15-mar; cierre 23-dic a 1-ene; se reanuda el 4-ene). Al llegar el PDF oficial de un mes, se reemplaza ese mes y se quita de `_proyectado`.

## Sonido
Con 🔔 SONIDO activado, el aviso suena **solo cuando aparece un número crítico nuevo** dentro de la prensa que estás viendo (al entrar a una prensa con críticos suena una vez; si se queda igual, no vuelve a sonar; si aparece otro número crítico distinto, suena de nuevo). En la pantalla de selección de prensas no suena. El sonido es un timbre propio tipo "power-up" (no es el audio de Nintendo, que es material con derechos de autor).

## Orden de la cola
▶ en prensa · críticos · se agota antes de su patrón · patrón en curso · verdes que no alcanzan · resto por patrón. ✋ orden manual de las posiciones 1 y 2.

## Ajustes (inicio de `index.html`)
`T` umbrales · `ALERT_H` alarma · `SH` turnos · `BASE_AT_SHIFT_START` · `FB` Firebase · `MAIL_API` / `WA_PC` / `MAIL_PC`.
