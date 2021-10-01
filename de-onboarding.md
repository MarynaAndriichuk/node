# Einbinden

Dieses Dokument ist ein Überblick über die Dinge, die wir neuen Mitarbeitern im Rahmen ihrer On-Board-Sitzung erzählen.

## Eine Woche vor der Onboarding-Sitzung

* Falls der neue Mitarbeiter noch kein Mitglied der GitHub Organisation ist, bestätigen Sie, dass er [Zwei-Faktor-Authentifizierung][] verwendet. Es wird nicht möglich sein, sie der Organisation hinzuzufügen, wenn sie keine Zwei-Faktor-Authentifizierung verwenden. Wenn sie SMS-Nachrichten von GitHub nicht erhalten können, versuchen Sie [mit einer TOTP Mobile App][].
* Melden Sie die angenommene Nominierung in einer TSC-Sitzung und in der TSC-Mailingliste an.
* Neue Collaborator-Installation vorschlagen [`node-core-utils`][] und [die Anmeldeinformationen][] dafür einrichten.

## Fünfzehn Minuten vor der Onboarding-Sitzung

* Fügen Sie vor der Onboarding-Sitzung den neuen Mitarbeiter [dem Mitarbeiterteam](https://github.com/orgs/nodejs/teams/collaborators) hinzu.
* Fragen Sie sie, ob sie einem Subsystem Team beitreten möchten. Siehe [Wer CC im Issue-Tracker][who-to-cc].

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
  * Mitgliedschaft: Erwägen Sie, Ihre Mitgliedschaft in der Organisation Node.js GitHub öffentlich zu machen. Dadurch wird die Identifizierung von Mitarbeitern erleichtert. Anweisungen wie dies zu tun ist, finden Sie unter [Organisationsmitgliedschaft öffentlich machen oder verstecken][].

* Benachrichtigungen:
  * [https://github.com/notifications](https://github.com/notifications) verwenden oder E-Mail einrichten
  * Das Beobachten des Haupt-Repos wird deinen Posteingang überfluten (mehrere hundert Benachrichtigungen an typischen Wochentagen), also sei vorbereitet

Das Projekt hat zwei Veranstaltungsorte für Diskussionen in Echtzeit:
* [`#nodejs-dev`](https://openjs-foundation.slack.com/archives/C019Y2T6STH) auf der [OpenJS Foundation](https://slack-invite.openjsf.org/)
* `#node-dev` auf [webchat.freenode.net](https://webchat.freenode.net/) ist ein großartiger Ort um mit dem TSC und anderen Mitarbeitern zu interagieren
  * Wenn es nach der Sitzung noch Fragen gibt, dann ist da ein guter Ort zum Nachfragen dabei!
  * Präsenz ist nicht obligatorisch, aber bitte schreibe eine Notiz dort, wenn zwangsweise zum `Meister` gedrückt wird

## Projektziele & Werte

* Mitarbeiter sind die Kollektivbesitzer des Projekts
  * Das Projekt hat die Ziele seiner Mitwirkenden

* Es gibt einige Ziele und Werte auf höherer Ebene
  * Empathie gegenüber Nutzern ist wichtig (dies ist zum Teil der Grund, warum wir Leute an Bord haben)
  * Generell: Versuchen Sie nett zu sein!
  * Das beste Ergebnis ist, dass Menschen, die zu unserem Issue-Tracker kommen, das Gefühl haben, dass sie wieder zurückkehren können.

* Es wird erwartet, dass Sie *folgen und* andere für den [Verhaltenskodex verantwortlich machen][].

## Fehlerverfolgung verwalten

* Du hast (meistens) kostenlos rein; zögere nicht, ein Problem zu schließen, wenn du sicher bist, dass es geschlossen werden sollte
  * Seien Sie nett über Schließungsprobleme! Lassen Sie die Menschen wissen, warum, und wenn nötig können Fragen und PRs wieder aufgegriffen werden

* [**Siehe "Labels"**](./doc/guides/onboarding-extras.md#labels)
  * Es gibt [einen Bot](https://github.com/nodejs-github-bot/github-bot) der die Label des Subsystems anwendet (z.B. `doc`, `Test`, `behauptet`, oder `Puffer`), so dass wir wissen, welche Teile des Codes die Pull-Requests modifiziert. Das ist natürlich nicht perfekt. Fühlen Sie sich frei, relevante Etiketten anzulegen und irrelevante Etiketten von Pull-Requests und Problemen zu entfernen.
  * `semver-{minor,major}`:
    * If a change has the remote *chance* of breaking something, use the `semver-major` label
    * Wenn Sie eine Bezeichnung `Semver-*` hinzufügen, fügen Sie einen Kommentar hinzu, der erklärt, warum Sie sie hinzufügen. Tun Sie es sofort, damit Sie nicht vergessen!
  * Bitte fügen Sie die [`Autorenfertige`][] Bezeichnung für PRs hinzu, falls zutreffend.

* Siehe [Wer CC im Issue-Tracker][who-to-cc].
  * Dies wird mit der Zeit natürlicher sein
  * Für viele der dort aufgelisteten Teams können Sie bei Interesse darum bitten, hinzugefügt zu werden
    * Einige sind WGs mit einem Prozess um Leute hinzuzufügen, andere sind nur für Benachrichtigungen vorhanden

* Wenn eine Diskussion erhitzt wird, Sie können verlangen, dass andere Mitarbeiter dies im Auge behalten, indem Sie ein Problem im privaten [nodejs/moderation](https://github.com/nodejs/moderation) repository öffnen.
  * Dies ist ein Repository auf das alle Mitglieder der `nodejs` GitHub Organisation (nicht nur Kollaboratoren im Node.js Kern) Zugriff haben. Sein Inhalt sollte nicht extern weitergegeben werden.
  * Die gesamte Moderationsrichtlinie [findest du hier](https://github.com/nodejs/admin/blob/HEAD/Moderation-Policy.md).

## Überprüfe PRs

* Das primäre Ziel ist es, die Codebase zu verbessern.
* Sekundär (aber nicht weit entfernt) ist es, dass die Person, die Code einreicht, erfolgreich ist. Ein Pull-Request von einem neuen Beitragenden ist eine Möglichkeit, die Gemeinschaft zu erweitern.
* Überprüfen Sie ein bisschen nach dem anderen. Überfordern Sie keine neuen Beitragszahler.
  * Es ist verlockend zur Mikrooptimierung. Nicht dieser Versuchung erliegen. Wir ändern oft V8. Techniken, die heute eine verbesserte Leistung bieten, können in Zukunft unnötig sein.
* Seien Sie sich bewusst: Ihre Meinung hat viel Gewicht!
* Nits (Anfragen für kleine Änderungen, die nicht unbedingt notwendig sind) sind in Ordnung, aber versuchen Sie, den Pull-Request nicht aufzuhalten.
  * Identifizieren Sie sie als Nits, wenn Sie kommentieren: `Nit: Ändern Sie foo() in bar().`
  * Wenn sie den Pull-Request blockieren, reparieren Sie ihn selbst beim Zusammenführen.
* Soweit es möglich ist, sollten Fragen nicht durch menschliche Überprüfer, sondern durch Werkzeuge ermittelt werden. Wenn Sie Kommentare zu Fragen hinterlassen, die durch Werkzeuge identifiziert werden könnten, aber nicht sind, sollten Sie die notwendigen Werkzeuge einführen.
* Minimale Wartezeit für Kommentare
  * Es gibt eine minimale Wartezeit, die wir versuchen, nicht triviale Veränderungen zu respektieren, so dass Menschen, die einen wichtigen Beitrag zu einem solchen verteilten Projekt leisten können, reagieren können.
  * Für nicht-triviale Änderungen lassen Sie den Pull-Request für mindestens 48 Stunden offen.
  * Wenn ein Pull-Request aufgegeben wird, prüfen Sie, ob es Sinn macht, ob Sie es übernommen haben (insbesondere, ob es nur noch Nits übrig hat).
* Änderung genehmigen
  * Mitarbeiter geben an, dass sie die Änderungen eines Pull-Requests mithilfe von GitHub Genehmigungsschnittstelle überprüft und genehmigt haben
  * Einige Leute kommentieren gern `LGTM` ("Scheint mir gut an")
  * Sie haben die Befugnis, die Arbeit eines anderen Mitarbeiters zu genehmigen.
  * Du kannst deine eigenen Pull-Requests nicht genehmigen.
  * Bei expliziter Verwendung von `angeforderten Änderungen`zeigen Einfühlungsvermögen an – Kommentare werden normalerweise behoben, auch wenn Sie sie nicht verwenden.
    * Wenn Sie dies tun, ist es schön, wenn Sie später verfügbar sind, um zu überprüfen, ob Ihre Kommentare angesprochen wurden
    * Wenn Sie sehen, dass die angeforderten Änderungen vorgenommen wurden, können Sie die `Änderungen eines anderen Mitarbeiters löschen:` Überprüfung.
    * Use `Changes requested` to indicate that you are considering some of your comments to block the PR from landing.

* Was gehört in Node.js:
  * Die Meinungen variieren – aus diesem Grund ist es gut, eine breite Mitarbeiterbasis zu haben!
  * Wenn Node.js es selbst braucht (aus historischen Gründen), dann gehört es in Node.js.
    * Das heißt, `url` ist da `http`, `Freelist` ist da `http`, etc.
  * Dinge, die nicht außerhalb des Kerns gemacht werden können, oder nur mit starken Schmerzen wie `async_hooks`.

* Kontinuierliche Integration (CI) Testen:
  * [https://ci.nodejs.org/](https://ci.nodejs.org/)
    * Es wird nicht automatisch ausgeführt. Sie müssen es manuell starten.
  * Anmelden auf CI ist in GitHub integriert. Melde dich jetzt an!
  * Sie werden `node-test-pull-request` meistens verwenden. Gehe jetzt!
    * Lesezeichen beachten: <https://ci.nodejs.org/job/node-test-pull-request/>
  * Um zum Formular zu gelangen, klicken Sie auf `Erstellen mit Parametern`. (Wenn du es nicht siehst, bedeutet das wahrscheinlich, dass du nicht eingeloggt bist!) Jetzt klicken!
  * Um CI-Tests von diesem Bildschirm aus zu starten, müssen Sie zwei Elemente des Formulars ausfüllen:
    * Das Feld `ZERTIFY_SAFE` sollte aktiviert sein. Durch Überprüfen Sie weisen darauf hin, dass Sie den zu testenden Code überprüft haben, und Sie sind zuversichtlich, dass er keinen bösartigen Code enthält. (Wir wollen nicht, dass Leute, die unsere CI-Hosts entführen, andere Hosts im Internet angreifen!)
    * Das Feld `PR_ID` sollte mit der Nummer ausgefüllt werden, die den Pull-Request identifiziert, der den Code enthält, den du testen möchtest. Wenn zum Beispiel die URL für den Pull-Request `https://github.com/nodejs/node/issues/7006`ist, dann setzen Sie `7006` in die `PR_ID`.
    * Die übrigen Elemente auf dem Formular sind typischerweise unverändert.
  * Wenn Sie Hilfe mit etwas CI im Zusammenhang benötigen:
    * Benutze #node-dev (IRC) um mit anderen Mitarbeitern zu sprechen.
    * Benutze #node-build (IRC) um mit den Build WG Mitgliedern zu sprechen, die die CI Infrastruktur pflegen.
    * Benutzen Sie den [Build WG Repo](https://github.com/nodejs/build) um Probleme für Build WG Mitglieder, die die CI Infrastruktur pflegen, einzureichen.

## Landing PRs

Siehe Collaborator Guide: [Pull-Requests für Landing Pull][].

Commits in einer PR, die zu einer logischen Änderung gehören, sollten zerquetscht werden. Das ist bei Onboarding-Übungen selten der Fall, daher muss dies während des Onboardings gesondert hervorgehoben werden.

<!-- TODO(joyeechueng): provide examples about "one logical change" -->

## Übung: Machen Sie einen PR, indem Sie sich zur README hinzufügen

* Beispiel: <https://github.com/nodejs/node/commit/b58fe52692659c0bc25ddbe6afa7f4ae2c7f14a8>
  * Für rohe Commit-Nachricht: `git show --format=%Bb58fe5269c0bc25ddbe6afa7f4ae2c7f14a8`
* Mitarbeiter sind in alphabetischer Reihenfolge nach GitHub Benutzernamen.
* Optional können Sie auch Ihre persönlichen Worte angeben.
* Fügen Sie die `Fixes: <collaborator-nomination-issue-url>` zur Commit-Nachricht hinzu, so dass die Nominierungs-Url automatisch geschlossen wird, wenn die Commit-Nachricht landet.
* Bezeichnen Sie Ihre Pull-Request mit dem `doc`, `Notabellenänderung`und `Schnellzug` Labels.
* CI auf dem PR ausführen. Verwende die `node-test-pull-request` CI-Aufgabe.
* Nach zwei Genehmigungen für die Änderung und zwei Genehmigungen für den Mitarbeiter zur Schnellverfolgung landen die PR.
* Hinterlassen Sie einen Kommentar in der PR: `Bitte 👍 Dieser Kommentar genehmigt Schnellverfolgung`.
* Wenn innerhalb einer angemessenen Frist nicht genügend Genehmigungen vorliegen, sollte die alleinige Zustimmung des TSC-Mitglieds ausreichend sein und die PR angelandet werden.
  * Achten Sie darauf, die `PR-URL hinzuzufügen: <full-pr-url>` und passend `Überprüft:` Metadaten.
  * [`node-core-utils`][] automatisiert die Generierung von Metadaten und den Landeprozess. Siehe die Dokumentation von [`git-node`][].
  * [`core-validate-commit`][] automatisiert die Validierung von Commit-Nachrichten. Dies wird während `git node land --final` des [`git-node`][] Befehls ausgeführt.

## Schlussnotizen

* Sorgen Sie sich nicht, Fehler zu machen: Jeder macht sie, es gibt viel zu verinnerlichen, und das braucht Zeit (und wir erkennen das!)
* Fast jeder Fehler, den Sie machen könnten, kann behoben oder rückgängig gemacht werden.
* Die bestehenden Mitarbeiter vertrauen Ihnen und sind dankbar für Ihre Hilfe!
* Andere Repositorien:
  * [https://github.com/nodejs/TSC](https://github.com/nodejs/TSC)
  * [https://github.com/nodejs/build](https://github.com/nodejs/build)
  * [https://github.com/nodejs/nodejs.org](https://github.com/nodejs/nodejs.org)
  * [https://github.com/nodejs/lesbarer Stream](https://github.com/nodejs/readable-stream)
  * [https://github.com/nodejs/LTS](https://github.com/nodejs/LTS)
  * [https://github.com/nodejs/citgm](https://github.com/nodejs/citgm)
* Die OpenJS Foundation veranstaltet regelmäßig Gipfeltreffen für aktive Mitwirkende am Node.js Projekt, auf denen wir persönliche Diskussionen über unsere Arbeit am Projekt führen. Die Stiftung verfügt über Reisekosten, um die Kosten der Teilnehmer zu decken, einschließlich Unterkünfte, Transport, Visagebühren usw. Schauen Sie sich das [Summit](https://github.com/nodejs/summit) Repository für Details an.

[Verhaltenskodex verantwortlich machen]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Pull-Requests für Landing Pull]: doc/guides/collaborator-guide.md#landing-pull-requests
[Organisationsmitgliedschaft öffentlich machen oder verstecken]: https://help.github.com/articles/publicizing-or-hiding-organization-membership/
[`Autorenfertige`]: doc/guides/collaborator-guide.md#author-ready-pull-requests
[`core-validate-commit`]: https://github.com/nodejs/core-validate-commit
[`git-node`]: https://github.com/nodejs/node-core-utils/blob/HEAD/docs/git-node.md
[`node-core-utils`]: https://github.com/nodejs/node-core-utils
[die Anmeldeinformationen]: https://github.com/nodejs/node-core-utils#setting-up-credentials
[Zwei-Faktor-Authentifizierung]: https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/
[mit einer TOTP Mobile App]: https://help.github.com/articles/configuring-two-factor-authentication-via-a-totp-mobile-app/
[who-to-cc]: doc/guides/collaborator-guide.md#who-to-cc-in-the-issue-tracker
