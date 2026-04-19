# Descripcion del problema

## Contexto del problema

Las islas CpG son regiones del ADN donde la frecuencia de citosinas (**C**) y guaninas (**G**) es significativamente mayor que en el resto del genoma. Estas regiones suelen encontrarse cerca de los promotores génicos y juegan un rol clave en la regulación de la expresión génica, ya que suelen estar menos metiladas que otras zonas del ADN.

En el resto del genoma, el dinucleótido **CG** es poco frecuente debido a procesos de metilación y mutación, pero en las islas CpG esta tendencia se invierte y los pares **CG** aparecen de forma sostenida a lo largo de una región continua.

---

## Idea inicial (enfoque ingenuo)

Una primera idea intuitiva es contar directamente la cantidad de pares **"CG"** en una secuencia de ADN. Bajo este enfoque, si una región contiene muchos "CG", se podría decidir que se trata de una isla CpG, y si contiene pocos, que no lo es.

Sin embargo, este enfoque es **limitado** por varias razones:

- No tiene en cuenta la continuidad de las regiones (no modela “bloques” de islas).
- No permite modelar la probabilidad de **entrar o salir** de una isla CpG.
- No captura la estructura estadística global de la secuencia.

Por estas razones, contar pares "CG" de manera directa no refleja adecuadamente la dinámica real del problema.

---

## Enfoque correcto: Cadenas Ocultas de Markov (HMM)

Para modelar correctamente el problema, se utiliza un **Hidden Markov Model (HMM)**, que asume que:

- Existe un **estado interno oculto** que no se observa directamente.
- Las observaciones dependen únicamente de ese estado oculto.
- El sistema evoluciona de manera secuencial.

En este caso, el ADN observado (secuencia de nucleótidos) es el resultado de un proceso oculto que alterna entre dos tipos de regiones.

---

## Definición de los estados

### Estados ocultos (no observables)

Estos representan el tipo de región en el que estamos:

- `I` → Región perteneciente a una **Isla CpG**
- `N` → Región que **No** es una isla CpG

Estos estados son *ocultos* porque no se observan directamente al mirar la secuencia.

### Estados observables

Son los símbolos que sí se observan en la secuencia:

- `A`, `C`, `G`, `T`

Estos corresponden a los nucleótidos reales del ADN.

---

