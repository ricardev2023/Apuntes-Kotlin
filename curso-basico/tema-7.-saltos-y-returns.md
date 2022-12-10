---
description: Explicación de las expresiones de salto en Kotlin.
---

# Tema 7. Saltos y Returns

Hay veces en las que nos encontramos dentro de un bucle pero, sí se da una condición especial, tenemos que salir de ese bucle y continuar con la ejecución del programa sin terminar dicho bucle.

También puede darse el caso que dadas determinadas condiciones queramos saltarnos parte de un bucle.

O incluso podría darse el caso de que dada determinada condición queramos terminar con la ejecución de una función.

Para todo lo anterior existen las expresiones de salto:

## BREAK

La expresión `break` se utiliza dentro de bucles para finalizar la ejecución de dicho bucle cuando se da una condición concreta.

```kotlin
var x: Int
do {
    println("Pruebe suerte, escriba un número del 1 al 10: ")
    x = readln().toInt()
    if (x == 6) break
    else println("mala suerte, vuelva a intentarlo")
} while (true)
println("Enhorabuena, ha escapado del bucle.")

```

{% hint style="warning" %}
`break` solo puede utilizarse en el cuerpo de un bucle.
{% endhint %}

## CONTINUE

En el caso de la expresión `continue`, lo que ocurre es que se evita la ejecución de todo o parte del bloque de código dentro del bucle cuando se cumple una condición determinada.

```kotlin
for (i in 1..10) {
    println("El número $i ")
    if (i != 3) println("no es el número 3")
    else continue
}
```

{% hint style="warning" %}
`continue` solo puede utilizarse en el cuerpo de un bucle.
{% endhint %}

## RETURN

Por último tenemos la expresión `return`.  Ésta expresión termina con la ejecución de una función devolviendo o no un valor a la función del nivel superior:

```kotlin
fun normal() {
    for (i in 1..10) {
        println(i)
        if (i == 3) return
    }
    println("Esto no se va a escribir nunca")
}

fun main() {
    normal()
    println("esto si que se va a escribir")
}
```

{% hint style="info" %}
En el ejemplo superior, lo que sucede es que la función normal() retorna cuando (i == 3)

Al retornar, el resto de la función normal() queda sin ejecutar.&#x20;
{% endhint %}

Como se puede ver, no se devuelve ningún valor en el ejemplo superior. Podría devolverse un valor como en el siguiente ejemplo:

```kotlin
fun normal(): String {
    for (i in 1..10) {
        println(i)
        if (i == 3) return "Retornando"
    }
    println("Esto no se va a escribir nunca")
    return "No va a llegar aquí"
}

fun main() {
    println(normal())
    println("esto si que se va a escribir")
}
```

## ETIQUETAS

Cualquier expresión en **Kotlin** puede ser marcada con una `label`. Las etiquetas tienen la forma de un identificador seguido del signo `@`. Por ejemplo: `abc@,` `miExpresion@` son etiquetas válidas. Para etiquetar una expresión, coloca una etiqueta delate de ella:

```kotlin
loop@ for (i in 1..100) {
    // ...
}
```

### Break y Continue con Etiquetas

Así, podemos utilizar `break` o `continue` con una etiqueta:

```kotlin
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (...) break@loop
    }
}

loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (...) continue@loop
    }
}
```

* Un `break` con una etiqueta, salta fuera del bucle marcado con dicha etiqueta. En el ejemplo de arriba, el `break` hace que la ejecución salte fuera de los dos bucles `for` anidados.
* un `continue` con una etiqueta, salta a la siguiente iteración del bucle etiquetado. Es decir, en el ejemplo superior saltaría a la siguiente iteración del bucle del nivel superior.

### Return con Etiquetas

{% hint style="danger" %}
No puedo explicarlo bien por que aún no entiendo su uso.
{% endhint %}

En Kotlin, las funciones así como los objetos pueden encontrarse anidados unos dentro de otros. El uso de `return` con etiquetas nos permite retornar de una función exterior y no solo de la función anidada de la que estaríamos retornando sin utilizar dicha etiqueta.

{% hint style="info" %}
El caso de uso más típico es retornar desde funciones lambda.
{% endhint %}

Para ver más información sobre esto:

{% embed url="https://kotlin.desarrollador-android.com/basico/returns-y-jumps/" %}
Fuente: desarrollador-android.com
{% endembed %}
