# Embarque

Este documento es un resumen de las cosas que le decimos a los nuevos Colaboradores en su sesión de incorporación.

## Una semana antes de la sesión de incorporación

* Si el nuevo colaborador aún no es miembro de la organización GitHub de los nodejs, confirme que están usando [autenticación de dos factores][]. No será posible añadirlos a la organización si no utilizan la autenticación de dos factores. Si no pueden recibir mensajes SMS de GitHub, pruebe [usando una aplicación móvil TOTP][]. No será posible añadirlos a la organización si no utilizan la autenticación de dos factores. Si no pueden recibir mensajes SMS de GitHub, pruebe [usando una aplicación móvil TOTP][].
* Anunciar la nominación aceptada en una reunión del TSC y en la lista de correo del TSC.
* Sugerir al nuevo colaborador instalar [`node-core-utils`][] y [configurar las credenciales][] para ello.

## Dieciocho minutos antes de la sesión de incorporación

* Antes de la sesión de incorporación, agregue el nuevo colaborador a [el equipo de colaboradores](https://github.com/orgs/nodejs/teams/collaborators).
* Pregunten si quieren unirse a algún equipo de subsistema. Pregunten si quieren unirse a algún equipo de subsistema. Véase [Quién a CC en el gestor de incidencias][who-to-cc].

## Sesión de embarque

* Esta sesión cubrirá:
  * [configuración local](#local-setup)
  * [objetivos & valores del proyecto](#project-goals--values)
  * [gestionar el gestor de incidencias](#managing-the-issue-tracker)
  * [revisando PRs](#reviewing-prs)
  * [aterrizando PRs](#landing-prs)

## Configuración local

* git:
  * Asegúrese de que tiene espacio en blanco=corregir: `git config --global --add
apply.whitespace fix`
  * Continuar siempre a PR desde tu propia bifurcación de GitHub
    * Las ramas en el repositorio `nodejs/node` son sólo para las líneas de lanzamiento
  * Agregue el repositorio de nodejs canónicos como mando `principal`:
    * `git remote add upstream git://github.com/nodejs/node.git`
  * Para actualizar desde `upstream`:
    * `git checkout master`
    * `git remote update -p` O `git fetch --all`
    * `git merge --ff-only upstream/master` (o `REMOTENAME/BRANCH`)
  * Crea una nueva rama para cada RP que envíes.
  * Membresía: Considere hacer pública su membresía en la organización GitHub de Node.js. Esto facilita la identificación de Colaboradores. Las instrucciones sobre cómo hacerlo están disponibles en [Publicar u ocultar la membresía de la organización][]. Esto facilita la identificación de Colaboradores. Las instrucciones sobre cómo hacerlo están disponibles en [Publicar u ocultar la membresía de la organización][].

* Notificaciones:
  * Utilice [https://github.com/notifications](https://github.com/notifications) o configure el correo electrónico
  * Ver el repositorio principal inundará tu bandeja de entrada (varios cientos de notificaciones en días de semana típicos), así que prepárate

El proyecto tiene dos espacios para la discusión en tiempo real:
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) en la [Fundación OpenJS](https://slack-invite.openjsf.org/)
* `#node-dev` en [webchat.freenode.net](https://webchat.freenode.net/) es un buen lugar para interactuar con el TSC y otros Colaboradores
  * Si hay alguna pregunta después de la sesión, hay un buen lugar para hacerla!
  * La presencia no es obligatoria, pero por favor deja una nota allí si presiona por la fuerza a `maestro`

## Objetivos & valores del proyecto

* Los colaboradores son los propietarios colectivos del proyecto
  * El proyecto tiene los objetivos de sus colaboradores

* Hay algunos objetivos y valores de más alto nivel
  * La empatía hacia los usuarios importa (esta es en parte la razón por la que abordamos a las personas)
  * Generalmente: ¡trate de ser agradable con la gente!
  * El mejor resultado es que las personas que acuden a nuestro gestor de problemas sientan que pueden volver de nuevo.

* Se espera que siga *y* responsabilice a otros ante el [Código de Conducta][].

## Gestión del rastreador de incidencias

* Tienes (mayormente) reposo libre; no dudes en cerrar un problema si estás seguro de que debería cerrarse
  * ¡Sé bueno acerca de cerrar problemas! ¡Sé bueno acerca de cerrar problemas! Dile a la gente por qué, y que los temas y PRs pueden ser reabiertos si es necesario

* [**Ver "Etiquetas"**](./doc/guides/onboarding-extras.md#labels)
  * Hay [un bot](https://github.com/nodejs-github-bot/github-bot) que aplica etiquetas de subsistema (por ejemplo, `doc`, `test`, `assert`, o `buffer`) para que sepamos qué partes del código base modifica la pull request. Por supuesto, no es perfecto. Siéntase libre de aplicar etiquetas relevantes y eliminar etiquetas irrelevantes de solicitudes de extracción y problemas. Por supuesto, no es perfecto. Siéntase libre de aplicar etiquetas relevantes y eliminar etiquetas irrelevantes de solicitudes de extracción y problemas.
  * `semver-{minor,major}`:
    * Si un cambio tiene la *posibilidad* remota de romper algo, usa la etiqueta `semver-major`
    * Al añadir una etiqueta `semver-*` , añade un comentario explicando por qué la estás añadiendo. ¡Hazlo de inmediato para que no lo olvides! ¡Hazlo de inmediato para que no lo olvides!
  * Por favor, añade la etiqueta [`lista de autor`][] para PRs, si es aplicable.

* Véase [Quién a CC en el gestor de incidencias][who-to-cc].
  * Esto ocurrirá de forma más natural con el tiempo
  * Para muchos de los equipos listados allí, puedes solicitar ser añadido si estás interesado
    * Algunos son WGs con algún proceso alrededor de añadir personas, otros sólo están ahí para las notificaciones

* Cuando una discusión se calienta, puede solicitar que otros Colaboradores lo vigilen abriendo un problema en el repositorio privado [nodejs/moderation](https://github.com/nodejs/moderation).
  * Este es un repositorio al que todos los miembros de la organización `nodejs` GitHub (no solo Colaboradores en el núcleo Node.js) tienen acceso. Su contenido no debe compartirse externamente. Su contenido no debe compartirse externamente.
  * Puedes encontrar la política de moderación completa [aquí](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Revisando PRs

* El objetivo principal es que el código base mejore.
* Secundario (pero no muy lejos) es que la persona que envía el código tenga éxito. Un pull request de un nuevo colaborador es una oportunidad para hacer crecer la comunidad. Un pull request de un nuevo colaborador es una oportunidad para hacer crecer la comunidad.
* Revisar un poco a la vez. Revisar un poco a la vez. No mencione nuevos colaboradores.
  * Es tentado para microoptimizar. No sucumbir a esa tumba. Cambiamos el V8 a menudo. Las técnicas que proporcionan un mejor desempeño hoy en día pueden ser innecesarias en el futuro.
* Ten en cuenta: ¡Tu opinión tiene mucho peso!
* Las nits (peticiones de pequeños cambios que no son esenciales) están bien, pero tratan de evitar paralizar la pull request.
  * Identifícalos como nits cuando comentes: `Nit: cambiar foo() a bar().`
  * Si están parando la solicitud de extracción, pégalos tú mismo en la fusión.
* En la medida de lo posible, las cuestiones deberían identificarse mediante herramientas y no mediante revisores humanos. En la medida de lo posible, las cuestiones deberían identificarse mediante herramientas y no mediante revisores humanos. Si deja comentarios sobre temas que podrían ser identificados por herramientas pero no lo son, considere implementar las herramientas necesarias.
* Tiempo mínimo de espera de los comentarios
  * Hay un tiempo de espera mínimo que intentamos respetar por los cambios no triviales para que las personas que puedan tener una aportación importante en un proyecto tan distribuido puedan responder.
  * Para cambios no triviales, deje el pull request abierto por al menos 48 horas.
  * Si un pull request es abandonado, compruebe si le importaría tomarlo (especialmente si tiene nits restantes).
* Aprobando un cambio
  * Los colaboradores indican que han revisado y aprobado los cambios en una solicitud de extracción usando la interfaz de aprobación de GitHub
  * A algunas personas les gusta comentar `LGTM` ("Me parece bien")
  * Usted tiene la autoridad para aprobar cualquier otro trabajo de colaborador.
  * No puedes aprobar tus propias solicitudes de extracción.
  * Al usar explícitamente `Cambios solicitados`, muestre empatía – los comentarios generalmente serán tratados incluso si no los utiliza.
    * Si lo hace, es bueno que esté disponible más tarde para comprobar si se han abordado sus comentarios
    * Si ves que se han realizado los cambios solicitados, puedes borrar la revisión de `Cambios solicitados` de otro colaborador.
    * Usa `Cambios solicitados` para indicar que estás considerando algunos de tus comentarios para bloquear el aterrizaje de PR.

* Lo que pertenece a Node.js:
  * Las opiniones varían – ¡es bueno tener una amplia base de colaboradores por esa razón!
  * Si Node.js mismo lo necesita (debido a razones históricas), entonces pertenece a Node.js.
    * Es decir, `url` está ahí debido a `http`, `freelist` está ahí debido a `http`, etc.
  * Cosas que no pueden hacerse fuera del núcleo, o solo con dolor significativo como `async_hooks`.

* Prueba de Integración Continua (CI):
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * No se ejecuta automáticamente. Necesitas iniciarlo manualmente. Necesitas iniciarlo manualmente.
  * Iniciar sesión en CI está integrado con GitHub. ¡Intenta iniciar sesión ahora! ¡Intenta iniciar sesión ahora!
  * Usará `node-test-pull-request` la mayoría de las veces. ¡Ve allí! ¡Ve allí!
    * Considere marcado: <https://ci.nodejs.org/job/node-test-pull-request/>
  * Para acceder al formulario para iniciar un trabajo, haz clic en `Construir con parámetros`. (Si no lo ves probablemente significa que no has iniciado sesión!) ¡Haz clic ahora! (Si no lo ves probablemente significa que no has iniciado sesión!) ¡Haz clic ahora!
  * Para iniciar la prueba de CI desde esta pantalla, necesita rellenar dos elementos en el formulario:
    * La casilla `CERTIFY_SAFE` debe estar marcada. Comprobándolo, indica que ha revisado el código que está a punto de probar y confía en que no contenga ningún código malicioso. (¡No queremos que la gente secuestre a nuestros hosts CI para atacar a otros hosts en Internet, por ejemplo!) Comprobándolo, indica que ha revisado el código que está a punto de probar y confía en que no contenga ningún código malicioso. (¡No queremos que la gente secuestre a nuestros hosts CI para atacar a otros hosts en Internet, por ejemplo!)
    * El recuadro `PR_ID` debe ser rellenado con el número que identifica el pull request que contiene el código que desea probar. El recuadro `PR_ID` debe ser rellenado con el número que identifica el pull request que contiene el código que desea probar. Por ejemplo, si la URL de la pull request es `https://github.com/nodejs/node/issues/7006`, entonces pon `7006` en el `PR_ID`.
    * Los elementos restantes en el formulario son típicamente sin cambios.
  * Si necesita ayuda con algo relacionado con CI:
    * Usa #node-dev (IRC) para hablar con otros Colaboradores.
    * Usa #node-build (IRC) para hablar con los miembros de Build WG que mantienen la infraestructura de CI.
    * Utilice el repositorio de [Construir WG](https://github.com/nodejs/build) para archivar problemas para los miembros de Build WG que mantienen la infraestructura de CI.

## PRs terrenos

Consulte la Guía del Colaborador: [Solicitudes de tierra][].

Los compromisos en una RP que pertenecen a un cambio lógico deben ser aplastados. Rara vez es el caso en los ejercicios de embarque, por lo que hay que señalar esto por separado durante la incorporación. Rara vez es el caso en los ejercicios de embarque, por lo que hay que señalar esto por separado durante la incorporación.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Ejercicio: Haz un PR añadiéndote al README

* Ejemplo: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * Para mensaje de commit crudo: `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* Los colaboradores están en orden alfabético por el nombre de usuario de GitHub.
* Opcionalmente, incluye tus pronombres personales.
* Agregue las `Soluciones: <collaborator-nomination-issue-url>` al mensaje de commit para que cuando el commit falle, la url del problema de nominación se cierre automáticamente.
* Etiqueta tu pull request con las etiquetas `doc`, `notable-change`y `fast track`.
* Ejecute CI en el PR. Ejecute CI en el PR. Utilice la tarea de `node-test-pull-request` CI.
* Después de dos aprobaciones de Colaborador para el cambio y dos aprobaciones de Colaborador para el seguimiento rápido, aterriza el PR.
* Deja un comentario en la PR: `Por favor :thumbnail _up: este comentario para aprobar un rápido seguimiento`.
* Si no hay suficientes aprobaciones dentro de un plazo razonable, considere suficiente la aprobación única del miembro del TSC de embarque y desembarque el PR.
  * Asegúrate de añadir la `PR-URL: <full-pr-url>` y los `revisados por:` metadatos.
  * [`node-core-utils`][] automatiza la generación de metadatos y el proceso de aterrizaje. Vea la documentación de [`git-node`][]. Vea la documentación de [`git-node`][].
  * [`core-validate-commit`][] automatiza la validación de mensajes de commit. Esto se ejecutará durante `git node land --final` del comando [`git-node`][]. Esto se ejecutará durante `git node land --final` del comando [`git-node`][].

## Notas finales

* No te preocupes por cometer errores: todo el mundo los comete, hay mucho que internalizar y eso lleva tiempo (¡y lo reconocemos!)
* Casi cualquier error que pueda cometer puede ser corregido o revertido.
* Los colaboradores existentes confían en usted y están agradecidos por su ayuda!
* Otros repositorios:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* La Fundación OpenJS acoge cumbres regulares para colaboradores activos del proyecto Node.js, donde tenemos discusiones cara a cara sobre nuestro trabajo en el proyecto. La Fundación cuenta con fondos de viajes para cubrir los gastos de los participantes incluyendo alojamiento, transporte, tasas de visado, etc. si es necesario. Echa un vistazo al repositorio de [Summit](https://github.com/nodejs/summit) para más detalles. La Fundación cuenta con fondos de viajes para cubrir los gastos de los participantes incluyendo alojamiento, transporte, tasas de visado, etc. si es necesario. Echa un vistazo al repositorio de [Summit](https://github.com/nodejs/summit) para más detalles.

[Código de Conducta]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Solicitudes de tierra]: doc/guides/collaborator-guide.md#landing-pull-requests
[Publicar u ocultar la membresía de la organización]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`lista de autor`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[configurar las credenciales]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[autenticación de dos factores]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[usando una aplicación móvil TOTP]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
