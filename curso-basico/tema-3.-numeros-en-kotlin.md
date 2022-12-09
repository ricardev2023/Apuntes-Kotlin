---
description: Explicación de operaciones con datos numéricos.
---

# Tema 3. Números en Kotlin

## OPERACIONES ARITMÉTICAS

### Suma

```kotlin
5 + 7    // 12 (Int)
5 + 7.0  // 12 (Double)
```

### Resta

```kotlin
7 - 5    // 2 (Int)
7 - 5.0  // 2 (Double)
```

### Multiplicación

```kotlin
2 * 3    // 6 (Int)
2 * 3.0  // 6 (Double)
```

### División entera

```kotlin
6 / 2    // 3 (Int)
6 / 2.0  // 3 (Double)
```

### Módulo&#x20;

```kotlin
 6 % 4    // 2 (Int)
 6 % 4.0  // 2 (Double)
```

{% hint style="warning" %}
**MUY IMPORTANTE**

El compilador de Kotlin realiza conversiones de tipos al realizar operaciones aritméticas como se ha visto en los ejemplos de arriba. Esto significa que:

* Si realizo operaciones con números que sean de tipo **Byte, Short o Int**, el resultado será siempre de tipo **Int**.
* Si realizo operaciones con números enteros y alguno de ellos es de tipo **Long**, el resultado siempre será de tipo **Long**.
* Si realizo operaciones entre números enteros y números decimales de tipo **Float**, el resultado será de tipo **Float**.
* Si realizo operaciones entre números de cualquier tipo y números de tipo **Double**, el resultado siempre será **Double**.
{% endhint %}

## ORDEN DE PRECEDENCIA

El orden de precedencia es el orden en el que se realizan las operaciones en una operación compleja. En el caso de Kotlin es el siguiente:

1. Paréntesis.
2. Operador unitario de signo.
3. División, Multiplicación, Módulo
4. Suma, resta

## INCREMENTOS Y DECREMENTOS

Estos operadores representados con "`++`" (incremento) y "`--`" (decremento) tienen una característica que los hace únicos y es que pueden actuar como prefijo o como sufijo:

#### Prefijo

Se realiza el incremento/decremento sobre la variable y luego es usada en la expresión que la contiene.

```kotlin
val num = 5

println(num)    // 5
println(++num)  // 6
println(num)    // 6
```

#### Sufijo

Se usa la variable en la expresión y luego si se aplica el incremento/decremento.

```kotlin
val num = 5

println(num)    // 5
println(num--)  // 5
println(num)    // 4
```

## OPERADORES DE ASIGNACIÓN COMPUESTA

Estos operadores son la combinación entre el operador de asignación y los operadores aritméticos, con el fin de usar como operando la variable inicial.

* `a += b` -> `a = a + b`
* `a -= b` -> `a = a - b`
* `a *= b` -> `a = a * b`
* `a /= b` -> `a = a / b`
* `a %= b` -> `a = a % b`

## FUNCIONES PARA CONVERTIR TIPOS

Como hemos visto, los tipos de datos pueden variar al realizar operaciones aritméticas pero eso no significa que yo no pueda tener datos de cualquier tipo tras realizar una operación. Para ello se utilizan funciones de conversión.

* **toInt()** Para convertir un número a **Int**.
* **toLong()** Para convertir un número a **Long**.
* **toShort()** Para convertir un número a **Short**.
* **toDouble()** Para convertir un número a **Double**.
* **toFloat()** Para convertir un número a **Float**.

```kotlin
var x = 4
var y = 5.0
var z = (x + y).toInt() 
```

## PAQUETE  KOTLIN.MATH

{% embed url="https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.math/" %}

Hay otras operaciones aritméticas un poco más avanzadas que no podemos hacer de manera directa con Kotlin. Sin embargo, existe el paquete `kotlin.math` que una vez importado aumenta la gama de operaciones que podemos realizar:

Operaciones como potencias, raíces, operaciones trigonométricas, logaritmos... Todo ello se puede hacer con el paquete `kotlin.math`.
