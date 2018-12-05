# You Don't Know JS: Up & Going
# Cápitulo 1: Introducción a la programación

Bienvenidos a la serie *You Don't Know JS* (*YDKJS*)

*Up & Going* is introductorio a varios conceptos básicos de programación -- por supuesto apuntando a JavaScript (normalmente abreviado a JS) específicamente -- a como acercarse y entender el resto de los títulos de esta serie. Especialmente si hasta ahora se está comenzando a programar y/o JavaScript, este libro explicará brevemente lo que se necesita para comenzar

Este libro comienza explicando los conceptos básicos de programación a un alto nivel. Es más apuntado a lectores que están comenzando a leer *YDKJS* con poca o nada experiencia de programación, y viendo este conjunto de libros para comenzar el camino introductorio de la programación, a través de los lentes de JavaScript.

El capítulo 1 está enfocado a una visión general de todas las cosas que se deberían aprender y practicar al querer entrar a *programar*. Hay también otros recursos introductorios fantásticos que le ayudarán a entender más estos temas a mayor profundidad, y recomiendo que los lea aparte de este capítulo.

Una vez se sienta cómo con los temas basicos de programación, capítulo que lo guiará a familiarizarse con la forma de escribir código en JavaScript. Capitulo dos introduce JavaScript, sin embargo, no de una manera profunda y no es una guia completa -- para eso están los restos de libros de *YDKJS*!

Si ya se siente cómodo con JavaScript, revise de primero el capítulo 3 como un repaso y una pequeña introducción a lo que debe esperar de *YDKJS*. Comenzemos.

## Código

Iniciemos desde los origenes.

Un programa, en ocasiones denominado *código fuente* o *código*, es un conjunto especial de instrucciones que indican a un computador que tareas debe realizar. Usalmente el código se almacena en un archivo de texto, sin embargo con JavaScript puedes escribir  y ejecutar código en la consola del navegador, de lo cual hablaremos más adelante.

Las reglas que validan el formato y el conjunto de instrucciones de un programa se denomina *Lenguaje de programación*, aveces referido también como la *sintaxis de un lenguaje*, de manera similar en que hay reglas en el Inglés que indican como pronunciar palabras y como crear oraciones válidas usando estas palabras y signos de puntuación.

### Sentencias 

En un lenguaje de programación, un conjunto de palabras, números, y operadores que llevan a cabo una tarea específica se denomina *sentencia*. En JavaScript, una sentencia podría verse de la siguiente forma: 

```js
a = b * 2;
```
Los caracteres `a` y `b` se denominan *variables* (ver "Variables"), que pueden ser vistas como cajas para guardar cualquier elemento. En programación, las variables guardan valores (Como por ejemplo el número `42`) que pueden ser usados por un programa. Puedes pensar en las variables como marcadores simbólicos para los valores por si mismos.

En contraste, el `2` es sencillamente un valor, lo que se conoce como *Literal value*, porque no se encuentra almacenando en ninguna variable.

Los caracteres `=` y `*` son *operadores* (ver "Operadores") -- que llevan a cabo acciones con los valores y variables de asignación y multiplicación matemática.

La mayoría de sentencias en JavaScript terminan con un punto y coma (`;`) al final de la misma.

La sentencia `a = b * 2;` le ordena al computador, leer el valor actual almacenado en la  variable `b`, multiplicar este valor por `2`, y guardar el resultado en una variable que llamamos `a`.

Los programas son una colección de varias sentencias, que en conjunto describen los pasos que requiere ejecutar un programa con determinado propósito.

### Expresiones 

Las declaraciones están hechas de una o más *expresiones*. Una expresión es cualquier referencia a una variable o valor, o un conjunto de variables o valores combinado con operadores.

Por ejemplo:

```js
a = b * 2;
```

Esta declaración tiene varias expresiones en ella:

* `2` es una *expresión literal de valor* 
* `b` es una *expresión de variable*, que significa buscar su valor actual
* `b * 2` es una *expresión aritmetica*, que significa hacer la multiplicación
* `a = b * 2` es una *expresión de asignación*, que significa asignar el resultado de la expresión `b * 2` a la variable `a` (más en el tema de asignación más adelante en el capítulo)

Una expresión general que tiene su propio lugar es también la llamada *expresión de declaración*, como la siguiente

```js
b * 2;
```

Esta forma de declaración es muy útil o común, ya que no tendría nungún efecto en el correr del programa. Ya que buscaría  el valor de `b` lo multiplicaría por `2`, y luego no haría nada con el resultado.

Una expresión más común es llamada declaraciones de *expresiones de llamada* (mirar "Funciones"), ya que la declaración de la función se llama a ella misma:

```js
alert( a );
```

### Ejecutando un programa

¿ Cómo una colleción de sentencias le ordenan a un computador que tareas debe realizar ? Un programa debe ser *ejectuado*, este proceso se conoce también como *Ejecutar el programa*.

Sentencias como `a = b * 2` son útiles para los desarrolladores en el momento de leer y escribir código, pero no es la forma en la que un computador entiende el código. Una utilidad especial de un computador (Ya sea un *Intérprete* o un *compilador*) se utiliza para interpretar el código que escribes en instrucciones que el computador puede entender.

En algunos lenguajes de programación, la traducción de instrucciones se realiza de arriba a abajo, línea por línea, cada vez que el programa se ejecuta, lo cual se conoce como *Interpretar* el código.

En otros lenguajes, la traducción es hecha antes de la ejecución, esto se conoce como *compilar* el código. Cuando el programa se *ejecuta* después del compilado, lo que se ejecuta en realidad son instrucciones de computador compiladas.

Se dice típicamente que JavaScript es un lenguaje *interpretado*, porque tu fuente de código JavaScript es procesada cada vez que se ejecuta. Pero esto no es del todo cierto. El motor de JavaScript realmente *compila* el programa sobre la marcha e inmediatamente ejecuta el código compilado.

**Nota:** Para mayor información sobre el compilado en JavaScript, dirigirse a los dos primeros capítulos de *Scope & Closures* libro de esta serie.

## Inténtelo usted mismo

Este capítulo introducirá cada concepto de programación con fragmentos de código simples, todos escritos en lenguaje JavaScript (¡Por supuesto!).

No se puede enfatizar lo suficiente: Mientras avanza en el capítulo -- Y podría necesitar tiempo para leérlo múltiples veces -- debe practicar cada uno de los conceptos escribiendo el código usted mismo. La manera más fácil de hacerlo es abrir la consola de la herramienta del desarrollador en el navegador de su preferencia (Firefox, Chrome, IE, etc.).

**Consejo:** Típicamente, puede iniciar la consola del desarrollador con un atajo del teclado o de un ítem de menu. Para información más detallada acerca de iniciar y usar la consola de su navegador favorito, dirigirse a "Mastering The Developer Tools Console" (http://blog.teamtreehouse.com/mastering-developer-tools-console). Para ingresar múltiples lineas en la consola sin ejecutar el código, se puede usar la combinación de teclas `<shift> + <enter>` e ingresar un salto de línea en el código. Una vez presionada la tecla `<enter>` por si sola, la consola ejecutara todo el código que se hubiese ingresado.

Vamos a familiarizarnos con el proceso de ejecutar código en la consola. Primero que todo, le sugiero abrir una pestaña nueva en su navegador. Yo prefiero hacer esto escribiendo `about:blank` en la barra de direcciones. Luego, asegúrese de que su consola de desarrollador esté abierta, como mencionamos previamente.

Ahora, ingrese este código y observe como se ejecuta:

```js
a = 21;

b = a * 2;

console.log( b );
```
Escribir el anterior código en la consola de Chrome debería mostrar algo como esto:

<img src="fig1.png" width="500">

Adelante, inténtelo. ¡La mejor forma de aprender programación es escribiendo código!

### Salida

En el código anterior, usamos `console.log(..)`. Brevemente, miremos de que se trata esa línea de código.

Usted pudo haberlo adivinado, pero es exactamente la forma en la que imprimimos texto (también conocido como *Salida* para el usuario) en la consola del desarrollador. Hay dos características de esto que debemos explicar. 

Primero, la parte `log( b )` se refiere a un llamado funcional (ver "Funciones"). Lo que sucede es que estamos ingresando la variable `b` a la función, lo cual implica tomar el valor de `b` e imprimirlo en la consola.

Segundo, la parte `console` es una referencia al objeto dónde la función `log(..)` se encuentra. Se habla de objetos y sus propiedades con más detalle en el capítulo 2.

Otra forma de producir salida es ejecutar la sentencia `alert(..)`. Por ejemplo:

```js
alert( b );
```
Si ejecuta esta sentencia, se dará cuenta que envés de imprimir salida en la consola, se mostrará una ventana con el contenido de la variable `b`. De cualquier manera, usar `console.log(..)` hace que el proceso de aprender a programar y ejecutar programas sea más sencillo que con el uso de `alert(..)`, porque se pueden imprimir muchos valores sin interrumpir la interfaz del navegador.

En este libro, usaremos `conosole.log(..)` para la salida.

### Entrada

Mientras discutíamos la salida, usted puede estar preguntándose por la *entrada* (es decir, recibir información del usuario).

La manera más común de recibir información para una página en HTML es mostrar elementos de tipo formulario (como cajas de texto) al usuario de modo que pueda escribir, y luego usar JS para leer esos valores y guardarlos en variables del programa.

Pero existe un modo más sencillo de obtener entrada del usuario, para efectos de aprendizaje y demostración como los que se harán a lo largo de este libro. Use la función `prompt(..)`:

```js
age = prompt( "Please tell me your age:" );

console.log( age );
```
Como pudo haber adivinado, el mensaje que se entrega a la función `prompt(..)` -- en este caso, `"Please tell me your age:"` -- es impreso en una ventana.

Debería verse algo como lo siguiente:

<img src="fig2.png" width="500">

Una vez se ingresa el texto al dar click en "OK", se observa que el valor que ingresó es guardado en la variable `age`, lo que puede verse cuando por *salida* usamos `console.log(..)`:

<img src="fig3.png" width="500">

Para mantener las cosas simples mientras aprendemos conceptos básicos de programación, los ejemplos en este libro no requerirán entrada. Pero ahora que usted conoce el uso de `prompt(..)`, puede querer retarse a si mismo intentando usar esta función en futuros ejemplos.

## Operadores

Los operadores son la forma en la que ejecutamos acciones en variables y valores. Hemos visto dos operadores de JavaScript, el `=` y el `*`.

El operador `*` lleva a cabo la multiplicación matemática. Sencillo, ¿ Verdad ?

El operador `=`es usado para la *asignación* -- Primero se calcula el valor en el *lado derecho* (Valor fuente) del `=` y luego se asigna a la variable especificada en el *lado izquierdo* (variable objetivo).

**Advertencia:** Esto puede parecer una forma extraña de especificar una asignación. Envés de `a = 42`, alguien puede preferir invertir el orden de tal modo que el valor fuente esté en el lado izquierdo y la variable objetivo esté en lado derecho, algo como `42 -> a` (¡Esto no es válido para JavaScript!). Desafortunadamente, `a = 42` en su orden, y las variaciones similares, siguen estando vigentes en los lenguajes de programación. Si se siente poco natural, solo dedique cierto tiempo practicando el orden en su mente para acostumbrarse a ello.  

Considere:

```js
a = 2;
b = a + 1;
```

Acá, se asigna el valor `2` a la variable `a`. Entonces, obtenemos el valor de la variable `a` (Siendo `2`), añadiendo `1` para obtener `3` como resultado, luego se guarda este valor en la variable `b`.

Mientras que no sea un operador técnico, necesitará la palabra clave `var` en cada programa, pues es la forma primaria de *declarar* (O crear) *var*iables (Ver "Variables").

Usted debe siempre declarar el nombre de una variable antes de usarla. Pero usted solo necesita declarar una variable una vez por cada *scope* (ver "Scope"); para que pueda ser usada tantas veces como se requiera. Por ejemplo:

```js
var a = 20;

a = a + 1;
a = a * 2;

console.log( a );	// 42
```
Acá hay algunos de los operadores más comunes en JavaScript:

* Asignación: `=` como en `a = 2`.
* Matemáticos: `+` (adición), `-` (sustracción), `*` (multiplicación), y `/` (división), como en `a * 3`.
* Asignación compuesta: `+=`, `-=`, `*=`, y `/=` son operadores compuestos que combinan una operación matemática con una asignación, como en `a += 2` (que es equivalente a escribir `a = a + 2`).
* Incremento/Decremento: `++` (incremento), `--` (decremento), como en `a++` (que es equivalente a escribir `a = a + 1`).
* Acceso a las propiedades de un objeto: `.` como en `console.log()`.

	Los objetos son valores que guardan otros valores en lugares con nombres específicos llamados propiedades. `obj.a` indica el valor de un objeto llamado `obj` con una propiedad de nombre `a`. Las propiedades pueden ser accedidas alternativamente como `obj["a"]`. Ver Capítulo 2.

* Igualdad: `==` (igual), `===` (estrictamente-igual), `!=` (distinto), `!==` (estrictamente distinto, como en `a == b`.

  Ver "Valores & tipos" en el capítulo 2.
* Comparación: `<` (menor que), `>` (mayor que), `<=` (menor o igual), `>=` (mayor o igual), como en `a <= b`.

   Ver "Valores & tipos" en el capítulo 2.
* Lógicos: `&&` (y), `||` (o), como en `a || b` que selecciona `a` *o* `b`.

	Estos operadores son usados para expresar condicionales compuestos (ver "Condicionales"), como si `a` *o* `b`sean verdaderos.

**Nota:** Para mayor detalle, y estudio de operadores no mencionados acá, vaya al sitio web de Mozilla Developer Network (MDN)'s "Expressions and Operators" (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators).

## Valores y tipos

Si le preguntara a un empleado de una tienda de teléfonos el costo de un teléfono, y el dijera "Noventa y nueve, noventa y nueve" (es decir, $99.99), el le estaría dando una cifra numérica real en dólares que representa lo que debería pagar (más impuestos) para comprarlo. Si usted quiere comprar dos de esos teléfonos, podría fácilmente hacer el cálculo mentalmente para duplicar el valor y obtener $199.98 como su costo base.

Si ese mismo empleado selecciona un teléfono similar pero menciona que este es "gratis" (tal vez con comillas aereas), el no estaría dandole un número, envés le estaría dando otro tipo de representación del costo que usted espera ($0.00) -- la palabra "gratis".

Cuando usted pregunte si el teléfono incluye un cargador, la respuesta podría ser únicamente "si" o "no".

En una forma similar, cuando usted exprese un valor en un programa, usted elige diferentes representaciones para esos valores pensando en lo que hará con ellos.

Estas diferentes representaciones para los valores se llaman *tipos* en terminología de programación. JavaScript posee tipos construídos para cada una de estas representaciones también llamados tipos *primitivos*:

* Cuando necesite hacer matemáticas, usted requerirá un `number`
* Cuando necesite imprimir un valor en pantalla, usted requerirá un `string` (uno o más caracteres, palabras, oraciones).
* Cuando necesite tomar una decisión en su programa, usted requerirá un `boolean` (`true` or `false`).

Los valores que son incluídos directamente en el código fuente son llamados *literales*. Los literales `string` están rodeados por comillas dobles `"..."` o comillas sencillas (`'...'`) -- la única diferencia es la preferencia estilística. Los literales `number` y `boolean` se presentan como son (es decir, `42`, `true`, etc.).

Considere:

```js
"I am a string";
'I am also a string';

42;

true;
false;
```

Además de los tipos `string`/`number`/`boolean`, es común en los lenguajes de programación proveer *arreglos*, *objetos*, *funciones* y más. Hablaremos más de esos valores y tipos en este capítulo y el siguiente.

### Conversión entre tipos

Si usted tiene un tipo de dato `number` pero necesita imprimirlo en pantalla, necesitará convertir el valor a tipo `string` y esta conversión en JavaScript es llamada "coercion". Similarmente, si alguien ingresa una serie de caractéres numéricos en un formulario de una página de ecommerce, es un `string`, pero si necesita usar ese valor para realizar operaciones matemáticas, necesitará *coercer* al dato a que sea un `number`. 

JavaScript provee difrentes facilidades para forzar la coerción entre *tipos*. Por ejemplo:

```js
var a = "42";
var b = Number( a );

console.log( a );	// "42"
console.log( b );	// 42
```
Usar `Number(..)` (una función construída) como se muestra, es una coerción *explícita* de cualquier otro tipo al tipo `number`. Esto 

Pero algo controversial que sucede es cuando intenta comparar dos valores que no son del mismo tipo, lo cual requeriría de una coerción *implícita*.

Cuando se compara la cadena `"99.99"` con el número `99.99`, la mayoría de personas estaría de acuerdo en que son equivalentes. Pero no son exactamente lo mismo, ¿Lo son? El mismo valor en dos representaciones distintas, dos *tipos* diferentes. Usted podría decir que son "vagamente iguales", ¿No lo haría?

Para ayudarlo en situaciones como estas, JavaScript aveces hará una coerción *implícita* para los tipos coincidentes.

Entonces si usa el `==` operador de igualdad débil para realizar la comparación `"99.99" == 99.99`, JavaScript convertirá el lado izquierdo `"99.99"` a su equivalente `99.99` tipo `number`. La comparación entonces se vuelve en `99.99 == 99.99`, lo cual por supuesto es `true`.

Mientras esté diseñado para ayudarlo, la coerción implícita puede crear confusión si usted no se ha tomado el tiempo para aprender las reglas que gobiernan este comportamiento. La mayoría de desarrolladores de JS nunca lo ha hecho, entonces el sentimiento común es que la coerción es confusa y afecta los programas con errores inesperados, por lo cual la coerción implícita debería ser evitada. Incluso se dice que es un fallo en el diseño del lenguaje.

De cualquier forma, la coerción implícita es un mecanismo que *puede ser aprendido*, y más aún *debe ser aprendido* por cualquiera que desee tomarse la programación en JavaScript seriamente. No solo deja de ser confuso cuando se aprenden las reglas, ¡En realidad puede mejorar sus programas! El esfuerzo vale la pena.

**Nota:** Para más información sobre coerción, vea el Capítulo 2 de este libro y el Capítulo 4 de *Types & Grammar* título de esta serie.

## Comentarios en el código

El empleado de la tienda de teléfonos podría anotar algunas de las características del telefono más recientemente lanzado o alguno de los planes que la compañía ofrece. Estas notas serían únicamente para el empleado -- No lo son para los clientes. Sin embargo, estas notas ayudan al empleado a hacer su trabajo de mejor forma al documentar los cómos y los porqués de lo que debería hablarle a sus clientes.

Una de las lecciones más importantes que puedes aprender sobre escribir código es que este no es únicamente para el computador. El código es tanto, sino más, para el desarrollador como lo es para el compilador.

Su computador solo tiene en cuenta el código de máquina, una serie de 0s y 1s, que resultan de la *compilación*. Hay un número casi que infinito de programas que podría escribir que producen la misma serie de 0s y de 1s. Las decisiones que usted toma sobre como escribir su programa importan -- no solo para usted, sino para los demás miembros de su equipo e incluso para usted mismo en el futuro.

Usted debería esforzarse no únicamente por escribir programas que funcionen correctamente, sino programas que tengan sentido al ser examinados. Usted puede atravesar un largo camino en el esfuerzo de elegir buenos nombres para sus variables (ver "Variables") y funciones (ver "Functions").

Pero otro aspecto importante son los comentarios en el código. Estos son bits de texto en su programa que son insertados puramente para explicarselo a un humano. El interprete/compilador siempre ignora estos comentarios.

Existen muchas opiniones sobre que hace a un código ser bien comentado; no podemos definir una regla universal sobre esto. Pero algunas observaciones y guías son útiles para este propósito:

* Código sin comentarios es subóptimo.
* Muchos comentarios (un comentario por línea, por ejemplo) es probablemente un signo de código pobremente escrito.
* Los comentarios deben explicar el *porqué*, no el *qué*. Estos pueden explicar el *cómo* si el código es particularmente confuso.

En JavaScript, existen dos tipos de comentarios en el código: Comentarios de una única línea y comentarios de múltiples líneas.

Considere:

```js
// This is a single-line comment

/* But this is
       a multiline
             comment.
                      */
```

El comentario de una línea `//`, es apropiado si usted agregará un comentario por encima de una sentencia sencilla, o al final de una línea. Todo dentro de esta línea después del `//` es tratado como un comentario (por lo cual es ignorado por el compilador) hasta el final de esta línea. No hay restricción sobre lo que puede aparecer dentro de un comentario de una línea única.

Considere:

```js
var a = 42;		// 42 is the meaning of life
```

The `/* .. */` multiline comment is appropriate if you have several lines worth of explanation to make in your comment.

Here's a common usage of multiline comments:

```js
/* The following value is used because
   it has been shown that it answers
   every question in the universe. */
var a = 42;
```

Este puede aparece en cualquier lugar de una líne, incluso en medio de una sentencia, porque `*/` lo termina. Por ejemplo: 

```js
var a = /* arbitrary value */ 42;

console.log( a );	// 42
```
Lo único que no puede aparecer en medio de un comentario multilínea es un `*/`, porque es interpretado como el final del comentario.

Usted definitivamente querrá empezar su aprendizaje en programación comenzando con el hábito de comentar código. Através de lo que resta del capítulo, usted verá que uso comentarios para explicar, así que haga lo mismo en su propia práctica. ¡Créame, todo aquel que lea su código se lo agradecerá! 

## Variables

Los programas más útiles requieren un seguimiento de un valor cada vez que este cambie en el transcurso del programa, pasando por diferentes operaciones mientras es llamado por las tareas que su programa está destinado a realizar.

La manera más sencilla de realizar esto en su programa, es asignar un valor a un contenedor simbólico, llamado *variable* -- llamado de este modo porque el valor en este contenedor puede *variar* en el tiempo tanto como se necesite.

En algunos lenguajes de programación, usted declara una variable (contenedor) para guardar un valor de un tipo específico, como un `number` o un `string`. El *tipado estático*, también conocido como *Tipado fuerte*, es típicamente citado como un beneficio para la correctitud de un programa porque previene conversiones de valor no intencionadas.

Otros lenguajes enfatizan en los tipos para valores envés de tipos para variables. el *Tipado débil*, también conocido *tipado dinámico*, permite a una variable almacenar cualquier tipo de valor en el tiempo.

Se dice comunmente que es un beneficio para la flexibilidad de un programa al permitir a una variable representar un valor sin importar el tipo que el valor tenga en el tiempo durante la lógica del programa.

JavaScript usa el último enfoque, *tipado dinámico*, lo que significa que las variables pueden guardar valores de cualquier *tipo* sin ningún *tipado* fuerte. 

Como se mencionó antes, declararemos una variable usando la sentencia ``var` -- note que no hay información sobre el *tipo* en la declaración. Considere este ejemplo:

```js
var amount = 99.99;

amount = amount * 2;

console.log( amount );		// 199.98

// convert `amount` to a string, and
// add "$" on the beginning
amount = "$" + String( amount );

console.log( amount );		// "$199.98"
```

La variable `cantidad` inicia guardando el número `99.99`, luego almacena el resultado de tipo `number` de `cantidad * 2`, lo cual es `199.98`.

La primera instrucción `consle.log(..)` tiene que hacer coerción *implícita* desde `number` a `string` para imprimirlo.

Luego la sentencia `cantidad = "$" + String(cantidad)` realiza coerción *explícita* del valor `199.98` a `string` y añade el caracter `"$"` al inicio. Hasta este punto, `cantidad` alamacena el `string` con valor `"$199.98"`, entonces el segundo `console.log(..)` no necesita realizar ninguna coerción para imprimirlo.

Los desarrolladores JavaScript notarán la flexibilidad de usar la variable `cantidad` para cada uno de los valores `99.99`, `199.98`, y `"$199.98"`. Los entusiastas del tipado estático podrían preferir una variable separado como `cantidadStr` para guardar el resultado final `"$199.98"`, puesto que es de un tipo diferente.

De cualquier modo, se dará cuenta que `cantidad` almacena un valor que cambia con el curso del programa, mostrando el propósito primario de las variables: gestionar el *estado* del programa. 

En otras palabras, el *estado* es seguir los cambios a los valores a medida que el programa se ejecuta.

Otro uso común de las variables es centralizar la asignación de valores. Esto es típicamente llamado *constantes*, cuando declara una variable con un valor e intención de *no cambiar* durante el programa.

Usted declara estas *constantes*, con frecuencia en la parte superior de un programa, así es conveniente para usted tener un lugar dónde cambie el valor si lo necesita. Por convención, las variables en JavaScript como las constantes se escriben con mayúscula sostenida, con guiones bajos `_` entre las palabras.

Acá hay un ejemplo sencillo:

```js
var TAX_RATE = 0.08;	// 8% sales tax

var amount = 99.99;

amount = amount * 2;

amount = amount + (amount * TAX_RATE);

console.log( amount );				// 215.9784
console.log( amount.toFixed( 2 ) );	// "215.98"
```

**Nota:** De forma similar en que `console.log(..)` es una función dónde `log(..)` es accedido como una propiedad del valor `console`, `toFixed(..)` acá hay una función que puede ser accedida en valores de tipo `number`. Los `number` en JavaScript no son formateados de forma automática para indicar dólares -- El motor no sabe cuál es su intención y no existe un tipo para monedas. `toFixed(..)` nos permite especificar a cuántos decimales nos gustaría redondear un número, y producir el `string` cuando es necesario.

La variable `TASA_DE_IMPUESTOS` es únicamente *constante* por convención -- No hay nada especial en este programa que prevenga a esta variable de ser cambiada. Pero si la ciudad aumenta el impuesto de ventas a 9%, podemos fácilmente actualizar el programa asignando a `TASA_DE_IMPUESTOS` el valor de `0.09` en un solo lugar, envés de encontrar todas las ocurrencias del valor `0.08`esparcido a lo largo del programa y actualizar todas ellas.

La versión más reciente de JavaScript en el momento en que se escribio este libro (comúnmente llamada "ES6") incluye una nueva forma de declarar *constantes*, mediante el uso de `const` envés de `var`:

```js
// as of ES6:
const TAX_RATE = 0.08;

var amount = 99.99;

// ..
```
Las constantes son útiles como variables con valores sin cambiar, excepto que las constantes previenen el cambio accidental de algún valor dónde sea que se haga después de la asignación inicial. Si usted intentó asignar algún valor distinto a `TASA_DE_IMPUESTOS` luego de su primera declaración, su programa podría rechazar el cambio (Y en modo estricto, fallar con un error --ver "Modo Estricto" en el capítulo 2).

¡Por cierto, ese tipo de "protección" contra errores es similar al enforzamiento del tipado estático, así que puede ver porqué los tipos estáticos pueden ser tan atractivos!

**Note:** Para más información sobre como variables con valores diferentes pueden ser usados en sus programas, vea *Types & Grammar* título de esta serie.

## Bloques

El empleado de la tienda de teléfonos puede atravesar una serie de pasos para completar una compra una vez pagado el teléfono.

De manera similar, en código es frecuentemente necesario agrupar sentencias, llamadas frecuentemente bloques. En JavaScript, un bloque es definido rodeando una o más sentencias con una pareja de corchetes `{ .. }`. Considere:

```js
var amount = 99.99;

// a general block
{
	amount = amount * 2;
	console.log( amount );	// 199.98
}
```
Esta particularidad `{ .. }` es un bloque general válido, pero no es como se ve realmente en los programas JS. Típicamente, bloques son añadidos a otras sentencias de control, como  la sentencia `if` (ver "Condicionales") o un ciclo (ver "Ciclos"). Por ejemplo: 

```js
var amount = 99.99;

// is amount big enough?
if (amount > 10) {			// <-- block attached to `if`
	amount = amount * 2;
	console.log( amount );	// 199.98
}
```
Explicaremos las sentencias `if` en la siguiente sección, pero como puede ver, el bloque `{ .. }` con las dos sentencias depende de `if (cantidad > 10)` ; las sentencias dentro del bloque serán ejecutadas si el condicional lo aprueba.

**Nota:** A diferencia de otras sentencias como `console.log(cantidad)`, una sentencia de bloque no necesita un punto y coma (`;`) para ser concluido.

## Conditionals

"Do you want to add on the extra screen protectors to your purchase, for $9.99?" The helpful phone store employee has asked you to make a decision. And you may need to first consult the current *state* of your wallet or bank account to answer that question. But obviously, this is just a simple "yes or no" question.

There are quite a few ways we can express *conditionals* (aka decisions) in our programs.

The most common one is the `if` statement. Essentially, you're saying, "*If* this condition is true, do the following...". For example:

```js
var bank_balance = 302.13;
var amount = 99.99;

if (amount < bank_balance) {
	console.log( "I want to buy this phone!" );
}
```

The `if` statement requires an expression in between the parentheses `( )` that can be treated as either `true` or `false`. In this program, we provided the expression `amount < bank_balance`, which indeed will either evaluate to `true` or `false` depending on the amount in the `bank_balance` variable.

You can even provide an alternative if the condition isn't true, called an `else` clause. Consider:

```js
const ACCESSORY_PRICE = 9.99;

var bank_balance = 302.13;
var amount = 99.99;

amount = amount * 2;

// can we afford the extra purchase?
if ( amount < bank_balance ) {
	console.log( "I'll take the accessory!" );
	amount = amount + ACCESSORY_PRICE;
}
// otherwise:
else {
	console.log( "No, thanks." );
}
```

Here, if `amount < bank_balance` is `true`, we'll print out `"I'll take the accessory!"` and add the `9.99` to our `amount` variable. Otherwise, the `else` clause says we'll just politely respond with `"No, thanks."` and leave `amount` unchanged.

As we discussed in "Values & Types" earlier, values that aren't already of an expected type are often coerced to that type. The `if` statement expects a `boolean`, but if you pass it something that's not already `boolean`, coercion will occur.

JavaScript defines a list of specific values that are considered "falsy" because when coerced to a `boolean`, they become `false` -- these include values like `0` and `""`. Any other value not on the "falsy" list is automatically "truthy" -- when coerced to a `boolean` they become `true`. Truthy values include things like `99.99` and `"free"`. See "Truthy & Falsy" in Chapter 2 for more information.

*Conditionals* exist in other forms besides the `if`. For example, the `switch` statement can be used as a shorthand for a series of `if..else` statements (see Chapter 2). Loops (see "Loops") use a *conditional* to determine if the loop should keep going or stop.

**Note:** For deeper information about the coercions that can occur implicitly in the test expressions of *conditionals*, see Chapter 4 of the *Types & Grammar* title of this series.

## Loops

During busy times, there's a waiting list for customers who need to speak to the phone store employee. While there's still people on that list, she just needs to keep serving the next customer.

Repeating a set of actions until a certain condition fails -- in other words, repeating only while the condition holds -- is the job of programming loops; loops can take different forms, but they all satisfy this basic behavior.

A loop includes the test condition as well as a block (typically as `{ .. }`). Each time the loop block executes, that's called an *iteration*.

For example, the `while` loop and the `do..while` loop forms illustrate the concept of repeating a block of statements until a condition no longer evaluates to `true`:

```js
while (numOfCustomers > 0) {
	console.log( "How may I help you?" );

	// help the customer...

	numOfCustomers = numOfCustomers - 1;
}

// versus:

do {
	console.log( "How may I help you?" );

	// help the customer...

	numOfCustomers = numOfCustomers - 1;
} while (numOfCustomers > 0);
```

The only practical difference between these loops is whether the conditional is tested before the first iteration (`while`) or after the first iteration (`do..while`).

In either form, if the conditional tests as `false`, the next iteration will not run. That means if the condition is initially `false`, a `while` loop will never run, but a `do..while` loop will run just the first time.

Sometimes you are looping for the intended purpose of counting a certain set of numbers, like from `0` to `9` (ten numbers). You can do that by setting a loop iteration variable like `i` at value `0` and incrementing it by `1` each iteration.

**Warning:** For a variety of historical reasons, programming languages almost always count things in a zero-based fashion, meaning starting with `0` instead of `1`. If you're not familiar with that mode of thinking, it can be quite confusing at first. Take some time to practice counting starting with `0` to become more comfortable with it!

The conditional is tested on each iteration, much as if there is an implied `if` statement inside the loop.

We can use JavaScript's `break` statement to stop a loop. Also, we can observe that it's awfully easy to create a loop that would otherwise run forever without a `break`ing mechanism.

Let's illustrate:

```js
var i = 0;

// a `while..true` loop would run forever, right?
while (true) {
	// stop the loop?
	if ((i <= 9) === false) {
		break;
	}

	console.log( i );
	i = i + 1;
}
// 0 1 2 3 4 5 6 7 8 9
```

**Warning:** This is not necessarily a practical form you'd want to use for your loops. It's presented here for illustration purposes only.

While a `while` (or `do..while`) can accomplish the task manually, there's another syntactic form called a `for` loop for just that purpose:

```js
for (var i = 0; i <= 9; i = i + 1) {
	console.log( i );
}
// 0 1 2 3 4 5 6 7 8 9
```

As you can see, in both cases the conditional `i <= 9` is `true` for the first 10 iterations (`i` of values `0` through `9`) of either loop form, but becomes `false` once `i` is value `10`.

The `for` loop has three clauses: the initialization clause (`var i=0`), the conditional test clause (`i <= 9`), and the update clause (`i = i + 1`). So if you're going to do counting with your loop iterations, `for` is a more compact and often easier form to understand and write.

There are other specialized loop forms that are intended to iterate over specific values, such as the properties of an object (see Chapter 2) where the implied conditional test is just whether all the properties have been processed. The "loop until a condition fails" concept holds no matter what the form of the loop.

## Functions

The phone store employee probably doesn't carry around a calculator to figure out the taxes and final purchase amount. That's a task she needs to define once and reuse over and over again. Odds are, the company has a checkout register (computer, tablet, etc.) with those "functions" built in.

Similarly, your program will almost certainly want to break up the code's tasks into reusable pieces, instead of repeatedly repeating yourself repetitiously (pun intended!). The way to do this is to define a `function`.

A function is generally a named section of code that can be "called" by name, and the code inside it will be run each time. Consider:

```js
function printAmount() {
	console.log( amount.toFixed( 2 ) );
}

var amount = 99.99;

printAmount(); // "99.99"

amount = amount * 2;

printAmount(); // "199.98"
```

Functions can optionally take arguments (aka parameters) -- values you pass in. And they can also optionally return a value back.

```js
function printAmount(amt) {
	console.log( amt.toFixed( 2 ) );
}

function formatAmount() {
	return "$" + amount.toFixed( 2 );
}

var amount = 99.99;

printAmount( amount * 2 );		// "199.98"

amount = formatAmount();
console.log( amount );			// "$99.99"
```

The function `printAmount(..)` takes a parameter that we call `amt`. The function `formatAmount()` returns a value. Of course, you can also combine those two techniques in the same function.

Functions are often used for code that you plan to call multiple times, but they can also be useful just to organize related bits of code into named collections, even if you only plan to call them once.

Consider:

```js
const TAX_RATE = 0.08;

function calculateFinalPurchaseAmount(amt) {
	// calculate the new amount with the tax
	amt = amt + (amt * TAX_RATE);

	// return the new amount
	return amt;
}

var amount = 99.99;

amount = calculateFinalPurchaseAmount( amount );

console.log( amount.toFixed( 2 ) );		// "107.99"
```

Although `calculateFinalPurchaseAmount(..)` is only called once, organizing its behavior into a separate named function makes the code that uses its logic (the `amount = calculateFinal...` statement) cleaner. If the function had more statements in it, the benefits would be even more pronounced.

### Scope

If you ask the phone store employee for a phone model that her store doesn't carry, she will not be able to sell you the phone you want. She only has access to the phones in her store's inventory. You'll have to try another store to see if you can find the phone you're looking for.

Programming has a term for this concept: *scope* (technically called *lexical scope*). In JavaScript, each function gets its own scope. Scope is basically a collection of variables as well as the rules for how those variables are accessed by name. Only code inside that function can access that function's *scoped* variables.

A variable name has to be unique within the same scope -- there can't be two different `a` variables sitting right next to each other. But the same variable name `a` could appear in different scopes.

```js
function one() {
	// this `a` only belongs to the `one()` function
	var a = 1;
	console.log( a );
}

function two() {
	// this `a` only belongs to the `two()` function
	var a = 2;
	console.log( a );
}

one();		// 1
two();		// 2
```

Also, a scope can be nested inside another scope, just like if a clown at a birthday party blows up one balloon inside another balloon. If one scope is nested inside another, code inside the innermost scope can access variables from either scope.

Consider:

```js
function outer() {
	var a = 1;

	function inner() {
		var b = 2;

		// we can access both `a` and `b` here
		console.log( a + b );	// 3
	}

	inner();

	// we can only access `a` here
	console.log( a );			// 1
}

outer();
```

Lexical scope rules say that code in one scope can access variables of either that scope or any scope outside of it.

So, code inside the `inner()` function has access to both variables `a` and `b`, but code in `outer()` has access only to `a` -- it cannot access `b` because that variable is only inside `inner()`.

Recall this code snippet from earlier:

```js
const TAX_RATE = 0.08;

function calculateFinalPurchaseAmount(amt) {
	// calculate the new amount with the tax
	amt = amt + (amt * TAX_RATE);

	// return the new amount
	return amt;
}
```

The `TAX_RATE` constant (variable) is accessible from inside the `calculateFinalPurchaseAmount(..)` function, even though we didn't pass it in, because of lexical scope.

**Note:** For more information about lexical scope, see the first three chapters of the *Scope & Closures* title of this series.

## Practice

There is absolutely no substitute for practice in learning programming. No amount of articulate writing on my part is alone going to make you a programmer.

With that in mind, let's try practicing some of the concepts we learned here in this chapter. I'll give the "requirements," and you try it first. Then consult the code listing below to see how I approached it.

* Write a program to calculate the total price of your phone purchase. You will keep purchasing phones (hint: loop!) until you run out of money in your bank account. You'll also buy accessories for each phone as long as your purchase amount is below your mental spending threshold.
* After you've calculated your purchase amount, add in the tax, then print out the calculated purchase amount, properly formatted.
* Finally, check the amount against your bank account balance to see if you can afford it or not.
* You should set up some constants for the "tax rate," "phone price," "accessory price," and "spending threshold," as well as a variable for your "bank account balance.""
* You should define functions for calculating the tax and for formatting the price with a "$" and rounding to two decimal places.
* **Bonus Challenge:** Try to incorporate input into this program, perhaps with the `prompt(..)` covered in "Input" earlier. You may prompt the user for their bank account balance, for example. Have fun and be creative!

OK, go ahead. Try it. Don't peek at my code listing until you've given it a shot yourself!

**Note:** Because this is a JavaScript book, I'm obviously going to solve the practice exercise in JavaScript. But you can do it in another language for now if you feel more comfortable.

Here's my JavaScript solution for this exercise:

```js
const SPENDING_THRESHOLD = 200;
const TAX_RATE = 0.08;
const PHONE_PRICE = 99.99;
const ACCESSORY_PRICE = 9.99;

var bank_balance = 303.91;
var amount = 0;

function calculateTax(amount) {
	return amount * TAX_RATE;
}

function formatAmount(amount) {
	return "$" + amount.toFixed( 2 );
}

// keep buying phones while you still have money
while (amount < bank_balance) {
	// buy a new phone!
	amount = amount + PHONE_PRICE;

	// can we afford the accessory?
	if (amount < SPENDING_THRESHOLD) {
		amount = amount + ACCESSORY_PRICE;
	}
}

// don't forget to pay the government, too
amount = amount + calculateTax( amount );

console.log(
	"Your purchase: " + formatAmount( amount )
);
// Your purchase: $334.76

// can you actually afford this purchase?
if (amount > bank_balance) {
	console.log(
		"You can't afford this purchase. :("
	);
}
// You can't afford this purchase. :(
```

**Note:** The simplest way to run this JavaScript program is to type it into the developer console of your nearest browser.

How did you do? It wouldn't hurt to try it again now that you've seen my code. And play around with changing some of the constants to see how the program runs with different values.

## Revisión

Aprender a programar no debería ser un proceso complejo ni abrumador. Solo hay que aprender unos conceptos y facilitará el proceso.

Estos actúan como bloques fundacionales. Para construir una torre, uno comienza primero colocando un bloque sobre otro bloque, y así hasta construirla. Lo mismo aplica para la programación. Aquí en está capítulo está los bloques esenciales para:

* Usted necesita *operadores* para tener acciones sobre valores
* Usted necesita valores y *tipos* para realizar hacer diferences tipos de acciones como Matemática a `numeros` o retornar de una función con `string`.
* Usted necesita *variables* para guardar datos (aka *estado*) durante la ejecución de su programa.
* Usted necesita *loops* para repetir las tareas hasta que una condición lógica la acabe. 
* Usted necesita *functions* para organizar su código en partes lógicas y reusables.


Los comentarios en el código, están para escribir de una forma más eficiente el código, lo que hace su programa más fácil de entender y hacerle mantenimiento, ó arreglarlo si luego aparecen problemas.

Finalmente, no de por sentado el poder de la práctica. La mejor manera de aprender a escribir código, es efectivamente, escribiendo código.

Estoy emocionado por que está tomando el camindo de aprender a programar. No olvide revisar otros recursos de introducción a la programación cómo libros, blogs, entrenamientos en línea, etc. Este capítulo y este libro son un gran comienzo, sin embargo, es apenas una introducción. 

En el siguiente capítulo, revisaremos muchos conceptos de este capítulo, sin embargo, desde el punto de vista de JavaScript, y con mucho más detalle. 
