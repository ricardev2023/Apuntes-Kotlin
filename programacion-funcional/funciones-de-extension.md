---
description: Explicación del concepto y uso de las funciones de extensión.
---

# Funciones de Extensión

## CONCEPTO

Las funciones de extensión nos permiten añadir funciones a cualquier clase aunque no tengamos acceso a su código fuente y sin tener que crear una clase que la extienda.

Se utilizan a menudo para extender las funcionalidades de los diferentes tipos de datos (que como ya sabemos, son clases en Kotlin) o para extender las funcionalidades que el framework de Android implementa.

{% hint style="success" %}
Nada impide crear una función de extensión de una clase que nosotros mismos hayamos creado. Sin embargo, si quisiéramos extender esa clase, es tan fácil como declarar dicha función como método de la clase a extender.

El caso de uso más normal de las funciones de Extensión es cuando no tenemos acceso al código fuente o no nos interesa modificarlo.&#x20;

Por eso, las clases base de Kotlin o las clases que componen el framework de Android son donde habitualmente las vamos a utilzar.
{% endhint %}

## IMPLEMENTACIÓN

Para implementar una función de extensión se debe seguir la siguiente sintaxis:

```kotlin
fun Clase.funcion(/*...*/) {/*...*/}
```

Un ejemplo práctico de su uso es, por ejemplo, una función de extensión de la clase `IntArray` para que sume todos los elementos del Array:

```kotlin
fun IntArray.suma(): Int {
    var suma = 0
    for (i in this) suma += i
    return suma
}
```

```kotlin
val array = IntArray(5) {5}
println(array.contentToString()) // [5, 5, 5, 5, 5]
println(array.suma())            // 25
```
