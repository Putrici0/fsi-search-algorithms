# Algoritmos de búsqueda

Este proyecto implementa y compara varios algoritmos de búsqueda aplicados al mapa clásico de Rumanía. El problema definido busca una ruta desde `A` hasta `B`, usando los costes de las aristas del grafo como distancia acumulada.

El objetivo principal del proyecto es observar las salidas de cada algoritmo y comparar especialmente las dos variantes de Branch and Bound:

- Branch and Bound sin subestimación.
- Branch and Bound con subestimación heurística.

## Archivos del proyecto

- `run.py`: ejecuta el problema de búsqueda y muestra los resultados de cada algoritmo.
- `search.py`: contiene la definición del problema, los nodos, el grafo de Rumanía y los algoritmos de búsqueda.
- `utils.py`: incluye estructuras auxiliares, funciones matemáticas y colas utilizadas por los algoritmos.

## Algoritmos implementados

### Búsqueda en anchura

La búsqueda en anchura explora primero los nodos menos profundos del árbol de búsqueda. Utiliza una cola FIFO, por lo que los nodos se expanden en el mismo orden en el que se generan.

En este problema encuentra una solución válida, aunque no necesariamente la de menor coste.

### Búsqueda en profundidad

La búsqueda en profundidad explora primero los nodos más profundos. Utiliza una pila, por lo que el último nodo generado es el primero en expandirse.

Puede llegar a una solución rápidamente en algunos casos, pero no garantiza encontrar la ruta óptima.

### Branch and Bound sin subestimación

Esta versión ordena la frontera usando únicamente el coste acumulado de la ruta, es decir, `g(n)`.

El algoritmo prioriza los caminos con menor coste acumulado hasta el momento. En el problema de Rumanía encuentra la ruta óptima desde `A` hasta `B`, pero necesita visitar más nodos que la versión con subestimación.

### Branch and Bound con subestimación

Esta versión incorpora una subestimación heurística mediante la función `h(n)`, que calcula la distancia en línea recta desde el nodo actual hasta el objetivo.

La prioridad se calcula con:

```text
f(n) = g(n) + h(n)
```

Donde:

- `g(n)` es el coste acumulado desde el nodo inicial hasta el nodo actual.
- `h(n)` es la estimación del coste restante hasta el objetivo.

Gracias a esta subestimación, el algoritmo encuentra la misma ruta óptima que Branch and Bound sin subestimación, pero generando y visitando menos nodos.

## Ejecución

Para ejecutar el proyecto:

```bash
py run.py
```

También puede ejecutarse con `python run.py` si Python está disponible en el `PATH`.

## Salidas obtenidas

Al ejecutar `run.py`, se muestran para cada algoritmo:

- Nodos generados.
- Nodos visitados.
- Coste total.
- Ruta solución.

Salida completa:

```text
Búsqueda en Anchura:
Nodos generados: 21
Nodos visitados: 16
Coste total: 450
Ruta solución: ['A', 'S', 'F', 'B']
Coste total: 450

Búsqueda en Profundidad:
Nodos generados: 18
Nodos visitados: 10
Coste total: 733
Ruta solución: ['A', 'T', 'L', 'M', 'D', 'C', 'P', 'B']
Coste total: 733

Branch and Bound:
Nodos generados: 31
Nodos visitados: 24
Coste total: 418
Ruta solución: ['A', 'S', 'R', 'P', 'B']
Coste total: 418

Branch and Bound con Subestimación:
Nodos generados: 16
Nodos visitados: 6
Coste total: 418
Ruta solución: ['A', 'S', 'R', 'P', 'B']
Coste total: 418
```

## Comparación de resultados

| Algoritmo | Ruta solución | Coste total | Nodos generados | Nodos visitados |
| --- | --- | ---: | ---: | ---: |
| Búsqueda en anchura | `A -> S -> F -> B` | 450 | 21 | 16 |
| Búsqueda en profundidad | `A -> T -> L -> M -> D -> C -> P -> B` | 733 | 18 | 10 |
| Branch and Bound | `A -> S -> R -> P -> B` | 418 | 31 | 24 |
| Branch and Bound con subestimación | `A -> S -> R -> P -> B` | 418 | 16 | 6 |

## Conclusión

Las dos versiones de Branch and Bound encuentran la ruta óptima:

```text
A -> S -> R -> P -> B
```

con un coste total de `418`.

La diferencia más importante está en la eficiencia. Branch and Bound sin subestimación genera `31` nodos y visita `24`, mientras que Branch and Bound con subestimación genera `16` nodos y visita solo `6`. Por tanto, la subestimación heurística reduce claramente el número de nodos explorados sin empeorar la solución obtenida.

## Autores

- [Pablo Llopis Parrilla](https://github.com/Putrici0)
