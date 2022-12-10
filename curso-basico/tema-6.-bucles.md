---
description: Explicación de bucles for, while y do...while.
---

# Tema 6. Bucles

Existen situaciones en las que necesitamos que una acción se repita un número determinado de veces. Para ello se utilizan las estructuras de iteración o bucles. En Kotlin podemos encontrar cuatro tipos de bucles:

## BUCLE FOR

El bucle `for` se utiliza para iterar sobre una colección de elementos y ejecutar un bloque de código con cada iteración:

```kotlin
for (i in 1..5) {
    println("Es la iteración número $i")
}

// Tambien puede ser una sentencia
for (i in 1..5) println("Es la iteración número $i")
```

Los bucles `for` son especialmente útiles para recorrer los elementos de una colección, vease una **lista** o un **mapa**.

### Iterar sobre un intervalo

{% embed url="https://kotlinlang.org/docs/idioms.html#iterate-over-a-range" %}
Fuente: kotlinlang.org
{% endembed %}

Como hemos visto en el ejemplo del bucle `for`,  existen diferentes formas de iterar sobre un intervalo en Kotlin, una de ellas es `1..5` aunque existen varias que se deben utilizar de forma idiomática (por convenio) en función de nuestras necesidades:

```kotlin
for (i in 1..100) { ... }  // intervalo cerrado, incluye 1 y 100.
for (i in 1 until 100) { ... } // intervalo medio abierto, no incluye 100.
for (x in 2..10 step 2) { ... } // intervalo cerrado con salto de 2 en 2.
for (x in 10 downTo 1) { ... } // intervalo inverso.
(1..10).forEach { ... } // otra forma de expresar un bucle for. Igual que C#
```

### Recorrer un Array

Para recorrer los elementos de un Array (o una Lista) podemos utilizar el bucle `for` de las siguientes maneras:

```kotlin
for (i in array.indices) {
    println(array[i])
}

for ((index, value) in array.withIndex()) {
    println("el elemento en el índice $index es $value")
}
```

## BUCLE WHILE

El bucle `while` permite repetir un bloque de código mientras una condición sea verdadera.

{% hint style="info" %}
La condición se evalúa antes de la primera iteración, por lo que si es falsa, no se realizará ninguna iteración.
{% endhint %}

```kotlin
var indice = 1

while (indice <= 10) {
    println(indice++)
}

// Tambien puede ser una sentencia
while (indice <= 10) println(indice++)
```

## BUCLE DO... WHILE

El bucle `do... while` es exactamente igual que el bucle `while` con la única diferencia de que la condición se evalúa después de cada iteración y no antes.&#x20;

&#x20;Un ejemplo práctico de su utilidad puede ser una clave de acceso:

```kotlin
var intentos = 0
var clave: Int

do {
    println("Intentos: ${intentos++}")
    println("Introduzca su código de acceso: ")
    clave = readln().toInt()
} while (clave != 1234 && intentos < 3)

if (clave == 1234) println("bienvenido")
    else println("Cuenta bloqueada.")
```

## REPEAT

`repeat()` técnicamente es una función y no una estructura iterativa, sin embargo, permite implementar iteraciones de otra manera que puede ser interesante para determinados usos.

{% embed url="https://www.develou.com/funcion-repeat-en-kotlin/" %}
Fuente: develou
{% endembed %}

repeat() nos permite iterar un bloque de código un número concreto de veces. Su sintaxis es la siguiente:

```kotlin
repeat(5) {
    println("prueba")
}
```

En este caso, se representará por consola el String "prueba" 5 veces.
