---
description: Explicación del concepto y uso de interfaces para aplicarlo.
---

# Herencia múltiple

## CONCEPTO

Algunos lenguajes orientados a objeto, como C++, Perl o Python, soportan la herencia múltiple. Es decir, pueden extender simultáneamente más de una clase. Esta característica presenta cierta ambigüedad a la hora de acceder a los atributos de los padres, lo que hace que aumente la complejidad del lenguaje.

Kotlin, no soporta herencia múltiple. Por lo que solo pueden extender de una clase; lo que simplifica en gran medida el lenguaje.&#x20;

Lo que sí que va a permitir este lenguaje es que una clase además de extender de su padre puedan implementar varios interfaces.

## INTERFACES

### Definición pura

La interfaz es una clase abstracta pura, es decir, una clase donde se indican los métodos, pero no se implementa ninguno.&#x20;

Permite al programador establecer una estructura que ha de seguir toda clase que implemente esta interfaz.&#x20;

En la interfaz solo se indica los nombres de los métodos, sus parámetros y tipos que retornan, pero no el código de cada método. Una interfaz también puede contener constantes, pero nunca pude campos de otro tipo.  **En Kotlin** estos campos se declaran dentro de un `companion object`.

### Definición específica en Kotlin

{% embed url="https://kotlinlang.org/docs/interfaces.html#properties-in-interfaces" %}
Fuente: kotlinlang.org
{% endembed %}

{% hint style="warning" %}
El lenguaje de programación Kotlin permite **implementar las funciones en la misma interfaz sin que esto genere errores**. Sin embargo, la idea de las interfaces es la que aparece arriba.

De la misma manera, en Kotlin **sí que puedo indicar un atributo**, sin embargo, en la clase que herede de la interfaz, tendré que hacer un override del atributo para evitar que me dé error.&#x20;

Esto es por que dicho atributo no se puede inicializar en la interfaz ya que las interfaces carecen de constructor.
{% endhint %}

```kotlin
interface SerVivo {
    fun breathe(): Boolean
    fun blink() = println("Acaba de parpadear")
    val eyes: Int

    companion object{
        val AZUL = 0x0000FF
    }
}
```

Si yo ahora quisiera crear una clase ser humano que herede de SerVivo, me encontraría lo siguiente:

```kotlin
class Serhumano(var name: String, var age: Int, var alive: Boolean): SerVivo {
    override val eyes: Int = 2
    
    override fun breathe(): Boolean {
        if (alive) {
            println("respira")
            return true
        } else {
            println("no respira")
            return false
        }
    }
}
```

Como vemos, la función blink hace falta sobreescribirla por que ya se encuentra implementada en la interfaz. Entonces a la hora de crear un objeto de tipo SerHumano, podemos acceder a todo lo anterior:

```kotlin
val enrique: SerHumano = SerHumano("Enrique", 55, true)
println("El ser se llama ${enrique.name}")
repeat(3){
    enrique.blink()
}
enrique.breathe()
enrique.alive = false
enrique.breathe()

/* Resultado
El ser se llama Enrique
Acaba de parpadear
Acaba de parpadear
Acaba de parpadear
respira
no respira */
```
