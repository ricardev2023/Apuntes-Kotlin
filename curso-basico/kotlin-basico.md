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

## STANDARD INPUT / OUTPUT

Standard I/O es la forma en la que nos referimos a mostrar información por consola (standard Output) y a recibir datos desde la consola (standard input).

### Standard Output

En Kotlin existen dos funciones básicas para mostrar información por consola:

```kotlin
print("hola ¿que tal? \n") // muestra por pantalla lo que queramos.
println("hola ¿que tal?")  // añade un salto de linea al final. 
```

Obviamente, Standard Output recibe datos de tipo String aunque si le pasamos otro tipo de datos lo convertirá a String por sí solo.

### Standard Input

Hay tres opciones para recibir input en Kotlin:

#### readline()!!

Es la primera función para Standard Input que se implementó en Kotlin y tiene problemas con los valores nulos. Es por eso que se acompaña siempre del operador `!!`

{% hint style="info" %}
**El operador !!**

Kotlin se desarrolló en parte para evitar que pudieran existir las (odiadas) excepciones de "Null Pointer Exception".&#x20;

Sin embargo, existe la posibilidad de que un puntero nulo suponga un fallo de seguridad en la arquitectura del programa. Es por eso que se desarrolló el operador `!!`.

Cuando se utiliza dicho operador y la variable es nula, salta la excepción NPE permitiéndonos tratarla y evitando un problema de seguridad peor.
{% endhint %}

```kotlin
val x = readLine()!!
```

#### readln()

Desde Kotlin 1.6.0 se aplicó la funcionalidad de `readLine()!!` a la función `readln()` . Es por eso que es preferible utilizar esta opción ya que es más moderna.

```kotlin
val x = readln()
```

#### Scanner

En el caso de que quiera introducir datos que no sean del tipo String, puede utilizar la clase de Java Scanner. Para ello hay que seguir los siguientes pasos:

1. Importar Scanner.
2. Generar un objeto Scanner.
3. Comenzar a recibir datos.

```kotlin
import java.util.Scanner    // Importamos

val numero = Scanner(System.`in`)    // Generamos un objeto Scanner

var enteredNumber1:Int = numero.nextInt()    // recibimos un Int
var enteredNumber2:Float = numero.nextFloat()    // recibimos un Float
var enteredBoolean:Boolean = numero.nextBoolean()    // recibimos un Booleano
```

Scanner es una forma más potente de recibir Input pero también es más costosa a nivel de recursos.

Por otro lado, aunque uno reciba los datos del tipo String con readln(), siempre puede transformarlos en el tipo que quiera como se ve en el [**Tema 3**](tema-3.-numeros-en-kotlin.md#funciones-para-convertir-tipos).
