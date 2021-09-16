# Embarque

This document is an outline of the things we tell new Collaborators at their onboarding session.

## Una semana antes de la sesión de incorporación

* If the new Collaborator is not yet a member of the nodejs GitHub organization, confirm that they are using [two-factor authentication][]. It will not be possible to add them to the organization if they are not using two-factor authentication. If they cannot receive SMS messages from GitHub, try [using a TOTP mobile app][].
* Announce the accepted nomination in a TSC meeting and in the TSC mailing list.
* Suggest the new Collaborator install [`node-core-utils`][] and [set up the credentials][] for it.

## Dieciocho minutos antes de la sesión de incorporación

* Prior to the onboarding session, add the new Collaborator to [the Collaborators team](https://github.com/orgs/nodejs/teams/collaborators).
* Pregunten si quieren unirse a algún equipo de subsistema. See [Who to CC in the issue tracker][who-to-cc].

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
  * Membership: Consider making your membership in the Node.js GitHub organization public. Esto facilita la identificación de Colaboradores. Instructions on how to do that are available at [Publicizing or hiding organization membership][].

* Notificaciones:
  * Use [https://github.com/notifications](https://github.com/notifications) or set up email
  * Watching the main repo will flood your inbox (several hundred notifications on typical weekdays), so be prepared

El proyecto tiene dos espacios para la discusión en tiempo real:
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) on the [OpenJS Foundation](https://slack-invite.openjsf.org/)
* `#node-dev` on [webchat.freenode.net](https://webchat.freenode.net/) is a great place to interact with the TSC and other Collaborators
  * If there are any questions after the session, a good place to ask is there!
  * Presence is not mandatory, but please drop a note there if force-pushing to `master`

## Objetivos & valores del proyecto

* Los colaboradores son los propietarios colectivos del proyecto
  * El proyecto tiene los objetivos de sus colaboradores

* Hay algunos objetivos y valores de más alto nivel
  * La empatía hacia los usuarios importa (esta es en parte la razón por la que abordamos a las personas)
  * Generalmente: ¡trate de ser agradable con la gente!
  * The best outcome is for people who come to our issue tracker to feel like they can come back again.

* You are expected to follow *and* hold others accountable to the [Code of Conduct][].

## Gestión del rastreador de incidencias

* You have (mostly) free rein; don't hesitate to close an issue if you are confident that it should be closed
  * ¡Sé bueno acerca de cerrar problemas! Let people know why, and that issues and PRs can be reopened if necessary

* [**Ver "Etiquetas"**](./doc/guides/onboarding-extras.md#labels)
  * There is [a bot](https://github.com/nodejs-github-bot/github-bot) that applies subsystem labels (for example, `doc`, `test`, `assert`, or `buffer`) so that we know what parts of the code base the pull request modifies. It is not perfect, of course. Feel free to apply relevant labels and remove irrelevant labels from pull requests and issues.
  * `semver-{minor,major}`:
    * If a change has the remote *chance* of breaking something, use the `semver-major` label
    * When adding a `semver-*` label, add a comment explaining why you're adding it. ¡Hazlo de inmediato para que no lo olvides!
  * Por favor, añade la etiqueta [`lista de autor`][] para PRs, si es aplicable.

* Véase [Quién a CC en el gestor de incidencias][who-to-cc].
  * Esto ocurrirá de forma más natural con el tiempo
  * For many of the teams listed there, you can ask to be added if you are interested
    * Some are WGs with some process around adding people, others are only there for notifications

* When a discussion gets heated, you can request that other Collaborators keep an eye on it by opening an issue at the private [nodejs/moderation](https://github.com/nodejs/moderation) repository.
  * This is a repository to which all members of the `nodejs` GitHub organization (not just Collaborators on Node.js core) have access. Its contents should not be shared externally.
  * You can find the full moderation policy [here](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Revisando PRs

* El objetivo principal es que el código base mejore.
* Secundario (pero no muy lejos) es que la persona que envía el código tenga éxito. A pull request from a new contributor is an opportunity to grow the community.
* Revisar un poco a la vez. No mencione nuevos colaboradores.
  * Es tentado para microoptimizar. No sucumbir a esa tumba. We change V8 often. Techniques that provide improved performance today may be unnecessary in the future.
* Ten en cuenta: ¡Tu opinión tiene mucho peso!
* Nits (requests for small changes that are not essential) are fine, but try to avoid stalling the pull request.
  * Identifícalos como nits cuando comentes: `Nit: cambiar foo() a bar().`
  * Si están parando la solicitud de extracción, pégalos tú mismo en la fusión.
* Insofar as possible, issues should be identified by tools rather than human reviewers. If you are leaving comments about issues that could be identified by tools but are not, consider implementing the necessary tooling.
* Tiempo mínimo de espera de los comentarios
  * There is a minimum waiting time which we try to respect for non-trivial changes so that people who may have important input in such a distributed project are able to respond.
  * Para cambios no triviales, deje el pull request abierto por al menos 48 horas.
  * If a pull request is abandoned, check if they'd mind if you took it over (especially if it just has nits left).
* Aprobando un cambio
  * Collaborators indicate that they have reviewed and approve of the changes in a pull request using GitHub’s approval interface
  * A algunas personas les gusta comentar `LGTM` ("Me parece bien")
  * Usted tiene la autoridad para aprobar cualquier otro trabajo de colaborador.
  * No puedes aprobar tus propias solicitudes de extracción.
  * When explicitly using `Changes requested`, show empathy – comments will usually be addressed even if you don’t use it.
    * If you do, it is nice if you are available later to check whether your comments have been addressed
    * If you see that the requested changes have been made, you can clear another collaborator's `Changes requested` review.
    * Use `Changes requested` to indicate that you are considering some of your comments to block the PR from landing.

* Lo que pertenece a Node.js:
  * Las opiniones varían – ¡es bueno tener una amplia base de colaboradores por esa razón!
  * If Node.js itself needs it (due to historical reasons), then it belongs in Node.js.
    * That is to say, `url` is there because of `http`, `freelist` is there because of `http`, etc.
  * Things that cannot be done outside of core, or only with significant pain such as `async_hooks`.

* Prueba de Integración Continua (CI):
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * No se ejecuta automáticamente. Necesitas iniciarlo manualmente.
  * Iniciar sesión en CI está integrado con GitHub. ¡Intenta iniciar sesión ahora!
  * Usará `node-test-pull-request` la mayoría de las veces. ¡Ve allí!
    * Considere marcado: <https://ci.nodejs.org/job/node-test-pull-request/>
  * Para acceder al formulario para iniciar un trabajo, haz clic en `Construir con parámetros`. (If you don't see it, that probably means you are not logged in!) Click it now! ¡Haz clic ahora!
  * To start CI testing from this screen, you need to fill in two elements on the form:
    * La casilla `CERTIFY_SAFE` debe estar marcada. By checking it, you are indicating that you have reviewed the code you are about to test and you are confident that it does not contain any malicious code. (We don't want people hijacking our CI hosts to attack other hosts on the internet, for example!)
    * The `PR_ID` box should be filled in with the number identifying the pull request containing the code you wish to test. For example, if the URL for the pull request is `https://github.com/nodejs/node/issues/7006`, then put `7006` in the `PR_ID`.
    * Los elementos restantes en el formulario son típicamente sin cambios.
  * Si necesita ayuda con algo relacionado con CI:
    * Usa #node-dev (IRC) para hablar con otros Colaboradores.
    * Use #node-build (IRC) to talk to the Build WG members who maintain the CI infrastructure.
    * Use the [Build WG repo](https://github.com/nodejs/build) to file issues for the Build WG members who maintain the CI infrastructure.

## PRs terrenos

Consulte la Guía del Colaborador: [Solicitudes de tierra][].

Commits in one PR that belong to one logical change should be squashed. It is rarely the case in onboarding exercises, so this needs to be pointed out separately during the onboarding.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Ejercicio: Haz un PR añadiéndote al README

* Example: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * For raw commit message: `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* Los colaboradores están en orden alfabético por el nombre de usuario de GitHub.
* Opcionalmente, incluye tus pronombres personales.
* Add the `Fixes: <collaborator-nomination-issue-url>` to the commit message so that when the commit lands, the nomination issue url will be automatically closed.
* Label your pull request with the `doc`, `notable-change`, and `fast-track` labels.
* Ejecute CI en el PR. Utilice la tarea de `node-test-pull-request` CI.
* After two Collaborator approvals for the change and two Collaborator approvals for fast-tracking, land the PR.
* Deja un comentario en la PR: `Por favor :thumbnail _up: este comentario para aprobar un rápido seguimiento`.
* If there are not enough approvals within a reasonable time, consider the single approval of the onboarding TSC member sufficient, and land the PR.
  * Be sure to add the `PR-URL: <full-pr-url>` and appropriate `Reviewed-By:` metadata.
  * [`node-core-utils`][] automates the generation of metadata and the landing process. Vea la documentación de [`git-node`][].
  * [`core-validate-commit`][] automatiza la validación de mensajes de commit. This will be run during `git node land --final` of the [`git-node`][] command.

## Notas finales

* Don't worry about making mistakes: everybody makes them, there's a lot to internalize and that takes time (and we recognize that!)
* Casi cualquier error que pueda cometer puede ser corregido o revertido.
* Los colaboradores existentes confían en usted y están agradecidos por su ayuda!
* Otros repositorios:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* The OpenJS Foundation hosts regular summits for active contributors to the Node.js project, where we have face-to-face discussions about our work on the project. The Foundation has travel funds to cover participants' expenses including accommodations, transportation, visa fees, etc. if needed. Check out the [summit](https://github.com/nodejs/summit) repository for details.

[Code of Conduct]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Solicitudes de tierra]: doc/guides/collaborator-guide.md#landing-pull-requests
[Publicizing or hiding organization membership]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`lista de autor`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[set up the credentials]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[two-factor authentication]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[using a TOTP mobile app]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
