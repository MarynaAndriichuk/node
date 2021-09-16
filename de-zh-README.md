<!--lint disable no-literal-urls-->
<p align="center">
  <a href="https://nodejs.org/">
    <img
      alt="Node.js"
      src="https://nodejs.org/static/images/logo-light.svg"
      width="400"
    />
  </a>
</p>

Node.js ist eine plattformübergreifende JavaScript-Laufzeitumgebung. Es führt JavaScript-Code außerhalb eines Browsers aus. Weitere Informationen zur Verwendung von Node.js finden Sie auf der [Node.js Website][]. Es führt JavaScript-Code außerhalb eines Browsers aus. Weitere Informationen zur Verwendung von Node.js finden Sie auf der [Node.js Website][].

Das Node.js Projekt verwendet ein [offenes Governance-Modell](./GOVERNANCE.md). Die [OpenJS Foundation][] unterstützt das Projekt. Die [OpenJS Foundation][] unterstützt das Projekt.

**Dieses Projekt ist an einen [Code of Conduct][] gebunden.**

# Inhaltsverzeichnis

* [Unterstützung](#support)
* [Freigabe-Typen](#release-types)
  * [Download](#download)
    * [Aktuelle und LTS-Versionen](#current-and-lts-releases)
    * [Nachts freigegeben](#nightly-releases)
    * [API-Dokumentation](#api-documentation)
  * [Binärdateien werden überprüft](#verifying-binaries)
* [Erstelle Node.js](#building-nodejs)
* [Sicherheit](#security)
* [Beitrag zu Node.js](#contributing-to-nodejs)
* [Aktuelle Projektteammitglieder](#current-project-team-members)
  * [TSC (Technischer Lenkungsausschuss)](#tsc-technical-steering-committee)
  * [Mitarbeiter](#collaborators)
  * [Freigabeschlüssel](#release-keys)
* [Lizenz](#license)

## Unterstützung

Auf der Suche nach Hilfe? Auf der Suche nach Hilfe? Schauen Sie sich die [Anweisungen für den Support](.github/SUPPORT.md) an.

## Freigabe-Typen

* **Aktuell**: In aktiver Entwicklung. **Aktuell**: In aktiver Entwicklung. Der Code für die aktuelle Version ist im Zweig für seine Hauptversionsnummer (z.B. [v15.x](https://github.com/nodejs/node/tree/v15.x)). Node.js veröffentlicht alle 6 Monate eine neue Hauptversion, die es erlaubt, Änderungen zu brechen. Das geschieht jedes Jahr im April und Oktober. Veröffentlichungen erscheinen jeden Oktober haben eine Unterstützung Lebensdauer von 8 Monaten. Releases erscheinen jeden April in LTS (siehe unten) jeden Oktober. Node.js veröffentlicht alle 6 Monate eine neue Hauptversion, die es erlaubt, Änderungen zu brechen. Das geschieht jedes Jahr im April und Oktober. Veröffentlichungen erscheinen jeden Oktober haben eine Unterstützung Lebensdauer von 8 Monaten. Releases erscheinen jeden April in LTS (siehe unten) jeden Oktober.
* **LTS**: Releases, die Langzeitunterstützung erhalten, mit einem Schwerpunkt auf Stabilität und Sicherheit. Jede gleich nummerierte Hauptversion wird zu einer LTS-Version. LTS Freigaben erhalten 12 Monate _Active LTS_ Support und weitere 18 Monate _Wartung_. LTS Release-Zeilen haben alphabetisch sortierte Code-Namen, beginnend mit v4 Argon. Es gibt keine kaputten Änderungen oder Feature-Ergänzungen, außer unter bestimmten besonderen Umständen. Jede gleich nummerierte Hauptversion wird zu einer LTS-Version. LTS Freigaben erhalten 12 Monate _Active LTS_ Support und weitere 18 Monate _Wartung_. LTS Release-Zeilen haben alphabetisch sortierte Code-Namen, beginnend mit v4 Argon. Es gibt keine kaputten Änderungen oder Feature-Ergänzungen, außer unter bestimmten besonderen Umständen.
* **Nachts**: Code aus dem aktuellen Zweig, alle 24 Stunden gebaut, wenn es Änderungen gibt. Mit Vorsicht verwenden. Mit Vorsicht verwenden.

Aktuelle und LTS-Versionen folgen [Semantische Versionierung](https://semver.org). Ein Mitglied des Release-Teams [signiert](#release-keys) jede aktuelle und LTS-Release. Weitere Informationen finden Sie in der [Release README](https://github.com/nodejs/Release#readme). Ein Mitglied des Release-Teams [signiert](#release-keys) jede aktuelle und LTS-Release. Weitere Informationen finden Sie in der [Release README](https://github.com/nodejs/Release#readme).

### Download

Binärdateien, Installateure und Quell-Tarballs sind unter <https://nodejs.org/en/download/> verfügbar.

#### Aktuelle und LTS-Versionen
<https://nodejs.org/download/release/>

Das [neueste](https://nodejs.org/download/release/latest/) Verzeichnis ist ein Alias für die aktuelle Version. Das neueste_Codename_ Verzeichnis ist ein Alias für die neueste Version einer LTS-Zeile. Zum Beispiel enthält das Verzeichnis [latest-fermium](https://nodejs.org/download/release/latest-fermium/) die neueste Version von Fermium (Node.js 14). Das neueste_Codename_ Verzeichnis ist ein Alias für die neueste Version einer LTS-Zeile. Zum Beispiel enthält das Verzeichnis [latest-fermium](https://nodejs.org/download/release/latest-fermium/) die neueste Version von Fermium (Node.js 14).

#### Nachts freigegeben
[https://nodejs.org/download/nachts/](https://nodejs.org/download/nightly/)

Jeder Verzeichnisname und Dateiname enthält ein Datum (in UTC) und die Commit-SHA im HEAD der Veröffentlichung.

#### API-Dokumentation

Dokumentation für die aktuelle Version ist unter <https://nodejs.org/api/>. Versionsspezifische Dokumentation ist in jedem Release-Verzeichnis in der _Dokumentation_ verfügbar. Versionsspezifische Dokumentation finden Sie auch unter <https://nodejs.org/download/docs/>. Versionsspezifische Dokumentation ist in jedem Release-Verzeichnis in der _Dokumentation_ verfügbar. Versionsspezifische Dokumentation finden Sie auch unter <https://nodejs.org/download/docs/>.

### Binärdateien werden überprüft

Downloadverzeichnisse enthalten eine `SHASUMS256.txt` Datei mit SHA Prüfsummen für die Dateien.

Um `SHASUMS256.txt` mit `curl` herunterzuladen:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt
```

Um zu überprüfen, ob eine heruntergeladene Datei mit der Prüfsumme übereinstimmt, führen Sie diese durch `sha256sum` mit einem Befehl aus:

```console
$ grep node-vx.y.z.tar.gz SHASUMS256.txt | sha256sum -c -
```

Für aktuelle und LTS ist die GPG-getrennte Signatur von `SHASUMS256.txt` in `SHASUMS256.txt.sig`. Sie können es mit `gpg` verwenden, um die Integrität von `SHASUMS256.txt` zu überprüfen. Du musst zuerst [die GPG-Schlüssel von Personen importieren, die berechtigt sind, Veröffentlichungen zu erstellen](#release-keys). Um die Schlüssel zu importieren: Sie können sie mit `gpg` verwenden, um die Integrität von `SHASUMS256.txt` zu überprüfen. Du musst zuerst [die GPG-Schlüssel von Personen importieren, die berechtigt sind, Veröffentlichungen zu erstellen](#release-keys). Um die Schlüssel zu importieren:

```console
$ gpg --keyserver pool.sks-keyservers.net --recv-keys DD8F2338BAE7501E3D5AC78C273792F7D83545D
```

Im unteren Teil dieser README finden Sie ein komplettes Skript zum Importieren aktiver Release-Schlüssel.

Als nächstes laden Sie die `SHASUMS256.txt.sig` für die Veröffentlichung herunter:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt.sig
```

Benutzen Sie dann `gpg --verify SHASUMS256.txt.sig SHASUMS256.txt` um die Signatur der Datei zu überprüfen.

## Erstelle Node.js

Siehe [BUILDING.md](BUILDING.md) für Anweisungen, wie man Node.js aus dem Quellcode baut und eine Liste der unterstützten Plattformen.

## Sicherheit

Informationen zum Melden von Sicherheitslücken in Node.js finden Sie unter [SECURITY.md](./SECURITY.md).

## Beitrag zu Node.js

* [Beitrag zum Projekt][]
* [Arbeitsgruppen][]
* [Strategische Initiativen][]
* [Technische Werte und Priorisierung][]

## Aktuelle Projektteammitglieder

Informationen über die Steuerung des Node.js Projekts finden Sie unter [GOVERNANCE.md](./GOVERNANCE.md).

### TSC (Technischer Lenkungsausschuss)

<!--lint disable prohibited-strings-->
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (sie/sie)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (he/him)
* [ChALkeR](https://github.com/ChALkeR) - **Сковорода Никита Андрееви<unk>** &lt;chalkerx@gmail.com&gt; (he/him)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (he/him)
* [Codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (sie/sie)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (he/him)
* [danielleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (sie/sie)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [Gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (he/him)
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (he/him)
* [Joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (sie/sie)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (he/him)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (he/him)
* [mmarchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (sie/sie)
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (he/him)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [targos](https://github.com/targos) - **Michaël Zasso** &lt;targos@protonmail.com&gt; (he/him)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [Trott](https://github.com/Trott) - **Reich Trott** &lt;rtrott@gmail.com&gt; (he/him)

### TSC emeriti

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (sie/sie)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [Chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (he/him)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt;  (he/they)
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (he/him)
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [isaacs](https://github.com/isaacs) - **Isaac Z. Schlueter** &lt;i@izs.me&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [nebrius](https://github.com/nebrius) - **Bryan Hughes** &lt;bryan@nebri.us&gt;
* [von Robotern](https://github.com/ofrobots) - **Ali Ijaz Scheich** &lt;ofrobots@google.com&gt; (he/him)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [rvagg](https://github.com/rvagg) - **Rod Vagg** &lt;r@va.gg&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [Diebstahl](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (he/him)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (he/him)
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;

### Mitarbeiter

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (sie/sie)
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [ak239](https://github.com/ak239) - **Aleksei Koziatinskii** &lt;ak239spb@gmail.com&gt;
* [AndreasMadsen](https://github.com/AndreasMadsen) - **Andreas Madsen** &lt;amwebdk@gmail.com&gt; (he/him)
* [antsmartian](https://github.com/antsmartian) - **Anto Aravinth** &lt;anto.aravinth.cse@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [AshCripps](https://github.com/AshCripps) - **Ash Cripps** &lt;acripps@redhat.com&gt;
* [bcoe](https://github.com/bcoe) - **Ben Coe** &lt;bencoe@gmail.com&gt; (he/him)
* [Bengl](https://github.com/bengl) - **Bryan English** &lt;bryan@bryanenglish.com&gt; (he/him)
* [benjamingr](https://github.com/benjamingr) - **Benjamin Gruenbaum** &lt;benjamingr@gmail.com&gt;
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (sie/sie)
* [bmeck](https://github.com/bmeck) - **Bradley Farias** &lt;bradley.meck@gmail.com&gt;
* [bmeurer](https://github.com/bmeurer) - **Benedikt Meurer** &lt;benedikt.meurer@gmail.com&gt;
* [Knochenkull](https://github.com/boneskull) - **Christopher Hiller** &lt;boneskull@boneskull.com&gt; (he/him)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (he/him)
* [bzoz](https://github.com/bzoz) - **Bartosz Sosnowski** &lt;bartosz@janeasystems.com&gt;
* [cclauss](https://github.com/cclauss) - **christliche Klauseln** &lt;cclauss@me.com&gt; (he/him)
* [ChALkeR](https://github.com/ChALkeR) - **Сковорода Никита Андрееви<unk>** &lt;chalkerx@gmail.com&gt; (he/him)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (he/him)
* [Codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (sie/sie)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (he/him)
* [danielleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (sie/sie)
* [davisjam](https://github.com/davisjam) - **Jamie Davis** &lt;davisjam@vt.edu&gt; (he/him)
* [DerekNonGeneric](https://github.com/DerekNonGeneric) - **Derek Lewis** &lt;DerekNonGeneric@inf.is&gt; (he/him)
* [devnexen](https://github.com/devnexen) - **David Carlier** &lt;devnexen@gmail.com&gt;
* [devsnek](https://github.com/devsnek) - **Gus Caplan** &lt;me@gus.host&gt; (sie/sie)
* [dmabupt](https://github.com/dmabupt) - **Xu Meng** &lt;dmabupt@gmail.com&gt; (he/him)
* [dnlup](https://github.com/dnlup) **Daniele Belardi** &lt;dwon.dnl@gmail.com&gt; (he/him)
* [edsadr](https://github.com/edsadr) - **Adrian Estrada** &lt;edsadr@gmail.com&gt; (he/him)
* [eugeneo](https://github.com/eugeneo) - **Eugene Ostroukhov** &lt;eostroukhov@google.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (he/him)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt; (he/they)
* [Flarna](https://github.com/Flarna) - **Gerhard Stöbich** &lt;deb2001-github@yahoo.de&gt;  (he/they)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gdams](https://github.com/gdams) - **George Adams** &lt;george.adams@uk.ibm.com&gt; (he/him)
* [Geek](https://github.com/geek) - **Wyatt Preul** &lt;wpreul@gmail.com&gt;
* [gengjiawen](https://github.com/gengjiawen) - **Jiawen Geng** &lt;technicalcute@gmail.com&gt;
* [GeoffreyBooth](https://github.com/geoffreybooth) - **Geoffrey Stand** &lt;webmaster@geoffreybooth.com&gt; (he/him)
* [Gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (he/him)
* [Guybedford](https://github.com/guybedford) - **Guy Bedford** &lt;guybedford@gmail.com&gt; (he/him)
* [HarshithaKP](https://github.com/HarshithaKP) - **Harshitha K P** &lt;harshitha014@gmail.com&gt; (sie/sie)
* [hashseed](https://github.com/hashseed) - **Yang Guo** &lt;yangguo@chromium.org&gt; (he/him)
* [sich selbst65](https://github.com/himself65) - **Zeyu Yang** &lt;himself65@outlook.com&gt; (he/him)
* [hiroppy](https://github.com/hiroppy) - **Yuta Hiroto** &lt;hello@hiroppy.me&gt; (he/him)
* [iansu](https://github.com/iansu) - **Ian Sutherland** &lt;ian@iansutherland.ca&gt;
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [JacksonTian](https://github.com/JacksonTian) - **Jackson Tian** &lt;shyvo1987@gmail.com&gt;
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (he/him)
* [jdalton](https://github.com/jdalton) - **John-David Dalton** &lt;john.david.dalton@gmail.com&gt;
* [jkrems](https://github.com/jkrems) - **Jan Krems** &lt;jan.krems@gmail.com&gt; (he/him)
* [joaocgreis](https://github.com/joaocgreis) - **João Reis** &lt;reis@janeasystems.com&gt;
* [Joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (sie/sie)
* [Juanarbol](https://github.com/juanarbol) - **Juan Jose<unk> Arboleda** &lt;soyjuanarbol@gmail.com&gt; (he/him)
* [JungMinu](https://github.com/JungMinu) - **Minwoo Jung** &lt;nodecorelab@gmail.com&gt; (he/him)
* [Lanze](https://github.com/lance) - **Lance Ball** &lt;lball@redhat.com&gt; (he/him)
* [Legenden](https://github.com/legendecas) - **Chengzhong Wu** &lt;legendecas@gmail.com&gt; (he/him)
* [Leko](https://github.com/Leko) - **Shingo Inoue** &lt;leko.noor@gmail.com&gt; (he/him)
* [linkgoron](https://github.com/linkgoron) - **Nitzan Uziely** &lt;linkgoron@gmail.com&gt;
* [lpinca](https://github.com/lpinca) - **Luigi Pinca** &lt;luigipinca@gmail.com&gt; (he/him)
* [lundibundi](https://github.com/lundibundi) - **Denys Otrishko** &lt;shishugi@gmail.com&gt; (he/him)
* [Lxxyx](https://github.com/Lxxyx) - **Zijian Liu** &lt;lxxyxzj@gmail.com&gt; (he/him)
* [mafintosh](https://github.com/mafintosh) - **Mathias Buus** &lt;mathiasbuus@gmail.com&gt; (he/him)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (he/him)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (he/him)
* [miladfarca](https://github.com/miladfarca) - **Milad Fa** &lt;mfarazma@redhat.com&gt; (he/him)
* [mildsunrise](https://github.com/mildsunrise) - **Alba Mendez** &lt;me@alba.sh&gt; (sie/sie)
* [misterdjules](https://github.com/misterdjules) - **Julien Gilli** &lt;jgilli@nodejs.org&gt;
* [mmarchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (sie/sie)
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (he/him)
* [von Robotern](https://github.com/ofrobots) - **Ali Ijaz Scheich** &lt;ofrobots@google.com&gt; (he/him)
* [oyyd](https://github.com/oyyd) - **Ouyang Yadong** &lt;oyydoibh@gmail.com&gt; (he/him)
* [panva](https://github.com/panva) - **Filip Skokan** &lt;panva.ip@gmail.com&gt;
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja D P** &lt;Pooja.D.P@ibm.com&gt; (sie/sie)
* [puzpuzpuz](https://github.com/puzpuzpuz) - **Andrey Pechkurov** &lt;apechkurov@gmail.com&gt; (he/him)
* [Qard](https://github.com/Qard) - **Stephen Belanger** &lt;admin@stephenbelanger.com&gt; (he/him)
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt; (he/him)
* [refack](https://github.com/refack) - **Refael Ackermann (וו<unk> ו<unk> ו<unk> י)** &lt;refack@gmail.com&gt; (he/ihm/ווו/ו<unk> ר)
* [rexagod](https://github.com/rexagod) - **Pranshu Srivastava** &lt;rexagod@gmail.com&gt; (he/him)
* [richardlau](https://github.com/richardlau) - **Richard Lau** &lt;rlau@redhat.com&gt;
* [rickyes](https://github.com/rickyes) - **Ricky Zhou** &lt;0x19951125@gmail.com&gt; (he/him)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [rubys](https://github.com/rubys) - **Sam Ruby** &lt;rubys@intertwingly.net&gt;
* [ruyadorno](https://github.com/ruyadorno) - **Ruy Adorno** &lt;ruyadorno@github.com&gt; (he/him)
* [rvagg](https://github.com/rvagg) - **Rod Vagg** &lt;rod@vagg.org&gt;
* [ryzokuken](https://github.com/ryzokuken) - **Ujjwal Sharma** &lt;ryzokuken@disroot.org&gt; (he/him)
* [saghul](https://github.com/saghul) - **Saúl Ibarra Corretgé** &lt;saghul@gmail.com&gt;
* [santigimeno](https://github.com/santigimeno) - **Santiago Gimeno** &lt;santiago.gimeno@gmail.com&gt;
* [seishun](https://github.com/seishun) - **Nikolai Vavilov** &lt;vvnicholas@gmail.com&gt;
* [shisama](https://github.com/shisama) - **Masashi Hirano** &lt;shisama07@gmail.com&gt; (he/him)
* [silverwind](https://github.com/silverwind) - **Roman Reiss** &lt;me@silverwind.io&gt;
* [srl295](https://github.com/srl295) - **Steven R Loomis** &lt;srloomis@us.ibm.com&gt;
* [starkwang](https://github.com/starkwang) - **Weijia Wang** &lt;starkwang@126.com&gt;
* [sxa](https://github.com/sxa) - **Stewart X Addison** &lt;sxa@redhat.com&gt; (he/him)
* [targos](https://github.com/targos) - **Michaël Zasso** &lt;targos@protonmail.com&gt; (he/him)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (he/him)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [trivikr](https://github.com/trivikr) - **Trivikram Kamat** &lt;trivikr.dev@gmail.com&gt;
* [Trott](https://github.com/Trott) - **Reich Trott** &lt;rtrott@gmail.com&gt; (he/him)
* [vdeturckheim](https://github.com/vdeturckheim) - **Vladimir de Turckheim** &lt;vlad2t@hotmail.com&gt; (he/him)
* [watilde](https://github.com/watilde) - **Daijiro Wachi** &lt;daijiro.wachi@gmail.com&gt; (he/him)
* [watson](https://github.com/watson) - **Thomas Watson** &lt;w@tson.dk&gt;
* [XadillaX](https://github.com/XadillaX) - **Khaidi Chu** &lt;i@2333.moe&gt; (he/him)
* [yashLadha](https://github.com/yashLadha) - **Yash Ladha** &lt;yash@yashladha.in&gt; (he/him)
* [yhwang](https://github.com/yhwang) - **Yihong Wang** &lt;yh.wang@ibm.com&gt;
* [yorkie](https://github.com/yorkie) - **Yorkie Liu** &lt;yorkiefixer@gmail.com&gt;
* [yosuke-furukawa](https://github.com/yosuke-furukawa) - **Yosuke Furukawa** &lt;yosuke.furukawa@gmail.com&gt;
* [ZYSzys](https://github.com/ZYSzys) - **Yongsheng Zhang** &lt;zyszys98@gmail.com&gt; (he/him)

### Mitarbeiter emeriti

* [andrasq](https://github.com/andrasq) - **Andras** &lt;andras@kinvey.com&gt;
* [AnnaMag](https://github.com/AnnaMag) - **Anna M. Kedzierska** &lt;anna.m.kedzierska@gmail.com&gt;
* [aqrln](https://github.com/aqrln) - **Alexey Orlenko** &lt;eaglexrlnk@gmail.com&gt; (he/him)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [brendanashworth](https://github.com/brendanashworth) - **Brendan Ashworth** &lt;brendan.ashworth@me.com&gt;
* [calvinmetcalf](https://github.com/calvinmetcalf) - **Calvin Metcalf** &lt;calvin.metcalf@gmail.com&gt;
* [Chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [claudiorodriguez](https://github.com/claudiorodriguez) - **Claudio Rodriguez** &lt;cjrodr@yahoo.com&gt;
* [DavidCai1993](https://github.com/DavidCai1993) - **David Cai** &lt;davidcai1993@yahoo.com&gt; (he/him)
* [digitalinfinity](https://github.com/digitalinfinity) - **Hitesh Kanwathirtha** &lt;digitalinfinity@gmail.com&gt; (he/him)
* [eljefedelrodeodeljefe](https://github.com/eljefedelrodeodeljefe) - **Robert Jefe Lindstaedt** &lt;robert.lindstaedt@gmail.com&gt;
* [estliberitas](https://github.com/estliberitas) - **Alexander Makarenko** &lt;estliberitas@gmail.com&gt;
* [firedfox](https://github.com/firedfox) - **Daniel Wang** &lt;wangyang0123@gmail.com&gt;
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (he/him)
* [glentiki](https://github.com/glentiki) - **Glen Keane** &lt;glenkeane.94@gmail.com&gt; (he/him)
* [iarna](https://github.com/iarna) - **Rebecca Turner** &lt;me@re-becca.org&gt;
* [imran-iq](https://github.com/imran-iq) - **Imran Iqbal** &lt;imran@imraniqbal.org&gt;
* [imyller](https://github.com/imyller) - **Ilkka Myller** &lt;ilkka.myller@nodefield.com&gt;
* [isaacs](https://github.com/isaacs) - **Isaac Z. Schlueter** &lt;i@izs.me&gt;
* [italoacasas](https://github.com/italoacasas) - **Italo A. Casas** &lt;me@italoacasas.com&gt; (he/him)
* [jasongin](https://github.com/jasongin) - **Jason Ginchereau** &lt;jasongin@microsoft.com&gt;
* [jbergstroem](https://github.com/jbergstroem) - **Johan Bergström** &lt;bugs@bergstroem.nu&gt;
* [jhamhader](https://github.com/jhamhader) - **Yuval Brik** &lt;yuval@brik.org.il&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [julianduque](https://github.com/julianduque) - **Julian Duque** &lt;julianduquej@gmail.com&gt; (he/him)
* [Kfarnung](https://github.com/kfarnung) - **Kyle Farnung** &lt;kfarnung@microsoft.com&gt; (he/him)
* [kunalspathak](https://github.com/kunalspathak) - **Kunal Pathak** &lt;kunal.pathak@microsoft.com&gt;
* [lucamaraschi](https://github.com/lucamaraschi) - **Luca Maraschi** &lt;luca.maraschi@gmail.com&gt; (he/him)
* [lxe](https://github.com/lxe) - **Aleksey Smolenchuk** &lt;lxe@lxe.co&gt;
* [maclover7](https://github.com/maclover7) - **Jon Moss** &lt;me@jonathanmoss.me&gt; (he/him)
* [Matthewloring](https://github.com/matthewloring) - **Matthew Loring** &lt;mattloring@google.com&gt;
* [micnic](https://github.com/micnic) - **Nicu Micleus<unk> anu** &lt;micnic90@gmail.com&gt; (he/him)
* [mikeal](https://github.com/mikeal) - **Mikeal Rogers** &lt;mikeal.rogers@gmail.com&gt;
* [monsanto](https://github.com/monsanto) - **Christopher Monsanto** &lt;chris@monsan.to&gt;
* [MoonBall](https://github.com/MoonBall) - **Chen Gang** &lt;gangc.cxy@foxmail.com&gt;
* [nicht-an-aardvark](https://github.com/not-an-aardvark) - **Teddy Katz** &lt;teddy.katz@gmail.com&gt; (he/him)
* [Olegas](https://github.com/Olegas) - **Oleg Elifantiev** &lt;oleg@elifantiev.ru&gt;
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [othiym23](https://github.com/othiym23) - **Forrest L Norvell** &lt;ogd@aoaioxxysz.net&gt; (he/him)
* [petkaantonov](https://github.com/petkaantonov) - **Petka Antonov** &lt;petka_antonov@hotmail.com&gt;
* [Phillipj](https://github.com/phillipj) - **Phillip Johnsen** &lt;johphi@gmail.com&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [pmq20](https://github.com/pmq20) - **Minqi Pan** &lt;pmq2001@gmail.com&gt;
* [princejwesley](https://github.com/princejwesley) - **Prince John Wesley** &lt;princejohnwesley@gmail.com&gt;
* [psmarshall](https://github.com/psmarshall) - **Peter Marshall** &lt;petermarshall@chromium.org&gt; (he/him)
* [rlidwka](https://github.com/rlidwka) - **Alex Kocharin** &lt;alex@kocharin.ru&gt;
* [rmg](https://github.com/rmg) - **Ryan Graham** &lt;r.m.graham@gmail.com&gt;
* [robertkowalski](https://github.com/robertkowalski) - **Robert Kowalski** &lt;rok@kowalski.gd&gt;
* [romankl](https://github.com/romankl) - **Roman Klauke** &lt;romaaan.git@gmail.com&gt;
* [ronkorving](https://github.com/ronkorving) - **Ron Korving** &lt;ron@ronkorving.nl&gt;
* [RReverser](https://github.com/RReverser) - **Ingvar Stepanyan** &lt;me@rreverser.com&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [sebdeckers](https://github.com/sebdeckers) - **Sebastiaan Deckers** &lt;sebdeckers83@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [stefanmb](https://github.com/stefanmb) - **Stefan Budeanu** &lt;stefan@budeanu.com&gt;
* [tellnes](https://github.com/tellnes) - **Christian Tellnes** &lt;christian@tellnes.no&gt;
* [Diebstahl](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (he/him)
* [Thlorenz](https://github.com/thlorenz) - **Thorsten Lorenz** &lt;thlorenz@gmx.de&gt;
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;
* [tunniclm](https://github.com/tunniclm) - **Mike Tunnicliffe** &lt;m.j.tunnicliffe@gmail.com&gt;
* [vkurchatkin](https://github.com/vkurchatkin) - **Vladimir Kurchatkin** &lt;vladimir.kurchatkin@gmail.com&gt;
* [vsemozhetbyt](https://github.com/vsemozhetbyt) - **Vse Mozhet Byt** &lt;vsemozhetbyt@gmail.com&gt; (he/him)
* [whitlockjc](https://github.com/whitlockjc) - **Jeremy Whitlock** &lt;jwhitlock@apache.org&gt;
<!--lint enable prohibited-strings-->

Mitarbeiter folgen dem [Collaborator Guide](./doc/guides/collaborator-guide.md) bei der Pflege des Node.js Projekts.

### Tricker

* [Ayase-252](https://github.com/Ayase-252) - **Qingyu Deng** &lt;i@ayase-lab.com&gt;
* [marsonya](https://github.com/marsonya) - **Akhil Marsonya** &lt;akhil.marsonya27@gmail.com&gt; (he/him)
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja Durgad** &lt;Pooja.D.P@ibm.com&gt;
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt;

### Freigabeschlüssel

Primäre GPG-Schlüssel für Node.js Releaser (einige Releaser signieren mit Unterschlüssel):

* **Beth Griggs** &lt;bgriggs@redhat.com&gt; `4ED778F539E3634C779C87C6D7062848A1AB005C`
* **Colin Ihrig** &lt;cjihrig@gmail.com&gt; `94AE36675C464D64BAFA68DD7434390BDBE9B9C5`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `74F12602B6F1C4E913FAA37AD3A89613643B6201`
* **James M Snell** &lt;jasnell@keybase.io&gt; `71DCFD284A79C3B38668286BC97EC7A07EDE3FC1`
* **Michaël Zasso** &lt;targos@protonmail.com&gt; `8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600`
* **Myles Borins** &lt;myles.borins@gmail.com&gt; `C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8`
* **Richard Lau** &lt;rlau@redhat.com&gt; `C82FA3AE1CBEDC6BE46B9360C43CEC45C17AB93C`
* **Rod Vagg** &lt;rod@vagg.org&gt; `DD8F2338BAE7501E3DD5AC78C273792F7D83545D`
* **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; `A48C2BEE680E841632CD4E44F07496B3EB3C1762`
* **Ruy Adorno** &lt;ruyadorno@hotmail.com&gt; `108F52B48DB57BB0CC439B2997B01419BD92F80A`
* **Shelley Vohr** &lt;shelley.vohr@gmail.com&gt; `B9E2F5981AA6E0CD28160D9FF13993A75599653C`

Um den kompletten Satz vertrauenswürdiger Release-Schlüssel zu importieren (einschließlich Unterschlüssel, die möglicherweise zur Signierung von Releases verwendet werden):

```bash
gpg --keyserver pool.sks-keyservers.net --recv-keys 4ED778F539E3634C779C87C6D7062848A1AB005C
gpg --keyserver pool.sks-keyservers.net --recv-keys 94AE36675C464D64BAFA68DD7434390BDBE9B9C5
gpg --keyserver pool.sks-keyservers.net --recv-keys 74F12602B6F1C4E913FAA37AD3A89613643B6201
gpg --keyserver pool.sks-keyservers.net --recv-keys 71DCFD284A79C3B38668286BC97EC7A07EDE3FC1
gpg --keyserver pool.sks-keyservers.net --recv-keys 8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600
gpg --keyserver pool.sks-keyservers.net --recv-keys C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8
gpg --keyserver pool.sks-keyservers.net --recv-keys C82FA3AE1CBEDC6BE46B9360C43CEC45C17AB93C
gpg --keyserver pool.sks-keyservers.net --recv-keys DD8F2338BAE7501E3DD5AC78C273792F7D83545D
gpg --keyserver pool.sks-keyservers.net --recv-keys A48C2BEE680E841632CD4E44F07496B3EB3C1762
gpg --keyserver pool.sks-keyservers.net --recv-keys 108F52B48DB57BB0CC439B2997B01419BD92F80A
gpg --keyserver pool.sks-keyservers.net --recv-keys B9E2F5981AA6E0CD28160D9FF13993A75599653C
```

Siehe den obigen Abschnitt unter [Binärdateien verifizieren](#verifying-binaries) , wie Sie diese Schlüssel verwenden, um eine heruntergeladene Datei zu überprüfen.

Andere Schlüssel, die verwendet werden, um einige frühere Versionen zu signieren:

* **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt; `9554F04D7259F04124DE6B476D5A82AC7E37093B`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `1C050899334244A8AF75E53792EF661D867B9DFA`
* **Evan Lucas** &lt;evanlucas@me.com&gt; `B9AE9905FFD7803F25714661B63B535A4C206CA9`
* **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; `77984A986EBC2AA786BC0F66B01FBB92821C587A`
* **Isaac Z. Schlueter** &lt;i@izs.me&gt; `93C7E9E91B49E432C2F75674B0A78B0A6C481CF6`
* **Italo A. Casas** &lt;me@italoacasas.com&gt; `56730D5401028683275BD23C23EFEFE93C4CFFFE`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`

## Lizenz

Node.js steht unter der [MIT Lizenz](https://opensource.org/licenses/MIT) zur Verfügung. Node.js enthält auch externe Bibliotheken, die unter einer Vielzahl von Lizenzen verfügbar sind.  Den vollständigen Lizenztext finden Sie unter [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE). Node.js enthält auch externe Bibliotheken, die unter einer Vielzahl von Lizenzen verfügbar sind.  Den vollständigen Lizenztext finden Sie unter [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE).

[Code of Conduct]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Beitrag zum Projekt]: CONTRIBUTING.md
[Node.js Website]: https://nodejs.org/
[OpenJS Foundation]: https://openjsf.org/
[Strategische Initiativen]: https://github.com/nodejs/TSC/blob/HEAD/Strategic-Initiatives.md
[Technische Werte und Priorisierung]: doc/guides/technical-values.md
[Arbeitsgruppen]: https://github.com/nodejs/TSC/blob/HEAD/WORKING_GROUPS.md
