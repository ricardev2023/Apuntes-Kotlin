---
description: Explicación de las características especiales de los sets.
---

# Tema 10. Colecciones. Set

Hasta ahora hemos visto Arrays y Listas que son ordenados y permiten elementos repetidos. Pero, ¿Qué ocurriría si tuviéramos una colección de varios gigabytes de elementos y éstos no pudieran ser iguales?

Los conjuntos (Sets) nos permiten:

* Generar una secuencia de elementos de longitud variable.
* De diferentes tipos.
* Sin duplicados, es decir, cada elemento es único.
* Sin orden concreto, es decir, los elementos no están indexados.
* Identificados con el mismo nombre.
* Nos permite operaciones entre ellos como la unión, intersección o diferencia.

## TIPOS DE CONJUNTOS

Los conjuntos se pueden dividir en dos tipos:

### Conjuntos de solo lectura

El diseño conceptual de un conjunto de solo lectura es la definición **** [**matemática de conjunto**](https://es.wikipedia.org/wiki/Conjunto).

Para crear un conjunto de solo lectura utilizamos la función `setOf()`.

```kotlin
val diasDeSemana = setOf(
    "lunes", "martes", "miercoles", "jueves", "viernes", 1, null, "jueves"
)
```

{% hint style="info" %}
Como vemos arriba, en la declaración del Conjunto hay dos elementos con el valor "jueves" sin embargo, en la construcción interna del conjunto, solo habrá una copia del mismo.

Esto no ocurre en las Listas o los Arrays en los que los datos se copian aunque estén repetidos.
{% endhint %}

### Conjuntos mutables

Como en el caso de las listas, los conjuntos mutables permiten añadir, modificar y eliminar elementos.

Para crear un conjunto mutable utilizamos la función `mutableSetOf()`.

```kotlin
val numeros = mutableSetOf(1, 3, 5, 7, 9, 11)
```

## FUNCIONES Y MÉTODOS

### Igualdad de conjuntos:

Dos conjuntos son iguales aunque sus elementos hayan sido incluidos en un orden diferente o el conjunto tenga copias.

```kotlin
val a = setOf(1, 2, 3, 4, 4, 4)
println(a == setOf(1, 2, 3, 4)) // true

println(setOf(1, 2, 3) == setOf(2, 3, 1)) // true
```

### Subconjuntos y Superconjuntos

#### Subconjunto

Un subconjunto **B** de un conjunto **A** es un conjunto que contiene algunos de los elementos de A (o quizá todos). Se denota por **B** **⊆** **A.**

#### Subconjunto propio

Un subconjunto propio **B** de un conjunto **A** es un conjunto que tiene algunos de los elementos de **A**, pero no todos. Se denota por **B ⊂ A.**

#### Superconjunto

Un superconjunto **A** de un conjunto **B** es un conjunto que contiene a **B**. Se denota por **A ⊇ B.**

**Superconjunto Propio**

Un superconjunto propio **A** de un conjunto $ es un conjunto que contiene a **B** y consta de al menos un elemento más. Se denota por **A ⊃ B.**

#### contains()

Para calcular si un elemento es pertenece a un conjunto, se puede utilizar la función `contains()`.

```kotlin
val numeros = mutableSetOf(1, 3, 5, 7, 9, 11)
println(numeros.contains(2)) // false
```

#### containsAll()

Para calcular si un subconjunto pertenece a un conjunto, o lo que es lo mismo, si es superconjunto del subconjunto, utilizamos la función `containsAll()`.

```kotlin
val numeros = mutableSetOf(1, 3, 5, 7, 9, 11)
println(numeros.containsAll(setOf(1, 5, 3, 11))) // true
```

### Añadir elementos

Para agregar elementos a un conjunto se utiliza la función add().

También se puede utilizar el [operador de asignación compuesta](tema-3.-numeros-en-kotlin.md#operadores-de-asignacion-compuesta) `+=`

```kotlin
val numeros = mutableSetOf(1, 3, 5, 7, 9, 11)
numeros.add(2)
numeros += 4
println(numeros) // [1, 3, 5, 7, 9, 11, 2, 4]
```

### Eliminar elementos

Para eliminar elementos de un conjunto se utiliza la función `remove()`.

También se puede utilizar el [operador de asignación compuesta](tema-3.-numeros-en-kotlin.md#operadores-de-asignacion-compuesta) -`=`

```kotlin
val numeros = mutableSetOf(1, 3, 5, 7, 9, 11)
numeros.remove(1)
numeros -= 7
println(numeros) // [3, 5, 9, 11, 2, 4]
```

### Otras funciones

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-set/" %}
Fuente: kotlinlang.org
{% endembed %}

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-set/" %}
Fuente: kotlinlang.org
{% endembed %}

## Operaciones entre conjuntos

### Unión

La unión de dos conjuntos **A** y **B** es un nuevo conjunto **A ∪ B** que contiene todos los elementos de **A** y/o todos los de **B**.

Para calcular la unión de dos o más conjuntos, se utiliza la función infix `union()`.

{% hint style="info" %}
Una [**función infix**](https://kotlinlang.org/docs/functions.html#infix-notation) es aquella que, para favorecer la legibilidad del texto, se puede utilizar como un operador, evitando escribir el punto y los paréntesis.&#x20;

Un buen ejemplo de una función infix es la función and().

`(1 > 2).and(2 < 1)`

`(1 > 2) and (2 < 1)`&#x20;
{% endhint %}

```kotlin
val numeros1 = mutableSetOf(1, 3, 5, 7, 9, 11)
val numeros2 = mutableSetOf(1, 4, 5, 8, 11)

println(numeros1 union numeros2) // [1, 3, 5, 7, 9, 11, 4, 8]
```

### Intersección

La intersección entre dos conjuntos **A** y **B** es un nuevo conjunto **A ∩ B** que contiene todos los elementos comunes de **A** y **B**.

Para calcular la intersección de dos o más conjuntos, se utiliza la función infix `intersect()`.

```kotlin
val numeros1 = mutableSetOf(1, 3, 5, 7, 9, 11)
val numeros2 = mutableSetOf(1, 4, 5, 8, 11)

println(numeros1 intersect numeros2) // [1, 5, 11]
```

### Diferencia

&#x20;La diferencia entre dos conjuntos **A** y **B** es un nuevo conjunto **A** - **B** que contiene todos los elementos de **A** que no están en **B.**

Para calcular la diferencia de dos o más conjuntos, se utiliza la función infix `subtract()`.

```kotlin
val numeros1 = mutableSetOf(1, 3, 5, 7, 9, 11)
val numeros2 = mutableSetOf(1, 4, 5, 8, 11)

println(numeros1 subtract numeros2) // [3, 7, 9]
```
