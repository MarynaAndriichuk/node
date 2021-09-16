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

Triagers bewerten neu geöffnete Probleme in Nodejs/node und nodejs/help Repositories. Derzeit gibt es kein GitHub Team für Triager. Derzeit gibt es kein GitHub Team für Triager.

Triagers haben:
* die Fähigkeit Probleme zu benennen
* die Möglichkeit, Themen zu kommentieren, zu schließen und neu zu öffnen

Sie:

* [Eine Anleitung für Triager](./doc/guides/contributing/issues.md#triaging-a-bug-report)

## Mitarbeiter

Node.js Core Collaborators pflegen das [nodejs/node][] GitHub Repository. Das GitHub Team für Node.js Core Collaborators ist @nodejs/collaborators. Mitarbeiter haben: Das GitHub Team für Node.js Core Collaborators ist @nodejs/collaborators. Mitarbeiter haben:

* Commit access to the [nodejs/node][] repository
* Zugriff auf die fortlaufende Integration von Node.js (CI)

Sowohl Mitarbeiter als auch Nicht-Mitarbeiter können Änderungen am Quellcode von Node.js vorschlagen. Der Mechanismus, um eine solche Änderung vorzuschlagen, ist eine GitHub Pull-Anfrage. Mitarbeiter überprüfen und verschmelzen (_landen_) Pull-Requests. Der Mechanismus, um eine solche Änderung vorzuschlagen, ist eine GitHub Pull-Anfrage. Mitarbeiter überprüfen und verschmelzen (_landen_) Pull-Requests.

Zwei Mitarbeiter müssen einen Pull-Request genehmigen, bevor der Pull-Request landen kann. (Eine Mitarbeiterfreigabe reicht aus, wenn der Pull-Request länger als 7 Tage geöffnet ist.) Die Genehmigung eines Pull-Requests bedeutet, dass der Mitarbeiter die Verantwortung für die Änderung übernimmt. Die Zustimmung muss von Mitarbeitern erteilt werden, die keine Autoren der Änderung sind. (Eine Mitarbeiterfreigabe reicht aus, wenn der Pull-Request länger als 7 Tage geöffnet ist.) Die Genehmigung eines Pull-Requests bedeutet, dass der Mitarbeiter die Verantwortung für die Änderung übernimmt. Die Zustimmung muss von Mitarbeitern erteilt werden, die keine Autoren der Änderung sind.

Wenn ein Mitarbeiter gegen eine vorgeschlagene Änderung ist, kann die Änderung nicht landen. Die Ausnahme ist, wenn der TSC trotz des Widerstands für die Annahme der Änderung stimmt. In der Regel ist die Einbeziehung des TSC unnötig. Oft führen Diskussionen oder weitere Änderungen dazu, dass Kollaborateure ihre Opposition aufheben. Die Ausnahme ist, wenn der TSC trotz des Widerstands für die Annahme der Änderung stimmt. In der Regel ist die Einbeziehung des TSC unnötig. Oft führen Diskussionen oder weitere Änderungen dazu, dass Kollaborateure ihre Opposition aufheben.

Sie:

* [Liste der Kollaboratoren](./README.md#current-project-team-members)
* [Eine Anleitung für Mitarbeiter](./doc/guides/collaborator-guide.md)

### Mitarbeiteraktivitäten

* Hilfe für Benutzer und Anfänger
* Code-und Dokumentationsänderungen, die das Projekt verbessern
* Überprüfen und kommentieren von Tickets und Pull-Requests
* Teilnahme an Arbeitsgruppen
* Pull-Requests zusammenführen

Der TSC kann inaktive Mitarbeiter entfernen oder mit dem _Emeritus_ Status versorgen. Emeriti kann beantragen, dass der TSC diese wieder in den aktiven Status zurücksetzt. Emeriti kann beantragen, dass der TSC diese wieder in den aktiven Status zurücksetzt.

## Technischer Lenkungsausschuss

Eine Teilmenge der Kollaboratoren bildet den Technischen Lenkungsausschuss (TSC). Eine Teilmenge der Kollaboratoren bildet den Technischen Lenkungsausschuss (TSC). Der TSC hat die endgültige Befugnis für dieses Projekt, einschließlich:

* Technische Richtung
* Projektverwaltung und -prozess (einschließlich dieser Richtlinie)
* Spendenrichtlinie
* GitHub repository hosting
* Verhaltensrichtlinien
* Pflege der Liste der Kollaboratoren

Die aktuelle Liste der TSC Mitglieder ist in [das Projekt README](./README.md#current-project-team-members).

Die [TSC Charter][] regelt den Betrieb der TSC. Die [TSC Charter][] regelt den Betrieb der TSC. Alle Änderungen an der Charta bedürfen der Zustimmung des OpenJS Foundation Cross-Project Council (CPC).

### TSC Besprechungen

Der TSC trifft sich in einem Sprachkonferenzgespräch. Jedes Jahr wählt der TSC einen Vorsitzenden für die Durchführung der Sitzungen. Der TSC trifft sich in einem Sprachkonferenzgespräch. Jedes Jahr wählt der TSC einen Vorsitzenden für die Durchführung der Sitzungen. Der TSC streamt seine Sitzungen für die öffentliche Betrachtung auf YouTube oder einem ähnlichen Dienst.

Die TSC-Agenda enthält Themen, die sich in einer Sackgasse befinden. Die TSC-Agenda enthält Themen, die sich in einer Sackgasse befinden. Die Tagesordnung zielt nicht darauf ab, alle Patches zu überprüfen oder zu genehmigen. Mitarbeiter überprüfen und genehmigen Patches auf GitHub. Mitarbeiter überprüfen und genehmigen Patches auf GitHub.

Jedes Mitglied der Community kann ein GitHub Problem erstellen, das eine Überprüfung des TSC verlangt. Wenn die Konsenssuche bei einem Thema scheitert, kann ein Mitarbeiter die Bezeichnung `tsc-agenda` anwenden. Das wird zur Tagesordnung des TSC-Treffens hinzugefügt. Wenn die Konsenssuche bei einem Thema scheitert, kann ein Mitarbeiter die Bezeichnung `tsc-agenda` anwenden. Das wird zur Tagesordnung des TSC-Treffens hinzugefügt.

Vor jedem TSC-Treffen teilt der Sitzungspräsident die Tagesordnung mit den Mitgliedern der TSC. Vor jedem TSC-Treffen teilt der Sitzungspräsident die Tagesordnung mit den Mitgliedern der TSC. TSC-Mitglieder können zu Beginn jeder Sitzung auch Punkte auf die Tagesordnung setzen. Der Sitzungsvorsitzende und der TSC können weder ein Veto einlegen noch Artikel entfernen. Der Sitzungsvorsitzende und der TSC können weder ein Veto einlegen noch Artikel entfernen.

Der TSC kann Personen zur Teilnahme an einer nicht stimmberechtigten Funktion einladen.

Während des Treffens sorgt der TSC-Vorsitz dafür, dass jemand Minuten braucht. Während des Treffens sorgt der TSC-Vorsitz dafür, dass jemand Minuten braucht. Nach der Sitzung stellt der TSC-Vorsitzende sicher, dass jemand einen Pull-Request mit dem Protokoll öffnet.

The TSC seeks to resolve as many issues as possible outside meetings using [the TSC issue tracker](https://github.com/nodejs/TSC/issues). Der Prozess im Issue-Tracker ist: Der Prozess im Issue-Tracker ist:

* Ein TSC-Mitglied öffnet ein Problem, das den Vorschlag/Ausgabe und @-Erwähnungen @nodejs/tsc erklärt.
* Der Vorschlag wird angenommen, wenn es nach 72 Stunden zwei oder mehr TSC-Zulassungen und keine TSC-Einwände gibt.
* Wenn es zu einer längeren Sackgasse kommt, kann ein TSC-Mitglied einen Antrag zur Abstimmung stellen.

## Nominierungen für Mitarbeiter

Bestehende Mitarbeiter können jemanden zum Mitarbeiter ernennen. Bestehende Mitarbeiter können jemanden zum Mitarbeiter ernennen. Nominees sollten bedeutende und wertvolle Beiträge in der Organisation Node.js haben.

Um einen neuen Kollaborator zu nominieren, öffnen Sie ein Problem im [nodejs/node][] Repository. Geben Sie eine Zusammenfassung der Beiträge des Kandidaten an. Zum Beispiel: Geben Sie eine Zusammenfassung der Beiträge des Kandidaten an. Zum Beispiel:

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
* Teilnahme an anderen Projekten, Teams und Arbeitsgruppen der Node.js Organisation
* Andere Teilnahme an der breiteren Node.js Community

Erwähnen Sie @nodejs/collaborators in der Ausgabe um andere Mitarbeiter über die Nominierung zu informieren.

Die Nominierung geht voraus, wenn keine Mitarbeiter nach einer Woche dagegen sind. Andernfalls scheitert die Nominierung. Andernfalls scheitert die Nominierung.

Es gibt Schritte, die ein Nominator im Voraus ergreifen kann, um eine Nominierung so reibungslos wie möglich zu gestalten. Es gibt Schritte, die ein Nominator im Voraus ergreifen kann, um eine Nominierung so reibungslos wie möglich zu gestalten. Um Rückmeldungen von anderen Mitarbeitern privat anzufordern, verwenden Sie die [Kollaboratoren-Diskussionsseite][] (nur Kollaboratoren können sie ansehen). Ein Nominator kann auch mit dem Nominierten zusammenarbeiten, um ihr Beitragsprofil zu verbessern. Ein Nominator kann auch mit dem Nominierten zusammenarbeiten, um ihr Beitragsprofil zu verbessern.

Mitarbeiter könnten jemanden mit wertvollen Beiträgen übersehen. Mitarbeiter könnten jemanden mit wertvollen Beiträgen übersehen. In diesem Fall kann der Mitwirkende ein Problem aufwerfen oder einen Mitarbeiter kontaktieren, um eine Nominierung zu beantragen.

### Einbinden

Nach der Nominierung ist ein TSC Mitglied an Bord des neuen Mitarbeiters. Siehe [den Onboarding-Leitfaden](./onboarding.md) für Details zum Onboarding-Prozess. Siehe [den Onboarding-Leitfaden](./onboarding.md) für Details zum Onboarding-Prozess.

## Konsensus Suchprozess

Der TSC folgt einem [Konsensus Sucht][] Entscheidungsmodell nach [TSC Charter][].

[Kollaboratoren-Diskussionsseite]: https://github.com/orgs/nodejs/teams/collaborators/discussions
[Konsensus Sucht]: https://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[TSC Charter]: https://github.com/nodejs/TSC/blob/HEAD/TSC-Charter.md
[nodejs/node]: https://github.com/nodejs/node
