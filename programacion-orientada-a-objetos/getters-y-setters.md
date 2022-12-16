---
description: Explicación de los métodos get y set.
---

# Getters y Setters

## APLICACIÓN [PRINCIPIO DE OCULTACIÓN](teoria-poo.md#principio-de-ocultacion)

Hasta ahora tenemos nuestra clase Slime de la siguiente manera:

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    var name: String
    var hp: Int
    var ap: Int
    var alive: Boolean = true

    init {
        if (name in BAD_WORDS) this.name = "BuenIntento" else this.name = name
        if (hp <= 100) this.hp = hp else this.hp = Random.nextInt(0, 100)
        if (ap <= 5) this.ap = ap else this.ap = Random.nextInt(0, 5)
    }  
    fun die() {
    this.alive = false
    }
}
```

Hemos diseñado un constructor que evita que el usuario pueda introducir valores superiores a 100 en hp y a 5 en ap.&#x20;

Sin embargo, el usuario aun puede acceder a dichos valores como miembros que son de la clase y modificarlos a su antojo, evitando dicha comprobación del constructor:

```kotlin
    val azulito: Slime = Slime("CuatroOjos", 1000000, 500)
    
    println("name: " + azulito.name)    // name: azulito
    println("hp: " + azulito.hp)        // hp: 53 (aleatorio 0  a 100)
    println("ap: " + azulito.ap)        // ap: 2 (aleatorio 0 a 5)
    println("alive: " + azulito.alive)  // alive: true
    azulito.hp = 1000000
    azulito.ap = 500
    println("hp: " + azulito.hp)        // hp: 1000000
    println("ap: " + azulito.ap)        // ap: 500
```

Para evitar eso debemos utilizar los modificadores de visibilidad que permiten restringir el acceso a diferentes partes del código (variables, clases, constructores...):

* `private`: Marca una declaración como visible en la clase o archivo actual.
* `protected`: Marca una declaración como visible en la clase y subclases de la misma.
* `internal`: Marca una declaración como visible en el módulo actual.
* `public`: Marca una declaración como visible en todas partes.

De esta manera estaríamos aplicando el principio de ocultación:

```kotlin
class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    private val name: String
    private var hp: Int
    private var ap: Int
    private var alive: Boolean = true
    /*...*/
```

```kotlin
// Las lineas de abajo, ahora darán error.
println("name: " + azulito.name)
println("hp: " + azulito.hp)
println("ap: " + azulito.ap)
println("alive: " + azulito.alive)
azulito.hp = 1000000
azulito.ap = 500
```

Sin embargo, ahora no podemos acceder a la información almacenada en las variables ni modificarla. Para eso se utilizan las funciones get y las funciones set.

## APLICACIÓN DE [ENCAPSULAMIENTO](teoria-poo.md#encapsulamiento)

### Funciones get()

Las funciones `get()` nos permiten acceder a la información almacenada dentro de las propiedades de un objeto:

{% hint style="success" %}
Cuando se crea un atributo `val`, el compilador crea una función `get()` por defecto que es la que en el ejemplo inmediatamente inferior estamos personalizando.&#x20;

No se crea función `set()` ya que una `val` no puede modificar su valor.
{% endhint %}

```kotlin
class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    var name: String    // esta no es private para el ejemplo
        get() = "Este Slime se llama: $field."
    private var hp: Int
        get() = "Este Slime tiene $field Puntos de Salud."
    private var ap: Int
        get() = "Este Slime tiene $field Puntos de Ataque."
    private var alive: Boolean = true
        get() = field
```

```kotlin
println(azulito.name) // Este Slime se llama: Azulito.
```

Sin embargo, al haber hecho nuestras variables privadas, no va a servir esta forma de ejecutar los **getters** ya que no tenemos capacidad de visualizarlos. &#x20;

Tendremos que utilizar la siguiente opción. Crear funciones miembro de la clase que hagan el trabajo de las funciones `get()`:

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
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
        
    fun die() {
    this.alive = false
    }
}
```

```kotlin
println("name: " + azulito.getName())
println("hp: " + azulito.getHp())
println("ap: " + azulito.getAp())
println("alive: " + azulito.getAlive())
```

### Funciones set()

Se utilizan para modificar el contenido de un atributo.&#x20;

{% hint style="success" %}
Cuando se crea un atributo `var`, el compilador crea una función `get()` por defecto, así como una función `set()` que es la que en el ejemplo inmediatamente inferior estamos personalizando.&#x20;
{% endhint %}

```kotlin
class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    var name: String    // esta no es private para el ejemplo
        get() = "Este Slime se llama: $field."
    private var hp: Int
        get() = "Este Slime tiene $field Puntos de Salud."
        set(value) {
            if (value > 100) field = Random.NextInt(0, 100) else field = value
        }
    private var ap: Int
        get() = "Este Slime tiene $field Puntos de Ataque."
        set(value) {
            if (value > 5) field = Random.NextInt(0, 5) else field = value
        }
    private var alive: Boolean = true
        get() = field
```

Sin embargo, como ha pasado anteriormente, no podemos hacer esto pues hemos hecho privados nuestros atributos.&#x20;

Para solventarlo vamos a crear unas funciones que actuen como los setter que hemos definido arriba:

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
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

    fun die() {
        this.alive = false
    }
}
```
