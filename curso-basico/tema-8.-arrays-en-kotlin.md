---
description: >-
  Explicación del funcionamiento de los Arrays y sus características
  diferenciadoras.
---

# Tema 8. Arrays en Kotlin

{% hint style="info" %}
La información básica de los Arrays se encuentra en el [**tema 2**](variables-y-tipos-de-datos.md#array).
{% endhint %}

un **Array** representa **más de un valor**. Específicamente, un array es una secuencia de valores que tienen **el mismo tipo de datos e identificados por un nombre común**.

En la memoria del dispositivo, los elementos del array se almacenan uno junto al otro.

Además el Array tiene un tamaño fijo.

## CREAR ARRAYS

Existen tres funciones que se pueden utilizar para crear datos de tipo Array:

* `arrayOf(elementos: T)` -> De esta manera podemos declarar un **Array** con sus elementos ya definidos:

```kotlin
var diasDeSemana: Array<String> = arrayOf(
    "lunes", "martes", "miercoles", "jueves", "viernes"
)
```

* `arrayOfNulls(tamaño: Int)` -> De esta manera se puede generar fácilmente un **Array** con un tamaño definido pero con datos de tipo **Null** en su interior, a la espera de modificarlo más adelante:

```kotlin
var sueldosMensuales: Array<Int> = arrayOfNulls(12) 
```

* `emptyArray()` -> Con esta función se genera fácilmente un **Array vacío**. Cuidado al generar Arrays vacíos ya que no se puede añadir datos en ellos.

```kotlin
var vacio = emptyArray<String>()
```

{% hint style="warning" %}
Para generar **Arrays** **vacíos** es obligatorio dar un tipo de datos a los elementos del Array aunque estos no existan.&#x20;
{% endhint %}

## UTILIZAR EL CONSTRUCTOR

Hay situaciones en las que queremos que los datos contenidos en un Array surjan de la ejecución de una función. En estos casos utilizamos el método constructor de la clase Array:

`Array(tamaño: Int) { sentencia }`

```kotlin
// Un array con los números negativos del -1 al -10.
val negativeNumbers = Array(10) { -(it + 1) }
```

{% hint style="info" %}
Esto puede ser útil también en las colecciones que se ven a continuación. Cada una de ellas tiene un método constructor de la misma manera que tienen los Arrays que se puede utilizar para lo mismo.
{% endhint %}

## ARRAYS MULTIDIMENSIONALES

Los arrays son equivalentes a vectores en matemáticas. Sin embargo, en Matemáticas se pueden crear vectores de vectores, lo que nos da una **Matriz**.&#x20;

En Kotlin, igual que en matemáticas, se pueden crear **Arrays de Arrays** para representar matrices. Lo único que hay que hacer es **anidar los Arrays**.

```kotlin
val matriz: Array<Array<Int>> = arrayOf(
    arrayOf(1, 2, 3),
    arrayOf(4, 5, 6),
    arrayOf(7, 8, 9)
)
```

{% hint style="info" %}
De la misma manera que se crean Arrays multidimensionales podemos crear Listas Multidimensionales con la característica de que se puede modificar la cantidad de elementos.
{% endhint %}

## FUNCIONES Y MÉTODOS

### Acceso a elementos

La forma más sencilla de acceder a elementos es utilizando los corchetes con un índice "`[n]`".

También se puede acceder a elementos utilizando la función `get(n)`.

```kotlin
var numeros = arrayOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
// Indices:           0  1  2  3  4  5  6  7  8  9

println(numeros[5])     // 6
println(numeros.get(5)) // 6
```

### Modificación de elementos

Los elementos dentro de un Array se pueden modificar, no así su cantidad. Para ello podemos utilizar el operador "`=`" o la función `set(n, valor)`

```kotlin
val vector = arrayOf(1, 2, 3, 4)
vector[0] = 10        // 10, 2, 3, 4
vector.set(3, 15)     // 10, 2, 3, 15
```

### Métodos

Los métodos son conjuntos de instrucciones definidas dentro de una clase, que realizan una determinada tarea y a las que podemos invocar mediante un nombre.

En el caso de los Arrays, existen tres métodos que pueden ser útiles a a la hora de recorrer el array por ejemplo:

* `array.size` -> Devuelve la cantidad de elementos que tiene el Array.
* `array.lastIndex` -> Devuelve el último índice del Array.
* `array.indices` -> Devuelve los índices del Array en la forma `0..lastIndex`

```kotlin
val vector = arrayOf(1, 2, 3, 4)

println(vector.size)        // 4
println(vector.indices)     // 0..3
println(vector.lastIndex)   // 3
```

### Funciones

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/" %}
Fuente: kotlinlang.org
{% endembed %}

## RECORRER ARRAYS

Uno de los usos típicos de los Arrays es recorrer sus elementos. Para ello utilizamos un bucle for y uno de los métodos que hemos visto anteriormente:

```kotlin
val vector = arrayOf(1, 2, 3, 4)
for (i in vector) println(i)
for (i in 0..vector.size - 1) println(vector[i])
for (i in 0..vector.lastIndex) println(vector[i])
for (i in vector.indices) println(vector[i])

println(vector.size)        // 4
println(vector.indices)     // 0..3
println(vector.lastIndex)   // 3
```

### Recorrer Arrays multidimensionales

Puede darse el caso en el que queramos recorrer todos los elementos de un Array multidimensional, ya sea para tratarlos o para pintarlos. Para ello se utilizan bucles for anidados:

```kotlin
val matriz: Array<Array<Int>> = arrayOf(
    arrayOf(1, 2, 3),
    arrayOf(4, 5, 6),
    arrayOf(7, 8, 9)
)
for (i in matriz.indices) {
    for (j in matriz[i].indices) print("${matriz[i][j]} ")
    println()
}

/* Resultado
1 2 3 
4 5 6 
7 8 9
*/
```

## INDICAR TIPO DE ELEMENTOS

En los casos donde se quiera indicar manualmente el tipo de los elementos que forman parte del Array, esto no se puede hacer con la función `arrayOf()`. Para ello se desarrollaron las siguientes funciones:

* `booleanArrayOf()`**:** para crear Arrays de tipo **boolean.**
* `intArrayOf()`**:** para crear Arrays de tipo **integer.**
* `shortArrayOf()`**:** para crear Arrays de tipo **Short.**
* `longArrayOf()`**:** para crear Arrays de tipo **long.**
* `floatArrayOf()`**:** para crear Arrays de tipo **float.**
* `doubleArrayOf()`**:** para crear Arrays de tipo **double.**
* `byteArrayOf()`**:** para crear Arrays de tipo **byte.**
* `charArrayOf()`**:** para crear Arrays de tipo **char.**
