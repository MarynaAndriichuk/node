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

Les triagers évaluent les problèmes récemment ouverts dans les dépôts nodejs/node et nodejs/help. Il n'y a pas d'équipe GitHub pour les triagers pour le moment.

Les triagers ont :
* la possibilité d'étiqueter les problèmes
* la possibilité de commenter, de fermer et de rouvrir les tickets

Voir:

* [Un guide pour les triagers](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Collaborateurs

Node.js Core Collaborators maintient le dépôt GitHub [nodejs/node][]. L'équipe GitHub pour Node.js Core Collaborators est @nodejs/collaborateurs. Les collaborateurs ont :

* Valider l'accès au dépôt [nodejs/node][]
* Accès aux travaux d'intégration continue (CI) de Node.js

Les Collaborators et les non-Collaborators peuvent proposer des modifications au code source de Node.js. Le mécanisme pour proposer un tel changement est une demande de pull GitHub. Les collaborateurs examinent et fusionnent (_land_) les demandes de tirage.

Deux Collaborateurs doivent approuver une demande de tirage avant que la demande de tirage ne puisse atterrir. (une approbation de Collaborator suffit si la demande d'ajout est ouverte depuis plus de 7 jours.) L'approbation d'une demande d'ajout indique que le Collaborateur accepte la responsabilité du changement. L'approbation d'une demande d'ajout indique que le Collaborateur accepte la responsabilité du changement. L'approbation doit être faite par des Collaborateurs qui ne sont pas des auteurs du changement.

Si un Collaborateur s'oppose à un changement proposé, le changement ne peut pas atterrir. L'exception est si le TSC vote pour approuver le changement malgré l'opposition. Habituellement, il n'est pas nécessaire d'impliquer le TSC. Souvent, les discussions ou les changements ultérieurs aboutissent à ce que les Collaborateurs retirent leur opposition.

Voir:

* [Liste des collaborateurs](./README.md#current-project-team-members)
* [Un guide pour les collaborateurs](./doc/guides/collaborator-guide.md)

### Activités du collaborateur

* Aider les utilisateurs et les contributeurs novices
* Contribuer au code et à la documentation pour améliorer le projet
* Revue et commentaires sur les demandes de fusion et les demandes de fusion
* Participation aux groupes de travail
* Fusion des demandes de fusion

La TSC peut supprimer les Collaborateurs inactifs ou leur fournir le statut _Émérique_. Les émérites peuvent demander à la TSC de les restaurer à un statut actif.

## Comité de pilotage technique

Un sous-ensemble des Collaborateurs forme le Comité de pilotage technique (CSC). La TSC a une autorité finale sur ce projet, y compris :

* Direction technique
* Gouvernance et processus du projet (y compris cette politique)
* Politique de contribution
* GitHub repository hosting
* Directives de conduite
* Maintenir la liste des collaborateurs

La liste actuelle des membres de la TSC est dans [le projet README](./README.md#current-project-team-members).

[La charte TSC][] régit les opérations du TSC. Toutes les modifications apportées à la Charte doivent être approuvées par le Conseil Cross-Project de la Fondation OpenJS (CPC).

### Réunions TSC

La TSC se réunit lors d'une conférence vocale. Chaque année, le TSC élit un président pour présider les réunions. La TSC diffuse ses réunions pour le public sur YouTube ou un service similaire.

Le programme de la TSC comprend des questions qui sont dans une impasse. Le but de l'ordre du jour n'est pas de revoir ou d'approuver tous les patchs. Les collaborateurs révisent et approuvent les patchs sur GitHub.

N'importe quel membre de la communauté peut créer un problème GitHub demandant que le TSC examine quelque chose. Si la recherche de consensus échoue pour un problème, un Collaborateur peut appliquer l'étiquette `tsc-agenda`. Cela l'ajoutera à l'ordre du jour de la réunion de la TSC.

Avant chaque réunion du TSC, le président de la réunion partagera l'ordre du jour avec les membres du TSC. Les membres du BST peuvent également ajouter des points à l'ordre du jour au début de chaque réunion. Le président de réunion et le TSC ne peuvent pas opposer leur veto ou supprimer des éléments.

Le TSC peut inviter les gens à participer à une activité sans droit de vote.

Lors de la réunion, le président de la TSC veille à ce que quelqu'un prenne des minutes. Après la réunion, le président de la TSC s'assure que quelqu'un ouvre une demande de tirage avec les procès-verbaux.

La TSC cherche à résoudre autant de problèmes que possible en dehors des réunions en utilisant [le traqueur de tickets TSC](https://github.com/nodejs/TSC/issues). Le processus dans le gestionnaire de tickets est :

* Un membre du TSC ouvre un problème expliquant la proposition/problème et @-mentions @nodejs/tsc.
* La proposition passe si, après 72 heures, il y a au moins deux approbations du TSC et aucune opposition du TSC.
* S'il y a une impasse prolongée, un membre du SCT peut faire une motion de vote.

## Nominations de collaborateur

Les Collaborateurs existants peuvent nommer quelqu'un pour devenir Collaborateur. Les candidats devraient avoir une contribution importante et précieuse dans l'organisation Node.js.

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
* Participation à d'autres projets, équipes et groupes de travail de l'organisation Node.js
* Autre participation à la communauté Node.js plus large

Mentionnez @nodejs/collaborators dans la question pour informer les autres Collaborateurs de la mise en candidature.

La nomination passe si aucun Collaborateur ne s'y oppose après une semaine. Dans le cas contraire, la nomination échoue.

Il y a des mesures que le candidat peut prendre à l'avance pour rendre une candidature aussi implacable que possible. Pour demander des commentaires à d'autres Collaborateurs en privé, utilisez la page de discussion [Collaborators][] (que seuls les Collaborateurs peuvent afficher). Un candidat peut également collaborer avec le candidat pour améliorer son profil de contribution.

Les collaborateurs pourraient oublier quelqu'un avec des contributions précieuses. Dans ce cas, le contributeur peut ouvrir un problème ou contacter un Collaborateur pour demander une candidature.

### Embarquement

Une fois la nomination terminée, un membre du TSC se retrouve à bord du nouveau collaborateur. Consultez [le guide d'intégration](./onboarding.md) pour plus de détails sur le processus d'intégration.

## Processus de recherche de consensus

La TSC suit un modèle de décision [Consensus Seeking][] selon la [Charte TSC][].

[Collaborators]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[La charte TSC]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[Charte TSC]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
