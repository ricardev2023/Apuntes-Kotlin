# Tema 1. Kotlin Básico

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

## PAQUETES E IMPORTACIONES

### Paquetes

{% embed url="https://kotlinlang.org/docs/packages.html" %}
Fuente: Kotlin.org
{% endembed %}

La declaración de paquetes va en el inicio de un archivo fuente usando la sentencia `package` y luego el nombre del paquete al que pertenecerá el archivo.

El hecho de declarar un paquete al inicio del archivo nos permite importar todas las funciones y clases de dicho archivo en otros importando dicho paquete.

```kotlin
package prueba.test

fun suma(x: Int, y: Int): Int {
    return x + y
}
class Ejemplo { /*...*/ }
```

En este caso, la función suma()  tendría como nombre completo: `prueba.test.suma()`.

Lo mismo ocurriría con la clase ejemplo: `prueba.test.Ejemplo`.

### Importaciones

Utilizando la directiva `import` podemos importar los paquetes que queramos a nuestro código fuente para así utilizar las funciones, clases y constantes de dicho paquete en nuestro código.

Siguiendo con el ejemplo:

```kotlin
package prueba.main

import prueba.test.*    // Importa todo del paquete.

val y = suma(3, 2)

```

Se pueden importar:

* Clases
* Funciones y propiedad de alto nivel.
* Funciones y propiedades en declaración de objetos.
* Enumeraciones de constantes.

Además, puedes importar de diferentes maneras:

```kotlin
// Solo un elemento del paquete:
import prueba.test.Ejemplo

// Puedes renombrar el elemento para evitar colisiones de nombres:
import prueba.test.Ejemplo as ejemploImportación

// Todo el contenido del paquete:
import prueba.test.*
```

{% hint style="warning" %}
Si las declaraciones de alto nivel están marcadas como `private`, en ese caso, solo pueden utilizarse en el archivo en el que se han declarado.
{% endhint %}
