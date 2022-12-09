---
description: Características diferenciadoras de las Strings.
---

# Tema 4. Strings en Kotlin

{% content-ref url="variables-y-tipos-de-datos.md" %}
[variables-y-tipos-de-datos.md](variables-y-tipos-de-datos.md)
{% endcontent-ref %}

## STRINGS

{% hint style="info" %}
La información que se encuentra en éste primer apartado tiene que ver con Programación Orientada a Objetos. Si no lo entiende no se preocupe, no es indispensable a estas alturas.

Se explica a nivel usuario en el Tema 2. Aquí se explica el por qué.
{% endhint %}

Las strings son objetos de la clase String:

```kotlin
class String : Comparable<String>, CharSequence
```

El hecho de que implementen una interfaz "CharSequence" permite que podamos acceder a cada unos de sus caracteres como datos del tipo char utilizando la función get() o su operador equivalente, los corchetes:

```kotlin
val texto = "hola"

println(texto.get(2)) // l
println(texto[2])     // l
```

## CONCATENAR STRINGS

Igual que en otros lenguajes de programación, los Strings se pueden concatenar utilizando el operador aritmético "`+`".&#x20;

```kotlin
val s = "hola"
val n = "programador"
println(s + " " + n)
```

{% hint style="danger" %}
Sin embargo, al contrario que en otros lenguajes de programación como Python, no se puede repetir una String utilizando el operador aritmético "`*`". Esto dará error.
{% endhint %}

## STRINGS CON MÚLTIPLES LINEAS

En ocasiones puede ser útil crear Strings que ocupen varias líneas y se lean exactamente como están (raw).  Para ello utilizamos tres comillas dobles seguidas:

```kotlin
val texto = """ 
    hola, esto es una prueba
    una prueba muy interesante
    de texto multilinea.
"""
println(texto)

/* Resultado
    hola, esto es una prueba
    una prueba muy interesante
    de texto multilinea.
*/
```

Para evitar que el texto quede como en el ejemplo, se utiliza la función `trimIndent()`.

```kotlin
val texto = """ 
    hola, esto es una prueba
    una prueba muy interesante
    de texto multilinea.
""".trimIndent()
println(texto)

/* Resultado
 hola, esto es una prueba
 una prueba muy interesante
 de texto multilinea.
*/
```

## PLANTILLAS DE STRING

Hay ocasiones en las que queremos introducir el valor de una variable en una String. Para eso utilizamos las plantillas. Hay dos opciones:

* `$id`, donde `id` es un identificador simple.
* `${e}`, donde `e` es una expresión valida en Kotlin.

```kotlin
// Ejemplo de utilizar el valor de una variable sin expresiones.
val x = "56"    // String
val texto = "tengo $x años"

val x = 56    // Int
val texto = "tengo ${x.toString()} años"
```
