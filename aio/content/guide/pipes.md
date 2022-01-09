# Transformar Información Usando Pipes

Usa los [pipes](guide/glossary#pipe "Definicion de pipe") para transformar strings, símbolos de monedas, fechas y otro tipo de información para mostrar.
Los Pipes son simples funciones que puedes usar en [la plantilla de expresión](/guide/glossary#template-expression "Definicion de plantilla de expresión") los cuales aceptan un valor de entrada y retornan ese valor transformado.
Los pipes son útiles porque puedes usarlos en toda la aplicación, habiéndolos declarado solo una vez.

Por ejemplo, puedes usar un pipe para mostrar una fecha como **April 15, 1988** en lugar de un string sin formato.

<div class="alert is-helpful">

Para ver la aplicación de muestra utilizada en este tema, consulte <live-example></live-example>.

</div>

Angular tiene incorporados pipes para las típicas transformaciones de datos, incluyendo transformaciones para la internacionalización (i18n), que utilizan información de la configuración regional para formatear los datos.
Los siguientes son pipes integrados de uso común para formatear datos:

- [`DatePipe`](api/common/DatePipe): Formatea un valor de fecha de acuerdo a las reglas locales.
- [`UpperCasePipe`](api/common/UpperCasePipe): Transforma todo el texto a mayúscula.
- [`LowerCasePipe`](api/common/LowerCasePipe): Transforma todo el texto a minúscula.
- [`CurrencyPipe`](api/common/CurrencyPipe): Transforma un numero a un string de moneda, formateado de acuerdo a las reglas locales.
- [`DecimalPipe`](/api/common/DecimalPipe): Transforma un numero en un string con punto decimal, formateado de acuerdo a las reglas locales.
- [`PercentPipe`](api/common/PercentPipe): Transforma un numero en un string con porcentaje, formateado de acuerdo a las reglas locales.

<div class="alert is-helpful">

- Para ver una lista completa de los pipes incorporados por defecto en angular, puedes ver [pipes API documentación](/api/common#pipes "Pipes API resumen de referencia").
- Para aprender mas acerca del uso de los pipes para la internalización (i18n), puedes ver [formatear información según configuración regional](/guide/i18n#i18n-pipes "[Formatear información según configuración regional").

</div>

Puedes crear tus propios pipes para encapsular una transformación personalizada y usar tus pipes personalizados en al expresión de plantilla.

## Prerrequisitos

Para usar pipes debe tener un conocimiento básico de lo siguiente:

- [Typescript](guide/glossary#typescript "Definición de Typescript") y programación de HTML5
- [Plantillas](guide/glossary#template "Definición de Plantilla") en HTML con estilos CSS
- [Componentes](guide/glossary#component "Definición de Componente")

## Usar un pipe en una plantilla

Para aplicar un pipe, se debe de usar el operador de pipe (`|`) seguido del _nombre_ del _name_ dentro de una plantilla de expresión. En el siguiente ejemplo, se ilustra esto para el pipe `date`, el cual es un pipe integrado de angular, puedes leer mas de el en [`DatePipe`](api/common/DatePipe).
Las pestañas del ejemplo muestran lo siguiente:

- `app.component.html` usa `date` en una plantilla separada para mostrar un cumpleaños.
- `hero-birthday1.component.ts` usa el mismo pipe como parte de una plantilla in-line en un componente que también establece el valor de cumpleaños.

<code-tabs>
  <code-pane
    header="src/app/app.component.html"
    region="hero-birthday-template"
    path="pipes/src/app/app.component.html">
  </code-pane>
  <code-pane
    header="src/app/hero-birthday1.component.ts"
    path="pipes/src/app/hero-birthday1.component.ts">
  </code-pane>
</code-tabs>

En el componente `birthday` el valor fluye a través del
[operador pipe](guide/template-expression-operators#pipe) ( | ) hasta la función [`date`](api/common/DatePipe).

{@a parameterizing-a-pipe}

## Transformar datos con parámetros y pipes encadenados

Utilice parámetros opcionales para ajustar la salida de un pipe.
Por ejemplo, puedes usar el [`CurrencyPipe`](api/common/CurrencyPipe "API reference") y pasarle como parámetro el código de un país, por ejemplo EUR.
La expresión de plantilla será `{{ amount | currency:'EUR' }}` lo cual transformara `amount` a formado moneda con euros.
Para agregar el parámetro, debes de agregar luego del nombre del pipe (`currency`) dos puntos (`:`) y el valor del parámetro (`'EUR'`).

Si el pipe que quieres usar, acepta múltiple parámetros, simplemente separa los valores de los mismos con dos puntos.
Por ejemplo, `{{ amount | currency:'EUR':'Euros '}}` agrega un segundo parámetro, el string literal `'Euros '`, al string de salida string. Puedes usar cualquier plantilla de expresión valida como parámetros, como un string literal on una propiedad de un componente.

Algunos pipes requieren al menos un parámetro y permiten otros parámetros como opcionales, un pipe de este tipo es [`SlicePipe`](/api/common/SlicePipe "API reference for SlicePipe"). Por ejemplo, `{{ slice:1:5 }}` crea un nuevo array o string que contiene un subconjunto de los elementos que comienzan con el elemento `1` y terminan con el elemento `5`.

### Ejemplo: Dar formato a una fecha

Las pestañas del siguiente ejemplo muestran cómo alternar entre dos formatos diferentes (`'shortDate'` y `'fullDate'`):

- La plantilla `app.component.html` usa el parámetro format para el [`DatePipe`](api/common/DatePipe) (llamada `date`) para mostrar la fecha como **04/15/88**.
- El componente `hero-birthday2.component.ts` vincula el parámetro de formato a la propiedad `format` en la sección de `plantilla` y agrega un botón para el evento click vinculado al método `toggleFormat()` del componente.
- El componente `hero-birthday2.component.ts` tiene un método `toggleFormat()` el cual alterna la propiedad `format` del componente entre una forma corta (`'shortDate'`) y una forma larga (`'fullDate'`).

<code-tabs>
  <code-pane
    header="src/app/app.component.html"
    region="format-birthday"
    path="pipes/src/app/app.component.html">
  </code-pane>
  <code-pane
    header="src/app/hero-birthday2.component.ts (template)"
    region="template"
    path="pipes/src/app/hero-birthday2.component.ts">
  </code-pane>
  <code-pane
    header="src/app/hero-birthday2.component.ts (class)"
    region="class"
    path="pipes/src/app/hero-birthday2.component.ts">
  </code-pane>
</code-tabs>

Haciendo click en el botón **Toggle Format** alterna el formato de la fecha entre **04/15/1988** y **Friday, April 15, 1988** como se puede ver en la Figura 1.

<div class="lightbox">
  <img src='generated/images/guide/pipes/date-format-toggle-anim.gif' alt="Date Format Toggle">
</div>

**Figura 1.** Haga click en el botón para alternar entre los formatos de fecha

<div class="alert is-helpful">

Para conocer mas acerca de las opciones de formato del pipe `date`, puede ver [DatePipe](api/common/DatePipe "DatePipe API Reference page").

</div>

### Ejemplo: Aplicando dos formatos con pipes encadenados

Puedes encadenar pipes para que la salida de uno pipe sea la entrada del siguiente.

En el siguiente ejemplo, los pipes encadenados primero aplican un formato al valor de la fecha y luego convierten los caracteres de la fecha a mayúscula.
La primera pestaña para el témplate `src/app/app.component.html` encadena los pipes `DatePipe` y `UpperCasePipe` para mostrar el cumpleaños como **APR 15, 1988**.
La segunda pestaña para el témplate `src/app/app.component.html` se pasa como parámetro `fullDate` al pipe `date` antes de encadenar `uppercase`, lo cual da como resultado **FRIDAY, APRIL 15, 1988**.

<code-tabs>
  <code-pane
    header="src/app/app.component.html (1)"
    region="chained-birthday"
    path="pipes/src/app/app.component.html">
  </code-pane>
  <code-pane
    header="src/app/app.component.html (2)"
    region="chained-parameter-birthday"
    path="pipes/src/app/app.component.html">
  </code-pane>
</code-tabs>

{@a Custom-pipes}

## Creando pipes para realizar transformaciones de datos personalizadas

Puedes crear un pipe personalizado para encapsular una transformación que no este incluida en los pipes del lenguaje.
Puedes usar pipe personalizados en la plantilla de expresión, de la misma manera que usas pipes integrados para transformar los valores de entradas en valores de salida para mostrar.

### Marcando una clase como un pipe

Para marcar una clase como un pipe y proporcionar metadata para configuración, debes aplicar el [decorator](/guide/glossary#decorator "Definición de decorador") [`@Pipe`](/api/core/Pipe "API reference for Pipe") a la clase.
Usa [UpperCamelCase](guide/glossary#case-types "Definición de case types") (la convención general para los nombres de clases) para los nombres de la clase del pipe, y [camelCase](guide/glossary#case-types "Definición de case types") para el string `name` correspondiente.
No use guiones en el `name`.
Para detalles y mas ejemplos, puedes ver [Nombre de los Pipe](guide/styleguide#pipe-names "Nombre de Pipe en Angular guia de estilo de codigo").

Use `name` en la plantilla de expresión como lo harías con un pipe incorporado de Angular.

<div class="alert is-important">

- Incluye tu pipe el campo `declarations` del decorador `NgModule` en orden para que esté disponible para una plantilla. Puedes ver el archivo `app.module.ts` en la aplicación de ejemplo (<live-example></live-example>). Para mas detalles, puedes ver [NgModules](guide/ngmodules "NgModules introduction").
- Registra tu pipe personalizado. El comando [`ng generate pipe`](cli/generate#pipe "ng generate pipe in the CLI Command Reference") de la [CLI de Angular](cli "CLI Overview and Command Reference") registrara tu pipe personalizado automáticamente en tu modulo.

</div>

### Usando la interface PipeTransform

Implemente la interface [`PipeTransform`](/api/core/PipeTransform "API reference for PipeTransform") en la clase de tu pipe personalizado para realizar la transformación.

Angular invoca el método `transform` con el valor de un enlace pasado en el primer argumento, y cualquier parámetro como segundo argumento en forma de lista y devuelve el valor transformado.

### Ejemplo: Transformar un valor exponencialmente

En un juego, es posible que quieras implementar una transformación que eleva un valor exponencialmente para aumentar el poder de un héroe.
Por ejemplo, si la puntuación del héroe es 2, aumentar el poder del héroe exponencialmente en 10 produce una puntuación de 1024.
Puede utilizar un pipe personalizado para esta transformación.

El siguiente ejemplo de código muestra dos definiciones de componentes:

- El componente `exponential-strength.pipe.ts` define un pipe personalizado llamado `exponentialStrength` con el método `transform` que realiza la transformación.
  Esto define un argumento para el método `transform` y un parámetro (`exponent`) para pasar al pipe.

- El componente `power-booster.component.ts` como usar un pipe con el valor especifico (`2`) y un parámetro de exponente (`10`).
  La Figure 2 muestra la salida.

<code-tabs>
  <code-pane
    header="src/app/exponential-strength.pipe.ts"
    path="pipes/src/app/exponential-strength.pipe.ts">
  </code-pane>
  <code-pane
    header="src/app/power-booster.component.ts"
    path="pipes/src/app/power-booster.component.ts">
  </code-pane>
</code-tabs>

<div class="lightbox">
  <img src='generated/images/guide/pipes/power-booster.png' alt="Power Booster">
</div>

**Figura 2.** Salida de el pipe `exponentialStrength`

<div class="alert is-helpful">

Para examinar el comportamiento del pipe `exponentialStrength` en <live-example></live-example>, cambia el valor y el exponente en la plantilla.

</div>

{@a change-detection}

## Detectar cambios con enlaces de información en pipes

Puedes usar [Enlaces de información](/guide/glossary#data-binding "Definition of data Enlace") con un pipe para mostrar valores y responder a acciones de usuarios.
Si la información es un valor de entrada primitivo, por ejemplo `String` o `Number`, una referencia a un objeto como entrada, por ejemplo `Date` o `Array`, Angular ejecuta el pipe cuando detecte un cambio en el valor o la referencia.

Por ejemplo, podría cambiar el pipe personalizado del ejemplo anterior para usar 2 caminos de enlace de información agregando el atributo `ngModel` al input de `amount` y `boost factor`, como se muestra en el siguiente ejemplo de código.

<code-example path="pipes/src/app/power-boost-calculator.component.ts" header="src/app/power-boost-calculator.component.ts">

</code-example>

El pipe `exponentialStrength` se ejecuta cada vez que el usuario cambia el valor de "normal power" o el "boost factor", como se muestra en la Figura 3.

<div class="lightbox">
  <img src='generated/images/guide/pipes/power-boost-calculator-anim.gif' alt="Power Boost Calculator">
</div>

**Figura 3.** Cambiando el amount y boost factor para el pipe `exponentialStrength`

Angular detecta cada cambio y inmediatamente ejecuta el pipe.
Esto esta bien cuando los valores de entrada son primitivos.
Sin embargo, si cambias alguna cosa _dentro_ de un objecto compuesto (por ejemplo el mes de una fecha, un elemento de un array o una propiedad de un objeto), ahí es cuando necesitas entender como funciona la detección de cambios de angular y como se usan los pipe `impuros`.

### Como funciona la detección de cambios

Angular busca cambios en los valores enlazados en un proceso de [detección de cambios](guide/glossary#change-detection "Definition of change detection") que corre luego de cada evento del DOM: cada pulsación de tecla, cada movimiento del mouse, tic del temporizador y respuesta del servidor.
El siguiente ejemplo, que no usa un pipe, demuestra como Angular usa su estrategia de detección de cambios predeterminada para monitorizar y actualizar en la pantalla cada héroe en el array de `heroes`.
Las pestañas del ejemplo muestran lo siguiente:

- En la plantilla `flying-heroes.component.html (v1)`, el repetidor `*ngFor` muestra los nombres de los héroes.
- Y la clase del componente `flying-heroes.component.ts (v1)` provee los héroes, agrega héroes en el array, y restablece el array.

<code-tabs>
  <code-pane
    header="src/app/flying-heroes.component.html (v1)"
    region="template-1"
    path="pipes/src/app/flying-heroes.component.html">
  </code-pane>
  <code-pane
    header="src/app/flying-heroes.component.ts (v1)"
    region="v1"
    path="pipes/src/app/flying-heroes.component.ts">
  </code-pane>
</code-tabs>

Angular actualiza la pantalla cada vez que el usuario agrega un héroe.
Si el usuario hace click en el botón **Reset**, Angular remplaza el array de `heroes` con un nuevo array igual al original y actualiza la pantalla.
Si tu agregas la habilidad de remover o cambiar un héroe, Angular puede detectar estos cambios y actualizar lo que se muestra en la pantalla también.

Sin embargo, ejecutando un pipe para actualizar la pantalla con cada cambio ralentizaría el rendimiento de su aplicación.
Entonces, Angular usa un algoritmo de detección de cambios más rápido para ejecutar un pipe, como se describe en la siguiente sección.

{@a pure-and-impure-pipes}

### Detectar cambios puros en datos primitivos y referencias de objetos.

Por defecto, los pipes están definidos como _puro_ entonces Angular ejecuta el pipe solo cuando detecta un _cambio puro_ en el valor de entrada.
Un cambio puro es un cambio en un valor de entrada primitivo (por ejemplo `String`, `Number`, `Boolean`, o `Symbol`), o cuando cambia una referencia a un objeto (por ejemplo `Date`, `Array`, `Function`, o `Object`).

{@a pure-pipe-pure-fn}

Un pipe puro debe usar una función pura, que es una que procesa la entrada y devuelve valores sin efectos secundarios.
En otras palabras, una función pura dada la misma entrada siempre debe de devolver la misma salida.

Con un pipe puro, Angular ignora los cambios dentro de la composición del objeto, como por ejemplo un elemento recién agregado a un array existente, porque chequear el valor primitivo o la referencia al objeto es mucho más rápido que realizar una verificación profunda de las diferencias dentro de los objetos.
Angular puede determinar rápidamente si puede omitir la ejecución del pipe y actualizar la vista.

Sin embargo, un pipe puro con un array como entrada puede no funcionar como te lo esperas.
Para demostrar este problema, cambia el ejemplo previo para filtrar la lista de héroes solo a héroes que puedan volar.
Se usa el pipe `FlyingHeroesPipe` en un repetidor `*ngFor` para mostrarlos en el siguiente código de ejemplo.
La pestañas del ejemplo, muestran lo siguiente:

- La plantilla (`flying-heroes.component.html (flyers)`) con el nuevo pipe.
- La implementación del pipe personalizado `FlyingHeroesPipe` en (`flying-heroes.pipe.ts`).

<code-tabs>
  <code-pane
    header="src/app/flying-heroes.component.html (flyers)"
    region="template-flying-heroes"
    path="pipes/src/app/flying-heroes.component.html">
  </code-pane>
  <code-pane
    header="src/app/flying-heroes.pipe.ts"
    region="pure"
    path="pipes/src/app/flying-heroes.pipe.ts">
  </code-pane>
</code-tabs>

La aplicación ahora se comporta de forma inesperada: Cuando el usuario agrega un héroe que vuela, ninguno de ellos aparece abajo de "Heroes who fly."
Esto sucede porque el código para agregar héroes lo hace agregándolos a array de `heroes`:

<code-example path="pipes/src/app/flying-heroes.component.ts" region="push" header="src/app/flying-heroes.component.ts"></code-example>

Sin embargo, por defecto el detector de cambios de angular ignora los elementos del array, por lo que el pipe no se ejecuta.

La razón es que Angular ignora los cambios en los elementos del array es que la _referencia_ al array no ha cambiado.
Dado que la referencia no cambio, Angular asume que el array es el mismo y no actualiza la vista.

Un camino para obtener el comportamiento deseado es cambiar la referencia del objeto en si.
Puedes remplazar el array con un nuevo array que contenga los nuevos elementos cambiados y pasarle el nuevo array como parámetro al pipe.
En el ejemplo anterior, tu puedes crear un array con un nuevo héroe agregado y asignar ese array a `heroes`. Angular detecta cambios en la referencia al array y ejecuta el pipe.

Para resumir, si cambias el array de entrada, el pipe pure no se ejecuta.
Si tu _remplazar_ el array de entrada, el pipe se ejecuta y actualiza la pantalla, puedes ver esto en la Figura 4.

<div class="lightbox">
  <img src='generated/images/guide/pipes/flying-heroes-anim.gif' alt="Flying Heroes">
</div>

**Figura 4.** El pipe `flyingHeroes` filtra los héroes que vuelan y los muestra en pantalla.

El ejemplo anterior muestra como cambiar el código de un componente para adaptarse a un pipe.

Para mantener su componente más simple e independiente de la plantilla HTML usa pipes, tu puedes como alternativa usar pipes _impuros_ para detectar cambios en un objeto compuesto como un array de arrays, esto se describe en la siguiente sección.

{@a impure-flying-heroes}

### Detectando cambios impuros dentro de objetos compuestos

Para ejecutar un pipe personalizado luego de un cambio _dentro_ de un objeto compuesto, como un cambio en un elemento de un array, necesitas definir tu pipe como `impure` para así poder detectar cambios impuros.
Angular ejecuta un pipe impuro cada vez que detecta un cambio con cada tecla presionada o movimiento del mouse.

<div class="alert is-important">

Mientras un pipe impuro puede ser muy útil, ten mucho cuidado al usar uno. A largo plazo, usar los pipe impuros podría hacer muchísimo mas lenta tu aplicación.

</div>

Convierte un pipe en un pipe impuro mediante la `configuracion`, colocando el atributo/bandera `pure` en `false`:

<code-example path="pipes/src/app/flying-heroes.pipe.ts" region="pipe-decorator" header="src/app/flying-heroes.pipe.ts"></code-example>

El siguiente código muestra la implementación completa del pipe impuro `FlyingHeroesImpurePipe`, que se extiendo de `FlyingHeroesPipe` y hereda sus características.
El ejemplo muestra como tu no tienes que cambiar cualquier cosa, si no, la única diferencia es establecer la bandera `pure` en `false` en la metadata del pipe.

<code-tabs>
  <code-pane
    header="src/app/flying-heroes.pipe.ts (FlyingHeroesImpurePipe)"
    region="impure"
    path="pipes/src/app/flying-heroes.pipe.ts">
  </code-pane>
  <code-pane
    header="src/app/flying-heroes.pipe.ts (FlyingHeroesPipe)"
    region="pure"
    path="pipes/src/app/flying-heroes.pipe.ts">
  </code-pane>
</code-tabs>

`FlyingHeroesImpurePipe` es un buen candidato para un pipe impuro porque la función `transformacion` es trivial y rápida:

<code-example path="pipes/src/app/flying-heroes.pipe.ts" header="src/app/flying-heroes.pipe.ts (filter)" region="filter"></code-example>

Tu puedes derivar `FlyingHeroesImpureComponent` de `FlyingHeroesComponent`.
Como se muestra en el siguiente código, solo cambia el pipe en la plantilla de cambios.

<code-example path="pipes/src/app/flying-heroes-impure.component.html" header="src/app/flying-heroes-impure.component.html (excerpt)" region="template-flying-heroes"></code-example>

<div class="alert is-helpful">

Para confirmar que la pantalla se actualiza a medida que el usuario agrega héroes, consulte <live-example></live-example>.

</div>

{@a async-pipe}

## Desempaquetar datos de un observable

Los [Observables](/guide/glossary#observable "Definition of observable") te permiten pasar datos entre partes de tu aplicación.
Los Observables son recomendados para el manejo de los eventos, programación asíncrona y manejar múltiples valores.
Los Observables pueden enviar uno o múltiples valores de cualquier tipo, en forma síncrona (como una función entrega valores cuando se llama) o de forma asíncrona programada.

<div class="alert is-helpful">

Para mas detalles y ejemplos de observables, puedes ver [Descripción general de Observables](/guide/observables#using-observables-to-pass-values "Using observables to pass values"").

</div>

Puedes usar el pipe incorporado de Angular [`AsyncPipe`](/api/common/AsyncPipe "API description of AsyncPipe") el cual acepta como entrada un observable y se subscribe a la entrada automáticamente.
Sin esto pipe, su código de componente tendría que subscribirse al observable para consumir sus valores, extraer los valores resueltos, y exponerlos para hacer un enlace en la vista y desuscribirse cuando el observable se destruye para evitar pérdidas de memoria. `AsyncPipe` es un pipe impuro que ahorra código repetitivo
en su componente para mantener la suscripción y seguir entregando valores de los observables a medida que llegan.

El siguiente ejemplo de código enlaza un observable de tipo string
(`message$`) a la vista con el `async` pipe.

<code-example path="pipes/src/app/hero-async-message.component.ts" header="src/app/hero-async-message.component.ts">

</code-example>

{@a no-filter-pipe}

## Almacenando en cache respuestas HTTP

Para [comunicarse con un servicio backend usando peticiones HTTP](/guide/http "Communicating with backend services using HTTP") el servicio `HttpClient` usa observables y ofrece el metodo `HTTPClient.get()` para obtener data desde el servidor.
El método asincrono envía una request HTTP y devuelve un observable que emite la respuesta.

Como se mostro en la sección previa, puedes usar el pipe impuro llamado `AsyncPipe`, el mismo, acepta un observable como entrada y se subscribe automáticamente a el.
Tu también puedes crear tu propio pipe impuro para hacer y cachear una petición HTTP.

Los pipes impuros se llaman siempre que se ejecuta la detección de cambios para un componente, que podría ser cada pocos milisegundos para `CheckAlways`.
Para evitar problemas de performance, debes llamar al servidor solo cuando cambia la URL solicitada, como se muestra en el siguiente ejemplo, el mismo usa el pipe para cachear la respuesta del servidor.
Las pestañas muestra lo siguiente:

- El pipe `fetch` (`fetch-json.pipe.ts`).
- (`hero-list.component.ts`) es un componente harness para demostrar la petición, usando una plantilla que define dos enlaces. El primer enlace en un pipe que pide los desde el archivo `heroes.json`. El segundo enlace encadena el pipe `fetch` con el pipe incorporado `JsonPipe` para mostrar la información de los heroes en formato JSON.

<code-tabs>
  <code-pane
    header="src/app/fetch-json.pipe.ts"
    path="pipes/src/app/fetch-json.pipe.ts">
  </code-pane>
  <code-pane
    header="src/app/hero-list.component.ts"
    path="pipes/src/app/hero-list.component.ts">
  </code-pane>
</code-tabs>

En el ejemplo anterior, un punto de interrupción en la petición de datos del pipe muestra lo siguiente:

- Cada enlace obtiene su propia instancia del pipe.
- Cada instancia del pipe cachea su propia URL y información y llama al servidor una sola vez.

Los pipes `fetch` y `fetch-json` muestran los héroes como puedes ver en la figura 5.

<div class="lightbox">
  <img src='generated/images/guide/pipes/hero-list.png' alt="Hero List">
</div>

**Figura 5.** El pipe `fetch` y `fetch-json` muestran los héroes

<div class="alert is-helpful">

El pipe [JsonPipe](api/common/JsonPipe "API description for JsonPipe") incorporado provee una forma de diagnosticar un fallo en el enlace o de inspeccionar un objeto para un enlace futuro.

</div>
