# Embarquement

This document is an outline of the things we tell new Collaborators at their onboarding session.

## Une semaine avant la session d'intégration

* If the new Collaborator is not yet a member of the nodejs GitHub organization, confirm that they are using [two-factor authentication][]. It will not be possible to add them to the organization if they are not using two-factor authentication. If they cannot receive SMS messages from GitHub, try [using a TOTP mobile app][].
* Announce the accepted nomination in a TSC meeting and in the TSC mailing list.
* Suggest the new Collaborator install [`node-core-utils`][] and [set up the credentials][] for it.

## Quinze minutes avant la session d'intégration

* Prior to the onboarding session, add the new Collaborator to [the Collaborators team](https://github.com/orgs/nodejs/teams/collaborators).
* Demandez-leur s'ils veulent rejoindre des équipes de sous-système. See [Who to CC in the issue tracker][who-to-cc].

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
  * Membership: Consider making your membership in the Node.js GitHub organization public. Cela facilite l'identification des Collaborateurs. Instructions on how to do that are available at [Publicizing or hiding organization membership][].

* Notifications:
  * Use [https://github.com/notifications](https://github.com/notifications) or set up email
  * Watching the main repo will flood your inbox (several hundred notifications on typical weekdays), so be prepared

Le projet a deux salles de discussion en temps réel :
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) on the [OpenJS Foundation](https://slack-invite.openjsf.org/)
* `#node-dev` on [webchat.freenode.net](https://webchat.freenode.net/) is a great place to interact with the TSC and other Collaborators
  * If there are any questions after the session, a good place to ask is there!
  * Presence is not mandatory, but please drop a note there if force-pushing to `master`

## Objectifs & valeurs du projet

* Les collaborateurs sont les propriétaires collectifs du projet
  * Le projet a les objectifs de ses contributeurs

* Il y a des objectifs et des valeurs de plus haut niveau
  * L'empathie envers les utilisateurs est importante (c'est en partie pourquoi nous embarquons des personnes)
  * Généralement: essayez d'être gentil avec les gens !
  * The best outcome is for people who come to our issue tracker to feel like they can come back again.

* You are expected to follow *and* hold others accountable to the [Code of Conduct][].

## Gestion du traqueur de tickets

* You have (mostly) free rein; don't hesitate to close an issue if you are confident that it should be closed
  * Soyez gentil lorsque vous fermez des tickets ! Let people know why, and that issues and PRs can be reopened if necessary

* [**Voir "Étiquettes"**](./doc/guides/onboarding-extras.md#labels)
  * There is [a bot](https://github.com/nodejs-github-bot/github-bot) that applies subsystem labels (for example, `doc`, `test`, `assert`, or `buffer`) so that we know what parts of the code base the pull request modifies. It is not perfect, of course. Feel free to apply relevant labels and remove irrelevant labels from pull requests and issues.
  * `semver-{minor,major}`:
    * If a change has the remote *chance* of breaking something, use the `semver-major` label
    * When adding a `semver-*` label, add a comment explaining why you're adding it. Faites-le tout de suite pour ne pas oublier !
  * Veuillez ajouter l'étiquette [`prête à l'auteur`][] pour les PR, le cas échéant.

* Voir [Qui CC dans le gestionnaire de tickets][who-to-cc].
  * Cela viendra plus naturellement au fil du temps
  * For many of the teams listed there, you can ask to be added if you are interested
    * Some are WGs with some process around adding people, others are only there for notifications

* When a discussion gets heated, you can request that other Collaborators keep an eye on it by opening an issue at the private [nodejs/moderation](https://github.com/nodejs/moderation) repository.
  * This is a repository to which all members of the `nodejs` GitHub organization (not just Collaborators on Node.js core) have access. Its contents should not be shared externally.
  * You can find the full moderation policy [here](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Révision des PRs

* Le but principal est que la base de code s'améliore.
* Secondaire (mais pas très loin) est pour la personne qui soumet le code pour réussir. A pull request from a new contributor is an opportunity to grow the community.
* Réviser un peu à la fois. Ne submergez pas de nouveaux contributeurs.
  * Il est tentant de micro-optimiser. Ne succombez pas à cette tentation. We change V8 often. Techniques that provide improved performance today may be unnecessary in the future.
* Soyez attentifs: Votre opinion a beaucoup de poids!
* Nits (requests for small changes that are not essential) are fine, but try to avoid stalling the pull request.
  * Identifiez-les en tant que nits lorsque vous commentez : `Nit: changer foo() en bar().`
  * S'ils bloquent la demande de tirage au sort, corrigez-les vous-même lors de la fusion.
* Insofar as possible, issues should be identified by tools rather than human reviewers. If you are leaving comments about issues that could be identified by tools but are not, consider implementing the necessary tooling.
* Temps d'attente minimum pour les commentaires
  * There is a minimum waiting time which we try to respect for non-trivial changes so that people who may have important input in such a distributed project are able to respond.
  * Pour les changements non triviaux, laissez la pull request ouverte pendant au moins 48 heures.
  * If a pull request is abandoned, check if they'd mind if you took it over (especially if it just has nits left).
* Approbation d'un changement
  * Collaborators indicate that they have reviewed and approve of the changes in a pull request using GitHub’s approval interface
  * Certaines personnes aiment commenter `LGTM` (« Ça me semble bien »)
  * Vous avez l’autorité d’approuver le travail de tout autre collaborateur.
  * Vous ne pouvez pas approuver vos propres pull requests.
  * When explicitly using `Changes requested`, show empathy – comments will usually be addressed even if you don’t use it.
    * If you do, it is nice if you are available later to check whether your comments have been addressed
    * If you see that the requested changes have been made, you can clear another collaborator's `Changes requested` review.
    * Use `Changes requested` to indicate that you are considering some of your comments to block the PR from landing.

* Qu'est-ce qui appartient à Node.js :
  * Les opinions varient – il est bon d’avoir une large base de collaborateur pour cette raison !
  * If Node.js itself needs it (due to historical reasons), then it belongs in Node.js.
    * That is to say, `url` is there because of `http`, `freelist` is there because of `http`, etc.
  * Things that cannot be done outside of core, or only with significant pain such as `async_hooks`.

* Tests d'intégration continue (CI) :
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * Il n'est pas exécuté automatiquement. Vous devez le démarrer manuellement.
  * La connexion sur CI est intégrée à GitHub. Essayez de vous connecter maintenant !
  * Vous utiliserez `node-test-pull-request` la plupart du temps. Allez là-bas !
    * Pensez à le mettre en signet : <https://ci.nodejs.org/job/node-test-pull-request/>
  * Pour accéder au formulaire pour démarrer une tâche, cliquez sur `Build with Parameters`. (If you don't see it, that probably means you are not logged in!) Cliquez maintenant !
  * To start CI testing from this screen, you need to fill in two elements on the form:
    * La case `CERTIFY_SAFE` doit être vérifiée. By checking it, you are indicating that you have reviewed the code you are about to test and you are confident that it does not contain any malicious code. (We don't want people hijacking our CI hosts to attack other hosts on the internet, for example!)
    * The `PR_ID` box should be filled in with the number identifying the pull request containing the code you wish to test. For example, if the URL for the pull request is `https://github.com/nodejs/node/issues/7006`, then put `7006` in the `PR_ID`.
    * Les éléments restants du formulaire sont généralement inchangés.
  * Si vous avez besoin d'aide avec quelque chose de lié au CI:
    * Utilisez #node-dev (IRC) pour parler à d'autres Collaborateurs.
    * Use #node-build (IRC) to talk to the Build WG members who maintain the CI infrastructure.
    * Use the [Build WG repo](https://github.com/nodejs/build) to file issues for the Build WG members who maintain the CI infrastructure.

## PRs d'atterrissage

Voir le Guide du collaborateur : [Atterrissage des demandes de tirage][].

Commits in one PR that belong to one logical change should be squashed. It is rarely the case in onboarding exercises, so this needs to be pointed out separately during the onboarding.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Exercice : Faites une PR vous ajoutant au README

* Example: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * For raw commit message: `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* Les collaborateurs sont par ordre alphabétique par nom d'utilisateur GitHub.
* Optionnellement, incluez votre prononciation personnelle.
* Add the `Fixes: <collaborator-nomination-issue-url>` to the commit message so that when the commit lands, the nomination issue url will be automatically closed.
* Label your pull request with the `doc`, `notable-change`, and `fast-track` labels.
* Exécutez CI sur le PR. Utilisez la tâche CI `node-test-pull-request`.
* After two Collaborator approvals for the change and two Collaborator approvals for fast-tracking, land the PR.
* Laissez un commentaire dans le PR: `Veuillez 👍 ce commentaire pour approuver le suivi rapide`.
* If there are not enough approvals within a reasonable time, consider the single approval of the onboarding TSC member sufficient, and land the PR.
  * Be sure to add the `PR-URL: <full-pr-url>` and appropriate `Reviewed-By:` metadata.
  * [`node-core-utils`][] automates the generation of metadata and the landing process. Voir la documentation de [`git-node`][].
  * [`core-validate-commit`][] automatise la validation des messages de commit. This will be run during `git node land --final` of the [`git-node`][] command.

## Notes finales

* Don't worry about making mistakes: everybody makes them, there's a lot to internalize and that takes time (and we recognize that!)
* Presque toute erreur que vous pourriez commettre peut être corrigée ou annulée.
* Les Collaborators existants vous font confiance et vous sont reconnaissants pour votre aide !
* Autres dépôts:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/readable-stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* The OpenJS Foundation hosts regular summits for active contributors to the Node.js project, where we have face-to-face discussions about our work on the project. The Foundation has travel funds to cover participants' expenses including accommodations, transportation, visa fees, etc. if needed. Check out the [summit](https://github.com/nodejs/summit) repository for details.

[Code of Conduct]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Atterrissage des demandes de tirage]: doc/guides/collaborator-guide.md#landing-pull-requests
[Publicizing or hiding organization membership]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`prête à l'auteur`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[set up the credentials]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[two-factor authentication]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[using a TOTP mobile app]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
