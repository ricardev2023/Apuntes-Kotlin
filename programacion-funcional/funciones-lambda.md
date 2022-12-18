---
description: >-
  Explicación de las funciones lambda, su sintaxis, sus características y sus
  usos.
---

# Funciones Lambda

## ANTECEDENTES

### [Funciones de orden superior](funciones-de-orden-superior.md)

Como ya hemos visto en el tema anterior, son funciones que tienen como argumento una función o incluso devuelven una función.

### Funciones como variable

Por otra parte, también podemos guardar funciones como variables en Kotlin aprovechándonos de los datos de tipo Función que implementa su gramática.

```kotlin
var suma = { x: Int, y: Int -> x + y  }
```

{% hint style="info" %}
El bloque de código anterior es completamente válido y además nos permite cambiar el bloque de código que se ejecuta, por ejemplo, en cada iteración.
{% endhint %}

## DEFINICIÓN

{% embed url="https://www.develou.com/lambdas-en-kotlin/" %}
Fuente: develou
{% endembed %}

En base a lo visto anteriormente, podemos definir el concepto de función lambda como:

> Una [función lambda](https://kotlinlang.org/docs/reference/lambdas.html#lambda-expressions-and-anonymous-functions) es un literal de función que puede ser usado como expresión. Esto quiere decir, una función que no está ligada a un identificador y que puedes usar como valor.

O, en otras palabras, una función anónima que utilizamos como valor de entrada en una función de orden superior.

## SINTÁXIS

&#x20;Continuando con la función suma, podemos escribirla así:

```kotlin
fun suma(x: Int, y: Int) = x + y
```

Para transformarla al formato lambda tenemos que hacerla anónima.

La sintaxis de un literal de lambda va escrita entre llaves `{...}` y su contenido es el siguiente:

* **Lista de parámetros** — Cada parámetro es una declaración de variable, aunque esta lista es opcional
* **Operador de flecha `->`** — Se omite si no usas lista de parámetros
* **Cuerpo del lambda** — Son las sentencias que van luego del operador de flecha

```kotlin
{ x: Int, y: Int -> x + y}
```

### Función lambda con cuerpo

Las funciones lambda tienen que devolver un valor, eso es indispensable. Sin embargo, el cuerpo de una función lambda puede tener varias sentencias:

```kotlin
// Función lambda para hayar la potencia de x elevado a y.
{ x: Int, y: Int -> 
    var res = 1
    for (i in 1..y) res *= x
    res
}
```

## IDENTIFICADOR IT

Cuando tu lambda usa un único argumento y no piensas cambiar su nombre por cuestiones de legibilidad, puedes usar el identificador `it`.

Esta variable se deduce implícitamente con el tipo inferido por el compilador y puedes referirte a ella como tu parámetro.

Vamos a mostrar un caso de uso con todo lo que hemos visto anteriormente:

```kotlin
var array1 = Array(5) { 5 }
var array2 = Array(5) { it }
var array3 = Array(5) { it * 2 }

println(array1.contentToString())    // [5, 5, 5, 5, 5]
println(array2.contentToString())    // [0, 1, 2, 3, 4]
println(array3.contentToString())    // [0, 2, 4, 6, 8]
```

{% hint style="info" %}
En el caso del tipo Array, el argumento que coge la lambda es el iterador. Por tanto, it será el número de iteración.
{% endhint %}

## ACCESO A VARIABLES EXTERNAS

Las lambdas pueden acceder a variables que se hayan inicializado fuera del código de la lambda:

```kotlin
fun recorrerArray(array: Array<Int>, fn: (Int) -> Unit) {
    for (i in array) {
        fn(i)
    }
}

fun main() {
    val array3 = Array(5) { it * 2 }
    var suma = 0
    recorrerArray(array3) {
        suma += it
    }
    println(suma)    // 20
}
```

## EJEMPLOS DE APLICACIÓN

Las lambdas tienen un caso de uso claro con las funciones de orden superior como lo que vamos a ver a continuación:

```kotlin
// Declaración de función de orden superior
fun calculadora(x: Int, y: Int, fn: (Int, Int) -> Int): Int {
    return fn(x, y)
}
// uso con lambdas
println("La suma de $x y $y es: ${calculadora(x, y, { x: Int, y: Int -> x + y })}")
println("La resta de $x y $y es: ${calculadora(x, y, { x: Int, y: Int -> x - y })}")
println("La multiplicación de $x por $y es: ${calculadora(x, y, 
{ x: Int, y: Int -> x * y })}")
println("La división de $x entre $y es: ${calculadora(x, y, 
{ x: Int, y: Int -> x / y })}")

println("La potencia de $x elevado a $y es: ${calculadora(x, y,
{ x: Int, y: Int -> 
    var res = 1
    for (i in 1..y) res *= x
    res
})}")

/* Resultado
La suma de 5 y 5 es: 10
La resta de 5 y 5 es: 0
La multiplicación de 5 por 5 es: 25
La división de 5 entre 5 es: 1
La potencia de 5 elevado a 5 es: 3125 */
```

### Omitir el paréntesis

Sin embargo, las lambdas por definición se pueden poner fuera de los paréntesis lo que hace el código más legible:

```kotlin
println("La suma de $x y $y es: ${calculadora(x, y) { x: Int, y: Int -> x + y }}")
```

### Ejemplo por partes

#### Ejemplo básico

```kotlin
// Implementación de una variable que almecena la cantidad de 'i' en una String.
val s = "Supercalifragilisticoespialidoso"
val iCounter = s.count({ char:Char -> char == 'i' })

println("En la frase: $s")        // En la frase: Supercalifragilisticoespialidoso
println("Hay $iCounter ies.")     // Hay 6 ies.
```

#### Ejemplo omitiendo los paréntesis

```kotlin
// La lambda se puede sacar de los paréntesis
val s = "Supercalifragilisticoespialidoso"
val iCounter = s.count() { char:Char -> char == 'i' }

// Los paréntesis vacíos se pueden omitir
val s = "Supercalifragilisticoespialidoso"
val iCounter = s.count { char:Char -> char == 'i' }
```

#### Ejemplo omitiendo el tipo de dato

```kotlin
// El tipo de dato se puede omitir ya que count se aplica solo a tipo char.
val s = "Supercalifragilisticoespialidoso"
val iCounter = s.count { char -> char == 'i' }
```

#### Ejemplo del identificador it

En el ejemplo anterior lo que hemos hecho ha sido renombrar el argumento como char. Eso se puede omitir tambien.

```kotlin
// Se puede omitir el argumento de manera explícita.
// De esta manera el argumento se llamará it implícitamente:
val s = "Supercalifragilisticoespialidoso"
val iCounter = s.count { it == 'i' }
```
