---
description: Explicación del concepto de funciones de orden superior y su aplicación.
---

# Funciones de Orden Superior

## CONCEPTO

{% embed url="https://www.develou.com/funciones-de-orden-superior-en-kotlin/" %}
Fuente: develou
{% endembed %}

Una [función de orden superior](https://kotlinlang.org/docs/reference/lambdas.html#higher-order-functions), es una función que puede recibir como argumento una o más funciones y/o retornar una función como resultado.

Esto es posible ya que el lenguaje de programación Kotlin incluye en su gramática tipos de datos función.

{% hint style="info" %}
Indirectamente se utilizan mucho ya que las funciones de orden superior son el origen de las funciones lambda que veremos en el siguiente tema.
{% endhint %}

## IMPLEMENTACIÓN

### Sintaxis

La sintaxis de una función de orden superior sigue la siguiente sintaxis:

```kotlin
fun(arg1: T, arg2: T, argfun: (Targ1, Targ2) -> Treturn): T
```

{% hint style="info" %}
Explicación de código

En el ejemplo anterior tenemos una función con dos argumentos normales pero el tercer argumento es una función.

El argumento función se declara con los tipos de sus argumentos entre paréntesis, una flecha y el tipo del return.&#x20;

Es indispensable hacer referencia al tipo del return del argumento función. Si no es un tipo explícito, utilizamos el tipo Unit.

Por último, como todas las funciones, el tipo del return de la función como tal.
{% endhint %}

### Ejemplo

```kotlin
fun calculadora(x: Int, y: Int, fn: (Int, Int) -> Int): Int {
    return fn(x, y)
}

fun suma(x: Int, y: Int) = x + y
fun resta(x: Int, y: Int) = x - y
fun mult(x: Int, y: Int) = x * y
fun divis(x: Int, y: Int) = x / y
```

Como puede ver, la función calculadora() recibe dos Int y una función y despues aplica dicha función sobre ambos Int.

Las cuatro funciones de las operaciones (suma, resta, mult y divis), son válidas para ser pasadas como argumento a la función calculadora() ya que tienen dos argumentos de tipo Int y devuelven un tipo Int tambien.

Por tanto, podemos llamar a la función calculadora con ellas:

```kotlin
val x: Int = 5
val y: Int = 5
println("La suma de $x y $y es: ${calculadora(x, y, ::suma)}")
println("La resta de $x y $y es: ${calculadora(x, y, ::resta)}")
println("La multiplicación de $x por $y es: ${calculadora(x, y, ::mult)}")
println("La división de $x entre $y es: ${calculadora(x, y, ::divis)}")

/*Respuesta
La suma de 5 y 5 es: 10
La resta de 5 y 5 es: 0
La multiplicación de 5 por 5 es: 25
La división de 5 entre 5 es: 1 */
```

{% hint style="info" %}
**El operador ::**

Se utiliza para la [reflexión](https://www.develou.com/reflexion-en-kotlin/) en Kotlin. (En enlace es externo pero muy útil)

En este caso, se utiliza la expresión `::nombreFuncion` para acceder a su referencia y pasarla en lugares que permitan literales de función.
{% endhint %}
