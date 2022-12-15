---
description: >-
  Explicación de la declaración de variables y conceptos como constructor,
  método set y método get.
---

# CLASES Y OBJETOS

{% hint style="success" %}
Vamos a trabajar toda la parte de Programación Orientada a Objetos sobre un proyecto en el cual vamos a crear un simulador de combate entre Slimes de Dragon Quest.

Los Slimes tienen características como: color, nombre, vida, poder de ataque...
{% endhint %}

<figure><img src="../.gitbook/assets/slimes.png" alt=""><figcaption><p>Slimes de Dragon Quest</p></figcaption></figure>

## DECLARAR CLASES

### Sintaxis

Para declarar una clase utilizamos siempre la siguiente sintaxis:

* palabra reservada `class`.
* nombre de clase.
* cabecera (opcional).
* cuerpo de la clase (opcional).
  * atributos de la clase.
  * métodos de la clase.

```kotlin
class Slime/*cabecera*/{
    /*atributos de la clase*/
    /*métodos de la clase*/
}
```

La **cabecera** en el caso anterior está vacía pero poco a poco veremos diferentes elementos que se declaran en ella como por ejemplo:

* Modificadores
* Declaración de parámetros
* Constructor primario
* Herencia
* Restricciones de tipo

```kotlin
// En Kotlin esta declaración de clase es válida

class Slime 
```

{% hint style="info" %}
Las clases se escriben siempre, por convenio, en CamelCase, con la primera letra en mayúscula. Exactamente igual que los tipos en Kotlin.
{% endhint %}

### Ejemplo de declaración

Ahora vamos a declarar la clase Slime. Un Slime tiene las siguientes características:

* Un nombre que los identifica. `name: String`.
* Una cantidad de vida concreta medida en HP. `hp: Int`.
* Una cantidad de poder de ataque medida en AP. `ap: Int`.
* Pueden estar vivos o no estarlos. `alive: Boolean`.
* Tienen un tipo en función del color. Pero lo implementaremos cuando veamos la **herencia**.

Pues bien, las anteriores características son los **atributos de la clase Slime**.

Además, podemos añadir un método que se utilizará cuando el Slime muera, llamado `die()`.

```kotlin
class Slime {
    val name: String = "slimePorDefecto"
    var hp: Int = 100
    var ap: Int = 5
    var alive: Boolean = true
    
    fun die() {
        alive = false
    }
}
```

### Encapsulamiento&#x20;

El [encapsulamiento](teoria-poo.md#encapsulamiento), como ya hemos definido consiste en reunir los datos que utliza una entidad en el mismo nivel de abstracción.&#x20;

En el caso anterior, si yo tuviera varias variables `alive` declaradas en diferentes niveles de mi programa, podría darse una colisión al llamar al método `die()` pues el compilador no sabe qué variable `alive` utilizar.

Para evitar éste problema, utilizamos la palabra reservada `this`.  Este elemento permite indicar a un método que está utilizando la variable de la misma clase y no otra.

Por tanto el código quedaría así:

```kotlin
class Slime {
    val name: String = "slimePorDefecto"
    var hp: Int = 100
    var ap: Int = 5
    var alive: Boolean = true
    
    fun die() {
        this.alive = false
    }
}
```

## DECLARAR INSTANCIAS

### Sintaxis

Tras **declarar una clase** podemos utilizarla para **declarar objetos en base a dicha clase**. Para ello utilizamos la misma sintaxis que se utiliza al declarar una variable de cualquier otro tipo:

```kotlin
val azulito: Slime = Slime()
```

### Acceso a miembros

Los miembros son los métodos y los atributos de nuestro objeto. Para acceder a ellos utilizamos la notación que ya conocemos:

```kotlin
println("name: " + azulito.name)
println("hp: " + azulito.hp)
println("ap: " + azulito.ap)
println("alive: " + azulito.alive)

println("\n${azulito.name} ha muerto.")
azulito.die()
println(println("alive: " + azulito.alive))

/* Resultado
name: slimePorDefecto
hp: 100
ap: 5
alive: true

slimePorDefecto ha muerto.
alive: false */
```

### Modificación de miembros

Como hemos visto anteriormente, según el [principio de ocultación](teoria-poo.md#principio-de-ocultacion), no deberíamos tener acceso libre a los miembros de la clase, sin embargo ahora mismo sí que lo tenemos.

Por ese motivo podemos cambiar los valores por defecto de nuestro Slime y lo podemos convertir en un Slime muy fuerte:

```kotlin
azulito.hp = 1000000
azulito.ap = 500

azulito.name = "Azulito" // Esto dará error por ser val.
```

Pero cómo puede ver, esto es una falta de seguridad, ya que puedo modificar dichos valores a voluntad pero sigo sin poder ponerle el nombre que quiero a mi Slime.&#x20;
