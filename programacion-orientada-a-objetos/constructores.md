---
description: Explicación de los tipos de constructores.
---

# Constructores

## DEFINICIÓN

```kotlin
val azulito: Slime = Slime() 
```

Si se fija, en el ejemplo superior estamos llamando a una función para inicializar nuestra variable.

{% hint style="success" %}
Esta función especial que inicializa una instancia de una clase se llama **constructor**.

Sí no se provee un constructor a la clase (como era el caso en nuestra clase Slime, el compilador genera uno sin parámetro por defecto. Como el del ejemplo.
{% endhint %}

Los constructores pueden ser **primarios** o **secundarios**.

## CONSTRUCTOR PRIMARIO

El constructor primario es parte de la cabecera de una clase. Este recibe como argumentos, aquellos datos que necesitas explícitamente para inicializar las propiedades al crear el objeto.

```kotlin
class Slime constructor(val name: String = "slimePorDefecto"){
    var hp: Int = 100
    var ap: Int = 5
    var alive: Boolean = true
    /*...*/
}
```

El constructor utiliza la palabra reservada `constructor`. Sin embargo, si no tiene anotaciones ni modificadores, se puede omitir.

```kotlin
class Slime (val name: String = "slimePorDefecto"){
/*...*/
```

Como puede ver, el constructor puede tener un valor por defecto o puede no tenerlo, igual que los [parámetros de una función](../programacion-funcional/tema-12.-funciones.md#parametros-con-valor-por-defecto), sin embargo, ahora puedo cambiar el nombre de mi objeto "azulito" aunque sea un val.

```kotlin
val azulito: Slime = Slime("Azulito")
```

### Bloques de inicialización

Los bloques de inicialización permiten añadir lógica a la inicialización de las propiedades.

Su sintaxis es la siguiente:

```kotlin
class Slime constructor(val name: String = "slimePorDefecto",
                        hp: Int = 100, 
                        ap: Int = 5) {
    var hp: Int
    var ap: Int
    var alive: Boolean = true
    
    init {
        if (hp <= 100) this.hp = hp else this.hp = 100
        if (ap <= 5) this.ap = ap else this.ap = 5
    }
```

{% hint style="info" %}
Como puede ver, los valores de **hp** y **a**p que se pasan al constructor ya no son val o var ya que esos no son atributos. Los atributos son los que están inicializados dentro de la clase.

Por otra parte, la [aplicación del encapsulamiento](teoria-poo.md#encapsulamiento) con el uso de la palabra reservada `this` tiene una aplicación fundamental aquí para diferenciar del **hp del constructor** y del **hp atributo**.
{% endhint %}

### Visibilidad del constructor

El constructor, igual que la clase en sí se puede modificar con los **modificadores de visibilidad** de Kotlin:

* `private`: Marca una declaración como visible en la clase o archivo actual.
* `protected`: Marca una declaración como visible en la clase y subclases de la misma.
* `internal`: Marca una declaración como visible en el módulo actual.
* `public`: Marca una declaración como visible en todas partes.

Esto lo utilizaremos mucho más para aplicar la [Herencia](teoria-poo.md#herencia) y el [principio de Ocultación](teoria-poo.md#principio-de-ocultacion) más adelante.

## CONSTRUCTOR SECUNDARIO

Si la lista de argumentos del constructor primario no satisface, en algun caso, la creación de objetos, se pueden crear constructores secundarios dentro del cuerpo de la clase.

Un ejemplo que podría darse en nuestro caso:

* Constructor primario solo para el nombre.
* Constructor secundario si me dan nombre y otros dos argumentos (hp y ap).

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

class Slime (name: String = "slimePorDefecto"){
    val name: String
    var hp: Int
    var ap: Int
    var alive: Boolean = true

    init {
        if (name in BAD_WORDS) this.name = "BuenIntento" else this.name = name
        this.hp = 100
        this.ap = 5
    }

    constructor(name: String, hp: Int, ap: Int): this(name) {
        if (hp <= 100) this.hp = hp else this.hp = Random.nextInt(0, 100)
        if (ap <= 5) this.ap = ap else this.ap = Random.nextInt(0, 5)
    }
    /*...*/
```

{% hint style="info" %}
**EXPLICACIÓN DEL CÓDIGO**

El **constructor primario** recibe un argumento:

* El nombre, si no le pone uno por defecto.

El **bloque init**:

* Trata el nombre comparándolo con una lista de palabras malsonantes y si coincide le cambia el nombre.
* Le da valor a hp y a ap por defecto.

El **constructor secundario**, recibe tres argumentos:

* El nombre se encuentra delegado al constructor primario (atención a la sintaxis de herencia). `:this(name)`
* Recibe tambien hp y ap por parámetro.
* Estos solo pueden ser unos determinados valores, si no lo son, son tratados y se inicializan de manera aleatoria en el intervalo marcado.
{% endhint %}

Se pueden tener tantos constructores secundarios como sean necesarios. Sin embargo, el ejemplo anterior se podría haber realizado igual de bien con un constructor primario y un bloque init:

```kotlin
val BAD_WORDS: Array<String> = arrayOf("Feo", "Tonto", "CuatroOjos")

class Slime (name: String = "slimePorDefecto", hp: Int = 100, ap: Int = 5){
    val name: String
    var hp: Int
    var ap: Int
    var alive: Boolean = true

    init {
        if (name in BAD_WORDS) this.name = "BuenIntento" else this.name = name
        if (hp <= 100) this.hp = hp else this.hp = Random.nextInt(0, 100)
        if (ap <= 5) this.ap = ap else this.ap = Random.nextInt(0, 5)
    /*...*/
    }
```

Y con eso hecho, si inicializamos un objeto de ésta clase intentando abusar recibiré lo siguiente:

```kotlin
val azulito: Slime = Slime("CuatroOjos", 1000000, 500)

println("name: " + azulito.name)
println("hp: " + azulito.hp)
println("ap: " + azulito.ap)
println("alive: " + azulito.alive)

/* Respuesta
name: BuenIntento
hp: 45
ap: 3
alive: true
*/
```
