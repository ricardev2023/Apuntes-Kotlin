---
description: Explicación del concepto de polimorfismo, tipos y aplicaciones reales.
---

# Polimorfismo

## CÓDIGO FUENTE

Se ha añadido una clase SlimeFuego para trabajar éste tema:

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

open class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    private val name: String
    private var hp: Int
    private var ap: Int
    private var alive: Boolean = true

    init {
        if (name in BAD_WORDS) this.name = "BuenIntento" else this.name = name
        if (hp <= 100) this.hp = hp else this.hp = Random.nextInt(0, 100)
        if (ap <= 5) this.ap = ap else this.ap = Random.nextInt(0, 5)
    }

    fun getName(): String = this.name
    fun getHp(): Int = this.hp
    fun getAp(): Int = this.ap
    fun getAlive(): Boolean = this.alive
    fun setHp(value: Int) {
        if (value > 100) this.hp = Random.nextInt(0, 100) else this.hp = value
    }
    fun setAp(value: Int) {
        if (value > 5) this.ap = Random.nextInt(0, 5) else this.ap = value
    }
    fun sayHello() = println("¡Hola soy ${getName()}")
    fun heal() {
        this.hp = 100
    }
    fun attack() = println("¡¡Al Ataque!!")
    fun evolve() {
        this.ap *= 2
    }
    fun die() {
        this.alive = false
    }
}

class SlimeAgua(name: String, hp: Int, ap: Int, lungs: Int): Slime(name, hp, ap) {
    private var waterResistance: Int
    private var timeUnderWater: Int = 0

    init{
        this.waterResistance = lungs * 120
    }
    fun getWaterResistance(): Int = this.waterResistance
    fun getTimeUnderWater(): Int = this.timeUnderWater
    fun breathe() {
        this.timeUnderWater = 0
    }
    fun immerse() {
        this.timeUnderWater++
    }
}

class SlimeFuego(name: String, hp: Int, ap: Int, ballTemperature: Int): Slime(name, hp, ap) {
    private val ballTemperature: Int = ballTemperature
    
    fun getBallTemperature(): Int = this.ballTemperature
}
```

## CLASES ABSTRACTAS

Una [clase abstracta](https://kotlinlang.org/docs/reference/classes.html#abstract-classes) es aquella que está marcada con el modificador `abstract` en su declaración. Esto evita que se creen instancias de la clase, pero no impide que se creen subclases a partir de ella.

Las clases abstractas son una pieza fundamental del polimorfismo ya que implementan métodos y atributos genéricos para que las subclases los puedan heredar, facilitando así la [abstracción](teoria-poo.md#abstraccion).

{% hint style="warning" %}
La diferencia entre utilizar una clase abstracta y una clase abierta para heredar es la capacidad de crear instancias de la primera. Sin embargo, **¿Cuándo utilizar una clase abstracta?**

Toda clase abstracta debe contener al menos un método abstracto.
{% endhint %}

### Métodos y Atributos abstractos

Los miembros de una clase abstracta también pueden ser marcados como `abstract`, lo que significa que no tendrán implementación, debido a que esta será exigida para las subclases.

```kotlin
abstract class ClaseAbstracta {
    val atributoNormal: String
    abstract val atributoAbstracto: Int

    abstract fun metodoAbstracto(): Array<Int>

    fun metodoNoAbstracto() {
        // Cuerpo
    }
}
```

## POLIMORFISMO

{% embed url="https://www.linkedin.com/pulse/el-polimorfismo-y-principio-de-substituci%C3%B3n-liskov-en-luis-vespa/" %}
Fuente: Luis Vespa (LinkedIn)
{% endembed %}

El [polimorfismo](teoria-poo.md#polimorfismo) es una de las características más importantes de la POO. Permite utilizar una interfaz única para hacer referencia a objetos de diferentes tipos. Existen dos tipos:

### Polimorfismo paramétrico

Permite que una función se escriba de forma genérica, de modo que pueda manejar valores de manera uniforme sin depender de su tipo.&#x20;

Este tipo de polimorfismo es tan común que se llama simplemente "Polimorfismo".

{% hint style="info" %}
**Funciones Polimórficas:**

Una función que puede evaluarse o aplicarse a valores de diferentes tipos se conoce como función polimórfica.
{% endhint %}

Para aplicar el polimorfismo paramétrico se puede hacer de dos maneras:

#### Polimorfismo paramétrico por herencia

En este caso, vamos a implementar la función de combate "`fight(Slime1, Slime2)`".&#x20;

Sin embargo, si no existiera el polimorfismo paramétrico tendría que implementar dicha función varias veces, cada una de ellas con unos argumentos diferentes en función del tipo de los Slime que combatan.

Gracias al polimorfismo y a la clase padre Slime que engloba a todas las clases hijo de SlimeTipo, podemos implementar una sola vez la función:

```kotlin
fun fight(x: Slime, y: Slime) {
    println("Comienza la batalla")
    println("En la esquina azul: ${x.getName()}")
    println("con un poder de: ${x.getAp()}")
    println("y una vida de: ${x.getHp()}")
    println()
    println("En la esquina roja: ${y.getName()}")
    println("con un poder de: ${y.getAp()}")
    println("y una vida de: ${y.getHp()}")
    println()
    while (x.getHp() > 0 && y.getHp() > 0) {
        x.attack()
        y.setHp(y.getHp() - x.getAp())
        y.attack()
        x.setHp(y.getHp() - y.getAp())
    }
    if (x.getHp() <= 0) {
        println("${y.getName()} es el ganador")
    } else println("${x.getName()} es el ganador")
}
```

```kotlin
val azulito: SlimeAgua = SlimeAgua("Azulito", 1000000, 500, 2)
val rojito: SlimeFuego = SlimeFuego("Rojito", 100, 5, 80)
fight(azulito, rojito)
```

Como vemos, la función coge como argumentos dos objetos de tipo `Slime`. Esto hace que todos los objetos que sean inferiores a `Slime` en el árbol genealógico puedan entrar en esa definición.&#x20;

Ese es el motivo por el que la llamada a la función fight no da error.

#### Polimorfismo paramétrico por clases abstractas

Lo mismo podemos hacer con una [clase abstracta](polimorfismo.md#clases-abstractas). De hecho, la clase Slime podría ser perfectamente una clase abstracta pues tiene un método "`attack`" que podríamos considerar abstracto y no se espera que se generen instancias de ella. Vamos a verlo muy resumido para el ejemplo:

```kotlin
abstract class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    /*...*/
    abstract fun attack()
    /*...*/
}

```

Con lo anterior, obligamos a cada una de las diferentes clases hijo a implementar su propia función `attack`.&#x20;

```kotlin
class SlimeAgua(name: String, hp: Int, ap: Int, lungs: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() = println("Ataque con chorro.")
}
class SlimeFuego(name: String, hp: Int, ap: Int, ballTemperature: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() = println("Ataque con bola de fuego.")
}
```

{% hint style="info" %}
Con los cambios que se han realizado, el ejemplo anterior funciona perfectamente, ya que en vez de heredar desde una clase `open`, heredan desde una clase `abstract`.

Sin embargo, ahora ya no se pueden crear objetos tipo Slime puesto que es una clase abstracta.

De la misma manera hemos aprendido a utilizar las funciones abstractas para generar funciones que aun llamándose igual, se comportan diferente en función del tipo del objeto. Esto es parte del **polimorfismo de subtipo** que vamos a ver ahora.
{% endhint %}

### Polimorfismo de subtipo

Como ya hemos visto en el anterior ejemplo, puede darse el caso de que tenga un método de la clase padre que en una de las clases hijo se comporta diferente a como se comporta en la clase padre.

En este caso vamos a estudiar dos posibilidades:

#### override

La palabra reservada `override` se utiliza en las clases hijo que desean cambiar el código de un método de la función padre por uno personalizado:

{% hint style="info" %}
Para el ejemplo vamos a volver a poner la clase Slime como clase open.
{% endhint %}

```kotlin
open class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    /*...*/
    open fun attack() = println("Al ataque!!")
    fun evolve() {
        this.ap *= 2
    }
}
```

Como vemos, la función `attack` ya no puede ser `abstract` pues daría error, para que se pueda sobreescribir como hemos hecho antes, utilizamos la palabra reservada `open` en la función tambien.&#x20;

```kotlin
class SlimeAgua(name: String, hp: Int, ap: Int, lungs: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() = println("Ataque con chorro.")
}
class SlimeFuego(name: String, hp: Int, ap: Int, ballTemperature: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() = println("Ataque con bola de fuego.")
}
```

#### super

Al contrario que la palabra reservada override, la palabra reservada super llama a una función de la clase padre.\
En el caso del ejemplo nos va a quedar muy claro:

```kotlin
class SlimeAgua(name: String, hp: Int, ap: Int, lungs: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() {
        super.attack()
        println("Ataque con chorro.")
    }
}
class SlimeFuego(name: String, hp: Int, ap: Int, ballTemperature: Int): Slime(name, hp, ap) {
    /*...*/
    override fun attack() {
        super.attack()
        println("Ataque con bola de fuego.")
    }
}
```

De esta manera, cuando lancemos la función `fight`, el log de la batalla quedará de la siguiente manera:

```kotlin
val azulito: SlimeAgua = SlimeAgua("Azulito", 1000000, 500, 2)
val rojito: SlimeFuego = SlimeFuego("Rojito", 100, 5, 80)
fight(azulito, rojito)

/* Respuesta
Comienza la batalla
En la esquina azul: Azulito
con un poder de: 0
y una vida de: 5

En la esquina roja: Rojito
con un poder de: 5
y una vida de: 100

Al ataque!!
Ataque con chorro.
Al ataque!!
Ataque con bola de fuego.
Rojito es el ganador */
```
