# Gobernanza del Proyecto Node.js

<!-- TOC -->

* [Triagers](#triagers)
* [Colaboradores](#collaborators)
  * [Actividades de colaborador](#collaborator-activities)
* [Comité Directivo Técnico](#technical-steering-committee)
  * [Reuniones TSC](#tsc-meetings)
* [Nominaciones de colaborador](#collaborator-nominations)
  * [Embarque](#onboarding)
* [Proceso de búsqueda de consenso](#consensus-seeking-process)

<!-- /TOC -->

## Triagers

Triagers assess newly-opened issues in the nodejs/node and nodejs/help repositories. No hay ningún equipo de GitHub para triagers en este momento.

Los triagers tienen:
* capacidad para etiquetar problemas
* capacidad para comentar, cerrar y reabrir peticiones

Ver:

* [Una guía para triagers](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Colaboradores

Los colaboradores principales de Node.js mantienen el repositorio [nodejs/node][] de GitHub. El equipo de GitHub para Colaboradores de Node.js es @nodejs/colaboradores. Los colaboradores tienen:

* Acceso al repositorio [nodejs/node][]
* Acceso a los trabajos de integración continua (CI) de Node.js

Both Collaborators and non-Collaborators may propose changes to the Node.js source code. El mecanismo para proponer tal cambio es una solicitud de GitHub. Los colaboradores revisan y fusionan (_tierra_) solicitudes de extracción.

Dos Colaboradores deben aprobar una pull request antes de que la pull request pueda aterrizar. (One Collaborator approval is enough if the pull request has been open for more than 7 days.) Approving a pull request indicates that the Collaborator accepts responsibility for the change. Aprobar una pull request indica que el Colaborador acepta la responsabilidad por el cambio. Approval must be from Collaborators who are not authors of the change.

Si un colaborador se opone a un cambio propuesto, entonces el cambio no puede aterrizar. The exception is if the TSC votes to approve the change despite the opposition. Por lo general, implicar al TSC es innecesario. Often, discussions or further changes result in Collaborators removing their opposition.

Ver:

* [Lista de colaboradores](./README.md#current-project-team-members)
* [Una guía para colaboradores](./doc/guides/collaborator-guide.md)

### Actividades de colaborador

* Ayudando usuarios y colaboradores novatos
* Contribuir con cambios de código y documentación que mejoran el proyecto
* Revisando y comentando asuntos y pull requests
* Participación en grupos de trabajo
* Combinando pull requests

The TSC can remove inactive Collaborators or provide them with _Emeritus_ status. Emeriti puede solicitar que el TSC los restaure al estado activo.

## Comité Directivo Técnico

Un subconjunto de los Colaboradores forma el Comité Directivo Técnico (TSC). El TSC tiene autoridad final sobre este proyecto, incluyendo:

* Dirección técnica
* Gobernanza y proceso del proyecto (incluyendo esta política)
* Política de contribución
* GitHub repository hosting
* Directrices de conducta
* Manteniendo la lista de colaboradores

The current list of TSC members is in [the project README](./README.md#current-project-team-members).

La Carta del TSC [][] gobierna las operaciones del TSC. All changes to the Charter need approval by the OpenJS Foundation Cross-Project Council (CPC).

### Reuniones TSC

El TSC se reúne en una llamada de conferencia de voz. Each year, the TSC elects a chair to run the meetings. The TSC streams its meetings for public viewing on YouTube or a similar service.

La agenda del TSC incluye cuestiones que se encuentran en un punto muerto. The intention of the agenda is not to review or approve all patches. Collaborators review and approve patches on GitHub.

Any community member can create a GitHub issue asking that the TSC review something. If consensus-seeking fails for an issue, a Collaborator may apply the `tsc-agenda` label. Eso lo añadirá al orden del día de la reunión del TSC.

Before each TSC meeting, the meeting chair will share the agenda with members of the TSC. TSC members can also add items to the agenda at the beginning of each meeting. La silla de la reunión y el TSC no pueden vetar ni quitar elementos.

El CTT puede invitar a personas a participar en una capacidad sin voto.

Durante la reunión, la silla TSC se asegura de que alguien tome minutos. After the meeting, the TSC chair ensures that someone opens a pull request with the minutes.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). The process in the issue tracker is:

* A TSC member opens an issue explaining the proposal/issue and @-mentions @nodejs/tsc.
* The proposal passes if, after 72 hours, there are two or more TSC approvals and no TSC opposition.
* Si se produce un estancamiento prolongado, un miembro de la CTT podrá presentar una propuesta de votación.

## Nominaciones de colaborador

Colaboradores existentes pueden nominar a alguien para convertirse en Colaborador. Nominees should have significant and valuable contributions across the Node.js organization.

Para nominar a un nuevo Colaborador, abra un problema en el repositorio [nodejs/node][]. Proporcionar un resumen de las contribuciones del nominado. Por ejemplo:

* Comandos en el repositorio [nodejs/node][].
  * Utilice el enlace `https://github.com/nodejs/node/commits?author=GITHUB_ID`
* Solicitudes y problemas abiertos en el repositorio [nodejs/node][].
  * Utilice el enlace `https://github.com/nodejs/node/issues?q=author:GITHUB_ID`
* Comentarios sobre pull requests y problemas en el repositorio [nodejs/node][]
  * Utilice el enlace `https://github.com/nodejs/node/issues?q=commenter:GITHUB_ID`
* Reseñas sobre pull requests en el repositorio [nodejs/node][]
  * Utilice el enlace `https://github.com/nodejs/node/pulls?q=reviewed-by:GITHUB_ID`
* Ayuda proporcionada a los usuarios finales y a los contribuyentes novatos
* Tirar peticiones y problemas abiertos en toda la organización Node.js
  * Utilice el enlace  `https://github.com/search?q=author:GITHUB_ID+org:nodejs`
* Comentarios sobre pull requests y problemas en toda la organización Node.js
  * Utilice el enlace `https://github.com/search?q=commenter:GITHUB_ID+org:nodejs`
* Participation in other projects, teams, and working groups of the Node.js organization
* Otra participación en la comunidad Node.js más amplia

Mention @nodejs/collaborators in the issue to notify other Collaborators about the nomination.

La nominación pasa si ningún Colaborador se opone a ella después de una semana. Otherwise, the nomination fails.

There are steps a nominator can take in advance to make a nomination as frictionless as possible. To request feedback from other Collaborators in private, use the [Collaborators discussion page][] (which only Collaborators may view). A nominator may also work with the nominee to improve their contribution profile.

Los colaboradores podrían pasar por alto a alguien con valiosas contribuciones. In that case, the contributor may open an issue or contact a Collaborator to request a nomination.

### Embarque

Después de la nominación pasa, un miembro del TSC integra el nuevo Colaborador. See [the onboarding guide](./onboarding.md) for details of the onboarding process.

## Proceso de búsqueda de consenso

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[Collaborators discussion page]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[2]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[3]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
