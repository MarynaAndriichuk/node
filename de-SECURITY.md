# Sicherheit

## Fehler in Node.js melden

Melde Sicherheitsfehler in Node.js über [HackerOne](https://hackerone.com/nodejs).

Ihr Bericht wird innerhalb von 24 Stunden bestätigt und Sie erhalten innerhalb von 48 Stunden eine detailliertere Antwort auf Ihren Bericht, die die nächsten Schritte bei der Bearbeitung Ihrer Einreichung angibt.

Nach der ersten Antwort auf Ihren Bericht das Sicherheitsteam wird sich bemühen, Sie über die Fortschritte auf dem Weg zu einer Korrektur und vollständigen Ankündigung auf dem Laufenden zu halten, und können zusätzliche Informationen oder Hinweise zu dem gemeldeten Problem anfordern.

### Node.js Bug Bounty Programm

Das Node.js Projekt engagiert sich in einem offiziellen Bug Bounty Programm für Sicherheitsforscher und verantwortliche öffentliche Enthüllungen.  Das Programm wird über die HackerOne Plattform verwaltet. Siehe <https://hackerone.com/nodejs> für weitere Details.

## Fehler in einem Drittanbieter-Modul melden

Sicherheitsfehler in Modulen von Drittanbietern sollten ihren jeweiligen Betreuern gemeldet werden und auch über den Knoten koordiniert werden. s Ecosystem Security Team via [HackerOne](https://hackerone.com/nodejs-ecosystem).

Details zu diesem Prozess finden Sie im [Arbeitsgruppen-Repository](https://github.com/nodejs/security-wg/blob/HEAD/processes/third_party_vuln_process.md).

Vielen Dank für die Verbesserung der Sicherheit von Node.js und seines Ökosystems. Ihre Bemühungen und die verantwortungsvolle Offenlegung werden sehr geschätzt und anerkannt.

## Offenlegungsrichtlinie

Hier ist die Sicherheits-Offenlegungsrichtlinie für Node.js

* Der Sicherheitsbericht wird empfangen und einem primären Handler zugewiesen. Diese Person koordiniert den Fix- und Release-Prozess. Das Problem wird bestätigt und eine Liste aller betroffenen Versionen ermittelt. Code wird geprüft, um mögliche ähnliche Probleme zu finden. Korrekturen sind für alle noch in Wartung befindlichen Veröffentlichungen vorbereitet. Diese Korrekturen werden nicht an das öffentliche Projektarchiv gebunden, sondern lokal bis zur Ankündigung gehalten.

* Ein empfohlenes Embargodatum für diese Verwundbarkeit wird gewählt und ein CVE (Common Vulnerabilities and Exposures (CVE®)) wird für die Verwundbarkeit angefordert.

* Am Embargo-Datum wird der Sicherheits-Mailingliste von Node.js eine Kopie der Ankündigung zugeschickt. Die Änderungen werden in das öffentliche Repository gepresst und neue Builds werden auf nodejs.org installiert. Innerhalb von 6 Stunden nach Bekanntgabe der Mailingliste wird eine Kopie der Ankündigungen im Blog Node.js veröffentlicht.

* Normalerweise wird das Embargodatum 72 Stunden ab der Ausstellung des Lebenslaufs festgelegt. Dies kann jedoch je nach der Schwere des Fehlers oder der Schwierigkeit bei der Anwendung eines Fehlers variieren.

* Dieser Prozess kann einige Zeit in Anspruch nehmen, insbesondere wenn die Koordination mit den Betreuern anderer Projekte erforderlich ist. Alle Anstrengungen werden unternommen, um den Fehler so rechtzeitig wie möglich zu behandeln; ist es jedoch wichtig, dass wir den oben genannten Release-Prozess verfolgen, um sicherzustellen, dass die Offenlegung in einer konsistenten Weise behandelt wird.

## Empfange Sicherheitsaktualisierungen

Sicherheitsbenachrichtigungen werden über die folgenden Methoden verteilt.

* <https://groups.google.com/group/nodejs-sec>
* [https://nodejs.org/de/blog/](https://nodejs.org/en/blog/)

## Kommentare zu dieser Richtlinie

Wenn Sie Vorschläge haben, wie dieser Prozess verbessert werden könnte, senden Sie bitte eine [Pull-Request](https://github.com/nodejs/nodejs.org) oder [ein Problem](https://github.com/nodejs/security-wg/issues/new) zur Diskussion ein.
