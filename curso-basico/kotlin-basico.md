# KOTLIN BÁSICO

## VERSIÓN ACTUAL

{% hint style="info" %}
En el momento de escribir ésta guía la **versión más reciente** de Kotlin era **1.8.0 RC**.
{% endhint %}

## FUNCIÓN MAIN()

Igual que en otros lenguajes clásicos como C, el **punto de entrada del programa en Kotlin es la función Main()**. Esto significa que solo se ejecutará aquello que se encuentre dentro de dicha función.&#x20;

```kotlin
fun suma(x: Int, y: Int): Int {
    return x + y
}

const val divisa = "EUR"
suma(1, 1)    //esto no se ejecutará.

fun main(args: Array<String>) {
    println(divisa)
}
```

## COMENTARIOS

Dado un bloque de código, a veces puede ser útil explicar qué hace o en qué consiste, o bien hacer que una línea no se ejecute por algún motivo, pero que siga presente en dicho código. Aquí entran en juego los comentarios, que son parte del código, pero no se ejecutan.

En Kotlin, se pueden diferenciar dos tipos de comentarios:

### Linea de comentarios

En este caso, el comentario solo ocupa desde su inicio hasta el salto de linea. Se representa con "`//`"

```kotlin
// Esto es un comentario.
val variable = 1 // Esto tambien es un comentario válido
```

### Comentario multilínea

Existe la opción de que el comentario ocupe varias líneas. En este caso utilizamos "`/*`" para abrir el comentario y "`*/`" para cerrarlo.

```kotlin
/* Esto es un comentario multilínea
que ocupa varias líneas
hasta que decidamos cerrarlo */
var variable = 1
```
