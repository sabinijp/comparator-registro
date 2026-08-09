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
