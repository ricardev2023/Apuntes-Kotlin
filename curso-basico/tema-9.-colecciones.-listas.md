---
description: Explicación de las características especiales de las listas.
---

# Tema 9. Colecciones. Listas

El mayor problema que encontramos con los Arrays es que debemos conocer el número de elementos antes de declarar el Array.

Las listas nos permiten:

* Generar una secuencia de valores de longitud variable.
* Del mismo tipo
* Con duplicados e incluso valores Null.
* Identificados con el mismo nombre.
* Los elementos son indexados igual que en los Arrays, desde 0.

## TIPOS DE LISTAS

Las listas se pueden dividir en dos tipos:

### Listas de solo lectura

Al igual que las variables val, las listas de solo lectura pueden ser consultadas tras su inicialización pero no se pueden utilizar funciones para modificar su contenido.

Para crear una lista de solo lectura se utiliza la función `listOf(elementos)`.

```kotlin
var diasDeSemana: List<String> = listOf(
    "lunes", "martes", "miercoles", "jueves", "viernes"
)
```

### Listas mutables

Las listas mutables permiten, además de ser consultadas, añadir, eliminar y cambiar elementos.

Para crear una lista mutable utilizamos la función `mutableListOf(elementos)`.

```kotlin
var numeros: MutableList<Int> = mutableListOf(1, 3, 5, 7, 9, 11)
```

## FUNCIONES Y MÉTODOS

### Miembros de List

Para acceder al estado de una lista no mutable existen una serie de funciones y métodos miembro muy prácticos:

* `size` para obtener la cantidad de elementos de la lista
* `list[index]` para obtener el elemento ubicado en `index`. Esta es la construcción para el operador de acceso posicional `get(index)`
* `indexOf(element)` para obtener el índice de la primera ocurrencia de `element`
* `lastIndexOf(element)` para obtener el índice de la última ocurrencia del `element`
* `subList(fromIndex, toIndex)` para obtener una porción de la lista en el rango (_fromIndex, toIndex)_

```kotlin
var diasDeSemana: List<String> = listOf(
    "lunes", "martes", "miercoles", "jueves", "viernes", "jueves"
)
println(diasdeSemana.size)   // 6
println(diasdeSemana[0])     // lunes
println(diasdeSemana.get(0)) // lunes
println(diasdeSemana.indexOf("jueves")) // 3
println(diasdeSemana.lastIndexOf("jueves")) // 5
println(diasdeSemana.subList(0, 4) // "lunes", "martes", "miercoles", "jueves", "viernes"
```

### Miembros de Mutable List

Para modificar el contenido de una lista mutable podemos utilizar:

* `add(element)` para añadir un nuevo ítem en la parte superior de la lista
* `add(index, element)` para insertar a ítem en un índice
* `removeAt(index)` para eliminar ítem en un índice
* `[index]=element`, para reemplazar un ítem en el índice. Esta construcción es equivalente al operador `set(index, element)`

```kotlin
var numeros: MutableList<Int> = mutableListOf(1, 3, 5, 7, 9, 11)
println(numeros) // [1, 3, 5, 7, 9, 11]
numeros.add(13)
println(numeros) // [1, 3, 5, 7, 9, 11, 13]
numeros.add(1, 2)
println(numeros) // [1, 2, 3, 5, 7, 9, 11, 13]
numeros.removeAt(4)
println(numeros) // [1, 2, 3, 5, 9, 11, 13]
numeros[0] = 0
println(numeros) // [0, 2, 3, 5, 9, 11, 13]
numeros.set(6, 99)
println(numeros) // [0, 2, 3, 5, 9, 11, 99]
```

### Funciones

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/" %}
Fuente:kotlinlang.org
{% endembed %}

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/" %}
Fuente:kotlinlang.org
{% endembed %}
