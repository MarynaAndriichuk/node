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

Los triagers evalúan problemas recientemente abiertos en los repositorios nodejs/node y nodejs/helps. No hay ningún equipo de GitHub para triagers en este momento. No hay ningún equipo de GitHub para triagers en este momento.

Los triagers tienen:
* capacidad para etiquetar problemas
* capacidad para comentar, cerrar y reabrir peticiones

Ver:

* [Una guía para triagers](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Colaboradores

Los colaboradores principales de Node.js mantienen el repositorio [nodejs/node][] de GitHub. El equipo de GitHub para Colaboradores de Node.js es @nodejs/colaboradores. Los colaboradores tienen: El equipo de GitHub para Colaboradores de Node.js es @nodejs/colaboradores. Los colaboradores tienen:

* Acceso al repositorio [nodejs/node][]
* Acceso a los trabajos de integración continua (CI) de Node.js

Colaboradores y no Colaboradores pueden proponer cambios en el código fuente de Node.js. El mecanismo para proponer tal cambio es una solicitud de GitHub. Los colaboradores revisan y fusionan (_tierra_) solicitudes de extracción. El mecanismo para proponer tal cambio es una solicitud de GitHub. Los colaboradores revisan y fusionan (_tierra_) solicitudes de extracción.

Dos Colaboradores deben aprobar una pull request antes de que la pull request pueda aterrizar. (Una aprobación de un colaborador es suficiente si el pull request ha estado abierto durante más de 7 días.) La aprobación de un pull request indica que el Colaborador acepta la responsabilidad del cambio. La aprobación debe ser de Colaboradores que no sean autores del cambio. (Una aprobación de un colaborador es suficiente si el pull request ha estado abierto durante más de 7 días.) La aprobación de un pull request indica que el Colaborador acepta la responsabilidad del cambio. La aprobación debe ser de Colaboradores que no sean autores del cambio.

Si un colaborador se opone a un cambio propuesto, entonces el cambio no puede aterrizar. La excepción es si el TSC vota a favor de aprobar el cambio a pesar de la oposición. Por lo general, implicar al TSC es innecesario. A menudo, los debates o cambios posteriores tienen como resultado que los Colaboradores eliminen su oposición. La excepción es si el TSC vota a favor de aprobar el cambio a pesar de la oposición. Por lo general, implicar al TSC es innecesario. A menudo, los debates o cambios posteriores tienen como resultado que los Colaboradores eliminen su oposición.

Ver:

* [Lista de colaboradores](./README.md#current-project-team-members)
* [Una guía para colaboradores](./doc/guides/collaborator-guide.md)

### Actividades de colaborador

* Ayudando usuarios y colaboradores novatos
* Contribuir con cambios de código y documentación que mejoran el proyecto
* Revisando y comentando asuntos y pull requests
* Participación en grupos de trabajo
* Combinando pull requests

El TSC puede remover Colaboradores inactivos o proporcionarles el estado de _Emérito_. Emeriti puede solicitar que el TSC los restaure al estado activo. Emeriti puede solicitar que el TSC los restaure al estado activo.

## Comité Directivo Técnico

Un subconjunto de los Colaboradores forma el Comité Directivo Técnico (TSC). Un subconjunto de los Colaboradores forma el Comité Directivo Técnico (TSC). El TSC tiene autoridad final sobre este proyecto, incluyendo:

* Dirección técnica
* Gobernanza y proceso del proyecto (incluyendo esta política)
* Política de contribución
* GitHub repository hosting
* Directrices de conducta
* Manteniendo la lista de colaboradores

La lista actual de miembros del TSC está en [el proyecto README](./README.md#current-project-team-members).

La Carta del TSC [][] gobierna las operaciones del TSC. La Carta del TSC [][] gobierna las operaciones del TSC. Todos los cambios en la Carta necesitan la aprobación del Consejo de la Fundación OpenJS Cross-Project (CPC).

### Reuniones TSC

El TSC se reúne en una llamada de conferencia de voz. Cada año, el CET elige una silla para dirigir las reuniones. El TSC se reúne en una llamada de conferencia de voz. Cada año, el CET elige una silla para dirigir las reuniones. El TSC transmite sus reuniones para su visualización pública en YouTube o un servicio similar.

La agenda del TSC incluye cuestiones que se encuentran en un punto muerto. La agenda del TSC incluye cuestiones que se encuentran en un punto muerto. La intención del orden del día no es revisar ni aprobar todos los parches. Colaboradores revisan y aprueban los parches en GitHub. Colaboradores revisan y aprueban los parches en GitHub.

Cualquier miembro de la comunidad puede crear un problema de GitHub pidiendo que el TSC revise algo. Si la búsqueda consensada falla en un problema, un colaborador puede aplicar la etiqueta `tsc-agenda`. Eso lo añadirá al orden del día de la reunión del TSC. Si la búsqueda consensada falla en un problema, un colaborador puede aplicar la etiqueta `tsc-agenda`. Eso lo añadirá al orden del día de la reunión del TSC.

Antes de cada reunión del TSC, el presidente de la reunión compartirá la agenda con los miembros del TSC. Antes de cada reunión del TSC, el presidente de la reunión compartirá la agenda con los miembros del TSC. Los miembros del TSC también pueden añadir elementos a la agenda al comienzo de cada reunión. La silla de la reunión y el TSC no pueden vetar ni quitar elementos. La silla de la reunión y el TSC no pueden vetar ni quitar elementos.

El CTT puede invitar a personas a participar en una capacidad sin voto.

Durante la reunión, la silla TSC se asegura de que alguien tome minutos. Durante la reunión, la silla TSC se asegura de que alguien tome minutos. Después de la reunión, la silla del TSC se asegura de que alguien abra una solicitud de extracción con los minutos.

El TSC busca resolver el mayor número posible de problemas en reuniones externas usando [el gestor de problemas](https://github.com/nodejs/TSC/issues) del TSC. El proceso del gestor de incidencias es: El proceso del gestor de incidencias es:

* Un miembro del TSC abre un tema explicando la propuesta/número y @-mentions @nodejs/tsc.
* La propuesta pasa si, después de 72 horas, hay dos o más aprobaciones del TSC y ninguna oposición del TSC.
* Si se produce un estancamiento prolongado, un miembro de la CTT podrá presentar una propuesta de votación.

## Nominaciones de colaborador

Colaboradores existentes pueden nominar a alguien para convertirse en Colaborador. Colaboradores existentes pueden nominar a alguien para convertirse en Colaborador. Los nominados deben tener contribuciones significativas y valiosas en toda la organización Node.js.

Para nominar a un nuevo Colaborador, abra un problema en el repositorio [nodejs/node][]. Proporcionar un resumen de las contribuciones del nominado. Por ejemplo: Proporcione un resumen de las contribuciones del nominado. Por ejemplo:

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
* Participación en otros proyectos, equipos y grupos de trabajo de la organización Node.js
* Otra participación en la comunidad Node.js más amplia

Mencionar a @nodejs/colaboradores en el número para notificar a otros Colaboradores sobre la nominación.

La nominación pasa si ningún Colaborador se opone a ella después de una semana. De lo contrario, la nominación falla. De lo contrario, la nominación falla.

Hay pasos que un nominador puede tomar de antemano para hacer una nominación lo más friccional posible. Hay pasos que un nominador puede tomar de antemano para hacer una nominación lo más friccional posible. Para solicitar comentarios de otros Colaboradores en privado, utilice la [página de discusión de Colaboradores][] (que sólo los Colaboradores pueden ver). Un nominador también puede trabajar con el nominado para mejorar su perfil de contribución. Un nominador también puede trabajar con el nominado para mejorar su perfil de contribución.

Los colaboradores podrían pasar por alto a alguien con valiosas contribuciones. Los colaboradores podrían pasar por alto a alguien con valiosas contribuciones. En ese caso, el colaborador puede abrir un asunto o ponerse en contacto con un Colaborador para solicitar una nominación.

### Embarque

Después de la nominación pasa, un miembro del TSC integra el nuevo Colaborador. Consulte [la guía de incorporación](./onboarding.md) para ver los detalles del proceso de incorporación. Consulte [la guía de incorporación](./onboarding.md) para ver los detalles del proceso de incorporación.

## Proceso de búsqueda de consenso

El TSC sigue un modelo de toma de decisiones de [Consenso de Búsqueda][] según la [Carta de TSC][].

[página de discusión de Colaboradores]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consenso de Búsqueda]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[2]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[3]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[4]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[5]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[Carta de TSC]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
