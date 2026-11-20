# Picas y Fijas en Excel · v1.0

Piensa en un código con dígitos distintos. Excel propone una jugada y usa tus pistas para reducir la lista de candidatos. Un cero inicial cuenta como dígito.

## Cómo jugar

1. Abre `Ejercicio-PyF-v1.0.xlsx` en Excel para Microsoft 365. En la hoja `Principal`, borra las pistas de la partida de ejemplo en D5:E13.
2. Indica la cantidad de cifras en B1. B2 sirve de recordatorio opcional del secreto para quien da las pistas.
3. Lee la propuesta en la columna C. En la misma fila escribe en D las picas (dígitos correctos en otra posición) y en E las fijas (dígitos correctos en su posición). Escribe 0 cuando corresponda.
4. Continúa desde la primera fila libre hasta que aparezca «Tu número es…». Desde G5 puedes inspeccionar los bloques de candidatos de cada ronda.

## Partida incluida

Para el secreto 863, la secuencia guardada es:

| Jugada | Picas | Fijas |
| --- | ---: | ---: |
| 012 | 0 | 0 |
| 345 | 1 | 0 |
| 567 | 0 | 1 |
| 487 | 1 | 0 |
| 598 | 1 | 0 |
| 863 | 0 | 3 |

## Cómo está construido

- `obtenerUniversoInicial` genera las secuencias de la longitud elegida y conserva las que tienen todos sus dígitos distintos.
- `filtrarUniversoIter` toma la propuesta de la ronda, calcula la pista que produciría cada candidato y conserva los compatibles. La fórmula principal usa `REDUCE` para acumular los bloques.
- `ordenarPorMenosOcurrencias` puntúa cada candidato sumando las apariciones de sus dígitos en el historial recibido. El orden ascendente da prioridad a los de menor puntaje. El conteo usa `SUMA(--(suposicionesAnteriores=digito))`, que también admite matrices calculadas.

Cada función tiene una hoja homónima. El directorio `formulas/` contiene las tres definiciones del administrador de nombres en sintaxis inglesa para revisar cambios en Git.

## Detalles de esta versión

La demostración de `filtrarUniversoIter!A18` usa cinco índices de columna fijos. Con la configuración guardada de tres cifras muestra un error. Para adaptar esa prueba a B1, sustituye el vector fijo por `SECUENCIA(1;Cifras_Número)`. La partida de la hoja Principal usa la longitud configurada.

Desde la segunda ronda, la expresión `cantidadCifras*iteracion-1` deja fuera la última cifra del historial disponible al calcular los puntajes.
