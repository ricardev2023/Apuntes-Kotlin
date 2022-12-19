---
description: >-
  Explicación conceptos como subclases, objetos anónimos, data class o enum
  class.
---

# Otros Conceptos

## SUBCLASES

Llamamos subclases a la implementación de clases dentro de otras clases. No es lo mismo que la herencia, sino clases que han sido declaradas dentro de una clase superior. Existen dos tipos:

### Clases anidadas

Las clases anidadas son clases que se han declarado dentro de otra clase de ámbito superior pero son completamente independientes de ella. Es decir, no heredan de la clase de ámbito superior ni tienen acceso a los miembros de la misma.

```kotlin
class Subclasses {
    private var name = "Padre"
    fun presentar(): String { return this.name }

    class Anidada{
        private val nameAnidada = "Anidada"
        fun presentar(): String { return this.nameAnidada }
    }
}
```

```kotlin
val anidada:Subclasses.Anidada = Subclasses.Anidada()
println(anidada.presentar()) // Anidada
```

{% hint style="info" %}
Como se puede ver en el ejemplo superior, no hay ninguna relación entre la `clase subclasses` y la `clase Anidada`.&#x20;
{% endhint %}

### Clases internas

Por otro lado encontramos las subclases internas. En este caso, las subclases internas si que pueden acceder a todos los miembros de la clase externa.

La sintaxis de una clase interna es utilizando el modificador `inner` en la cabecera:

```kotlin
class Subclasses {
    private var name = "Padre"
    fun presentar(): String { return this.name }
    
    class Anidada{
        private val nameAnidada = "Anidada"
        fun presentar(): String { return this.nameAnidada }
    }
    inner class Interna{
        private val nameInterna = "Interna"
        fun presentar(): String { return "hola, soy ${this.nameInterna}, hija de ${name}" }
    }
}
```

```kotlin
val interna:Subclasses.Interna = Subclasses().Interna()
println(interna.presentar()) // hola, soy Interna, hija de Padre
```

{% hint style="info" %}
Es muy importante ver que, como la clase interna tiene acceso a los miembros de la clase externa, para inicializar la clase interna hay que llamar al constructor de la clase externa también `Subclasses().Interna()`.
{% endhint %}

## OBJETOS COMPAÑEROS

Un **companion object** es un objeto que se declara dentro de una clase pero que puede ser llamado sin necesidad de crear una instancia de dicha clase.

{% hint style="info" %}
En cierto modo son el equivalente a los objetos estáticos de lenguajes como Java.
{% endhint %}

### Declaración

```kotlin
class ClaseEjemplo {
    companion object {
        val propiedad: Int = 10

        fun metodo() = println("Método de ejemplo.")
    }
}
```

### Acceso

Tal y como se ha creado la clase `ClaseEjemplo`, podemos acceder al atributo `propiedad` y al método `metodo()` sin necesidad de crear un objeto del tipo `ClaseEjemplo`.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>println(ClaseEjemplo.propiedad) // 10
</strong>ClaseEjemplo.metodo() // Método de ejemplo.
</code></pre>

{% hint style="info" %}
El hecho de que un objeto compañero sea un objeto, hace que tenga las mismas características que los objetos:

* Puedo especificarle un nombre.
* Puedo aplicarle herencia.
* Puedo implementarle interfaces.
* Puedo declararle funciones y propiedades de extensión.
{% endhint %}

## OBJETOS ANÓNIMOS

{% embed url="https://www.develou.com/expresiones-de-objetos-en-kotlin/" %}
Fuente: develou
{% endembed %}

Las [expresiones de objetos](https://kotlinlang.org/docs/object-declarations.html#object-expressions) u objetos anónimos son el reemplazo a las clases internas anónimas de Java.

Su propósito es permitirte declarar una clase y crear una instancia de la misma en una sola expresión asignable. Donde no es necesario asignarle nombre a la clase o a su instancia.

Usa la palabra `object` y luego declara el cuerpo del mismo para asignar la instancia:

```kotlin
val enrique = object {
    var alive: Boolean = true
    
    fun apodo() = println("me llaman Enriquito")
}
enrique.apodo() // me llaman Enriquito
```

{% hint style="info" %}
Con los objetos anónimos no podemos crear más instancias de la misma clase pues es una clase anónima tambien.
{% endhint %}

## DATA CLASS

{% embed url="https://kotlinlang.org/docs/data-classes.html" %}
Fuente: kotlinlang.org
{% endembed %}

Una data class no es más que una clase que almacena datos. Es decir, una clase compuesta de atributos sin ningún método.

La ventaja de utilizar `data classes` en vez de clases normales es que Kotlin nos aporta una cantidad inmensa de código autogenerado:

* Las propiedades declaradas en el constructor: esto técnicamente no es exclusivo de una _`data class`_, pero nos evita todo tener que generar getters y setters para todo.
* Las funciones de Any.kt `equals()` y `hashCode()`.
* Una serie de funciones llamadas `componentX()`,  que son la base de la desestructuración. Con ellas podemos [recorrer los valores de un mapa](../curso-basico/tema-11.-colecciones.-mapas.md#recorrer-un-mapa) separando claves de valores.&#x20;
* Un método `copy()`, que nos será de mucha utilidad cuando utilicemos objetos inmutables.

```kotlin
data class star(var name: String = "" , 
                val radius: Float = 0f, 
                var galaxy: String = ""
) {
    var alive = true
}
```

```kotlin
var sol : star = star("Sol", 696340f, "Vía Láctea")
println(sol)

var betelgeuse : star = star("Betelgeuse", 617100000f, "Orión")
betelgeuse.alive = false
println(betelgeuse.alive)

var nueva : star = star()
println(nueva)
```

## ENUM CLASS

{% embed url="https://blog.logrocket.com/kotlin-enum-classes-complete-guide/" %}
Fuente: logrocket.com
{% endembed %}

Una funcionalidad de gran utilidad cuando programamos es tener la habilidad de indicar que una variable solo va a tener un número finito de valores posibles. Por ejemplo, los días de la semana o los nombres de los meses ya están preestablecidos.

Para conseguir esto, la mayoría de lenguajes de programación implementan enumeraciones. Sin embargo, Kotlin implementa las enum class que son mucho más versátiles que las enumeraciones al darnos todo el poder de las clases.

Esto se traduce en el hecho de que las enum class pueden tener propiedades y métodos personalizados, así como implementar interfaces, objetos anónimos y mucho más.

Además, el uso de enum classes permite hacer el código más facil de leer así como evitar errores.&#x20;

### Definir una enum class

```kotlin
enum class Day {   
    MONDAY, 
    TUESDAY,
    WEDNESDAY, 
    THURSDAY, 
    FRIDAY, 
    SATURDAY,
    SUNDAY
}
```

Esta es la forma más básica de definir una clase enum.&#x20;

### Métodos internos

Kotlin nos provee con dos métodos internos para las enum class que son muy útiles:

* **ordinal:** Nos devuelve el índice en el que se encuentra la variable en la enumeración.
* **name:** Nos devuelve el nombre de la variable.

```kotlin
for (day in DAY.values())
        println(
        "[${day.ordinal}] -> ${day.name}"
        )
/* Resultado
[0] -> MONDAY
[1] -> TUESDAY
[2] -> WEDNESDAY
[3] -> THURSDAY
[4] -> FRIDAY
[5] -> SATURDAY
[6] -> SUNDAY */
```

### Inicializar una enum class

Al ser clases pueden tener uno o más constructores, aunque lo más sencillo es pasarle los valores directamente al constructor de las constantes que no son más que instancias de la enum class:

```kotlin
enum class Day(val dayOfWeek: Int) {    
    MONDAY(1), 
    TUESDAY(2),
    WEDNESDAY(3), 
    THURSDAY(4), 
    FRIDAY(5), 
    SATURDAY(6),
    SUNDAY(7)
}
```

### Operaciones complejas

Una enum class puede tener todo lo que una clase puede tener, aunque a veces varía un poco la sintaxis:

```kotlin
enum class Day {
    MONDAY(1, "Monday"),
    TUESDAY(2, "Tuesday"),
    WEDNESDAY(3, "Wednesday"),
    THURSDAY(4, "Thursday"),
    FRIDAY(5, "Friday"),
    SATURDAY(6, "Saturday"),
    SUNDAY(7, "Sunday"); // end of the constants

    // custom properties with default values
    var dayOfWeek: Int? = null
    var printableName : String? = null

    constructor()

    // custom constructors
    constructor(
        dayOfWeek: Int,
        printableName: String
    ) {
        this.dayOfWeek = dayOfWeek
        this.printableName = printableName
    }

    // custom method
    fun customToString(): String {
        return "[${dayOfWeek}] -> $printableName"
    }
    
    companion object {
    fun getNumberOfDays() = values().size
    }
    
}
```

## CLASES SELLADAS

{% embed url="https://www.adictosaltrabajo.com/2019/06/27/clases-selladas-y-enumerados-en-kotlin/" %}
Fuente: adictosaltrabajo.com
{% endembed %}

### Concepto

La principal limitación de las `enum class` es que todos los elementos de la enumeración son objetos de la clase enum class y por lo tanto tienen los mismo atributos y métodos.

Para solucionar ese problema se desarrollaron las clases selladas que se utilizan como enumeraciones pero en las que cada elemento es una subclase con sus atributos y métodos propios.

### Ventajas

* La más importante es que **cada subclase puede tener sus propios atributos y sus propios métodos**, a diferencia de las `enum class`, cuyos elementos siguen todos la misma estructura.
* Además, las `enum class` solamente pueden tener una instancia, mientras que las subclases de clases selladas **pueden tener varias instancias**, cada una con su estado, **o una** si la definimos como _object_.

### Declaración de sealed class

```kotlin
sealed class Operation {
    class Add(val value: Int) : Operation()
    class Substract(val value: Int) : Operation()
    class Multiply(val value: Int) : Operation()
    class Divide(val value: Int) : Operation()
}
```

Si ahora tratamos de realizar una operación when, nos exigirá dar un comportamiento a cada subclase de la clase sellada, sino, no compilará:

```kotlin
fun execute(x: Int, op: Operation) = when (op) {
    is Operation.Add -> x + op.value
    is Operation.Substract -> x - op.value
    is Operation.Multiply -> x * op.value
    is Operation.Divide -> x / op.value
}
```

{% hint style="info" %}
Además, como se ve arriba, no es necesaria sentencia else debido a que ya están todas las subclases cubiertas.
{% endhint %}

Las `sealed class` tienen un potencial muy grande y permiten implementar de manera sencilla ideas muy complejas.&#x20;
