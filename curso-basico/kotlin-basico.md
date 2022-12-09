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
