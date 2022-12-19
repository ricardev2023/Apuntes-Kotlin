---
description: Explicación de la implementación de la herencia.
---

# Herencia

## [HERENCIA](teoria-poo.md#herencia)

Para explicar este concepto vamos a extender un poco la clase Slime antes de empezar:

<pre class="language-kotlin"><code class="lang-kotlin">val BAD_WORDS: Array&#x3C;String> = arrayOf("Feo", "Tonto", "CuatroOjos")

<strong>open class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
</strong>    private val name: String
    private var hp: Int
    private var ap: Int
    private var alive: Boolean = true

    init {
        if (name in BAD_WORDS) this.name = "BuenIntento" else this.name = name
        if (hp &#x3C;= 100) this.hp = hp else this.hp = Random.nextInt(0, 100)
        if (ap &#x3C;= 5) this.ap = ap else this.ap = Random.nextInt(0, 5)
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
</code></pre>

{% hint style="info" %}
**Explicación del código**

Se han añadido funciones muy sencillas como `sayHello`,  `heal`, `attack` o `evolve`. Estas funciones me permitirán explicar los conceptos que faltan de POO.
{% endhint %}

El problema que tenemos que solucionar actualmente es que tenemos Slimes de varios colores. Cada color de Slime tiene su propio tipo y por tanto sus ataques serán diferentes así como sus métodos.

Por ejemplo, el slime azul será de tipo agua y podrá mantener la respiración bajo el agua más que el resto. El rojo, de tipo fuego, tendrá resistencia a altas temperaturas. Sin embargo, todos ellos comparten todas las propiedades de la clase Slime.

La clase `Slime` en este caso se convertirá en la clase Padre o Superclase de las clases específicas de `SlimeAgua` o `SlimeFuego`.&#x20;

Las clases específicas `SlimeAgua` y `SlimeFuego` compartirán las propiedades de la clase padre `Slime` y además podrán tener las suyas particulares. Esto es lo que conocemos como [Herencia](teoria-poo.md#herencia).

### La clase Any

La clase Any es la raíz de la jerarquía de clases en Kotlin. Esto significa que cualquier clase que no herede explícitamente de otra superclase, lo hará implícitamente de la clase Any.

Esta clase Any tiene tres métodos según su implementación en [Any.kt](https://github.com/JetBrains/kotlin/blob/master/core/builtins/native/kotlin/Any.kt):

* `equals()`: Indica si otro objeto es igual al actual.
* `hashCode()`: Retorna el código hash asociado al objeto.
* `toString()`: Retorna la representación en `String` del objeto.

### Sintaxis

La sintaxis para aplicar la herencia es muy sencilla en Kotlin:

```kotlin
open class Padre
class Descendiente: Padre()
```

#### Modificador open

Las clases por defecto tienen el modificador `final`, lo que significa que son el útimo eslabón de su arbol genealógico. **Para que se pueda heredar de la clase Padre**, hay que añadir a su cabecera el modificador `open`.

#### Constructor primario

En el caso de que haya un constructor primario en la clase padre, habrá que inicializarlo en la clase descendiente:

```kotlin
open class Padre(val Arg1: T, val Arg2: T)
class Descendiente(Arg1: T, Arg2: T, val Arg3: T): Padre(Arg1, Arg2)
```

{% hint style="info" %}
Es importante darse cuenta de la inicialización de las variables en el ejemplo superior. `Arg1` y `Arg2` no están inicializadas en la clase `descendiente` por que se van a inicializar en el constructor de la clase `padre`.
{% endhint %}

#### Constructor secundario

Si la clase padre no tiene constructor primario o deseas realizar la llamada del mismo, desde un constructor secundario de la subclase, entonces usa la palabra reservada `constructor` junto a la palabra reservada `super` para la llamada.

```kotlin
open class Padre(val Arg1: T, val Arg2: T)

class Descendiente: Padre {
    constructor(Arg1: T, Arg2: T, val Arg3: T) : super(Arg1, Arg2)
}
```

### Aplicación práctica

La sintaxis de aplicación de la herencia es la siguiente:

```kotlin
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
        this.waterResistance++
    }
}
```

{% hint style="success" %}
Como puede ver, los argumentos que se le pasan a la clase `SlimeAgua` pero pertenecen a la clase `Slime`, no se inicializan con **val o var**.

`lungs` tampoco se inicializa con val o var por que no es un atributo, sino que se utiliza para inicializar el atributo `waterResistance`.

La clase `SlimeAgua` luego llama al constructor de la clase `Slime` de la que hereda para que se cree una instancia de la misma y poder crearse a partir de esa una instancia de la clase `SlimeAgua`.

Después nos encontramos con las propiedades que son exclusivas de la clase `SlimeAgua`. Tanto atributos como métodos pueden ser específicos.&#x20;
{% endhint %}

Ahora si que podemos hacer un objeto azulito como dios manda:

```kotlin
val azulito: SlimeAgua = SlimeAgua("CuatroOjos", 1000000, 500, 2)

println("name: " + azulito.getName())
println("hp: " + azulito.getHp())
println("ap: " + azulito.getAp())
println("alive: " + azulito.getAlive())
println("water Resistance: " + azulito.getWaterResistance())
println("time under Water: " + azulito.getTimeUnderWater())
azulito.sayHello()
azulito.heal()
println("hp: " + azulito.getHp())
azulito.attack()
repeat(10) {
    azulito.immerse()
}
println("time under Water: " + azulito.getTimeUnderWater())
println("\n${azulito.getName()} ha muerto.")
azulito.die()
println(println("alive: " + azulito.getAlive()))

/* 
name: BuenIntento
hp: 25
ap: 2
alive: true
water Resistance: 240
time under Water: 0
¡Hola soy BuenIntento
hp: 100
¡¡Al Ataque!!
time under Water: 10

BuenIntento ha muerto.
alive: false */
```

Se ve en el ejemplo anterior que azulito tiene acceso a todos los miembros de `Slime` así como a las propiedades específicas de `SlimeAgua`.
