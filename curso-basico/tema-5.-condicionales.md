---
description: >-
  Uso de operadores lógicos y de comparación para utilizar sentencias
  condicionales.
---

# Tema 5. Condicionales

## DATOS BOOLEANOS

Al comparar dos variables o utilizar operadores lógicos, el resultado será siempre un dato de tipo [**Boolean**](variables-y-tipos-de-datos.md#booleanos).

### Tablas de verdad

Dadas dos variables lógicas, **A** y **B**,  podemos definir los operadores básicos mediante tablas de verdad, donde el valor verdadero se representa con la letra **V** o bien con un **1**, mientras que el valor falso se representa mediante la letra **F** o bien con un **0**.

La tabla de verdad para la variable **A** sería

|  A  |
| :-: |
|  V  |
|  F  |

La tabla de verdad para la variable **B** sería

|  B  |
| :-: |
|  V  |
|  F  |

#### **Negación**

El operador negación aplicado a una variable (unario) se representa con ¬ y devuelve el valor contrario. **Equivalente a NO**.

|  A  | ¬ A |
| :-: | :-: |
|  V  |  F  |
|  F  |  V  |

#### **Conjunción**

La conjunción entre dos variables se representa con ∧ y devuelve verdadero únicamente cuando ambas variables valen verdadero. **Equivalente a Y**.

|  A  |  B  | A ∧ B |
| :-: | :-: | :---: |
|  V  |  V  |   V   |
|  V  |  F  |   F   |
|  F  |  V  |   F   |
|  F  |  F  |   F   |

#### **Disyunción**

La disyunción entre dos variables se representa con ∨ y devuelve verdadero cuando al menos una de las variables lógicas vale verdadero. **Equivalente a O**.

|  A  |  B  | A ∨ B |
| :-: | :-: | :---: |
|  V  |  V  |   V   |
|  V  |  F  |   V   |
|  F  |  V  |       |
|  F  |  F  |   F   |

### Operadores lógicos

Los operadores lógicos son aquellos que nos permiten implementar las tablas de verdad en código Kotlin:

#### Negación (NOT)

Se utiliza el operador "`!`" para la negación:

```kotlin
var verdad: Boolean = true
var falso: Boolean = !verdad    // false
```

#### Conjunción (AND)

Se utiliza el operador "`&&`" para la conjunción:

```kotlin
var verdad1 = true
var verdad2 = true
var falso = false

var x = verdad1 && verdad2    // true
var x = verdad1 && falso      // false
var x = verdad2 && falso      // false
```

#### Disyunción (OR)

Se utiliza el operador "`||`" para la disyunción:

```kotlin
var verdad1 = true
var verdad2 = true
var falso1 = false
var falso2 = false

var x = verdad1 || verdad2    // true
var x = verdad1 || falso1     // true
var x = verdad2 || falso1     // true
var x = falso1 || falso2      // false
```

### Operadores de comparación

Los operadores de comparación nos permiten comparar datos y obtener resultados booleanos:

| Operador |     Significado     |
| :------: | :-----------------: |
|     >    | Estrictamente mayor |
|    >=    |    Mayor o igual    |
|     <    | Estrictamente menor |
|    <=    |    Menor o igual    |
|    ==    |        Igual        |
|    !=    |      Diferente      |

```kotlin
7 == 7    // true
7 == 7.0  // error
7 == "7"  // error
7 == 8    // false

7 != 8    // true

7 > 8     // false
7 < 8     // true

7 >= 7    // true
7 <= 7    // true
```

{% hint style="warning" %}
Como pueden ver en el ejemplo superior, en Kotlin no se pueden comparar datos de distintos tipos.

De esta manera se evitan comportamientos inesperados que sí que se dan en lenguajes como Python o Javascript.
{% endhint %}

## IF / ELSE IF / ELSE

### if

Cuando queremos comprobar si se cumple alguna condición, utilizamos el operador de decisión `if`. **SOLO SE EJECUTA SI EL RESULTADO DE LA CONDICIÓN ES TRUE**. La sintaxis que debemos seguir es la siguiente:

<pre class="language-kotlin"><code class="lang-kotlin"><strong>// Si el código a ejecutar es solo una sentencia
</strong><strong>if (condición) println("código")
</strong><strong>
</strong><strong>// Si el código a ejecutar es más de una sentencia
</strong>if (condición) {
    println("código")
    println("código 2")
}
</code></pre>

### else

En un bloque `if`, si no se cumple la condición, no se ejecuta el código. Lo normal es que queramos que, si no se cumple la condición, se ejecute un bloque de código diferente. Para ello se utiliza el bloque `else`.

```kotlin
if (condicion) {
    println("la condición se cumple")
} else {
    println("la condición no se cumple")
}
```

### else if

También puede darse el caso de que existan más de dos escenarios, para ello utilizamos un bloque `else if` que presenta una segunda condición que, de no cumplirse la primera, será comprobada antes de saltar al bloque `else`.

```kotlin
if (condicion1) {
    println("la condición 1 se cumple")
} else if (condicion2) {
    println("la condición 1 no se cumple")
    println("pero la condición 2 si.")
} else println("No se cumple ninguna condición.")
```

{% hint style="success" %}
La forma en que están escritos los ejemplos superiores es la **** [**forma idiomática**](https://kotlinlang.org/docs/idioms.html#if-expression) (por convenio) de escribir éste tipo de bloques:

* Espacio entre el if/else if/else y los paréntesis.
* Espacio entre los paréntesis y la llave.
* La llave se cierra en una nueva linea.
* El siguiente bloque se escribe en la misma linea que la llave de cierre.
* Si solo hay una sentencia, no se utiliza llave para el bloque else.
{% endhint %}

Un ejemplo de su uso podría ser:

```kotlin
println("Escriba su edad: ")
val age = readln().toInt()
val precio: Int
if (age < 18) {
    println("Eres un niño.")
    precio = 0
} else if (age <= 75) {
    println("Usted es un adulto.")
    precio = 10
} else {
    println("Usted es un anciano.")
    precio = 7
}
if (precio == 0) println("Entrada gratuita.") 
else println("Su entrada cuesta $precio€. Gracias!")
```

## WHEN

Se puede dar el caso de que necesitemos ejecutar un bloque de código en función del valor de una variable o del valor que devuelva una sentencia.&#x20;

Para evitar la repetición de bloques `if` con la misma condición y cambiando el valor, se implementó el bloque condicional `when`. Su sintaxis es la siguiente:

```
when (sentencia / variable) {
    valor1 -> código1
    valor2 -> {
        código2
        código2
        }
    valor3 -> código3
    else -> código4
} 
```

Un ejemplo de su aplicación puede ser:

```kotlin
println("Escriba su edad: ")
val age = readln().toInt()
    
when (age) {
    0 -> println("Eres un recién nacido.")
    1, 2 -> println("Eres un bebé.")
    3, 4, 5, 6, 7, 8 -> println("Eres un niño.")
    9, 10, 11, 12 -> println("Eres un joven.")
    13, 14, 15, 16, 17, 18 -> {
        println("Eres un adolescente.")
        println("Respeta a tus mayores.")
    {
    else -> println("Eres un adulto.")
}
```

{% hint style="info" %}
Los bloques `if` y `when` se pueden anidar unos dentro de otros, llegando a alcanzar estructuras muy complejas y poderosas.
{% endhint %}
