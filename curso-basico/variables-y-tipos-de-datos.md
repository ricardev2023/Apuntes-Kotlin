---
description: Explicación de los tipos de variables y los tipos de datos en Kotlin.
---

# Tema 2. Variables y Tipos de Datos

## VARIABLES,  VALORES Y CONSTANTES

### Variable

Consta de un espacio en el sistema de almacenaje (memoria principal de un ordenador) y un nombre simbólico (un identificador) que está asociado a dicho espacio.

Dicho de otro modo, una variable es la relación que hay entre un nombre y un objeto ubicado en algún lugar de la memoria del ordenador.

Definir una variable "entera" hará que en la memoria principal se reserve un espacio tal que esta variable (aunque no tenga aun valor) quepa en el almacenamiento.

Como su nombre indica, su valor puede cambiar durante la ejecución del programa.

{% hint style="success" %}
El uso de datos variables es muy útil para situaciones en las que el valor contenido en dicho espacio de memoria debe modificarse. Por ejemplo, es el resultado de una operación matemática que se repite de manera iterativa por ejemplo.
{% endhint %}

Una variable se declara de la siguiente manera:

```kotlin
var x = 1
var y = "hola"

y = "adiós"   // El valor cambia sin problemas.  
x = 2        // El valor cambia sin problemas. 
```

{% hint style="warning" %}
**Una variable puede cambiar de valor pero no de tipo de dato.**&#x20;

En el ejemplo anterior, no podemos dar a x el  valor de y por que daría error.
{% endhint %}

### Valores

Por el contrario, los valores son datos que no se van a poder reasignar.&#x20;

```kotlin
val x = 1
val y = "hola"

y = "adiós"     // Nos dará error, un valor no puede ser modificado.
```

En éste caso, **que no se pueda reasignar el valor, no significa que no se pueda modificar su valor.** Existen métodos que pueden cambiar parte de la información contenida dentro de un valor de manera legal:

```kotlin
val l = mutableListOf<Int>(2, 2, 2)
println(l)
l.add(3)    // Add es un método de mutableListOf (ya se verá lo que es eso).
println(l)

// Respuesta
[2, 2, 2]    // Esto es un val
[2, 2, 2, 3] // Hemos modificado el contenido del valor.
    
```

### Constantes

Las **constantes** son un tipo especial de valores de los cuales **desde el principio sabemos su valor** y éste valor **puede ser declarado de manera estática.**

```kotlin
// Declaramos una función que sume dos argumentos:
fun suma(x: Int, y: Int): Int {
    return x + y
}

// La declaración de val es completamente correcta:
val resultado = suma(1, 1)    // resutado = 2 

// No se puede declarar const val con un valor dinámico:
const val resultado = suma(1, 1)    // error

// Para declarar const val tenemos que hacerlo de manera estática:
const val resultado = 2
const val divisa = "EUR"
```

Además, una constante debe ser declarada siempre como variable global, es decir, fuera de cualquier función. Sin embargo, si que puede ser declarada dentro de una clase:

```kotlin
const val divisa = "EUR"

fun main(args: Array<String>) {
    println(divisa)
}
```

## TIPOS DE DATOS BÁSICOS

### Char

Hace referencia a cualquier carácter que escribamos con nuestro teclado. Debe ir entre comillas simples.

```kotlin
val c: Char = 'h'
```

### Integer Types

Son números enteros, es decir, sin decimales. Hay varios tipos de menor a mayor tamaño de memoria:

#### Byte

Es el tipo entero más pequeño. Ocupa, como su nombre indica, un byte (8 bits) y por tanto puede tener valores de `-128 a 127` (256 opciones o 2^8).

```kotlin
val b: Byte = 8
```

#### Short

Es el siguiente tipo más pequeño. Ocupa 2 bytes (16 bits) y puede tener valores de `-32768 a 32767` (2^16 opciones).

```kotlin
val s: Short = 400
```

#### Int

Es el tipo numérico entero por defecto, es decir, si no se define tipo para una variable numérica entera, el compilador interpreta que es un Int. Por ese motivo es redundante definirlo.

Ocupa 4 bytes (32 bits) y puede tener valores `entre -2147483648 y 2147483647`.

```kotlin
val i = 600000
val i: Int = 7
val i = 7    // Este tambien será de tipo Int
```

#### Long

Es el tipo entero más grande. Ocupa 8 bytes de memoria (64 bits). En este caso, si el dato no cabe en una variable Int se tipara de tipo Long. Sin embargo, se puede añadir una "L" al final para definir que sea de tipo Long.

```kotlin
val l = 3000000000000
val l = 3000000000L
val l: Long = 3000 
```

### Floating-Point Types

Son números decimales. Hay dos tipos de menor a mayor:

#### Float

Ocupa 32 bits y permite almacenar hasta 7 decimales. Para declararlo hay que añadir al número una "f" al final de manera obligatoria.

```kotlin
val f: Float = 3.1416f
val f = 3.1416f    // Tambien es del tipo Float.
```

#### Double

Es el tipo numérico decimal por defecto. Ocupa 64 bits y permite almacenar hasta 16 decimales.

```kotlin
val d: Double = 3.14
val d = 3.14    // Tambien es de tipo Double por defecto.
```

### Booleanos

Es un tipo de dato que se utiliza en conjunción con los operadores de decisión que se verán más adelante.

Puede tener dos valores: "true" o "false"

{% hint style="warning" %}
Al contrario que en otros lenguajes como **R**, no se puede escribir "true" o "false"  de ninguna manera que no sea con todas las letras en minúscula.
{% endhint %}

```kotlin
val t = true
val f = false
val incorrecta = False    // Ésta declaración dará error.
```

### Strings

Este tipo de dato almacena cadenas de caracteres y como tal, pueden ser accedidos sus caracteres como si de una lista se tratara.

Se declaran siempre entre comillas dobles:

```kotlin
val s = "hola"
println(s[0])    // h
println(s[1])    // o
println(s[2])    // l
println(s[3])    // a
```

### Array

{% embed url="https://developer.android.com/codelabs/basic-android-kotlin-collections?hl=es-419#1" %}

Un array es la forma más sencilla de agrupar un número arbitrario de valores en tus programas.

un **Array** representa **más de un valor**. Específicamente, un array es una secuencia de valores que tienen **el mismo tipo de datos**.

En la memoria del dispositivo, los elementos del array se almacenan uno junto al otro.  Esto tiene dos implicaciones importantes:

* Si usas su índice, puedes acceder a un elemento de array rápidamente. Puedes acceder a cualquier elemento aleatorio de un array desde su índice y esperar que demore la misma cantidad de tiempo para acceder a cualquier otro elemento aleatorio. Por eso se dice que los arrays tienen _acceso aleatorio_.
* Un array tiene un tamaño fijo. Esto significa que no puedes agregar elementos a un array que supere este tamaño. Si intentas acceder al elemento en el índice 100 de un array de 100 elementos, se arrojará una excepción porque el índice más alto es 99 (recuerda que el primer índice es 0, no 1). Sin embargo, puedes modificar los valores de los índices del array.

```kotlin
val a = arrayOf<Int> (1, 2, 3, 4)
println(a[0]) // 1
println(a[1]) // 2
println(a[2]) // 3
println(a[3]) // 4
```

Se puede modificar el valor de un dato del Array por su índice (siempre y cuando sea una var):

```kotlin
var planetas = arrayOf<String> ("Tierra", "Urano", "Neptuno")
println(planetas.contentToString())    // [Tierra, Urano, Neptuno]

planetas[0] = "Marte"
println(planetas.contentToString())    // [Marte, Urano, Neptuno]
```

{% hint style="success" %}
Los Arrays son muy útiles para agregar información. Sin embargo si es necesario añadir o eliminar información al Array, es necesario crear uno nuevo lo que no es eficiente a nivel de recursos.&#x20;

Para realizar operaciones con la información contenida surgen las Colecciones.
{% endhint %}

### Colecciones

{% hint style="info" %}
Las colecciones se desarrollaran en profundidad más adelante.
{% endhint %}

En Kotlin existen tres tipos de colecciones, cada una con sus características especiales:

#### List

Una lista es una colección redimensionable y ordenada que, por lo general, se implementa como un array que puede cambiar de tamaño. Cuando el array alcanza su capacidad máxima y tratas de insertar un nuevo elemento, el array se copia en un nuevo array más grande.

Existen dos tipos:

* **List** es una interfaz que define las propiedades y los métodos relacionados con una colección ordenada de solo lectura de los elementos.
* **MutableList** extiende la interfaz **List** con la definición de métodos para modificar una lista, como agregar o quitar elementos.

```kotlin
val l = listOf<Int> (1, 2, 3, 4)
val L = mutableListOf<Int> (1, 2, 3, 4)
```

#### Set

Un conjunto es una colección que no tiene un orden específico y no permite valores duplicados.

Los conjuntos tienen las siguientes dos propiedades importantes:

1. La búsqueda de un elemento específico en un conjunto es rápido, en comparación con las listas, especialmente para las colecciones grandes. Si bien el `indexOf()` de una `List` requiere que se verifique cada elemento desde el principio hasta que se encuentre una coincidencia, en promedio, se necesita la misma cantidad de tiempo para verificar si un elemento está en un conjunto, ya sea el primer elemento o el número cien mil.
2. Los conjuntos suelen usar más memoria que las listas para la misma cantidad de datos, ya que a menudo se necesitan más índices de array que los datos del conjunto.

Al igual que `List` y `MutableList`, hay un `Set` y un `MutableSet`. `MutableSet` implementa `Set`, por lo que cualquier clase que implemente `MutableSet` debe usar ambos elementos.

```kotlin
val s = setOf<Int> (1, 2, 3, 4, 5)
val S = mutableSetOf<Int> (1, 2, 3, 4, 5)
```

#### Map

Un **`Map` ** es una colección que consta de claves y valores. Se llama un mapa porque las claves únicas se _asignan_ a otros valores.

Las claves de un mapa son únicas. Sin embargo, los valores de un mapa no lo son. Dos claves diferentes podrían mapear al mismo valor.

Acceder a un valor desde un mapa por su clave suele ser más rápido que realizar una búsqueda en una lista grande, como con `indexOf()`.

Los mapas se pueden declarar con las funciones `mapOf()` o `mutableMapOf()`. Los mapas requieren dos tipos genéricos separados por comas: uno para las claves y otro para los valores.

```kotlin
val m = mapOf (
    1 to "uno",
    2 to "dos",
    3 to "tres"
)
val m = mutableMapOf (
    1 to "uno",
    2 to "dos",
    3 to "tres"
)
```

## INICIALIZAR VARIABLES

No es necesario declarar un valor para la variable al inicializarla, hay ocasiones en las que conviene inicializar la variable con un tipo y darle un valor más adelante en la ejecución del código.

```kotlin
val k: Int

// .......

k = 4
```
