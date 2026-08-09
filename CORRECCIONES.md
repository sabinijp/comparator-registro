# Correcciones (erratum)

La honestidad del registro incluye documentar los errores. Los archivos ya sellados **no se
modifican** (son inmutables por diseño: su `.ots` prueba qué se registró y cuándo). Cuando se detecta
un error, se deja el original como está y se publica la corrección acá + un registro nuevo con los
valores corregidos.

---

## 2026-08-09 · Fluminense vs Independiente Rivadavia (mapeo de rival)

- **Dónde:** `picks/2026-08-08.json`, pick de Fluminense.
- **Qué pasó:** el rival *Independiente Rivadavia* (Mendoza) se mapeó por error a un rating
  **fusionado** llamado "Independiente" en los datos, que mezcla a Independiente de Avellaneda (ARG)
  con Independiente del Valle (ECU). El lado y la cuota del pick eran correctos; sólo la probabilidad
  del modelo y el EV quedaron mal calculados (subvaluados).
- **Registrado (erróneo):** `2 Independiente @ 5.26`, prob modelo **0.2677**, EV **+41 %**.
- **Corregido:** `2 Ind. Rivadavia @ 5.26`, prob modelo **0.31**, EV **+64 %** — mismo lado, misma
  cuota. Registrado y sellado en `picks/2026-08-09.json` (antes del partido del 11-ago).
- **Causa raíz:** el rating "Independiente" en `conmebol.csv` está fusionado (dos clubes distintos).
  Pendiente de-fusionarlo; hasta entonces, Independiente del Valle queda **excluido** del modelo
  (por eso no hay pick para Tolima vs IDV).

El archivo `picks/2026-08-08.json` se conserva sin cambios, con su prueba original.

---

## 2026-08-09 · De-fusión de clubes homónimos (Santa Fe vs River Plate)

- **Dónde:** `picks/2026-08-09.json`, pick de Santa Fe vs River Plate.
- **Qué pasó:** los datos tenían **tres pares de clubes distintos fusionados** bajo un mismo nombre
  (mismo nombre en países distintos, al que se le había quitado el código de país): *Independiente*
  (Avellaneda ARG + del Valle ECU), *River Plate* (Argentina + Uruguay) y *Libertad* (Paraguay +
  Ecuador). Se de-fusionaron por país. Al limpiar el rating de **River Plate (Argentina)** —quitándole
  los partidos del River uruguayo— River quedó más fuerte, y el pick cambió.
- **Registrado (con datos fusionados):** `1 Santa Fe @ 2.75`, prob modelo **0.44**, EV **+20 %**.
- **Corregido:** con River (ARG) limpio, Santa Fe local baja a prob **0.35**; el mejor lado pasa a
  ser `2 River Plate @ 2.74`, prob **0.37**, EV **+2 %** → **ya no es apuesta** (EV < 5 %). Registrado
  en `picks/2026-08-09_2.json`.
- **Efecto colateral positivo:** *Independiente del Valle* ganó rating propio → se pudo agregar el pick
  **Tolima vs IDV** (`2 IDV @ 2.77`, EV +5 %), que antes no se podía modelar.

Los archivos previos se conservan sin cambios, con sus pruebas originales.
