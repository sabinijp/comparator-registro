# Comparator · registro público de picks (verificable)

Este repo publica los **picks (value/EV)** del modelo *antes* de que se jueguen los partidos, de forma
que **cualquiera pueda comprobar que el dato existía antes del evento** — sin tener que confiar en mí,
en GitHub ni en nadie.

## Por qué la fecha es confiable (y por qué el commit de git NO alcanza)

La fecha de un commit de git es **falsificable** (`GIT_COMMITTER_DATE` se puede poner a cualquier
valor). Por eso la prueba de "existió antes de T" **no** la da git, sino **[OpenTimestamps](https://opentimestamps.org)**:
cada archivo de picks tiene un `.ots` que ancla su hash SHA-256 en la **blockchain de Bitcoin**. La
fecha del bloque de Bitcoin es pública e inmutable, así que el `.ots` prueba que el JSON existía antes
de ese bloque — y por lo tanto antes de los partidos listados adentro.

## Estructura

```
picks/AAAA-MM-DD.json       # picks registrados ese día (inmutable): equipos, cuota, prob del modelo, EV
picks/AAAA-MM-DD.json.ots   # prueba OpenTimestamps (Bitcoin) del hash del JSON
registered.json             # índice de fixtures ya registrados
```

Cada pick incluye: partido y fecha, lado elegido, cuota de apertura, probabilidad del modelo, EV, y si
era apuesta (`is_bet`, EV ≥ 5 %) o casi-pick.

## Cómo verificar (cualquiera puede)

**Opción A — web, sin instalar nada:** entrá a <https://opentimestamps.org>, subí el `.json` y su
`.ots`. Te muestra el bloque de Bitcoin y la fecha en que quedó anclado.

**Opción B — línea de comandos:**

```bash
pip install opentimestamps-client
ots verify picks/2026-08-08.json.ots        # usa un nodo Bitcoin o un explorador de bloques
ots info    picks/2026-08-08.json.ots        # ver la estructura de la prueba
```

Si el hash del JSON no coincide, la verificación falla: es imposible cambiar un pick después sin que
la prueba se rompa.

> Nota honesta: OpenTimestamps sólo prueba que un dato existía **antes** de cierto momento. Sirve para
> los picks registrados **antes** del partido; no permite "probar" retroactivamente algo ya jugado.
