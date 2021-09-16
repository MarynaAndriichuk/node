# Embarquement

Ce document est un aperçu des choses que nous disons aux nouveaux Collaborateurs lors de leur session d'intégration.

## Une semaine avant la session d'intégration

* Si le nouveau Collaborator n'est pas encore membre de l'organisation GitHub de nodejs, confirmez qu'ils utilisent [l'authentification à deux facteurs][]. Il ne sera pas possible de les ajouter à l'organisation si elle n'utilise pas l'authentification à deux facteurs. S'ils ne peuvent pas recevoir de SMS de GitHub, essayez [en utilisant une application mobile TOTP][].
* Annoncez la nomination acceptée lors d'une réunion de la TSC et dans la liste de diffusion de la TSC.
* Suggérez le nouveau Collaborator installer [`node-core-utils`][] et [configurer les identifiants][] pour lui.

## Quinze minutes avant la session d'intégration

* Avant la session d'intégration, ajoutez le nouveau Collaborateur à [l'équipe Collaborators](https://github.com/orgs/nodejs/teams/collaborators).
* Demandez-leur s'ils veulent rejoindre des équipes de sous-système. Voir [Qui CC dans le gestionnaire de tickets][who-to-cc].

## Session d'intégration

* Cette session couvrira:
  * [configuration locale](#local-setup)
  * [objectifs & valeurs du projet](#project-goals--values)
  * [gestion du traqueur de tickets](#managing-the-issue-tracker)
  * [examen des PRs](#reviewing-prs)
  * [PRs d'atterrissage](#landing-prs)

## Configuration locale

* git:
  * Assurez-vous que vous avez whitespace=fix : `git config --global --add
apply.whitespace fix`
  * Toujours continuer vers la PR depuis votre propre fork GitHub
    * Les branches dans le dépôt `nodejs/node` ne sont que pour les lignes de publication
  * Ajouter le dépôt canonical nodejs en tant que `amont` distant :
    * `git remote add git://github.com/nodejs/node.git`
  * Pour mettre à jour depuis `amont`:
    * `Git checkout master`
    * `git update distante -p` OU `git fetch --all`
    * `git merge --ff-only upstream/master` (ou `REMOTENAME/BRANCH`)
  * Créer une nouvelle succursale pour chaque RP que vous soumettez.
  * Adhésion : Envisagez de rendre votre adhésion à l'organisation GitHub Node.js publique. Cela facilite l'identification des Collaborateurs. Instructions sur la façon de le faire sont disponibles sur [la publication ou la dissimulation de l'adhésion à l'organisation][].

* Notifications:
  * Utilisez [https://github.com/notifications](https://github.com/notifications) ou configurez l'e-mail
  * En regardant le dépôt principal, vous inonderez votre boîte de réception (plusieurs centaines de notifications les jours typiques de la semaine), alors soyez préparé

Le projet a deux salles de discussion en temps réel :
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) sur la [Fondation OpenJS](https://slack-invite.openjsf.org/)
* `#node-dev` sur [webchat.freenode.net](https://webchat.freenode.net/) est un excellent endroit pour interagir avec le TSC et les autres Collaborateurs.
  * Si vous avez des questions après la séance, un bon endroit est là !
  * Presence n'est pas obligatoire, mais veuillez y déposer une note si vous forcez la poussée vers `master`

## Objectifs & valeurs du projet

* Les collaborateurs sont les propriétaires collectifs du projet
  * Le projet a les objectifs de ses contributeurs

* Il y a des objectifs et des valeurs de plus haut niveau
  * L'empathie envers les utilisateurs est importante (c'est en partie pourquoi nous embarquons des personnes)
  * Généralement: essayez d'être gentil avec les gens !
  * Le meilleur résultat est que les personnes qui viennent sur notre système de suivi de tickets aient l'impression de pouvoir revenir à nouveau.

* Vous devez suivre *et* tenir les autres responsables devant le [Code de conduite][].

## Gestion du traqueur de tickets

* Vous avez (principalement) un rein-gratuit ; n'hésitez pas à fermer un ticket si vous êtes sûr qu'il devrait être fermé
  * Soyez gentil lorsque vous fermez des tickets ! Dites aux gens pourquoi, et que les questions et les relations publiques peuvent être rouvertes si nécessaire

* [**Voir "Étiquettes"**](./doc/guides/onboarding-extras.md#labels)
  * Il y a [un bot](https://github.com/nodejs-github-bot/github-bot) qui applique les étiquettes du sous-système (par exemple, `doc`, `test`, `affirmer`, ou `tampon`) afin de savoir quelles parties du code de base la demande d'ajout modifie. Ce n'est pas parfait, bien sûr. N’hésitez pas à appliquer des étiquettes pertinentes et à supprimer les étiquettes non pertinentes des demandes de fusion et des problèmes.
  * `semver-{minor,major}`:
    * Si un changement a la chance *distante* de casser quelque chose, utilisez l'étiquette `semver-major`
    * Lors de l'ajout d'une étiquette `semver-*` , ajoutez un commentaire expliquant pourquoi vous l'ajoutez. Faites-le tout de suite pour ne pas oublier !
  * Veuillez ajouter l'étiquette [`prête à l'auteur`][] pour les PR, le cas échéant.

* Voir [Qui CC dans le gestionnaire de tickets][who-to-cc].
  * Cela viendra plus naturellement au fil du temps
  * Pour de nombreuses équipes listées dans la liste, vous pouvez demander à être ajouté si vous êtes intéressé
    * Certains sont des WGs avec certains processus autour de l'ajout de personnes, d'autres sont seulement là pour les notifications

* Quand une discussion est chauffée, vous pouvez demander à d'autres Collaborators de garder un œil sur cela en ouvrant un problème dans le dépôt privé [nodejs/moderation](https://github.com/nodejs/moderation).
  * Il s'agit d'un dépôt auquel tous les membres de l'organisation GitHub `nodejs` (pas seulement les Collaborators sur Node.js) ont accès. Son contenu ne doit pas être partagé à l'extérieur.
  * Vous pouvez trouver la politique de modération complète [ici](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Révision des PRs

* Le but principal est que la base de code s'améliore.
* Secondaire (mais pas très loin) est pour la personne qui soumet le code pour réussir. Une demande d'attraction d'un nouveau contributeur est une occasion de faire grandir la communauté.
* Réviser un peu à la fois. Ne submergez pas de nouveaux contributeurs.
  * Il est tentant de micro-optimiser. Ne succombez pas à cette tentation. Nous changeons souvent de V8. Les techniques qui améliorent la performance de nos jours peuvent s'avérer inutiles à l'avenir.
* Soyez attentifs: Votre opinion a beaucoup de poids!
* Nits (demandes de petits changements qui ne sont pas essentiels) sont corrects, mais essayez d'éviter le blocage de la demande de tirage au sort.
  * Identifiez-les en tant que nits lorsque vous commentez : `Nit: changer foo() en bar().`
  * S'ils bloquent la demande de tirage au sort, corrigez-les vous-même lors de la fusion.
* Dans la mesure du possible, les questions devraient être identifiées par des outils plutôt que par des examinateurs humains. Si vous laissez des commentaires sur des questions qui pourraient être identifiées par des outils mais qui ne le sont pas, envisagez de mettre en œuvre les outils nécessaires.
* Temps d'attente minimum pour les commentaires
  * Il y a un minimum de temps d'attente que nous essayons de respecter pour les changements non triviaux afin que les personnes qui peuvent avoir une contribution importante dans un tel projet distribué soient en mesure de répondre.
  * Pour les changements non triviaux, laissez la pull request ouverte pendant au moins 48 heures.
  * Si une demande d'ajout est abandonnée, vérifiez si vous l'aurez pris en charge (surtout si elle a juste des nits restants).
* Approbation d'un changement
  * Les collaborateurs indiquent qu'ils ont examiné et approuvé les changements dans une pull request en utilisant l'interface d'approbation de GitHub
  * Certaines personnes aiment commenter `LGTM` (« Ça me semble bien »)
  * Vous avez l’autorité d’approuver le travail de tout autre collaborateur.
  * Vous ne pouvez pas approuver vos propres pull requests.
  * Lorsque vous utilisez explicitement `Modifications demandées`, montrer de l'empathie - les commentaires seront généralement abordés même si vous ne les utilisez pas.
    * Si vous le faites, c'est bien si vous êtes disponible plus tard pour vérifier si vos commentaires ont été pris en compte
    * Si vous voyez que les modifications demandées ont été faites, vous pouvez effacer les `Modifications demandées par un autre collaborateur` de la revue.
    * Utilisez `Modifications demandées` pour indiquer que vous envisagez certains de vos commentaires pour empêcher la PR d'atterrir.

* Qu'est-ce qui appartient à Node.js :
  * Les opinions varient – il est bon d’avoir une large base de collaborateur pour cette raison !
  * Si Node.js lui-même en a besoin (pour des raisons historiques), alors il appartient à Node.js.
    * C'est-à-dire que `url` est là à cause de `http`, `freelist` est là à cause de `http`, etc.
  * Des choses qui ne peuvent pas être faites en dehors du noyau, ou seulement avec une douleur significative comme `async_hooks`.

* Tests d'intégration continue (CI) :
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * Il n'est pas exécuté automatiquement. Vous devez le démarrer manuellement.
  * La connexion sur CI est intégrée à GitHub. Essayez de vous connecter maintenant !
  * Vous utiliserez `node-test-pull-request` la plupart du temps. Allez là-bas !
    * Pensez à le mettre en signet : <https://ci.nodejs.org/job/node-test-pull-request/>
  * Pour accéder au formulaire pour démarrer une tâche, cliquez sur `Build with Parameters`. (Si vous ne le voyez pas, cela signifie probablement que vous n'êtes pas connecté!) Cliquez maintenant ! Cliquez maintenant !
  * Pour commencer le test CI à partir de cet écran, vous devez remplir deux éléments sur le formulaire :
    * La case `CERTIFY_SAFE` doit être vérifiée. En vérifiant, vous indiquez que vous avez vérifié le code que vous êtes sur le point de tester et que vous êtes sûr qu'il ne contient aucun code malveillant. (Nous ne voulons pas que les gens qui détournent nos hôtes CI attaquent d'autres hôtes sur Internet, par exemple !)
    * La boîte `PR_ID` doit être remplie avec le numéro identifiant la pull request contenant le code que vous souhaitez tester. Par exemple, si l'URL de la pull request est `https://github.com/nodejs/node/issues/7006`, puis mettez `7006` dans le `PR_ID`.
    * Les éléments restants du formulaire sont généralement inchangés.
  * Si vous avez besoin d'aide avec quelque chose de lié au CI:
    * Utilisez #node-dev (IRC) pour parler à d'autres Collaborateurs.
    * Utilisez #node-build (IRC) pour parler aux membres de Build WG qui maintiennent l'infrastructure CI.
    * Utilisez le [dépôt WG de Build](https://github.com/nodejs/build) pour archiver les problèmes pour les membres de Build WG qui maintiennent l'infrastructure CI.

## PRs d'atterrissage

Voir le Guide du collaborateur : [Atterrissage des demandes de tirage][].

Les commits dans un RP qui appartiennent à un changement logique devraient être écrasés. C'est rarement le cas pour les exercices d'embarquement, et il faut donc le souligner séparément lors de l'embarquement.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Exercice : Faites une PR vous ajoutant au README

* Exemple: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * Pour le message de commit brut : `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* Les collaborateurs sont par ordre alphabétique par nom d'utilisateur GitHub.
* Optionnellement, incluez votre prononciation personnelle.
* Ajoute les `correctifs : <collaborator-nomination-issue-url>` au message de commit afin que lorsque la livraison se termine, l'url du problème de nomination soit automatiquement fermée.
* Étiquetez votre pull request avec les étiquettes `doc`, `notable-change`et `fast-track`.
* Exécutez CI sur le PR. Utilisez la tâche CI `node-test-pull-request`.
* Après deux approbations de Collaborator pour le changement et deux approbations de Collaborator pour le suivi rapide, atterrir le PR.
* Laissez un commentaire dans le PR: `Veuillez 👍 ce commentaire pour approuver le suivi rapide`.
* S'il n'y a pas assez d'autorisations dans un délai raisonnable, considérez que l'approbation unique du membre du TSC à bord suffit et atterrissez la PR.
  * N'oubliez pas d'ajouter les métadonnées `PR-URL : <full-pr-url>` et la `Revue <code> appropriée -By:` métadonnées.
  * [`node-core-utils`][] automatise la génération de métadonnées et le processus d'atterrissage. Voir la documentation de [`git-node`][].
  * [`core-validate-commit`][] automatise la validation des messages de commit. Cela sera exécuté pendant `git node land --final` de la commande [`git-node`][].

## Notes finales

* Ne vous inquiétez pas de faire des erreurs : tout le monde les fait, il y a beaucoup à internaliser et cela prend du temps (et nous le reconnaissons !)
* Presque toute erreur que vous pourriez commettre peut être corrigée ou annulée.
* Les Collaborators existants vous font confiance et vous sont reconnaissants pour votre aide !
* Autres dépôts:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* La Fondation OpenJS organise régulièrement des sommets pour les contributeurs actifs au projet Node.js, où nous avons des discussions en face à face à propos de notre travail sur le projet. La Fondation dispose de fonds de voyage pour couvrir les dépenses des participants, y compris l'hébergement, le transport, les frais de visa, etc. si nécessaire. Consultez le dépôt [Summit](https://github.com/nodejs/summit) pour plus de détails.

[Code de conduite]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Atterrissage des demandes de tirage]: doc/guides/collaborator-guide.md#landing-pull-requests
[la publication ou la dissimulation de l'adhésion à l'organisation]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`prête à l'auteur`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[configurer les identifiants]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[l'authentification à deux facteurs]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[en utilisant une application mobile TOTP]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
