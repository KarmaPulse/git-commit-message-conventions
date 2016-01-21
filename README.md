# Convenciones para mensajes de commits
Git es una gran herramienta para llevar un control de los cambios realizados en nuestro código a lo largo del tiempo, sin embargo, esto se vuelve una tarea imposible de realizar si en cada repositorio encontramos mensajes de commits como los siguientes:

![combo-de-cambios](/img/combo-de-cambios.png)

![espacios-raros](/img/espacios-raros.png)

![metrics-01](/img/metrics-01.png)

![metrics-02](/img/metrics-02.png)

![metrics-03](/img/metrics-03.png)

![service-auth-01](/img/service-auth-01.png)

Para terminar de una vez por todas con este tipo de prácticas y hacer un uso más correcto de la poderosa herramienta que es git, se han definido una serie de convenciones que deberás aplicar a la hora de redactar un mensaje de commit.

## Tabla de Contenido
* [Objetivos](#objetivos)
* [Log de cambios](#log-de-cambios)
	- [Comandos útiles](#comandos-útiles)
* [Información clara y detallada de los cambios realizados](#información-clara-y-detallada-de-los-cambios-realizados)
* [Formato del mensaje](#formato-del-mensaje)
	- [Primera línea del mensaje type, scope y subject](#primera-línea-del-mensaje-type,-scope-y-subject)
	- [Type](#type)
	- [Scope](#scope)
	- [Subject](#subject)
	- [Inicia el subject con mayúscula](#inicial-el-subject-con-mayúscula)
	- [No termines el subject con un punto](#no-termines-el-subject-con-un-punto)
	- [Usa el modo imperativo en el subject](#usa-el-modo-imperativo-en-el-subject)
* [Body](#body)
	- [Cada linea del body no debe exceder los 72 caracteres](#cada-linea-del-body-no-debe-exceder-los-72-caracteres)
	- [El body debe responder las preguntas ¿qué cambió? y ¿por qué? en vez del ¿cómo cambió?](#el-body-debe-responder-las-preguntas-¿qué-cambió?-y-¿por-qué?-en-vez-del-¿cómo-cambió?)
	- [El body puede ser omitido](#el-body-puede-ser-omitido)
* [Footer](#footer)
* [Tips](#tips)
	- [El mensaje se redacto mal](#el-mensaje-se-redacto-mal)

## Objetivos
Los principales objetivos que se buscan cumplir con la aplicación de estas convenciones son los siguientes:

- Ofrecer información clara y detallada acerca de los cambios realizados
- Poder generar, vía script, un log de cambios (CHANGELOG.md) que agrupe los commits más relevantes de cada versión

## Log de cambios

Lo más probable es que alguna vez te hayas topado, en algún repositorio, con el archivo CHANGELOG.md y si has sido lo suficientemente curioso como para leerlo, te habrás dado cuenta de que este contiene la información de los cambios, correcciones, adiciones y mejoras que contempla la versión liberada del proyecto.

Este tipo de archivos tiene cierta disposición, la cual hace más fácil ubicar dichos cambios y correcciones.

En nuestro caso, el archivo CHANGELOG.md se encuentra compuesto por tres secciones principales: nuevas funcionalidades (new features), correcciones de bugs (bug fixes) y cambios a lógicas previamente establecidas (breaking changes); cambios que se tiene que considerar para no romper nada. Este es generado automáticamente cada vez que se libera una nueva versión (release). Es posible editar el log de cambios una vez generado.

### Comandos útiles
```
git log <last release> HEAD --grep <type>
```
Lista todos los subjects (primera línea del mensaje del commit) agrupados por el tipo de cambios del último release (tag).

*Nota: Se está trabajando en el script para lograr este objetivo*

## Información clara y detallada de los cambios realizados

Como seguramente habrás leído o escuchado alguna vez, “la información es poder” y, en el caso de git, esta es una verdad aplicada, ya que con cada commit que realices, estás brindando el poder (tanto a ti como a los demás) de moverse en cualquier punto del ciclo de desarrollo del proyecto. Esto es algo bastante útil y valioso dado que nos permite regresar sobre nuestros pasos, probar nuevos caminos o simplemente observar la evolución de nuestro desarrollo. Pero para lograr obtener este poder, es necesario que nuestros mensajes de commits estén construidos de tal forma que cada línea redactada nos muestre cada cambio, adición o refactorización realizada.

Esta forma la veremos a lo largo de los siguientes párrafos.

## Formato del mensaje
El formato que debes de usar y respetar para todos los mensajes de commits es el siguiente:

```
<type>(<scope>): <subject>
<línea en blanco>
<body>
<línea en blanco>
<footer>
```

Existen reglas para poder rellenar cada elemento pero, como regla general, tenemos que todo lo que se ponga en el mensaje del commit tiene que estar redactado en **inglés**.

### Primera línea del mensaje type, scope y subject
La primera línea del mensaje contiene información corta y concisa acerca del cambio realizado. Esta línea se encuentra compuesta por tres partes principales:

- Type: Indica el tipo de cambio realizado
- Scope: Indica qué parte del proyecto fue modificada
- Subject: Indica de forma concisa el cambio realizado

Como regla primordial, esta línea no debe rebasar los 100 caracteres, esto con el fin de que sea fácil de leer en github y en la mayoría de clientes GUI para git. Si no te es posible respetar este límite o suele ser una tarea complicada, lo más probable es que estés englobando demasiados cambios en un solo commit, para solucionar esto haz uso de commits atómicos, los cuales tratan, a grandes rasgos, de hacer un commit por cada feature o fix.

#### Type
Como se mencionaba anteriormente, **type** se utiliza para indicar el tipo de cambio realizado. Para poder ubicar y tener un mejor control en los cambios que se realizan sobre los repositorios, se han establecido una serie de etiquetas las cuales engloban los tipos de cambios mas comunes:

- feat: Indica la adición de una nueva funcionalidad
- fix: Indica la corrección de un bug
- docs: Indica la adición de documentación
- style: Indica correcciones en la indentación, eliminación o adición de espacios, etc.
- refactor: Indica la refactorización de una lógica o función
- test: Indica la adición de un test faltante
- chore: Indica mantenimiento del código

Estos son los únicos valores aceptados en **type**.

#### Scope
El **scope** indica qué sección, funcionalidad o lógica del proyecto se ha modificado. Dado que cada proyecto puede variar bastante uno del otro, asignar este valor se puede tornar un poco complicado, es por esto que se recomienda siempre tener en mente contestar la pregunta **¿qué parte cambio?**, para poder asignar este valor.

#### Subject
En el **subject** se describe de la manera más clara y concisa posible qué fue lo que se modificó. Podemos considerar al subject como una de las partes más importantes del mensaje, por esa razón, además de pensar bastante bien lo que vamos a escribir, es necesario seguir las siguientes reglas.

##### Inicia el subject con mayúscula
Esto es tan simple como suena. Inicia la parte del subject con mayúscula.

*Correcto*
```
feat(clients): Add CRUD client
```

*Incorrecto*
```
feat(clients): add CRUD client
```

##### No termines el subject con un punto
Las reglas de puntuación son innecesarias en el subject, más cuando tienes un límite de 100 caracteres.

*Correcto*
```
fix(clients): Fix update client
```

*Incorrecto*
```
fix(clients): Fix update client.
```

##### Usa el modo imperativo en el subject

Escribir en forma imperativa significa hablar o escribir como si se estuviera dando una orden o comando. Por ejemplo:

- Clean your room
- Close the door
- Take out the trash

Cada una de las reglas aplicadas al subject están escritas en forma imperativa (ej. no termines el subject con un punto).

El modo imperativo puede sonar un poco rudo, es por eso que casi no lo usamos al hablar, pero es excelente para los subjects de commits. Una de esto es que el mismo git utiliza el modo imperativo cuando crea un commit.

Por ejemplo, el mensaje que usa git por defecto para un merge es:
```
Merge branch 'myfeature'
```

Y cuando hacemos un git revert
```
Revert "Add the thing with the stuff"

This reverts commit cc87791524aedd593cff5a74532befe7ab69ce9d.
```

O cuando hacemos click en el botón “Merge” de GitHub para hacer un pull request:
```
Merge pull request #123 from someuser/somebranch
```

Por esta razón, al escribir los subjects en forma imperativa, estamos siguiendo las convenciones internas de git. Por ejemplo:

- Refactor subsystem X for readability
- Update getting started documentation
- Remove deprecated methods
- Release version 1.0.0

Esto puede resultar algo raro al principio ya que estamos acostumbrados a hablar en forma indicativa, la cual utilizamos para reportar hechos. Es por eso que los subjects terminan viéndose de esta forma:

- Fixed bug with Y
- Changing behavior of X

Y aveces los subjects terminan siendo descripciones de lo que contiene el commit:

- More fixes for broken stuff
- Sweet new API methods

Es por eso que para evitar cualquier confusión, podemos seguir la siguiente regla a la hora de definir nuestro subject.

**Un subject apropiado siempre debe de poder completar la siguiente sentencia:**

If applied, this commit will *inserte subject aquí*

Por Ejemplo:

- If applied, this commit will *refactor subsystem X for readability*
- If applied, this commit will *update getting started documentation*
- If applied, this commit will *remove deprecated methods*
- If applied, this commit will *release version 1.0.0*
- If applied, this commit will *merge pull request #123 from user/branch*

En cambio, si no usamos la forma imperativa, obtenemos algo como esto:

- If applied, this commit will *fixed bug with Y*
- If applied, this commit will *changing behavior of X*
- If applied, this commit will *more fixes for broken stuff*
- If applied, this commit will *sweet new API methods*

Por ultimo, cabe señalar que el modo imperativo se utiliza solo para el subject del mensaje, para todo lo demás es posible omitir esta restricción.

## Body

En el **body** encontramos una descripción extensa y detalla del cambio realizado. Esta sección se encuentra separada del **subject ** por medio de un salto de línea, la separación es muy importante ya que delimita el texto que aparece cuando hacemos uso del comando git log. Aquí solo es necesario seguir las siguientes reglas.

### Cada linea del body no debe exceder los 72 caracteres

Git no ajusta el texto automáticamente. Al escribir el **body** del commit, debes tener en mente la correcta alineación y ajustar el texto manualmente.

La recomendado aquí es no sobrepasar los 72 caracteres por linea, con esto git tiene el espacio suficiente para sangrar el texto siempre y cuando éste se mantenga por debajo de los 80 caracteres.

Un buen editor puede ayudar en esta tarea, mi recomendación es configurar sublimetext para redactar los commits o configurar VIM para que rompa el texto a los 72 caracteres cuando se escriba un commit.

### El body debe responder las preguntas ¿qué cambió? y ¿por qué? en vez del ¿cómo cambió?

El siguiente commit es una gran ejemplo de como se responden las preguntas ¿qué cambió? y ¿por qué?

```
commit eb0b56b19017ab5c16c745e6da39c53126924ed6
Author: Pieter Wuille <pieter.wuille@gmail.com>
Date:   Fri Aug 1 22:57:55 2014 +0200

   Simplify serialize.h's exception handling

   Remove the 'state' and 'exceptmask' from serialize.h's stream
   implementations, as well as related methods.

   As exceptmask always included 'failbit', and setstate was always
   called with bits = failbit, all it did was immediately raise an
   exception. Get rid of those variables, and replace the setstate
   with direct exception throwing (which also removes some dead
   code).

   As a result, good() is never reached after a failure (there are
   only 2 calls, one of which is in tests), and can just be replaced
   by !eof().

   fail(), clear(n) and exceptions() are just never called. Delete
   them.
```

Observemos la forma y nivel de detalle con el que está escrito este **body** y pensemos en todo el tiempo que el autor le ha ahorrado a sus compañeros (o a él mismo) al tomarse el tiempo de escribir sobre los cambios que realizó. De no haberlo hecho, seguramente esta información se hubieran perdido a través del tiempo.

Generalmente el código es autoexplicativo (aunque si el código es demasiado complejo, es necesario hacer uso de comentarios con el afán de explicar los detalles que no se ven a primera vista) por lo que en la mayoría de los casos es posible omitir detalles acerca de los cambios realizados. Por tal motivo es necesario que sólo te centres en dejar claro el por qué decidiste hacer el cambio en primer lugar, la manera en que las cosas funcionaban antes del cambio (y qué es lo que estaba mal con eso), la manera en la que funciona ahora y por qué decidiste resolverlo de la manera en que lo resolviste.

La persona encargada del mantenimiento y/o tu yo del futuro te lo agradecerán.

### El body puede ser omitido

Existen ocaciones las que no será necesario agregar el body. Éstas se pueden dar porque los cambios, adiciones o refactorizaciónes realizadas son tan pequeñas o sencillas que la primera línea del mensaje es más que suficiente para indicar qué es lo que sucedió, si te encuentras en una situación como esta, siéntete libre de omitir el body.

## Footer

Como última sección tenemos al footer. Aquí se deben indicar todos aquellos cambios críticos realizados y que pueden romper cosas, así como la forma en la que se deben realizar las migraciones correspondientes. Esta sección, al igual que el body, debe respetar la regla de los 72 caracteres, puede ser omitida y debe estar precedida de la palabra **BREAKING CHANGE:** como se muestra en el siguiente ejemplo.

```
BREAKING CHANGE: isolate scope bindings definition has changed and
    the inject option for the directive controller injection was removed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
      myBind: 'bind',
      myExpression: 'expression',
      myEval: 'evaluate',
      myAccessor: 'accessor'
    }

    After:

    scope: {
      myAttr: '@',
      myBind: '@',
      myExpression: '&',
      // myEval - usually not useful, but in cases where the expression is assignable, you can use '='
      myAccessor: '=' // in directive's template change myAccessor() to myAccessor
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

## Tips

Finalmente te dejo algunos tips relacionados con git.

### El mensaje se redacto mal

Para cuando redactemos mal un mensaje y ya hayamos hecho el commit https://help.github.com/articles/changing-a-commit-message/
