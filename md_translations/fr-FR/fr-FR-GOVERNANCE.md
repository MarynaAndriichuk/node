# Gouvernance du projet Node.js

<!-- TOC -->

* [Triageurs](#triagers)
* [Collaborateurs](#collaborators)
  * [Activités du collaborateur](#collaborator-activities)
* [Comité de pilotage technique](#technical-steering-committee)
  * [Réunions TSC](#tsc-meetings)
* [Nominations de collaborateur](#collaborator-nominations)
  * [Embarquement](#onboarding)
* [Processus de recherche de consensus](#consensus-seeking-process)

<!-- /TOC -->

## Triageurs

Triagers assess newly-opened issues in the nodejs/node and nodejs/help repositories. Il n'y a pas d'équipe GitHub pour les triagers pour le moment.

Les triagers ont :
* la possibilité d'étiqueter les problèmes
* la possibilité de commenter, de fermer et de rouvrir les tickets

Voir:

* [Un guide pour les triagers](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Collaborateurs

Node.js Core Collaborators maintient le dépôt GitHub [nodejs/node][]. L'équipe GitHub pour Node.js Core Collaborators est @nodejs/collaborateurs. Les collaborateurs ont :

* Valider l'accès au dépôt [nodejs/node][]
* Accès aux travaux d'intégration continue (CI) de Node.js

Both Collaborators and non-Collaborators may propose changes to the Node.js source code. Le mécanisme pour proposer un tel changement est une demande de pull GitHub. Les collaborateurs examinent et fusionnent (_land_) les demandes de tirage.

Deux Collaborateurs doivent approuver une demande de tirage avant que la demande de tirage ne puisse atterrir. (One Collaborator approval is enough if the pull request has been open for more than 7 days.) Approving a pull request indicates that the Collaborator accepts responsibility for the change. Approval must be from Collaborators who are not authors of the change.

Si un Collaborateur s'oppose à un changement proposé, le changement ne peut pas atterrir. The exception is if the TSC votes to approve the change despite the opposition. Habituellement, il n'est pas nécessaire d'impliquer le TSC. Often, discussions or further changes result in Collaborators removing their opposition.

Voir:

* [Liste des collaborateurs](./README.md#current-project-team-members)
* [Un guide pour les collaborateurs](./doc/guides/collaborator-guide.md)

### Activités du collaborateur

* Aider les utilisateurs et les contributeurs novices
* Contribuer au code et à la documentation pour améliorer le projet
* Revue et commentaires sur les demandes de fusion et les demandes de fusion
* Participation aux groupes de travail
* Fusion des demandes de fusion

The TSC can remove inactive Collaborators or provide them with _Emeritus_ status. Les émérites peuvent demander à la TSC de les restaurer à un statut actif.

## Comité de pilotage technique

Un sous-ensemble des Collaborateurs forme le Comité de pilotage technique (CSC). La TSC a une autorité finale sur ce projet, y compris :

* Direction technique
* Gouvernance et processus du projet (y compris cette politique)
* Politique de contribution
* GitHub repository hosting
* Directives de conduite
* Maintenir la liste des collaborateurs

The current list of TSC members is in [the project README](./README.md#current-project-team-members).

[La charte TSC][] régit les opérations du TSC. All changes to the Charter need approval by the OpenJS Foundation Cross-Project Council (CPC).

### Réunions TSC

La TSC se réunit lors d'une conférence vocale. Each year, the TSC elects a chair to run the meetings. The TSC streams its meetings for public viewing on YouTube or a similar service.

Le programme de la TSC comprend des questions qui sont dans une impasse. The intention of the agenda is not to review or approve all patches. Collaborators review and approve patches on GitHub.

Any community member can create a GitHub issue asking that the TSC review something. If consensus-seeking fails for an issue, a Collaborator may apply the `tsc-agenda` label. Cela l'ajoutera à l'ordre du jour de la réunion de la TSC.

Before each TSC meeting, the meeting chair will share the agenda with members of the TSC. TSC members can also add items to the agenda at the beginning of each meeting. Le président de réunion et le TSC ne peuvent pas opposer leur veto ou supprimer des éléments.

Le TSC peut inviter les gens à participer à une activité sans droit de vote.

Lors de la réunion, le président de la TSC veille à ce que quelqu'un prenne des minutes. After the meeting, the TSC chair ensures that someone opens a pull request with the minutes.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). The process in the issue tracker is:

* A TSC member opens an issue explaining the proposal/issue and @-mentions @nodejs/tsc.
* The proposal passes if, after 72 hours, there are two or more TSC approvals and no TSC opposition.
* S'il y a une impasse prolongée, un membre du SCT peut faire une motion de vote.

## Nominations de collaborateur

Les Collaborateurs existants peuvent nommer quelqu'un pour devenir Collaborateur. Nominees should have significant and valuable contributions across the Node.js organization.

Pour nommer un nouveau collaborateur, ouvrez un ticket dans le dépôt [nodejs/node][]. Fournir un résumé des contributions du candidat. Par exemple :

* Commits dans le dépôt [nodejs/node][].
  * Utilisez le lien `https://github.com/nodejs/node/commits?author=GITHUB_ID`
* Demandes d'ajout et problèmes ouverts dans le dépôt [nodejs/node][].
  * Utilisez le lien `https://github.com/nodejs/node/issues?q=author:GITHUB_ID`
* Commentaires sur les demandes d'ajout et les problèmes dans le dépôt [nodejs/node][]
  * Utilisez le lien `https://github.com/nodejs/node/issues?q=commenter:GITHUB_ID`
* Avis sur les demandes d'ajout dans le dépôt [nodejs/node][]
  * Utilisez le lien `https://github.com/nodejs/node/pulls?q=reviewed-by:GITHUB_ID`
* Aide fournie aux utilisateurs finaux et aux contributeurs novices
* Demandes de fusion et problèmes ouverts dans l'organisation Node.js
  * Utilisez le lien  `https://github.com/search?q=author:GITHUB_ID+org:nodejs`
* Commentaires sur les demandes de fusion et les problèmes au sein de l'organisation Node.js
  * Utilisez le lien `https://github.com/search?q=commenter:GITHUB_ID+org:nodejs`
* Participation in other projects, teams, and working groups of the Node.js organization
* Autre participation à la communauté Node.js plus large

Mention @nodejs/collaborators in the issue to notify other Collaborators about the nomination.

La nomination passe si aucun Collaborateur ne s'y oppose après une semaine. Otherwise, the nomination fails.

There are steps a nominator can take in advance to make a nomination as frictionless as possible. To request feedback from other Collaborators in private, use the [Collaborators discussion page][] (which only Collaborators may view). A nominator may also work with the nominee to improve their contribution profile.

Les collaborateurs pourraient oublier quelqu'un avec des contributions précieuses. In that case, the contributor may open an issue or contact a Collaborator to request a nomination.

### Embarquement

Une fois la nomination terminée, un membre du TSC se retrouve à bord du nouveau collaborateur. See [the onboarding guide](./onboarding.md) for details of the onboarding process.

## Processus de recherche de consensus

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[Collaborators discussion page]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[La charte TSC]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
