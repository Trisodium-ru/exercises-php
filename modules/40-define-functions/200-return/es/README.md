Las funciones que definimos en lecciones anteriores terminaban su ejecución imprimiendo algún dato en la pantalla:

```php
<?php

function saludo()
{
    print_r('¡Hola, Hexlet!');
}
```

Sin embargo, este tipo de funciones no son muy útiles, ya que no podemos usar sus resultados dentro del programa. Para poder hacerlo, necesitamos que las funciones retornen un valor, y eso es lo que aprenderemos en esta lección.

Consideremos el caso del procesamiento de correos electrónicos. Cuando un usuario se registra en un sitio web, puede ingresar su correo electrónico de cualquier manera:

* Agregar espacios en blanco al principio o al final `_soporte@hexlet.io__`
* Usar letras en diferentes casos `SOPORTE@hexlet.io`

Si almacenamos el correo electrónico en la base de datos en este formato, el usuario no podrá acceder al sitio web si ingresa la dirección sin espacios y en un caso diferente.

Para evitar esto, debemos preparar el correo electrónico para ser almacenado en la base de datos. Esto implica convertirlo a minúsculas y eliminar los espacios en blanco alrededor del texto. Esta tarea se resuelve en un par de líneas:

```php
<?php

function guardarCorreo()
{
    $correo = "  SoPORTE@hexlet.IO";
    // Eliminamos espacios en blanco alrededor
    // La función trim() elimina los espacios en blanco del principio y el final de una cadena
    $correoRecortado = trim($correo);
    $correoPreparado = strtolower($correoRecortado);
    print_r($correoPreparado);
    // Aquí se realizaría el almacenamiento en la base de datos
}
```

Este código es posible gracias al retorno de valores. Las funciones `trim()` y `strtolower()` no imprimen nada en la pantalla. En cambio, devuelven el resultado de su trabajo, lo que nos permite asignarlo a variables.

Si estas funciones imprimieran en la pantalla en lugar de retornar valores, no podríamos asignar el resultado a una variable, tal como no podemos hacer con la función `saludo()` definida anteriormente:

```php
<?php

$mensaje = saludo();
// Para ver "null", necesitamos usar la función var_dump()
var_dump($mensaje); // => NULL
```

Modificaremos la función `saludo()` para que comience a retornar datos en lugar de imprimirlos. Para hacerlo, necesitamos usar la instrucción de retorno en lugar de imprimir en pantalla:

```php
<?php

function saludo()
{
    return '¡Hola, Hexlet!';
}
```

La instrucción `return` es especial. Toma la expresión que se encuentra a su derecha y la devuelve al código que llamó a la función. Tan pronto como PHP encuentra `return`, la ejecución de la función termina:

![Sum-php](assets/sum-php.jpg)

```php
<?php

// Ahora podemos usar el resultado de la función
$mensaje = saludo();
print_r($mensaje); // => '¡Hola, Hexlet!'
// También podemos realizar acciones con el resultado
print_r(strtoupper($mensaje)); // => '¡HOLA, HEXLET!'
```

Cualquier código después de `return` no se ejecuta:

```php
<?php

function saludo()
{
    return '¡Hola, Hexlet!';
    print_r('Nunca me ejecutaré');
}
```

Incluso si una función retorna datos, esto no impide que imprima en pantalla. Además de retornar valores, también podemos imprimir:

```php
<?php

function saludo()
{
    print_r('Apareceré en la consola');
    return '¡Hola, Hexlet!';
}
// Imprimirá el texto en pantalla y retornará el valor
$mensaje = saludo();
```

No solo podemos retornar un valor específico. Dado que `return` trabaja con expresiones, prácticamente cualquier cosa puede estar a su derecha. Aquí debemos seguir los principios de legibilidad del código:

```php
<?php

function saludo()
{
    $mensaje = '¡Hola, Hexlet!';
    return $mensaje;
}
```

Aquí no estamos retornando la variable en sí, siempre estamos retornando el valor que está contenido en esa variable. Aquí tienes un ejemplo con cálculos:

```php
<?php

function dobleCinco()
{
    // o return 5 + 5
    $resultado = 5 + 5;
    return $resultado;
}
```

Para poner a prueba tus conocimientos, intenta responder esta pregunta. ¿Qué imprimirá este código?

```php
<?php

// Definición
function ejecutar()
{
    // Return
    return 5;
    return 10;
}
// Uso
ejecutar(); // => ?
```
