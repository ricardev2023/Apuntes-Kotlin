# Tema 12. Funciones

## FUNCIÓN

Una función es una pieza de código reutilizable que solo se ejecuta cuando es llamada.

### Sintaxis

```kotlin
fun funcion(argumento1: tipo, argumentoN: tipo):tipo_return {
    bloque de código
    return n: tipo_return
}
```

Un ejemplo completo:

```kotlin
fun suma(x: String, y: String): Int {
    return x.toInt() + y.toInt()
}
```

Los elementos de la declaración de una función son los siguientes.

* **Nombre de la función** -> Es el nombre que eliges para la función. Por convenio se escribe en  camelCase.
* **Lista de parámetros** -> Datos de entrada para la función. Definidos como `nombre: tipo` y separados por comas.
* **Tipo de retorno** -> Tipo de dato de salida de la función. Si la función retorna un valor es obligatorio definir su tipo.
* **Cuerpo de la función** -> Son todas las sentencias que realizan la tarea para llegar al resultado final.&#x20;
* **Retorno** ->Usa la expresión `return` para devolver el valor.

### Llamada a una función

Para llamar a una función utilizamos su nombre seguido de un conjunto de paréntesis `()`. Dentro de dichos paréntesis es donde se pondrán los parámetros si fueran necesarios.

```kotlin
fun suma(x: String, y: String): Int {
    return x.toInt() + y.toInt()
}

println(suma("2", "5"))
```

### Función con cuerpo de expresión

Si la función se reduce a una expresión, se puede reducir a función con cuerpo de expresión:

```kotlin
fun suma(x: Int, y: Int) = x + y

println(suma(2, 4))
```

### Función sin retorno

También se pueden implementar funciones que no tengan retorno. En este caso, el compilador implementa la función con un retorno por defecto de tipo Unit (equivalente al retorno tipo Void de Java).

```kotlin
fun par(x: Int) {
    if (x % 2 == 0) println("$x es par")
    else println("$x es impar")
}
// Esta función retorna Unit aunque para nosotros sea transparente.
```

## PARÁMETROS

### Pasar parámetros por nombre

Los parámetros se pueden pasar en Kotlin de la manera que hemos visto en los ejemplos de arriba o indicando el nombre de los parametros que estamos pasando a la función.&#x20;

{% hint style="warning" %}
Esto tiene como beneficio que se pueden desordenar, sin embargo, si quiero pasar solo algunos de los parámetros con nombre y otros no, solo puedo pasarlos de manera ordenada para evitar errores de compilación.
{% endhint %}

```kotlin
fun suma(x: Int, y: Int) = x + y

println(suma(2, 4)) // paso los parámetros de la manera tradicional.
println(suma(x = 2, y = 4)) // paso los parámetros con nombre.
println(suma(x = 2, 4)) // paso los parámetros mezclados, sin errores.
println(suma(y = 4, 2)) // esto dará error.
```

### Parámetros con valor por defecto

Igual que en otros lenguajes, Kotlin permite incluir un valor por defecto a los parámetros de una función para que lo tomen en caso de que no se pase un valor para dicho parámetro:

```kotlin
fun suma(x: Int = 2, y: Int = 4) = x + y

println(suma(2, 4)) // paso los parámetros de la manera tradicional.
println(suma(3)) // la función toma los valores 3 y 4 para la función.
println(suma()) // la función toma los valores por defecto 2 y 4 para la función.
println(suma(y = 4)) // la función toma el valor por defecto de x que es 2.
```

### Número variable de argumentos

Se puede hacer que un argumento reciba un número arbitrario de elementos. Estos elementos se almacenarán en un Array con el nombre del argumento.

Para ello utilizamos la palabra clave `vararg` delante del argumento:

```kotlin
fun suma(vararg x: Int): Int {
    var suma = 0
    for (i in x) suma += i
    return suma
}
println(suma(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)) // todos los elementos son parte de x.
```

## AMBITO DE LAS FUNCIONES

{% embed url="https://programandoointentandolo.com/2018/03/funciones-en-kotlin.html" %}
Fuente: programandoointentandolo.com
{% endembed %}

### Funciones de nivel superior

Son aquellas que están definidas a nivel de [paquete](../curso-basico/kotlin-basico.md#paquetes-e-importaciones).  Es decir, fuera de clases, objetos o interfaces.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>package prueba.test
</strong><strong>
</strong><strong>fun suma(x: Int = 2, y: Int = 4) = x + y
</strong></code></pre>

### Funciones miembro

Las funciones miembro son las funciones que se definen dentro de una clase o un objeto. &#x20;

Para llamarlas debemos de poner por delante el nombre del objeto `objeto.nombreFuncion()` o el de la clase si es un método «estatico» (Companion object) y que además de los propios parámetros que pueda tener la función también pueden acceder a las propiedades de la clase.

```kotlin
println("7".toInt()) // es una función miembro en la que se llama a un objeto
```

### Funciones locales

Son funciones que están declaradas en otras funciones.  Estas funciones pueden acceder a variables que están declaradas en su ámbito o en ámbitos superiores.

```kotlin
fun eliminaPares(numeros: List<Int>): List<Int> {
    var resultado: MutableList<Int> = ArrayList()

    // Funcion local
    fun esPar(numero: Int): Boolean = (numero % 2 == 0)

    for (numero in numeros) {
        if (!esPar(numero)) {
            resultado.add(numero)
        }
    }

    return resultado
}
```

## VARIABLES DE UNA FUNCIÓN

### Variables globales

Aquellas que están creadas en el nivel superior, es decir, a nivel de paquete.&#x20;

Por regla general, estas suelen ser las `const val` para  poder utilizarlas en cualquier ámbito del programa.

### Variables locales

Las variables locales han sido declaradas en el interior de una función o una clase y solo pueden ser utilizadas en este ámbito.

{% hint style="info" %}
Si yo declaro una variable dentro de un bucle `while` para controlar el número de iteraciones, me daré cuenta de que esta variable solo se puede utilizar dentro del bucle y, por tanto, no puedo utilizarla como parte de la **condición** del `while`.

Esto es el ámbito de una variable.&#x20;
{% endhint %}
