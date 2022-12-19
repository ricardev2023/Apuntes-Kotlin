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

## NULL SAFETY

{% embed url="https://kotlinlang.org/docs/null-safety.html" %}
Fuente: kotlinlang.org
{% endembed %}

Kotlin se desarrolló en parte para evitar que pudieran existir las (odiadas) excepciones de "Null Pointer Exception".&#x20;

Sin embargo, existe la posibilidad de que un puntero nulo suponga un fallo de seguridad en la arquitectura del programa. Es por eso que se desarrollaron los operadores `?` y `!!`.

Las únicas maneras de que en Kotlin nos encontremos con una NPE son:

* Llamada explicita a `throw NullPointerException()`.
* Utilización del operador `!!`.
* Inconsistencias en inicializaciones (avanzado):
  * Un `this` sin inicializar disponible en un constructor utilizado en el código ([leaking this](https://stackoverflow.com/questions/53866865/leaking-this-in-constructor-warning-should-apply-to-final-classes-as-well-as)).
  * El constructor de una superclase llama a un miembro cuya implementación en la clase derivada utiliza un estado no inicializado.
* Interoperabilidad con Java.

### Operador ?

Este operador se utiliza a la hora de Castear (dar un tipo) una variable y nos permite que el tipo pueda ser también nulo.

```kotlin
val stringONulo: String?
val intONulo: Int?
```

### Operador !!

Con este operador, nosotros le estamos asegurando al compilador que una variable no va a ser nula.

Cuando se utiliza dicho operador y la variable es nula, salta la excepción NPE permitiéndonos tratarla y evitando un problema de seguridad peor.

```kotlin
var string: String
val lista = listOf("hola", "adios", "que", "tal")

for (i in 0.. lista.size) {
    string = lista.elementAtOrNull(i)!! // Esto devolverá NPE en la última iteración
    println(string)
}
/*
hola
adios
que
tal
Exception in thread "main" java.lang.NullPointerException
*/

// Para evitarlo se puede utilizar el operador ?:
var string: String?
val lista = listOf("hola", "adios", "que", "tal")

for (i in 0.. lista.size) {
    string = lista.elementAtOrNull(i) 
    println(string)
}
/*
hola
adios
que
tal
null
*/
```

### Operador Elvis

Por último tenemos el operador Elvis. Este operador nos permite ejecutar una expresión si la variable es nula, mientras que si es no nula, utilizará la referencia de dicha variable.&#x20;

Se llama operador Elvis por que se parece al cantante de country Elvis Presley "`?:`"

<figure><img src="../.gitbook/assets/elvis.png" alt=""><figcaption><p>Fuente: stackoverflow.com</p></figcaption></figure>

El operador Elvis evaluará la expresión del lado derecho solo si la expresión de la izquierda es nula.

Si tenemos el siguiente código:

```kotlin
fun main(args: Array<String>) {
    var str: String? = null
    var str1: String? = "Hi, Welcome!"
    var l:  Int = if (str != null) str.length else -1
    var l1:  Int = if (str1 != null) str1.length else -1
    println("str's legth is ${l}")
    println("str1's length is ${l1}")
}
/* Resultado
str's legth is -1
str1's legth is 12 */
```

Podemos simplificar los bloques `if, else` si utilizamos el `operador elvis`:

```kotlin
fun main(args: Array<String>) {
    var str: String? = null
    var str1: String? = "Hi, Welcome!"
    var l:  Int = str ?.length ?: -1
    var l1:  Int = str1 ?.length ?: -1
    println("str's legth is ${l}")
    println("str1's length is ${l1}")
}
/* Resultado
str's legth is -1
str1's legth is 12 */
```

{% hint style="success" %}
El operador Elvis es la espina dorsal de la seguridad ante nulos ya que facilita la capacidad de realizar comprobaciones y ofrece código alternativo en el caso de que la variable tenga un valor nulo.
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

## TYPEALIAS

{% embed url="https://kotlinlang.org/docs/type-aliases.html" %}
Fuente: kotlinlang.org
{% endembed %}

Los alias nos permiten referirnos a partes de nuestro código con nombres más expresivos y sencillos para facilitar la lectura del código. Su sintaxis es la siguiente:

```kotlin
typealias alias = codigoAlQueSeRefiere
```

#### Ejemplos de Typealias

<pre class="language-kotlin"><code class="lang-kotlin"><strong>// Alias para tipos
</strong><strong>typealias NodeSet = Set&#x3C;Network.Node>
</strong>typealias FileTable&#x3C;K> = MutableMap&#x3C;K, MutableList&#x3C;File>>
// Alias para funciones
typealias MyHandler = (Int, String, Any) -> Unit
typealias Predicate&#x3C;T> = (T) -> Boolean
// Alias para clases internas
typealias AInner = A.Inner
typealias BInner = B.Inner
</code></pre>

## DESESTRUCTURACIÓN

Existen tipos de datos que almacenan en un mismo valor varios datos e incluso estos datos pueden ser de diferentes tipos. Por ejemplo, un Array de Arrays almacena en cada uno de sus elementos un Array con diferentes elementos a su vez. O un mapa que almacena una clave y un valor en cada uno de sus elementos.

Para poder separar estos diferentes datos en variables diferentes se implementó la desestructuración.

La desestructuración de un tipo permite desempacar un valor compuesto por varios datos en diferentes variables. La sintaxis es la siguiente:

```kotlin
val person = "Anonimo" to 54

// Desestructuración del par
val (name, age) = person
```

### Uso del guión bajo

En el caso de que no queramos desestructurar todas las variables, podemos omitir algunas poniendo un guión bajo (\_) en el lugar en el que le asignaríamos un nombre:

```kotlin
val nums = Triple(1, 2, 3)

val all = nums
println(all)    // (1, 2, 3)
val (first) = nums
println(first)    // 1
val (first1, second1) = nums
println("$first1  $second1")    // 1  2
val (first2, second2, third2) = nums
println("$first2  $second2  $third2")    // 1  2  3
val (first3, _, third3) = nums
println("$first3 $third3")    // 1 3
val (_, _, third4) = nums
println("$third4")    // 3
```

### Funciones de componente

La desestructuración es posible gracias a la existencia de funciones de componentes o funciones `componentN()`. Internamente el compilador invoca a estas funciones desde el objeto a desestructurar, con el objetivo de declarar e inicializar múltiples variables.

```kotlin
val person = "Anonimo" to 54

// Desestructuración del par
val name = person.component1()
val age = person.component2()
```
