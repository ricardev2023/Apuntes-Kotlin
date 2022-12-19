---
description: Explicación del concepto, usos y tipos.
---

# Funciones de Alcance

## DEFINICIÓN

{% embed url="https://medium.com/droid-latam/kotlin-traducido-funciones-de-alcance-scope-functions-b5b21b656392" %}
Fuente: Martin Beltrame (medium)
{% endembed %}

Las funciones de alcance sirven para hacer nuestro código más legible. Cuando tenemos varias lineas de código que operan con un objeto, estas se pueden cambiar por una función de alcance que aclara el código.

> Por tanto, las **funciones de alcance** son aquellas cuyo único propósito es ejecutar un bloque de código dentro del contexto de un objeto.

La librería estandar cuenta actualmente con las siguientes funciones de alcance:

* `also`
* `let`
* `apply`
* `run`
* `with`

## DIFERENCIAS

Hay dos elementos que las diferencian:

#### Como accedemos al objeto:

* Para las funciones `let` y `also` utilizamos la palabra reservada **it**.
* Para **** `run`, `with` y `apply` utilizamos **this**.

#### Que valor retorna

* `apply` y `also` devuelven el objeto como tal.
* `let`, `run` y `with` devuelven el valor de retorno del lambda, es decir, retorna el valor de nuestra última sentencia ejecutada.

## TIPOS

### also

`also`, tiene un buen uso cuando realizamos algunas acciones que no están estrictamente relacionadas con el objeto en sí, pero que lo utilizan como argumento.

Se lee como: _y también realiza lo siguiente._

```kotlin
data class Zapato(
    var size: Int = 38,
    var color: String = "Negro",
    var stock: Int = 10
)

// Sin utilizar el with
fun main() {
    val zapatoNuevo = Zapato()

    val datosZapato = zapatoNuevo.apply {
        size = 42
        color = "Rojo"
        stock = 25
    }.toString()

    print(datosZapato)
}

// Utilizando el with
fun main() {
    val zapatoNuevo = Zapato().apply {
        size = 42
        color = "Rojo"
        stock = 25
    }.also {
        print(it)
    }
}
```

Como `apply` devuelve la nueva instancia de `Zapato()` almacenada en `zapatoNuevo`, podemos utilizar `also` para imprimirlo.

### let

`let`,  se suele utilizar en dos situaciones distintas:

* Cuando queremos ejecutar un bloque de código solo con valores no nulos.&#x20;
* Para invocar una o más funciones con resultados en cadena.

La función `let` siempre va acompañada de una lambda.

```kotlin
fun main() {
    val invoice = Invoice(
        "Fabricia",
        listOf(
            InvoiceLine(5.0),
            InvoiceLine(4.0),
            InvoiceLine(6.0)
        )
    )

    val invoiceDetail = invoice.let {
        val total = it.lines.sumOf { line -> line.unitCost }
        "La factura de ${it.customer} tiene un total de $total"
    }

    println(invoiceDetail)
}
```

### apply

`apply`, es común utilizarlo para la inicialización de objetos.

Se lee como: _aplicar las siguientes asignaciones al objeto._

<pre class="language-kotlin"><code class="lang-kotlin">// Esta es la clase de la que queremos generar una instancia
data class Zapato(
    var size: Int = 38,
    var color: String = "Negro",
    var stock: Int = 10
)
<strong>
</strong><strong>// Ahora inicializamos el objeto con apply
</strong>fun main() {
    val zapatoNuevo = Zapato().apply {
        size = 42
        color = "Rojo"
        stock = 25
    }
}
</code></pre>

### run

`run` se suele utilizar cuando inicializamos una variable seguido de una interacción con la misma.

Tiene la particularidad de que no siempre es necesario utilizar el **`this` ** para referenciar al objeto dentro del scope:

```kotlin
fun main() {
    val resultado = "Ejemplo".run {
        println("El String \"$this\" tiene $length caracteres")
        length
    }
}
```

{% hint style="info" %}
Lo normal sería utilizar "`$this.length`" pero Kotlin lo reconoce sin necesidad de la palabra reservada.
{% endhint %}

### with

`with`, a diferencia de las demás funciones, **** pasa al objeto como parámetro en vez de ser el objeto quién llame a la función. Se suele utilizar en contextos donde no necesitamos obtener un resultado en sí mismo, sino que queremos aplicar una operación con/sobre el objeto.

Se lee como: _con este objeto, hacemos lo siguiente._

```kotlin
val numbers = mutableListOf("one", "two", "three")
val firstAndLast = with(numbers) {
    "The first element is ${first()}," +
    " the last element is ${last()}"
}
print(firstAndLast)
```
