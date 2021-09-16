# Einbinden

This document is an outline of the things we tell new Collaborators at their onboarding session.

## Eine Woche vor der Onboarding-Sitzung

* If the new Collaborator is not yet a member of the nodejs GitHub organization, confirm that they are using [two-factor authentication][]. It will not be possible to add them to the organization if they are not using two-factor authentication. If they cannot receive SMS messages from GitHub, try [using a TOTP mobile app][].
* Announce the accepted nomination in a TSC meeting and in the TSC mailing list.
* Suggest the new Collaborator install [`node-core-utils`][] and [set up the credentials][] for it.

## Fünfzehn Minuten vor der Onboarding-Sitzung

* Prior to the onboarding session, add the new Collaborator to [the Collaborators team](https://github.com/orgs/nodejs/teams/collaborators).
* Fragen Sie sie, ob sie einem Subsystem Team beitreten möchten. See [Who to CC in the issue tracker][who-to-cc].

## Onboarding-Sitzung

* Diese Sitzung wird abdecken:
  * [lokale Einrichtung](#local-setup)
  * [projektziele & Werte](#project-goals--values)
  * [den Issue-Tracker verwalten](#managing-the-issue-tracker)
  * [überprüfe PRs](#reviewing-prs)
  * [LandingPRs](#landing-prs)

## Lokales Setup

* git:
  * Stellen Sie sicher, dass Sie Whitespace=fix: `git config --global --add
apply.whitespace fix`
  * Immer weiter mit PR von deinem eigenen GitHub Fork
    * Zweige im `nodejs/node` Repository sind nur für Release-Zeilen
  * Füge das kanonische nodejs Repository als `Upstream` hinzu:
    * `git remote add upstream git://github.com/nodejs/node.git`
  * Zum Aktualisieren von `Upstream`:
    * `git Checkout Master`
    * `git remote update -p` ODER `git retriech --all`
    * `git merge --ff-only upstream/master` (oder `REMOTENAME/BRANCH`)
  * Erstelle einen neuen Zweig für jeden PR den du einreichst.
  * Membership: Consider making your membership in the Node.js GitHub organization public. Dadurch wird die Identifizierung von Mitarbeitern erleichtert. Instructions on how to do that are available at [Publicizing or hiding organization membership][].

* Benachrichtigungen:
  * Use [https://github.com/notifications](https://github.com/notifications) or set up email
  * Watching the main repo will flood your inbox (several hundred notifications on typical weekdays), so be prepared

Das Projekt hat zwei Veranstaltungsorte für Diskussionen in Echtzeit:
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) on the [OpenJS Foundation](https://slack-invite.openjsf.org/)
* `#node-dev` on [webchat.freenode.net](https://webchat.freenode.net/) is a great place to interact with the TSC and other Collaborators
  * If there are any questions after the session, a good place to ask is there!
  * Presence is not mandatory, but please drop a note there if force-pushing to `master`

## Projektziele & Werte

* Mitarbeiter sind die Kollektivbesitzer des Projekts
  * Das Projekt hat die Ziele seiner Mitwirkenden

* Es gibt einige Ziele und Werte auf höherer Ebene
  * Empathie gegenüber Nutzern ist wichtig (dies ist zum Teil der Grund, warum wir Leute an Bord haben)
  * Generell: Versuchen Sie nett zu sein!
  * The best outcome is for people who come to our issue tracker to feel like they can come back again.

* You are expected to follow *and* hold others accountable to the [Code of Conduct][].

## Fehlerverfolgung verwalten

* You have (mostly) free rein; don't hesitate to close an issue if you are confident that it should be closed
  * Seien Sie nett über Schließungsprobleme! Let people know why, and that issues and PRs can be reopened if necessary

* [**Siehe "Labels"**](./doc/guides/onboarding-extras.md#labels)
  * There is [a bot](https://github.com/nodejs-github-bot/github-bot) that applies subsystem labels (for example, `doc`, `test`, `assert`, or `buffer`) so that we know what parts of the code base the pull request modifies. It is not perfect, of course. Feel free to apply relevant labels and remove irrelevant labels from pull requests and issues.
  * `semver-{minor,major}`:
    * If a change has the remote *chance* of breaking something, use the `semver-major` label
    * When adding a `semver-*` label, add a comment explaining why you're adding it. Tun Sie es sofort, damit Sie nicht vergessen!
  * Bitte fügen Sie die [`Autorenfertige`][] Bezeichnung für PRs hinzu, falls zutreffend.

* Siehe [Wer CC im Issue-Tracker][who-to-cc].
  * Dies wird mit der Zeit natürlicher sein
  * For many of the teams listed there, you can ask to be added if you are interested
    * Some are WGs with some process around adding people, others are only there for notifications

* When a discussion gets heated, you can request that other Collaborators keep an eye on it by opening an issue at the private [nodejs/moderation](https://github.com/nodejs/moderation) repository.
  * This is a repository to which all members of the `nodejs` GitHub organization (not just Collaborators on Node.js core) have access. Its contents should not be shared externally.
  * You can find the full moderation policy [here](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Überprüfe PRs

* Das primäre Ziel ist es, die Codebase zu verbessern.
* Sekundär (aber nicht weit entfernt) ist es, dass die Person, die Code einreicht, erfolgreich ist. A pull request from a new contributor is an opportunity to grow the community.
* Überprüfen Sie ein bisschen nach dem anderen. Überfordern Sie keine neuen Beitragszahler.
  * Es ist verlockend zur Mikrooptimierung. Nicht dieser Versuchung erliegen. We change V8 often. Techniques that provide improved performance today may be unnecessary in the future.
* Seien Sie sich bewusst: Ihre Meinung hat viel Gewicht!
* Nits (requests for small changes that are not essential) are fine, but try to avoid stalling the pull request.
  * Identifizieren Sie sie als Nits, wenn Sie kommentieren: `Nit: Ändern Sie foo() in bar().`
  * Wenn sie den Pull-Request blockieren, reparieren Sie ihn selbst beim Zusammenführen.
* Insofar as possible, issues should be identified by tools rather than human reviewers. If you are leaving comments about issues that could be identified by tools but are not, consider implementing the necessary tooling.
* Minimale Wartezeit für Kommentare
  * There is a minimum waiting time which we try to respect for non-trivial changes so that people who may have important input in such a distributed project are able to respond.
  * Für nicht-triviale Änderungen lassen Sie den Pull-Request für mindestens 48 Stunden offen.
  * If a pull request is abandoned, check if they'd mind if you took it over (especially if it just has nits left).
* Änderung genehmigen
  * Collaborators indicate that they have reviewed and approve of the changes in a pull request using GitHub’s approval interface
  * Einige Leute kommentieren gern `LGTM` ("Scheint mir gut an")
  * Sie haben die Befugnis, die Arbeit eines anderen Mitarbeiters zu genehmigen.
  * Du kannst deine eigenen Pull-Requests nicht genehmigen.
  * When explicitly using `Changes requested`, show empathy – comments will usually be addressed even if you don’t use it.
    * If you do, it is nice if you are available later to check whether your comments have been addressed
    * If you see that the requested changes have been made, you can clear another collaborator's `Changes requested` review.
    * Use `Changes requested` to indicate that you are considering some of your comments to block the PR from landing.

* Was gehört in Node.js:
  * Die Meinungen variieren – aus diesem Grund ist es gut, eine breite Mitarbeiterbasis zu haben!
  * If Node.js itself needs it (due to historical reasons), then it belongs in Node.js.
    * That is to say, `url` is there because of `http`, `freelist` is there because of `http`, etc.
  * Things that cannot be done outside of core, or only with significant pain such as `async_hooks`.

* Kontinuierliche Integration (CI) Testen:
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * Es wird nicht automatisch ausgeführt. Sie müssen es manuell starten.
  * Anmelden auf CI ist in GitHub integriert. Melde dich jetzt an!
  * Sie werden `node-test-pull-request` meistens verwenden. Gehe jetzt!
    * Lesezeichen beachten: <https://ci.nodejs.org/job/node-test-pull-request/>
  * Um zum Formular zu gelangen, klicken Sie auf `Erstellen mit Parametern`. (If you don't see it, that probably means you are not logged in!) Click it now! Jetzt klicken!
  * To start CI testing from this screen, you need to fill in two elements on the form:
    * Das Feld `ZERTIFY_SAFE` sollte aktiviert sein. By checking it, you are indicating that you have reviewed the code you are about to test and you are confident that it does not contain any malicious code. (We don't want people hijacking our CI hosts to attack other hosts on the internet, for example!)
    * The `PR_ID` box should be filled in with the number identifying the pull request containing the code you wish to test. For example, if the URL for the pull request is `https://github.com/nodejs/node/issues/7006`, then put `7006` in the `PR_ID`.
    * Die übrigen Elemente auf dem Formular sind typischerweise unverändert.
  * Wenn Sie Hilfe mit etwas CI im Zusammenhang benötigen:
    * Benutze #node-dev (IRC) um mit anderen Mitarbeitern zu sprechen.
    * Use #node-build (IRC) to talk to the Build WG members who maintain the CI infrastructure.
    * Use the [Build WG repo](https://github.com/nodejs/build) to file issues for the Build WG members who maintain the CI infrastructure.

## Landing PRs

Siehe Collaborator Guide: [Pull-Requests für Landing Pull][].

Commits in one PR that belong to one logical change should be squashed. It is rarely the case in onboarding exercises, so this needs to be pointed out separately during the onboarding.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Übung: Machen Sie einen PR, indem Sie sich zur README hinzufügen

* Example: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * For raw commit message: `git show --format=%Bb58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8`
* Mitarbeiter sind in alphabetischer Reihenfolge nach GitHub Benutzernamen.
* Optional können Sie auch Ihre persönlichen Worte angeben.
* Add the `Fixes: <collaborator-nomination-issue-url>` to the commit message so that when the commit lands, the nomination issue url will be automatically closed.
* Label your pull request with the `doc`, `notable-change`, and `fast-track` labels.
* CI auf dem PR ausführen. Verwende die `node-test-pull-request` CI-Aufgabe.
* After two Collaborator approvals for the change and two Collaborator approvals for fast-tracking, land the PR.
* Hinterlassen Sie einen Kommentar in der PR: `Bitte 👍 Dieser Kommentar genehmigt Schnellverfolgung`.
* If there are not enough approvals within a reasonable time, consider the single approval of the onboarding TSC member sufficient, and land the PR.
  * Be sure to add the `PR-URL: <full-pr-url>` and appropriate `Reviewed-By:` metadata.
  * [`node-core-utils`][] automates the generation of metadata and the landing process. Siehe die Dokumentation von [`git-node`][].
  * [`core-validate-commit`][] automatisiert die Validierung von Commit-Nachrichten. This will be run during `git node land --final` of the [`git-node`][] command.

## Schlussnotizen

* Don't worry about making mistakes: everybody makes them, there's a lot to internalize and that takes time (and we recognize that!)
* Fast jeder Fehler, den Sie machen könnten, kann behoben oder rückgängig gemacht werden.
* Die bestehenden Mitarbeiter vertrauen Ihnen und sind dankbar für Ihre Hilfe!
* Andere Repositorien:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/lesbarer Stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* The OpenJS Foundation hosts regular summits for active contributors to the Node.js project, where we have face-to-face discussions about our work on the project. The Foundation has travel funds to cover participants' expenses including accommodations, transportation, visa fees, etc. if needed. Check out the [summit](https://github.com/nodejs/summit) repository for details.

[Code of Conduct]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Pull-Requests für Landing Pull]: doc/guides/collaborator-guide.md#landing-pull-requests
[Publicizing or hiding organization membership]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`Autorenfertige`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[set up the credentials]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[two-factor authentication]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[using a TOTP mobile app]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
