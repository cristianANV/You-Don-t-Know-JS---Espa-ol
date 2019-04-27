# You Don't Know JS: Async & Performance
# Capítulo 1: Asincronía: Ahora y Después

Una de las partes más importantes y a menudo malinterpretada de la programación en lenguajes como JS (JavaScript) es cómo expresar y manipular el comportamiento del programa durante un período de tiempo.

No se trata sólamente de lo que sucede desde el inicio de un ciclo `for` hasta su final, lo cual claramente toma *algún tiempo* (microsegundos a milisegundos) para llevarse a cabo. Se trata de lo que sucede cuando una parte de su programa se ejecuta *ahora*, y otra parte *después* -- Hay una brecha entre *ahora* y *después* donde su programa no se está ejecutando de manera activa.

Prácticamente todos los programas no triviales que se han escrito (especialmente en JS) han tenido que, de una manera u otra, gestionar esta brecha, ya sea esperando entradas del usuario, solicitando información a una base de datos o a un sistema de archivos, enviando datos a través de una red y esperando por una respuesta, o realizando una tarea repetitiva en un intervalo fijo de tiempo (como en una animación). En todos esos casos, su programa tendrá que gestionar el estado durante la brecha oportunamente. Como se dice popularmente en Londrés (del abismo entre la puerta del metro y la plataforma): "cuidado con la brecha".

De hecho, la relación entre las partes *ahora* y *después* de su programa está en el corazón de la programación asíncrona.

La programación asíncrona ha existido desde los comienzos de JS, sin lugar a duda. Pero la mayoría de los desarrolladores JS nunca han considerado seriamente cómo y por qué ésta surge en sus programas, o no han explorado *otras* formas de gestionarla. La solución *suficientemente buena* siempre ha sido la humilde función de retorno de llamada (callback). Muchos, hasta el día de hoy, insistirán en que los callbacks son más que suficiente.

Pero a medida que JS va creciendo tanto en alcance como en complejidad, satisfacer las demandas cada vez más grandes de un lenguaje de programación de primera clase que se ejecuta en navegadores y servidores y en cada dispositivo concebible en medio, los dolores por los cuales gestionamos la asincronía se vuelven cada vez más intensos, y claman por soluciones que sean más competentes y razonables.

Si bien todo esto puede parecer muy abstracto en este momento, le aseguro que lo abordaremos de manera más completa y concreta a medida que avancemos en este libro. Exploraremos una variedad de técnicas emergentes para la programación asíncrona en JS en los siguientes capítulos.

Pero antes de llegar allá, tenemos que entender mucho mejor qué es asincronía y cómo opera en JS.

## Un Programa en Pedazos

Usted podría escribir su programa JS en un solo archivo *.js*, pero casi siempre su programa está compuesto de varios pedazos, solo uno de los cuales se va a ejecutar *ahora*, y el resto se ejecutarán *después*. La unidad más común de un *pedazo* es el `function`.

El problema que parecen tener la mayoría de los nuevos desarrolladores en JS es que *después* no sucede inmediatamente después del *ahora*. En otras palabras, las tareas que no pueden completarse *ahora* son, por definición, completadas asíncronamente, y por lo tanto no tendremos comportamiento de bloqueo como usted podría esperar o querer intuitivamente.

Considere:

```js
// ajax(..) es una función Ajax arbitraria dada por una librería
var data = ajax( "http://some.url.1" );

console.log( data );
// Ups! generalmente `data` no tendrá los resultados del Ajax
```

Usted probablemente sabe que las peticiones estándar de Ajax no se completan síncronamente, lo que significa que la función `ajax(..)` aun no tiene ningún valor de retorno para ser asignado a la variable ´data´. Si `ajax(..)` *pudiera* bloquear hasta que la respuesta se retornara, entonces la asignación `data = ..` funcionaría bien.

Pero así no es como hacemos Ajax. Hacemos una petición asíncrona Ajax *ahora*, y no tendremos los resultados de vuelta hasta *después*.

La forma más simple (pero definitivamente no la única, o ¡necesariamente la mejor!) de "esperar" desde *ahora* hasta *después* es usar una función, comúnmente llamada una función de llamada de retorno:

```js
// ajax(..) es una función Ajax arbitraria dada por una librería
ajax( "http://some.url.1", function myCallbackFunction(data){

	console.log( data ); // Genial, ¡tengo algo en `data`!

} );
```

**Precaución:** Usted puede haber escuchado que es posible hacer peticiones Ajax síncronas. Aunque eso es técnicamente cierto, usted nunca jamás debe hacerlo, bajo ninguna circunstancia, porque bloquea la interfaz de usuario del navegador (botones, menús, desplazamiento, etc.) y además previene cualquier interacción de usuario. Es una idea terrible, y siempre debería ser evitada.

Antes de que proteste en desacuerdo, no, su deseo de evitar el desorden de llamadas de retorno *no* es justificación para usar Ajax síncrono de bloqueo.

Por ejemplo, considere este código:

```js
function ahora() {
	return 21;
}

function despues() {
	respuesta = respuesta * 2;
	console.log( "El significado de la vida:", respuesta );
}

var respuesta = ahora();

setTimeout( despues, 1000 ); // El significado de la vida: 42
```

Hay dos pedazos de código en este programa: lo que correrá *ahora*, y lo que correrá *después*. Debería ser algo obvio cuáles son esos pedazos, pero seamos super explícitos: 

Ahora:
```js
function ahora() {
	return 21;
}

function despues() { .. }

var answer = ahora();

setTimeout( despues, 1000 );
```

Después:
```js
respuesta = respuesta * 2;
console.log( "El significado de la vida:", respuesta );
```

El pedazo *ahora* corre de inmediato, tan pronto como usted ejecute el programa. Pero `setTimeout(..)` también crea un evento (una espera) que sucede *después*, así que los contenidos de la función `despues()` se ejecutarán en otro momento (1000 milisegundos después).

Todas las veces que usted envuelve una porción de código dentro de un `function` y especifica que debería ser ejecutado en respuesta a algún evento (temporizador, click de mouse, respuesta Ajax, etc.), usted está creando un pedazo de código para *después*, y por lo tanto introduce asincronía en su programa.

### Consola Asíncrona

No hay especificación o conjunto de requerimientos alrededor de cómo funcionan los métodos de `console.*` -- no son parte de JavaScript oficialmente, en vez de esto son agregados a JS por el *ambiente de alojamiento* (vea el título *Tipos y Gramática* de esta serie de libros).

Así que diferentes navegadores y ambientes de JS hacen como les parezca, lo que algunas veces lleva a un comportamiento confuso.

En particular, hay algunos navegadores y algunas condiciones en los que `console.log(..)` no imprime inmediatamente lo que le es dado. La razón principal de que esto podría pasar es porque la entrada/salida es una parte muy lenta y que bloquea en muchos programas (no solo en JS). Así que podría desempeñarse mejor (desde la perspectiva de página/interfaz de usuario) para un navegador que maneje `console` I/O asíncronamente en segundo plano, tal vez sin usted siquiera saber que esto ocurrió.

Un escenario no muy común, pero posible, en el que esto podría ser *observable* (no desde el código en sí pero desde afuera):

```js
var a = {
	index: 1
};

// más tarde
console.log( a ); // ??

// aun más tarde
a.index++;
```

Normalmente esperaríamos ver que el objeto `a` sea fotografiado en el momento exacto de la declaración `console.log(..)`, imprimiendo algo como `{ index: 1 }`, de forma que en la siguiente declaración cuando ocurre `a.index++`, se está modificando algo diferente que, o estrictamente después de, la salida de `a`.

La mayor parte del tiempo, el anterior código probablemente producirá una representación del objeto en la consola de su herramienta de desarrollo que es lo que usted esperaría. Pero es posible que este mismo código pueda correr en una situación en la que el navegador sienta que necesitaba diferir la entrada/salida de la consola a segundo plano, en cuyo caso es *posible* que para el momento en que el objeto es representado en la consola del navegador, el `a.index++` ya ha sucedido, y muestre `{ index: 2 }`.

Es un blanco en movimiento saber bajo qué condiciones exactamente la entrada/salida de la `console` será diferida, o incluso si esto será observable. Simplemente sepa de esta posible asincronía en la entrada/salida en caso de que alguna vez tenga problemas depurando cuando los objetos han sido modificados *después* de una declaración `console.log(..)` y aun así usted vea que se muestran las modificaciones inesperadas.

**Nota:** Si usted se encuentra este raro escenario, la mejor opción es usar puntos de interrupción en su depurador de JS en vez de depender de la salida de la `console`. La siguiente mejor opción sería forzar una "fotografía" del objeto en cuestión serializándolo en un `string`, como con `JSON.stringify(..)`.

## Ciclo de Eventos

Vamos a hacer una afirmación (tal vez aterradora): a pesar de permitir código JS asíncrono claramente (como el temporizador que acabamos de ver), hasta hace poco (ES6), en realidad JavaScript nunca había tenido ninguna noción directa de asincronía integrada en sí mismo.

**¿¡Qué!?** Eso parece una afirmación alocada, ¿verdad? De hecho, es bastante acertada. El motor de JS en sí nunca ha hecho nada a parte de ejecutar un solo pedazo de su programa en un momento dado, cuando se le pide.

"Cuando se le pide." ¿Por quién? ¡Esa es la parte importante!

El motor de JS no se ejecuta en aislamiento. Se ejecuta dentro del *ambiente de alojamiento*, el cual es para la mayoría de desarrolladores el navegador de internet. En los últimos años (pero no exclusivamente), JS se ha expandido más allá del navegador hacia otros ambientes, tales como servidores, por medio de cosas como Node.js. De hecho, hoy en día JavaScript se integra dentro de todo tipo de dispositivos, desde robots hasta bombillas.

Pero el "hilo" en común (para que conste, éste no es un chiste medio sutil sobre asincronía) de todos estos ambientes es que tienen un mecanismo en ellos que maneja la ejecución *en el tiempo* de múltiples pedazos de su programa, cada vez invocando el motor de JS, llamado el "ciclo de eventos."

En otras palabras, el motor de JS no ha tenido un sentido innato del *tiempo*, sino que ha sido un ambiente de ejecución por demanda para cualquier fragmento arbitrario de JS. Es el ambiente que lo rodea el que siempre ha *programado* "eventos" (ejecuciones de código JS). 

Así que, por ejemplo, cuando su programa JS hace peticiones Ajax para obtener algunos datos de un servidor, usted configura el código "respuesta" en una función (comúnmente denominada "llamada de retorno"), y el motor JS le dice al ambiente de alojamiento, "Oye, Voy a suspender la ejecución por ahora, pero cuando sea que termine con esa petición en la red, y tenga algunos datos, por favor *llame* esta función *de retorno*."

El navegador entonces se encuentra configurado para escuchar la respuesta de la red, y cuando tenga algo para darle, programa la función de llamada de retorno para que sea ejecutada, insertándola dentro del *ciclo de eventos*.

Entonces ¿qué es el *ciclo de eventos*?

Vamos a conceptualizarlo primero con un poco de pseudo-código:

```js
// `cicloDeEventos` es un arreglo que actúa como una cola (primero que entra, primero que sale)
var cicloDeEventos = [ ];
var evento;

// se ejecuta "para siempre"
while (true) {
	// hace una "marcación"
	if (cicloDeEventos.length > 0) {
		// obtiene el siguiente evento en cola
		evento = cicloDeEventos.shift();

		// ahora, ejecute el siguiente evento
		try {
			evento();
		}
		catch (err) {
			reporteError(err);
		}
	}
}
```

Esto es, por supuesto, pseudo-código vastamente simplificado para ilustrar los conceptos. Pero debería ser suficiente para ayudar a tener un mejor entendimiento.

Como usted puede ver, se esta ejecutando continuamente un ciclo representado por el ciclo `while`, y cada iteración de este ciclo es llamado una "marcación." Por cada marcación, si un evento está esperando en la cola, se saca y se ejecuta. Estos eventos son sus funciones de llamada de retorno.

Es importante notar que `setTimeout(..)` no pone su llamada de retorno en la cola del ciclo de eventos. Lo que hace es configurar un temporizador; cuando el temporizador expira, el ambiente ubica su llamada de retorno en el ciclo de eventos, tal que alguna marcación futura la tomará y la ejecutará.

¿Qué pasa si ya hay 20 ítems en el ciclo de eventos en ese momento? Su llamada de retorno espera. Se pone en línea detrás de las demás -- normalmente no hay forma de vaciar previamente la cola y saltarse la línea. Esto explica por qué los temporizadores del `setTimeout(..)` podrían no dispararse con una exactitud temporal perfecta. Usted tiene garantizado (más o menos) que su llamada de retorno no se disparará *antes* del intervalo de tiempo que usted especifica, pero puede pasar en o después de ese tiempo, dependiendo del estado de la cola de eventos.

Entonces, en otras palabras, su programa está generalmente dividido en montones de pequeños pedazos, que ocurren uno tras otro en la cola del ciclo de eventos. Y técnicamente, otros eventos no relacionados directamente con su programa pueden ser intercalados dentro de la cola también.

**Nota:** Mencionamos "hasta hace poco" en relación con ES6 cambiando la naturaleza de donde la cola del ciclo de eventos es administrada. Es sobretodo un tecnicismo formal, pero ES6 ahora especifica cómo el ciclo de eventos trabaja, lo que significa que técnicamente está bajo la supervisión del motor de JS, y no solamente en el *ambiente de alojamiento*. Una razón principal para este cambio es la introducción de Promesas en ES6, las cuales discutiremos en el Capítulo 3, porque requieren la habilidad de tener control directo y granular sobre operaciones programadas en la cola del ciclo de eventos (vea la discusión de `setTimeout(..0)` en la sección de "Cooperación")

## Parallel Threading

It's very common to conflate the terms "async" and "parallel," but they are actually quite different. Remember, async is about the gap between *now* and *later*. But parallel is about things being able to occur simultaneously.

The most common tools for parallel computing are processes and threads. Processes and threads execute independently and may execute simultaneously: on separate processors, or even separate computers, but multiple threads can share the memory of a single process.

An event loop, by contrast, breaks its work into tasks and executes them in serial, disallowing parallel access and changes to shared memory. Parallelism and "serialism" can coexist in the form of cooperating event loops in separate threads.

The interleaving of parallel threads of execution and the interleaving of asynchronous events occur at very different levels of granularity.

For example:

```js
function later() {
	answer = answer * 2;
	console.log( "Meaning of life:", answer );
}
```

While the entire contents of `later()` would be regarded as a single event loop queue entry, when thinking about a thread this code would run on, there's actually perhaps a dozen different low-level operations. For example, `answer = answer * 2` requires first loading the current value of `answer`, then putting `2` somewhere, then performing the multiplication, then taking the result and storing it back into `answer`.

In a single-threaded environment, it really doesn't matter that the items in the thread queue are low-level operations, because nothing can interrupt the thread. But if you have a parallel system, where two different threads are operating in the same program, you could very likely have unpredictable behavior.

Consider:

```js
var a = 20;

function foo() {
	a = a + 1;
}

function bar() {
	a = a * 2;
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

In JavaScript's single-threaded behavior, if `foo()` runs before `bar()`, the result is that `a` has `42`, but if `bar()` runs before `foo()` the result in `a` will be `41`.

If JS events sharing the same data executed in parallel, though, the problems would be much more subtle. Consider these two lists of pseudocode tasks as the threads that could respectively run the code in `foo()` and `bar()`, and consider what happens if they are running at exactly the same time:

Thread 1 (`X` and `Y` are temporary memory locations):
```
foo():
  a. load value of `a` in `X`
  b. store `1` in `Y`
  c. add `X` and `Y`, store result in `X`
  d. store value of `X` in `a`
```

Thread 2 (`X` and `Y` are temporary memory locations):
```
bar():
  a. load value of `a` in `X`
  b. store `2` in `Y`
  c. multiply `X` and `Y`, store result in `X`
  d. store value of `X` in `a`
```

Now, let's say that the two threads are running truly in parallel. You can probably spot the problem, right? They use shared memory locations `X` and `Y` for their temporary steps.

What's the end result in `a` if the steps happen like this?

```
1a  (load value of `a` in `X`   ==> `20`)
2a  (load value of `a` in `X`   ==> `20`)
1b  (store `1` in `Y`   ==> `1`)
2b  (store `2` in `Y`   ==> `2`)
1c  (add `X` and `Y`, store result in `X`   ==> `22`)
1d  (store value of `X` in `a`   ==> `22`)
2c  (multiply `X` and `Y`, store result in `X`   ==> `44`)
2d  (store value of `X` in `a`   ==> `44`)
```

The result in `a` will be `44`. But what about this ordering?

```
1a  (load value of `a` in `X`   ==> `20`)
2a  (load value of `a` in `X`   ==> `20`)
2b  (store `2` in `Y`   ==> `2`)
1b  (store `1` in `Y`   ==> `1`)
2c  (multiply `X` and `Y`, store result in `X`   ==> `20`)
1c  (add `X` and `Y`, store result in `X`   ==> `21`)
1d  (store value of `X` in `a`   ==> `21`)
2d  (store value of `X` in `a`   ==> `21`)
```

The result in `a` will be `21`.

So, threaded programming is very tricky, because if you don't take special steps to prevent this kind of interruption/interleaving from happening, you can get very surprising, nondeterministic behavior that frequently leads to headaches.

JavaScript never shares data across threads, which means *that* level of nondeterminism isn't a concern. But that doesn't mean JS is always deterministic. Remember earlier, where the relative ordering of `foo()` and `bar()` produces two different results (`41` or `42`)?

**Note:** It may not be obvious yet, but not all nondeterminism is bad. Sometimes it's irrelevant, and sometimes it's intentional. We'll see more examples of that throughout this and the next few chapters.

### Run-to-Completion

Because of JavaScript's single-threading, the code inside of `foo()` (and `bar()`) is atomic, which means that once `foo()` starts running, the entirety of its code will finish before any of the code in `bar()` can run, or vice versa. This is called "run-to-completion" behavior.

In fact, the run-to-completion semantics are more obvious when `foo()` and `bar()` have more code in them, such as:

```js
var a = 1;
var b = 2;

function foo() {
	a++;
	b = b * a;
	a = b + 3;
}

function bar() {
	b--;
	a = 8 + b;
	b = a * 2;
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

Because `foo()` can't be interrupted by `bar()`, and `bar()` can't be interrupted by `foo()`, this program only has two possible outcomes depending on which starts running first -- if threading were present, and the individual statements in `foo()` and `bar()` could be interleaved, the number of possible outcomes would be greatly increased!

Chunk 1 is synchronous (happens *now*), but chunks 2 and 3 are asynchronous (happen *later*), which means their execution will be separated by a gap of time.

Chunk 1:
```js
var a = 1;
var b = 2;
```

Chunk 2 (`foo()`):
```js
a++;
b = b * a;
a = b + 3;
```

Chunk 3 (`bar()`):
```js
b--;
a = 8 + b;
b = a * 2;
```

Chunks 2 and 3 may happen in either-first order, so there are two possible outcomes for this program, as illustrated here:

Outcome 1:
```js
var a = 1;
var b = 2;

// foo()
a++;
b = b * a;
a = b + 3;

// bar()
b--;
a = 8 + b;
b = a * 2;

a; // 11
b; // 22
```

Outcome 2:
```js
var a = 1;
var b = 2;

// bar()
b--;
a = 8 + b;
b = a * 2;

// foo()
a++;
b = b * a;
a = b + 3;

a; // 183
b; // 180
```

Two outcomes from the same code means we still have nondeterminism! But it's at the function (event) ordering level, rather than at the statement ordering level (or, in fact, the expression operation ordering level) as it is with threads. In other words, it's *more deterministic* than threads would have been.

As applied to JavaScript's behavior, this function-ordering nondeterminism is the common term "race condition," as `foo()` and `bar()` are racing against each other to see which runs first. Specifically, it's a "race condition" because you cannot predict reliably how `a` and `b` will turn out.

**Note:** If there was a function in JS that somehow did not have run-to-completion behavior, we could have many more possible outcomes, right? It turns out ES6 introduces just such a thing (see Chapter 4 "Generators"), but don't worry right now, we'll come back to that!

## Concurrency

Let's imagine a site that displays a list of status updates (like a social network news feed) that progressively loads as the user scrolls down the list. To make such a feature work correctly, (at least) two separate "processes" will need to be executing *simultaneously* (i.e., during the same window of time, but not necessarily at the same instant).

**Note:** We're using "process" in quotes here because they aren't true operating system–level processes in the computer science sense. They're virtual processes, or tasks, that represent a logically connected, sequential series of operations. We'll simply prefer "process" over "task" because terminology-wise, it will match the definitions of the concepts we're exploring.

The first "process" will respond to `onscroll` events (making Ajax requests for new content) as they fire when the user has scrolled the page further down. The second "process" will receive Ajax responses back (to render content onto the page).

Obviously, if a user scrolls fast enough, you may see two or more `onscroll` events fired during the time it takes to get the first response back and process, and thus you're going to have `onscroll` events and Ajax response events firing rapidly, interleaved with each other.

Concurrency is when two or more "processes" are executing simultaneously over the same period, regardless of whether their individual constituent operations happen *in parallel* (at the same instant on separate processors or cores) or not. You can think of concurrency then as "process"-level (or task-level) parallelism, as opposed to operation-level parallelism (separate-processor threads).

**Note:** Concurrency also introduces an optional notion of these "processes" interacting with each other. We'll come back to that later.

For a given window of time (a few seconds worth of a user scrolling), let's visualize each independent "process" as a series of events/operations:

"Process" 1 (`onscroll` events):
```
onscroll, request 1
onscroll, request 2
onscroll, request 3
onscroll, request 4
onscroll, request 5
onscroll, request 6
onscroll, request 7
```

"Process" 2 (Ajax response events):
```
response 1
response 2
response 3
response 4
response 5
response 6
response 7
```

It's quite possible that an `onscroll` event and an Ajax response event could be ready to be processed at exactly the same *moment*. For example, let's visualize these events in a timeline:

```
onscroll, request 1
onscroll, request 2          response 1
onscroll, request 3          response 2
response 3
onscroll, request 4
onscroll, request 5
onscroll, request 6          response 4
onscroll, request 7
response 6
response 5
response 7
```

But, going back to our notion of the event loop from earlier in the chapter, JS is only going to be able to handle one event at a time, so either `onscroll, request 2` is going to happen first or `response 1` is going to happen first, but they cannot happen at literally the same moment. Just like kids at a school cafeteria, no matter what crowd they form outside the doors, they'll have to merge into a single line to get their lunch!

Let's visualize the interleaving of all these events onto the event loop queue.

Event Loop Queue:
```
onscroll, request 1   <--- Process 1 starts
onscroll, request 2
response 1            <--- Process 2 starts
onscroll, request 3
response 2
response 3
onscroll, request 4
onscroll, request 5
onscroll, request 6
response 4
onscroll, request 7   <--- Process 1 finishes
response 6
response 5
response 7            <--- Process 2 finishes
```

"Process 1" and "Process 2" run concurrently (task-level parallel), but their individual events run sequentially on the event loop queue.

By the way, notice how `response 6` and `response 5` came back out of expected order?

The single-threaded event loop is one expression of concurrency (there are certainly others, which we'll come back to later).

### Noninteracting

As two or more "processes" are interleaving their steps/events concurrently within the same program, they don't necessarily need to interact with each other if the tasks are unrelated. **If they don't interact, nondeterminism is perfectly acceptable.**

For example:

```js
var res = {};

function foo(results) {
	res.foo = results;
}

function bar(results) {
	res.bar = results;
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

`foo()` and `bar()` are two concurrent "processes," and it's nondeterminate which order they will be fired in. But we've constructed the program so it doesn't matter what order they fire in, because they act independently and as such don't need to interact.

This is not a "race condition" bug, as the code will always work correctly, regardless of the ordering.

### Interaction

More commonly, concurrent "processes" will by necessity interact, indirectly through scope and/or the DOM. When such interaction will occur, you need to coordinate these interactions to prevent "race conditions," as described earlier.

Here's a simple example of two concurrent "processes" that interact because of implied ordering, which is only *sometimes broken*:

```js
var res = [];

function response(data) {
	res.push( data );
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

The concurrent "processes" are the two `response()` calls that will be made to handle the Ajax responses. They can happen in either-first order.

Let's assume the expected behavior is that `res[0]` has the results of the `"http://some.url.1"` call, and `res[1]` has the results of the `"http://some.url.2"` call. Sometimes that will be the case, but sometimes they'll be flipped, depending on which call finishes first. There's a pretty good likelihood that this nondeterminism is a "race condition" bug.

**Note:** Be extremely wary of assumptions you might tend to make in these situations. For example, it's not uncommon for a developer to observe that `"http://some.url.2"` is "always" much slower to respond than `"http://some.url.1"`, perhaps by virtue of what tasks they're doing (e.g., one performing a database task and the other just fetching a static file), so the observed ordering seems to always be as expected. Even if both requests go to the same server, and *it* intentionally responds in a certain order, there's no *real* guarantee of what order the responses will arrive back in the browser.

So, to address such a race condition, you can coordinate ordering interaction:

```js
var res = [];

function response(data) {
	if (data.url == "http://some.url.1") {
		res[0] = data;
	}
	else if (data.url == "http://some.url.2") {
		res[1] = data;
	}
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

Regardless of which Ajax response comes back first, we inspect the `data.url` (assuming one is returned from the server, of course!) to figure out which position the response data should occupy in the `res` array. `res[0]` will always hold the `"http://some.url.1"` results and `res[1]` will always hold the `"http://some.url.2"` results. Through simple coordination, we eliminated the "race condition" nondeterminism.

The same reasoning from this scenario would apply if multiple concurrent function calls were interacting with each other through the shared DOM, like one updating the contents of a `<div>` and the other updating the style or attributes of the `<div>` (e.g., to make the DOM element visible once it has content). You probably wouldn't want to show the DOM element before it had content, so the coordination must ensure proper ordering interaction.

Some concurrency scenarios are *always broken* (not just *sometimes*) without coordinated interaction. Consider:

```js
var a, b;

function foo(x) {
	a = x * 2;
	baz();
}

function bar(y) {
	b = y * 2;
	baz();
}

function baz() {
	console.log(a + b);
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

In this example, whether `foo()` or `bar()` fires first, it will always cause `baz()` to run too early (either `a` or `b` will still be `undefined`), but the second invocation of `baz()` will work, as both `a` and `b` will be available.

There are different ways to address such a condition. Here's one simple way:

```js
var a, b;

function foo(x) {
	a = x * 2;
	if (a && b) {
		baz();
	}
}

function bar(y) {
	b = y * 2;
	if (a && b) {
		baz();
	}
}

function baz() {
	console.log( a + b );
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

The `if (a && b)` conditional around the `baz()` call is traditionally called a "gate," because we're not sure what order `a` and `b` will arrive, but we wait for both of them to get there before we proceed to open the gate (call `baz()`).

Another concurrency interaction condition you may run into is sometimes called a "race," but more correctly called a "latch." It's characterized by "only the first one wins" behavior. Here, nondeterminism is acceptable, in that you are explicitly saying it's OK for the "race" to the finish line to have only one winner.

Consider this broken code:

```js
var a;

function foo(x) {
	a = x * 2;
	baz();
}

function bar(x) {
	a = x / 2;
	baz();
}

function baz() {
	console.log( a );
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

Whichever one (`foo()` or `bar()`) fires last will not only overwrite the assigned `a` value from the other, but it will also duplicate the call to `baz()` (likely undesired).

So, we can coordinate the interaction with a simple latch, to let only the first one through:

```js
var a;

function foo(x) {
	if (a == undefined) {
		a = x * 2;
		baz();
	}
}

function bar(x) {
	if (a == undefined) {
		a = x / 2;
		baz();
	}
}

function baz() {
	console.log( a );
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

The `if (a == undefined)` conditional allows only the first of `foo()` or `bar()` through, and the second (and indeed any subsequent) calls would just be ignored. There's just no virtue in coming in second place!

**Note:** In all these scenarios, we've been using global variables for simplistic illustration purposes, but there's nothing about our reasoning here that requires it. As long as the functions in question can access the variables (via scope), they'll work as intended. Relying on lexically scoped variables (see the *Scope & Closures* title of this book series), and in fact global variables as in these examples, is one obvious downside to these forms of concurrency coordination. As we go through the next few chapters, we'll see other ways of coordination that are much cleaner in that respect.

### Cooperation

Another expression of concurrency coordination is called "cooperative concurrency." Here, the focus isn't so much on interacting via value sharing in scopes (though that's obviously still allowed!). The goal is to take a long-running "process" and break it up into steps or batches so that other concurrent "processes" have a chance to interleave their operations into the event loop queue.

For example, consider an Ajax response handler that needs to run through a long list of results to transform the values. We'll use `Array#map(..)` to keep the code shorter:

```js
var res = [];

// `response(..)` receives array of results from the Ajax call
function response(data) {
	// add onto existing `res` array
	res = res.concat(
		// make a new transformed array with all `data` values doubled
		data.map( function(val){
			return val * 2;
		} )
	);
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

If `"http://some.url.1"` gets its results back first, the entire list will be mapped into `res` all at once. If it's a few thousand or less records, this is not generally a big deal. But if it's say 10 million records, that can take a while to run (several seconds on a powerful laptop, much longer on a mobile device, etc.).

While such a "process" is running, nothing else in the page can happen, including no other `response(..)` calls, no UI updates, not even user events like scrolling, typing, button clicking, and the like. That's pretty painful.

So, to make a more cooperatively concurrent system, one that's friendlier and doesn't hog the event loop queue, you can process these results in asynchronous batches, after each one "yielding" back to the event loop to let other waiting events happen.

Here's a very simple approach:

```js
var res = [];

// `response(..)` receives array of results from the Ajax call
function response(data) {
	// let's just do 1000 at a time
	var chunk = data.splice( 0, 1000 );

	// add onto existing `res` array
	res = res.concat(
		// make a new transformed array with all `chunk` values doubled
		chunk.map( function(val){
			return val * 2;
		} )
	);

	// anything left to process?
	if (data.length > 0) {
		// async schedule next batch
		setTimeout( function(){
			response( data );
		}, 0 );
	}
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

We process the data set in maximum-sized chunks of 1,000 items. By doing so, we ensure a short-running "process," even if that means many more subsequent "processes," as the interleaving onto the event loop queue will give us a much more responsive (performant) site/app.

Of course, we're not interaction-coordinating the ordering of any of these "processes," so the order of results in `res` won't be predictable. If ordering was required, you'd need to use interaction techniques like those we discussed earlier, or ones we will cover in later chapters of this book.

We use the `setTimeout(..0)` (hack) for async scheduling, which basically just means "stick this function at the end of the current event loop queue."

**Note:** `setTimeout(..0)` is not technically inserting an item directly onto the event loop queue. The timer will insert the event at its next opportunity. For example, two subsequent `setTimeout(..0)` calls would not be strictly guaranteed to be processed in call order, so it *is* possible to see various conditions like timer drift where the ordering of such events isn't predictable. In Node.js, a similar approach is `process.nextTick(..)`. Despite how convenient (and usually more performant) it would be, there's not a single direct way (at least yet) across all environments to ensure async event ordering. We cover this topic in more detail in the next section.

## Jobs

As of ES6, there's a new concept layered on top of the event loop queue, called the "Job queue." The most likely exposure you'll have to it is with the asynchronous behavior of Promises (see Chapter 3).

Unfortunately, at the moment it's a mechanism without an exposed API, and thus demonstrating it is a bit more convoluted. So we're going to have to just describe it conceptually, such that when we discuss async behavior with Promises in Chapter 3, you'll understand how those actions are being scheduled and processed.

So, the best way to think about this that I've found is that the "Job queue" is a queue hanging off the end of every tick in the event loop queue. Certain async-implied actions that may occur during a tick of the event loop will not cause a whole new event to be added to the event loop queue, but will instead add an item (aka Job) to the end of the current tick's Job queue.

It's kinda like saying, "oh, here's this other thing I need to do *later*, but make sure it happens right away before anything else can happen."

Or, to use a metaphor: the event loop queue is like an amusement park ride, where once you finish the ride, you have to go to the back of the line to ride again. But the Job queue is like finishing the ride, but then cutting in line and getting right back on.

A Job can also cause more Jobs to be added to the end of the same queue. So, it's theoretically possible that a Job "loop" (a Job that keeps adding another Job, etc.) could spin indefinitely, thus starving the program of the ability to move on to the next event loop tick. This would conceptually be almost the same as just expressing a long-running or infinite loop (like `while (true) ..`) in your code.

Jobs are kind of like the spirit of the `setTimeout(..0)` hack, but implemented in such a way as to have a much more well-defined and guaranteed ordering: **later, but as soon as possible**.

Let's imagine an API for scheduling Jobs (directly, without hacks), and call it `schedule(..)`. Consider:

```js
console.log( "A" );

setTimeout( function(){
	console.log( "B" );
}, 0 );

// theoretical "Job API"
schedule( function(){
	console.log( "C" );

	schedule( function(){
		console.log( "D" );
	} );
} );
```

You might expect this to print out `A B C D`, but instead it would print out `A C D B`, because the Jobs happen at the end of the current event loop tick, and the timer fires to schedule for the *next* event loop tick (if available!).

In Chapter 3, we'll see that the asynchronous behavior of Promises is based on Jobs, so it's important to keep clear how that relates to event loop behavior.

## Statement Ordering

The order in which we express statements in our code is not necessarily the same order as the JS engine will execute them. That may seem like quite a strange assertion to make, so we'll just briefly explore it.

But before we do, we should be crystal clear on something: the rules/grammar of the language (see the *Types & Grammar* title of this book series) dictate a very predictable and reliable behavior for statement ordering from the program point of view. So what we're about to discuss are **not things you should ever be able to observe** in your JS program.

**Warning:** If you are ever able to *observe* compiler statement reordering like we're about to illustrate, that'd be a clear violation of the specification, and it would unquestionably be due to a bug in the JS engine in question -- one which should promptly be reported and fixed! But it's vastly more common that you *suspect* something crazy is happening in the JS engine, when in fact it's just a bug (probably a "race condition"!) in your own code -- so look there first, and again and again. The JS debugger, using breakpoints and stepping through code line by line, will be your most powerful tool for sniffing out such bugs in *your code*.

Consider:

```js
var a, b;

a = 10;
b = 30;

a = a + 1;
b = b + 1;

console.log( a + b ); // 42
```

This code has no expressed asynchrony to it (other than the rare `console` async I/O discussed earlier!), so the most likely assumption is that it would process line by line in top-down fashion.

But it's *possible* that the JS engine, after compiling this code (yes, JS is compiled -- see the *Scope & Closures* title of this book series!) might find opportunities to run your code faster by rearranging (safely) the order of these statements. Essentially, as long as you can't observe the reordering, anything's fair game.

For example, the engine might find it's faster to actually execute the code like this:

```js
var a, b;

a = 10;
a++;

b = 30;
b++;

console.log( a + b ); // 42
```

Or this:

```js
var a, b;

a = 11;
b = 31;

console.log( a + b ); // 42
```

Or even:

```js
// because `a` and `b` aren't used anymore, we can
// inline and don't even need them!
console.log( 42 ); // 42
```

In all these cases, the JS engine is performing safe optimizations during its compilation, as the end *observable* result will be the same.

But here's a scenario where these specific optimizations would be unsafe and thus couldn't be allowed (of course, not to say that it's not optimized at all):

```js
var a, b;

a = 10;
b = 30;

// we need `a` and `b` in their preincremented state!
console.log( a * b ); // 300

a = a + 1;
b = b + 1;

console.log( a + b ); // 42
```

Other examples where the compiler reordering could create observable side effects (and thus must be disallowed) would include things like any function call with side effects (even and especially getter functions), or ES6 Proxy objects (see the *ES6 & Beyond* title of this book series).

Consider:

```js
function foo() {
	console.log( b );
	return 1;
}

var a, b, c;

// ES5.1 getter literal syntax
c = {
	get bar() {
		console.log( a );
		return 1;
	}
};

a = 10;
b = 30;

a += foo();				// 30
b += c.bar;				// 11

console.log( a + b );	// 42
```

If it weren't for the `console.log(..)` statements in this snippet (just used as a convenient form of observable side effect for the illustration), the JS engine would likely have been free, if it wanted to (who knows if it would!?), to reorder the code to:

```js
// ...

a = 10 + foo();
b = 30 + c.bar;

// ...
```

While JS semantics thankfully protect us from the *observable* nightmares that compiler statement reordering would seem to be in danger of, it's still important to understand just how tenuous a link there is between the way source code is authored (in top-down fashion) and the way it runs after compilation.

Compiler statement reordering is almost a micro-metaphor for concurrency and interaction. As a general concept, such awareness can help you understand async JS code flow issues better.

## Review

A JavaScript program is (practically) always broken up into two or more chunks, where the first chunk runs *now* and the next chunk runs *later*, in response to an event. Even though the program is executed chunk-by-chunk, all of them share the same access to the program scope and state, so each modification to state is made on top of the previous state.

Whenever there are events to run, the *event loop* runs until the queue is empty. Each iteration of the event loop is a "tick." User interaction, IO, and timers enqueue events on the event queue.

At any given moment, only one event can be processed from the queue at a time. While an event is executing, it can directly or indirectly cause one or more subsequent events.

Concurrency is when two or more chains of events interleave over time, such that from a high-level perspective, they appear to be running *simultaneously* (even though at any given moment only one event is being processed).

It's often necessary to do some form of interaction coordination between these concurrent "processes" (as distinct from operating system processes), for instance to ensure ordering or to prevent "race conditions." These "processes" can also *cooperate* by breaking themselves into smaller chunks and to allow other "process" interleaving.
