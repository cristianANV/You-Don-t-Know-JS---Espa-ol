# You Don't Know JS: Up & Going
# Capítulo 3: Dentro de YDKJS

¿De qué se trata esta serie? Coloquémoslo simple, es sobre tomar seriamente la tarea de aprender *todas las partes de Javascript*, no sólo las partes del subconjunto del lenguaje que algunos llaman "las partes buenas", y no sólo la mínima cantidad que usted necesita para realizar bien sus tareas en el trabajo.

Desarrolladores serios en otros lenguajes esperan colocar todo su esfuerzo para aprender la mayor parte (o todo) sobre los lenguajes (o el lenguaje) con los que ellos escriben principalmente, pero los desarrolladores de JS parece que están fuera de esta multitud debido a que ellos no suelen aprender muchas cosas sobre este lenguaje. Esto no es tan bueno, y no es algo que debamos continuar permitiendo que sea la norma.

La serie de libros "Usted no sabe JS" (*UNSJS*) o en inglés *You Don't Know JS* (*YDKJS*) se encuentra en el marcado contraste de los típicos enfoques de aprender JS, y es diferente a casí cualquier otro libro sobre JS que usted vaya a leer. Aquí lo desafía a ir más allá de su zona de confort y realizarse a sí mismo preguntas como "¿por qué?" para cada simple comportamiento que usted encuentre. ¿Está listo para ese desafío?

Voy a usar este capítulo final para resumir brevemente qué es lo que espero del resto de la serie de libros, y cómo ir de la manera más efectiva para construir una base de aprendizaje en JS sobre *YDKJS*.

## Alcance & Clausuras

Quizás una de las cosas más fundamentales que usted necesitará rápidamente entender es cómo el alcance de las variables realmente funciona en JavaScript. No es suficiente tener *creencias* difusas puntuales acerca del alcance.

El título *Alcance & y Clausuras* empieza por desmitificar la típica idea equivocada que JS es un "lenguaje interpretado" y por lo tanto no compilado. No.

El motor de JS compila su código justo antes de (¡Y a veces durante!) la ejecución. Así que nosotros tendremos un entendimiento algo más profundo sobre el enfoque que el compilador utiliza en nuestro código para entender cómo encuentra y trata con las declaraciones de variables y funciones. En el camino, veremos la típica metáfora para el manejo del alcance de variables en JS, llamado en inglés "Hoisting".

Este entendimiento crítico sobre el "alcance léxico" es en lo que nos basaremos para nuestra exploración de las clausuras para el último capítulo del libro. La clausura es quizás el concepto más importante de todo JS, pero si usted no ha primero comprendido firmemente cómo el alcance funciona, la clausura probablemente permanecerá lejos de su comprensión.

Una aplicación importante de la clausura es el patrón modular, como fue introducido brevemente en este libro en el Capítulo 2. El patrón modular es quizás el patrón de organización de código más frecuente en todo JS; un entendimiento profundo de dicho patrón debería ser una de sus más altas prioridades.

## this & Prototipos de Objetos

Quizás uno de los conceptos erróneos más extendidos y constantes acerca de JavaScript es que la palabra clave `this` se refiere a la función donde aparece. Totalmente erróneo.

La palabra clave `this` está dinámicamente enlazada en cómo la función en cuestión es ejecutada, y resulta que hay cuatro reglas simples para entender y determinar completamente el enlazamiento de `this`.

El mecanismo de prototipo de objeto está cercanamente relacionado a la palabra clave `this`, el cual es una búsqueda en cadena de propiedades, similar a como el alcance léxico de variables es localizado. Pero envolverlo todo en prototipos es la otra gran idea equivocada que se tiene sobre JS: la idea de emular (falsamente) clases y herencia (llamada como "herencia prototípica").

Desafortunadamente, el deseo de traer el patrón de diseño de clase y herencia pensando en JavaSript es lo peor que usted podría intentar hacer, porque mientras la sintaxis puede engañarle en pensar que hay algo como las clases, realmente el mecanismo de prototipo es fundamentalmente lo contrario a su comportamiento.

Lo que está en discusión es si es mejor ignorar la desigualdad de los conceptos y pretender que lo que usted está implementando es "herencia", o si es más apropiado aprender y aceptar cómo funciona realmente el sistema de prototipos de objetos. Este último se denomina más apropiadamente "delegación de comportamiento".

Esto es más que una preferencia sintáctica. La delegación es un patrón de diseño completamente diferente y más poderoso, que reemplaza la necesidad de diseñar con clases y herencia. Sin embargo, estas afirmaciones son absolutamente distintas para casi cualquier otra publicación de blog, libro y conferencia sobre el tema durante toda la vida de JavaScript.

Las afirmaciones que hago con respecto a la delegación frente a la herencia no provienen de una aversión al lenguaje y su sintaxis, sino del deseo de ver la verdadera capacidad del lenguaje aprovechado adecuadamente y así eliminar la confusión y frustración sin fin sobre este tema.

Pero el caso que planteo acerca de los prototipos y la delegación es uno mucho más complicado de lo que voy a hacer aquí. Si usted está listo para reconsiderar todo lo que usted piensa y sabe acerca de las "clases" y "herencia" en JavaScript, le ofrezco la oportunidad de "tomar la píldora roja" (*Matrix* 1999) y consultar los capitulos 4-6 de este título llamado *this & Prototipos de Objetos* de esta serie.

## Tipos y Gramática

El tercer título de esta serie primeramente se enfoca en abordar otro tema muy controversial: la coerción de tipos. Quizás ningún tópico causa mayor frustración en los desarrolladores de JS que cuando se habla acerca de las confusiones alrededor de la coerción implícita.

En gran medida, la sabiduría convencional es que la coerción implícita es una "mala parte" del lenguaje y debería evitarse a toda costa. De hecho, algunos han ido tan lejos en llamarlo una "falla" en el diseño del lenguaje. En realidad hay herramientas cuyo su único trabajo es no hacer nada más que escanear su código y quejarse si usted está haciendo algo remotamente parecido a la coerción.

Pero es realmente la coerción tan confusa, tan mala, tan traicionera, que su código está condenado desde el momento que usted lo usa?

Yo digo que no. Después de haber abordado y entendido cómo los tipos y valores realmente funcionan en los Capítulos 1-3, el Capítulo 4 se encarga de este debate y explica por completo cómo la coerción funciona en todos los aspectos. Veremos qué partes de la coerción son realmente sorprendentes y qué partes realmente tienen completo sentido si se les da el tiempo para aprender.

Pero no estoy sólo sugiriendo que la coerción es razonable y se puede aprender, estoy afirmando que la coerción es una herramienta increíblemente útil y totalmente subestimada que *usted debería usar en su código*. Estoy diciendo que esa coerción, cuando se usa adecuadamente, no sólo funciona, sino hace que su código sea mejor. Seguramente todos los que no están de acuerdo con esto se burlarán de esta posición sobre la coerción, pero creo que es una de las principales claves para aumentar tu juego en JS.

Usted quiere seguir lo que la gente dice, o está dispuesto a colocar a un lado todas las suposiciones y mirar la coerción con una prespectiva fresca? El título *Tipos y Gramática* de esta serie cambiará su forma de pensar.

## Async & Performance

The first three titles of this series focus on the core mechanics of the language, but the fourth title branches out slightly to cover patterns on top of the language mechanics for managing asynchronous programming. Asynchrony is not only critical to the performance of our applications, it's increasingly becoming *the* critical factor in writability and maintainability.

The book starts first by clearing up a lot of terminology and concept confusion around things like "async," "parallel," and "concurrent," and explains in depth how such things do and do not apply to JS.

Then we move into examining callbacks as the primary method of enabling asynchrony. But it's here that we quickly see that the callback alone is hopelessly insufficient for the modern demands of asynchronous programming. We identify two major deficiencies of callbacks-only coding: *Inversion of Control* (IoC) trust loss and lack of linear reason-ability.

To address these two major deficiencies, ES6 introduces two new mechanisms (and indeed, patterns): promises and generators.

Promises are a time-independent wrapper around a "future value," which lets you reason about and compose them regardless of if the value is ready or not yet. Moreover, they effectively solve the IoC trust issues by routing callbacks through a trustable and composable promise mechanism.

Generators introduce a new mode of execution for JS functions, whereby the generator can be paused at `yield` points and be resumed asynchronously later. The pause-and-resume capability enables synchronous, sequential looking code in the generator to be processed asynchronously behind the scenes. By doing so, we address the non-linear, non-local-jump confusions of callbacks and thereby make our asynchronous code sync-looking so as to be more reason-able.

But it's the combination of promises and generators that "yields" our most effective asynchronous coding pattern to date in JavaScript. In fact, much of the future sophistication of asynchrony coming in ES7 and later will certainly be built on this foundation. To be serious about programming effectively in an async world, you're going to need to get really comfortable with combining promises and generators.

If promises and generators are about expressing patterns that let our programs run more concurrently and thus get more processing accomplished in a shorter period, JS has many other facets of performance optimization worth exploring.

Chapter 5 delves into topics like program parallelism with Web Workers and data parallelism with SIMD, as well as low-level optimization techniques like ASM.js. Chapter 6 takes a look at performance optimization from the perspective of proper benchmarking techniques, including what kinds of performance to worry about and what to ignore.

Writing JavaScript effectively means writing code that can break the constraint barriers of being run dynamically in a wide range of browsers and other environments. It requires a lot of intricate and detailed planning and effort on our parts to take a program from "it works" to "it works well."

The *Async & Performance* title is designed to give you all the tools and skills you need to write reasonable and performant JavaScript code.

## ES6 & Beyond

No matter how much you feel you've mastered JavaScript to this point, the truth is that JavaScript is never going to stop evolving, and moreover, the rate of evolution is increasing rapidly. This fact is almost a metaphor for the spirit of this series, to embrace that we'll never fully *know* every part of JS, because as soon as you master it all, there's going to be new stuff coming down the line that you'll need to learn.

This title is dedicated to both the short- and mid-term visions of where the language is headed, not just the *known* stuff like ES6 but the *likely* stuff beyond.

While all the titles of this series embrace the state of JavaScript at the time of this writing, which is mid-way through ES6 adoption, the primary focus in the series has been more on ES5. Now, we want to turn our attention to ES6, ES7, and ...

Since ES6 is nearly complete at the time of this writing, *ES6 & Beyond* starts by dividing up the concrete stuff from the ES6 landscape into several key categories, including new syntax, new data structures (collections), and new processing capabilities and APIs. We cover each of these new ES6 features, in varying levels of detail, including reviewing details that are touched on in other books of this series.

Some exciting ES6 things to look forward to reading about: destructuring, default parameter values, symbols, concise methods, computed properties, arrow functions, block scoping, promises, generators, iterators, modules, proxies, weakmaps, and much, much more! Phew, ES6 packs quite a punch!

The first part of the book is a roadmap for all the stuff you need to learn to get ready for the new and improved JavaScript you'll be writing and exploring over the next couple of years.

The latter part of the book turns attention to briefly glance at things that we can likely expect to see in the near future of JavaScript. The most important realization here is that post-ES6, JS is likely going to evolve feature by feature rather than version by version, which means we can expect to see these near-future things coming much sooner than you might imagine.

The future for JavaScript is bright. Isn't it time we start learning it!?

## Review

The *YDKJS* series is dedicated to the proposition that all JS developers can and should learn all of the parts of this great language. No person's opinion, no framework's assumptions, and no project's deadline should be the excuse for why you never learn and deeply understand JavaScript.

We take each important area of focus in the language and dedicate a short but very dense book to fully explore all the parts of it that you perhaps thought you knew but probably didn't fully.

"You Don't Know JS" isn't a criticism or an insult. It's a realization that all of us, myself included, must come to terms with. Learning JavaScript isn't an end goal but a process. We don't know JavaScript, yet. But we will!
