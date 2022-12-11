---
description: Explicación de las características especiales de los mapas.
---

# Tema 11. Colecciones. Mapas

Las colecciones que hemos visto hasta ahora tienen casos de usos muy útiles pero, imagine que tiene que crear un sistema de organización para una biblioteca. Cada libro (valor) irá marcado con un código único (una clave) para identificarlo. Esto se da con mucha asiduidad en el mundo real.

Un mapa es una colección que almacena sus elementos en pares clave valor, de la siguiente manera:

* Puede generar una secuencia de elementos (clave - valor) de longitud variable.
* Ni las claves ni los valores no deben ser del mismo tipo.&#x20;
* Las claves son únicas, habiendo solo un valor asignado a cada clave.
* Los valores se pueden repetir para claves diferentes.
* Identificados con el mismo nombre.

## TIPOS DE MAPAS

Los mapas se pueden dividir en dos tipos:

### Mapas de solo lectura

Un mapa de solo lectura permite únicamente consultar los datos en su interior. Como un diccionario tradicional.

Para crear un mapa de solo lectura utilizamos la función `mapOf()`.&#x20;

```kotlin
val config: Map<String, String> = mapOf(
    "nombre" to "Catrina",
    "idioma" to "Español",
    "logo" to "logo.png",
    "pagina" to "www.site.com"
)

println("$config")
// {nombre=Catrina, idioma=Español, logo=logo.png, pagina=www.site.com}
```

### Mapa mutable

Un mapa mutable permite añadir, eliminar y modificar elementos del mapa.

Para crear un mapa mutable utilizamos la función `mutableMapOf()`.

```kotlin
val libros = mutableMapOf(
    "Harry Poter" to 10
    "Sinsajo" to 7
    "Yo, Robot" to 9
    "Yo, Robot" to 7
)
println(libros) // {Harry Poter=10, Sinsajo=7, Yo, Robot=7}
```

{% hint style="info" %}
En el ejemplo superior se ha utilizado dos veces la clave "Yo, Robot". Pero como pueden ver, en el resultado final, solo se puede ver una copia de la misma con el último valor asigando.

En cambio, hay dos claves con valor 7 asignado y eso no genera ningún problema a la ejecución del programa.
{% endhint %}

## FUNCIONES Y MÉTODOS

### Métodos

Existen una serie de atributos y métodos que permiten conocer el estado de un Mapa:

* `entries`: retorna un tipo `Set<Entry<K,V>>` de solo lectura de todos los pares clave-valor.
* `keys`: retorna un `Set<K>` de solo lectura de todas las claves.
* `size`: retorna el número de entradas en el mapa.
* `values`: retornar una `Collection<V>` de solo lectura con los valores en el mapa.

```kotlin
val config: Map<String, String> = mapOf(
    "nombre" to "Catrina",
    "idioma" to "Español",
    "logo" to "logo.png",
    "pagina" to "www.site.com"
)

println(config.size)        // 4
println(config.entries)     // [nombre=Catrina, idioma=Español, logo=logo.png, pagina=www.site.com]
println(config.keys)        // [nombre, idioma, logo, pagina]
println(config.values)      // [Catrina, Español, logo.png, www.site.com]
```

### Funciones de lectura

* `mapa[clave]`: Esta sintaxis permite obtener el valor a partir de la clave en el corchete. Es la construcción equivalente al operador `get(clave)`
* `getOrDefault(key, defaultValue)`: Obtiene el valor correspondiente a la clave, de lo contrario retorna a `defaultValue`
* `isEmpty()`: Retorna `true` si el mapa no contiene entradas y `false` en caso contrario
* `containsKey(key)`: Retorna `true` si `key` existe en el mapa. Esto es equivalente a usar el operador `in` al comparar la clave frente al mapa.
* `containsValue(value)`: Retorna `true` si una o varias claves se relacionan con `value`.

```kotlin
val config: Map<String, String> = mapOf(
    "nombre" to "Catrina",
    "idioma" to "Español",
    "logo" to "logo.png",
    "pagina" to "www.site.com"
)
println(config["nombre"])                    // Catrina
println(config.get("nombre"))                // Catrina
println(config.getOrDefault("edad", "NA"))   // NA
println(config.isEmpty())                    // false
println(config.containsKey("logo"))          // true
println("logo" in config)                    // true
println(config.containsValue("Frances"))     // false
println("Frances" in config.values)          // false
```

### Añadir / Modificar entradas

Se utiliza la función put(clave, valor) para modificar una entrada. Si la clave no existe, se añade una nueva entrada al Mapa.

```kotlin
val libros = mutableMapOf(
    "Harry Poter" to 10
    "Sinsajo" to 7
    "Yo, Robot" to 9
    "Yo, Robot" to 7
)
libros.put("Yo, Robot", 10)
libros.put("Canción de Hielo y Fuego", 0)
println(libros) 
// {Harry Poter=10, Sinsajo=7, Yo, Robot=10, Canción de Hielo y Fuego=0}
```

### Eliminar entradas

Para eliminar entradas utilizamos la función `remove(key)`.

```kotlin
val libros = mutableMapOf(
    "Harry Poter" to 10
    "Sinsajo" to 7
    "Yo, Robot" to 9
    "Yo, Robot" to 7
)
libros.remove("Sinsajo")
println(libros) // {Harry Poter=10, Yo, Robot=7}
```

Otra función para eliminar entradas es `remove(key, value)` que solo eliminará la entrada si el valor coincide con el marcado. Si consigue eliminar la entrada devolverá true y en caso negativo devolverá false.

```kotlin
val libros = mutableMapOf(
    "Harry Poter" to 10
    "Sinsajo" to 7
    "Yo, Robot" to 9
    "Yo, Robot" to 7
)
println(libros.remove("Sinsajo", 10)) // false
```

### Otras funciones

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-map/" %}
Fuente: kotlinlang.org
{% endembed %}

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/" %}
Fuente: kotlinlang.org
{% endembed %}

## Recorrer un mapa

Debido a la naturaleza de pares de un mapa, la mayoría de las veces va a ser recomendable desestructurar las declaraciones para acceder a las claves por un lado y a los valores por otro.

{% hint style="info" %}
****[**Desestructura las declaraciones**](https://kotlinlang.org/docs/destructuring-declarations.html)****

Se denomina desestructurar declaraciones al hecho de desestructurar un objeto en varias variables.&#x20;

`val (name, age) = person`
{% endhint %}

Por tanto, para recorrer un mapa solo necesitaremos un bucle `for`.

```kotlin
val config: Map<String, String> = mapOf(
    "nombre" to "Catrina",
    "idioma" to "Español",
    "logo" to "logo.png",
    "pagina" to "www.site.com"
)

for ((clave, valor) in config) println("$clave -> $valor")
/*
nombre -> Catrina
idioma -> Español
logo -> logo.png
pagina -> www.site.com
*/
```
