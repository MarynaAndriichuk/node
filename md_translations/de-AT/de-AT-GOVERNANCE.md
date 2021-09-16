# Node.js Projektsteuerung

<!-- TOC -->

* [Tricker](#triagers)
* [Mitarbeiter](#collaborators)
  * [Mitarbeiteraktivitäten](#collaborator-activities)
* [Technischer Lenkungsausschuss](#technical-steering-committee)
  * [TSC Besprechungen](#tsc-meetings)
* [Nominierungen für Mitarbeiter](#collaborator-nominations)
  * [Einbinden](#onboarding)
* [Konsensus Suchprozess](#consensus-seeking-process)

<!-- /TOC -->

## Tricker

Triagers assess newly-opened issues in the nodejs/node and nodejs/help repositories. Derzeit gibt es kein GitHub Team für Triager.

Triagers haben:
* die Fähigkeit Probleme zu benennen
* die Möglichkeit, Themen zu kommentieren, zu schließen und neu zu öffnen

Sie:

* [Eine Anleitung für Triager](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Mitarbeiter

Node.js Core Collaborators pflegen das [nodejs/node][] GitHub Repository. Das GitHub Team für Node.js Core Collaborators ist @nodejs/collaborators. Mitarbeiter haben:

* Commit access to the [nodejs/node][] repository
* Zugriff auf die fortlaufende Integration von Node.js (CI)

Both Collaborators and non-Collaborators may propose changes to the Node.js source code. Der Mechanismus, um eine solche Änderung vorzuschlagen, ist eine GitHub Pull-Anfrage. Mitarbeiter überprüfen und verschmelzen (_landen_) Pull-Requests.

Zwei Mitarbeiter müssen einen Pull-Request genehmigen, bevor der Pull-Request landen kann. (One Collaborator approval is enough if the pull request has been open for more than 7 days.) Approving a pull request indicates that the Collaborator accepts responsibility for the change. Die Genehmigung eines Pull-Requests deutet darauf hin, dass der Mitarbeiter die Verantwortung für die Änderung übernimmt. Approval must be from Collaborators who are not authors of the change.

Wenn ein Mitarbeiter gegen eine vorgeschlagene Änderung ist, kann die Änderung nicht landen. The exception is if the TSC votes to approve the change despite the opposition. In der Regel ist die Einbeziehung des TSC unnötig. Often, discussions or further changes result in Collaborators removing their opposition.

Sie:

* [Liste der Kollaboratoren](./README.md#current-project-team-members)
* [Eine Anleitung für Mitarbeiter](./doc/guides/collaborator-guide.md)

### Mitarbeiteraktivitäten

* Hilfe für Benutzer und Anfänger
* Code-und Dokumentationsänderungen, die das Projekt verbessern
* Überprüfen und kommentieren von Tickets und Pull-Requests
* Teilnahme an Arbeitsgruppen
* Pull-Requests zusammenführen

The TSC can remove inactive Collaborators or provide them with _Emeritus_ status. Emeriti kann beantragen, dass der TSC diese wieder in den aktiven Status zurücksetzt.

## Technischer Lenkungsausschuss

Eine Teilmenge der Kollaboratoren bildet den Technischen Lenkungsausschuss (TSC). Der TSC hat die endgültige Befugnis für dieses Projekt, einschließlich:

* Technische Richtung
* Projektverwaltung und -prozess (einschließlich dieser Richtlinie)
* Spendenrichtlinie
* GitHub repository hosting
* Verhaltensrichtlinien
* Pflege der Liste der Kollaboratoren

The current list of TSC members is in [the project README](./README.md#current-project-team-members).

Die [TSC Charter][] regelt den Betrieb der TSC. All changes to the Charter need approval by the OpenJS Foundation Cross-Project Council (CPC).

### TSC Besprechungen

Der TSC trifft sich in einem Sprachkonferenzgespräch. Each year, the TSC elects a chair to run the meetings. The TSC streams its meetings for public viewing on YouTube or a similar service.

Die TSC-Agenda enthält Themen, die sich in einer Sackgasse befinden. The intention of the agenda is not to review or approve all patches. Collaborators review and approve patches on GitHub.

Any community member can create a GitHub issue asking that the TSC review something. If consensus-seeking fails for an issue, a Collaborator may apply the `tsc-agenda` label. Das wird zur Tagesordnung des TSC-Treffens hinzugefügt.

Before each TSC meeting, the meeting chair will share the agenda with members of the TSC. TSC members can also add items to the agenda at the beginning of each meeting. Der Sitzungsvorsitzende und der TSC können weder ein Veto einlegen noch Artikel entfernen.

Der TSC kann Personen zur Teilnahme an einer nicht stimmberechtigten Funktion einladen.

Während des Treffens sorgt der TSC-Vorsitz dafür, dass jemand Minuten braucht. After the meeting, the TSC chair ensures that someone opens a pull request with the minutes.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). The process in the issue tracker is:

* A TSC member opens an issue explaining the proposal/issue and @-mentions @nodejs/tsc.
* The proposal passes if, after 72 hours, there are two or more TSC approvals and no TSC opposition.
* Wenn es zu einer längeren Sackgasse kommt, kann ein TSC-Mitglied einen Antrag zur Abstimmung stellen.

## Nominierungen für Mitarbeiter

Bestehende Mitarbeiter können jemanden zum Mitarbeiter ernennen. Nominees should have significant and valuable contributions across the Node.js organization.

Um einen neuen Kollaborator zu nominieren, öffnen Sie ein Problem im [nodejs/node][] Repository. Geben Sie eine Zusammenfassung der Beiträge des Kandidaten an. Zum Beispiel:

* Commits im [nodejs/node][] repository.
  * Benutze den Link `https://github.com/nodejs/node/commits?author=GITHUB_ID`
* Pull-Requests und Issues, die im [nodejs/node][] Repository geöffnet wurden.
  * Benutze den Link `https://github.com/nodejs/node/issues?q=author:GITHUB_ID`
* Kommentare zu Pull-Requests und Problemen im [nodejs/node][] Repository
  * Benutze den Link `https://github.com/nodejs/node/issues?q=commenter:GITHUB_ID`
* Bewertungen bei Pull-Requests im [nodejs/node][] Repository
  * Benutze den Link `https://github.com/nodejs/node/pulls?q=reviewed-by:GITHUB_ID`
* Hilfe für Endbenutzer und Anfänger zur Verfügung gestellt
* Pull-Anfragen und Probleme, die während der Organisation Node.js geöffnet wurden
  * Benutze den Link  `https://github.com/search?q=author:GITHUB_ID+org:nodejs`
* Kommentare zu Pull-Requests und Problemen in der gesamten Node.js-Organisation
  * Benutze den Link `https://github.com/search?q=commenter:GITHUB_ID+org:nodejs`
* Participation in other projects, teams, and working groups of the Node.js organization
* Andere Teilnahme an der breiteren Node.js Community

Mention @nodejs/collaborators in the issue to notify other Collaborators about the nomination.

Die Nominierung geht voraus, wenn keine Mitarbeiter nach einer Woche dagegen sind. Otherwise, the nomination fails.

There are steps a nominator can take in advance to make a nomination as frictionless as possible. To request feedback from other Collaborators in private, use the [Collaborators discussion page][] (which only Collaborators may view). A nominator may also work with the nominee to improve their contribution profile.

Mitarbeiter könnten jemanden mit wertvollen Beiträgen übersehen. In that case, the contributor may open an issue or contact a Collaborator to request a nomination.

### Einbinden

Nach der Nominierung ist ein TSC Mitglied an Bord des neuen Mitarbeiters. See [the onboarding guide](./onboarding.md) for details of the onboarding process.

## Konsensus Suchprozess

The TSC follows a [Consensus Seeking][] decision-making model per the [TSC Charter][].

[Collaborators discussion page]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Consensus Seeking]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
