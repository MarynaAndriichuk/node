# Erstelle Node.js

Abhängig von der Plattform oder den Funktionen, die Sie benötigen, kann der Build-Prozess variieren. Nachdem Sie eine Binärdatei erstellt haben, können Sie die Testsuite ausführen, um zu bestätigen, dass die Binärdatei wie geplant funktioniert, ein guter nächster Schritt ist.

Wenn Sie einen Testfehler reproduzieren können, suchen Sie ihn im [Node.js Issue-Tracker](https://github.com/nodejs/node/issues) oder stellen Sie ein neues Problem ein.

## Inhaltsverzeichnis!

* [Unterstützte Platformen](#supported-platforms)
  * [Eingabe](#input)
  * [Strategie](#strategy)
  * [Plattformliste](#platform-list)
  * [Unterstützte Toolchains](#supported-toolchains)
  * [Offizielle binäre Plattformen und Toolchains](#official-binary-platforms-and-toolchains)
    * [OpenSSL asm Unterstützung](#openssl-asm-support)
  * [Vorherige Versionen dieses Dokuments](#previous-versions-of-this-document)
* [Erstelle Node.js auf unterstützten Plattformen](#building-nodejs-on-supported-platforms)
  * [Hinweis über Python](#note-about-python)
  * [Unix und MacOS](#unix-and-macos)
    * [Unix-Voraussetzungen](#unix-prerequisites)
    * [macOS prerequisites](#macos-prerequisites)
    * [Erstelle Node.js](#building-nodejs-1)
    * [Installiere Node.js](#installing-nodejs)
    * [Führende Tests](#running-tests)
    * [Laufende Abdeckung](#running-coverage)
    * [Dokumentation erstellen](#building-the-documentation)
    * [Debug-Build erstellen](#building-a-debug-build)
    * [Bau eines ASAN-Builds](#building-an-asan-build)
    * [Häufige Umbauten bei der Entwicklung beschleunigen](#speeding-up-frequent-rebuilds-when-developing)
    * [Fehlerbehebung von Unix- und MacOS-Versionen](#troubleshooting-unix-and-macos-builds)
  * [Fenster](#windows)
    * [Voraussetzungen](#prerequisites)
      * [Option 1: Manuelle Installation](#option-1-manual-install)
      * [Option 2: Automatisierte Installation mit Boxstarter](#option-2-automated-install-with-boxstarter)
    * [Erstelle Node.js](#building-nodejs-2)
  * [Android/Android-basierte Geräte (z.B. Firefox-OS)](#androidandroid-based-devices-eg-firefox-os)
* [`Intl` (ECMA-402) Unterstützung](#intl-ecma-402-support)
  * [Build mit vollständiger ICU-Unterstützung (alle Locales werden von ICU unterstützt)](#build-with-full-icu-support-all-locales-supported-by-icu)
    * [Unix/macOS](#unixmacos)
    * [Fenster](#windows-1)
  * [Trimmed: `small icu` (nur Englisch) Unterstützung](#trimmed-small-icu-english-only-support)
    * [Unix/macOS](#unixmacos-1)
    * [Fenster](#windows-2)
  * [Gebäude ohne Intl Unterstützung](#building-without-intl-support)
    * [Unix/macOS](#unixmacos-2)
    * [Fenster](#windows-3)
  * [Vorhandene ICU verwenden (nur Unix/macOS)](#use-existing-installed-icu-unixmacos-only)
  * [Baue mit einer bestimmten ICU](#build-with-a-specific-icu)
    * [Unix/macOS](#unixmacos-3)
    * [Fenster](#windows-4)
* [Erstelle Node.js mit FIPS-konformer OpenSSL](#building-nodejs-with-fips-compliant-openssl)
* [Erstelle Node.js mit externen Kernmodulen](#building-nodejs-with-external-core-modules)
  * [Unix/macOS](#unixmacos-4)
  * [Fenster](#windows-5)
* [Hinweis für nachgelagerte Distributoren von Node.js](#note-for-downstream-distributors-of-nodejs)

## Unterstützte Platformen

Diese Liste der unterstützten Plattformen ist aktuell ab dem Branch/Release, zu dem sie gehört.

### Input

Node.js setzt auf V8 und libuv. Wir nehmen eine Teilmenge ihrer unterstützten Plattformen an.

### Strategie

Es gibt drei Unterstützungsstufen:

* **Stufe 1**: Diese Plattformen repräsentieren die Mehrheit der Benutzer von Node.js. Die Node.js Build Working Group unterhält die Infrastruktur für die vollständige Testabdeckung. Testfehler auf den Plattformen Stufe 1 blockieren Releases.
* **Stufe 2**: Diese Plattformen repräsentieren kleinere Segmente der Benutzerbasis Node.js. Die Node.js Build Working Group unterhält die Infrastruktur für die vollständige Testabdeckung. Testfehler auf Ebene 2 Plattformen blockieren Releases. Infrastrukturprobleme könnten die Veröffentlichung von Binärdateien für diese Plattformen verzögern.
* **Experimentell**: Kann nicht kompilieren oder Testsuite nicht bestehen. Das Kernteam erstellt keine Releases für diese Plattformen. Testfehler auf experimentellen Plattformen blockieren keine Releases. Beiträge zur Verbesserung der Unterstützung dieser Plattformen sind willkommen.

Plattformen können sich zwischen den Stufen zwischen den Hauptauslöserlinien bewegen. Die folgende Tabelle wird diese Änderungen widerspiegeln.

### Plattformliste

Die Unterstützung zur Kompilierung/Ausführung von Node.js hängt von Betriebssystem, Architektur und libc-Version ab. Die folgende Tabelle listet die Unterstützungsstufe für jede unterstützte Kombination auf. Eine Liste von [unterstützten Kompilierungstoolchains](#supported-toolchains) wird auch für Ebene 1 Plattformen geliefert.

**Führen Sie für Produktionsanwendungen nur Node.js auf unterstützten Plattformen aus.**

Node.js unterstützt keine Plattform-Version, wenn ein Hersteller die Unterstützung abgelaufen ist. Mit anderen Worten: Node.js unterstützt nicht das Ausführen auf End-of-Life (EoL) Plattformen. Dies gilt unabhängig von den Einträgen in der nachstehenden Tabelle.

| Betriebssystem | Architekturen    | Versionen                       | Support-Typ                                                        | Notizen                                                                     |
| -------------- | ---------------- | ------------------------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| GNU/Linux      | x64              | kernel >= 3.10, glibc >= 2.17   | Rang 1                                                             | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, Debian 9, EL 7 <sup>[2](#fn2)</sup> |
| GNU/Linux      | x64              | kernel >= 3.10, musl >= 1.1.19  | Experimentell                                                      | e.g. Alpine 3.8                                                             |
| GNU/Linux      | x86              | kernel >= 3.10, glibc >= 2.17   | Experimentell                                                      | Herabgestuft ab Node.js 10                                                  |
| GNU/Linux      | arm64            | kernel >= 4.5, glibc >= 2.17    | Rang 1                                                             | e.g. Ubuntu 16.04, Debian 9, EL 7 <sup>[3](#fn3)</sup>                      |
| GNU/Linux      | armv7            | Kernel >= 4.14, glibc >= 2.24   | Rang 1                                                             | e.g. Ubuntu 18.04, Debian 9                                                 |
| GNU/Linux      | armv6            | Kernel >= 4.14, glibc >= 2.24   | Experimentell                                                      | Herabgestuft ab Node.js 12                                                  |
| GNU/Linux      | ppc64le >=power8 | kernel >= 3.10.0, glibc >= 2.17 | Rang 2                                                             | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, EL 7  <sup>[2](#fn2)</sup>          |
| GNU/Linux      | s390x            | kernel >= 3.10.0, glibc >= 2.17 | Rang 2                                                             | e.g. EL 7 <sup>[2](#fn2)</sup>                                              |
| Fenster        | x64, x86 (WoW64) | >= Windows 8.1/2012 R2          | Rang 1                                                             | <sup>[4](#fn4),[5](#fn5)</sup>                                              |
| Fenster        | x86 (nativ)      | >= Windows 8.1/2012 R2          | Stufe 1 (läuft) / Experimentell (Kompilieren) <sup>[6](#fn6)</sup> |                                                                             |
| Fenster        | x64, x86         | Windows Server 2012 (nicht R2)  | Experimentell                                                      |                                                                             |
| Fenster        | arm64            | >= Windows 10                   | Stufe 2 (Kompilierung) / Experimentell (läuft)                     |                                                                             |
| macOS          | x64              | >= 10.13                        | Rang 1                                                             |                                                                             |
| macOS          | arm64            | >= 11                           | Experimentell                                                      |                                                                             |
| SmartOS        | x64              | >= 18                           | Rang 2                                                             |                                                                             |
| AIX            | ppc64be >=power7 | >= 7.2 TL04                     | Rang 2                                                             |                                                                             |
| FreeBSD        | x64              | >= 11                           | Experimentell                                                      | Herabgestuft ab Node.js 12  <sup>[7](#fn7)</sup>                            |

<em id="fn1">1</em>: GCC 8 wird nicht auf der Basisplattform bereitgestellt. Benutzer benötigen die [Toolchain Test-Builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) oder ähnlich dem Quellcode eines neueren Compilers.

<em id="fn2">2</em>: GCC 8 wird nicht auf der Basisplattform bereitgestellt. Benutzer benötigen den [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) oder höher, um einen neueren Compiler zu erstellen.

<em id="fn3">3</em>: Ältere Kernel-Versionen können für ARM64 funktionieren. Die Node.js Test-Infrastruktur testet jedoch nur >= 4.5.

<em id="fn4">4</em>: Unter Windows, der Knoten wird ausgeführt. s in Windows-Terminal-Emulatoren wie `mintty` erfordert die Verwendung von [winpty](https://github.com/rprichard/winpty) für die Ttty-Kanäle (e. . `winpty node.exe script.js`). In "Git bash", wenn Sie den Knoten-Shell Alias (`Knoten` ohne `aufrufen. Axt` Erweiterung), `winzig` wird automatisch verwendet.

<em id="fn5">5</em>: Das Windows Subsystem für Linux (WSL) wird nicht unterstützt, aber der GNU/Linux-Build-Prozess und die Binärdateien sollten funktionieren. Die Community wird sich nur mit Problemen befassen, die auf nativen GNU/Linux-Systemen reproduzieren. Probleme, die nur auf WSL reproduzieren, sollten im [WSL Issue-Tracker](https://github.com/Microsoft/WSL/issues) gemeldet werden. Es wird nicht empfohlen, das Windows-Programm (`node.exe`) in WSL auszuführen. Ohne Problemumgehungen wie die Umleitung von Stdio wird es nicht funktionieren.

<em id="fn6">6</em>: Das Ausführen von Node.js auf x86 Windows sollte funktionieren und Binärdateien werden bereitgestellt. Allerdings laufen Tests in unserer Infrastruktur nur auf WoW64. Außerdem ist das Kompilieren auf x86 Windows experimentell und möglicherweise nicht möglich.

<em id="fn7">7</em>: Der Standard-FreeBSD 12.0 Compiler ist Clang 6.0.1, aber FreeBSD 12.1 aktualisiert auf 8.0.1. Andere Clang/LLVM-Versionen sind über den Paketmanager des Systems verfügbar, einschließlich Clang 9.0.

### Unterstützte Toolchains

Abhängig von der Hostplattform kann die Auswahl der Toolchains variieren.

| Betriebssystem | Compiler-Versionen                                                 |
| -------------- | ------------------------------------------------------------------ |
| Linux          | GCC >= 8.3                                                         |
| Fenster        | Visual Studio >= 2019 mit dem Windows 10 SDK auf einem 64-Bit-Host |
| macOS          | Xcode >= 11 (Apple LLVM >= 11)                                     |

### Offizielle binäre Plattformen und Toolchains

Binärdateien unter <https://nodejs.org/download/release/> werden erstellt am:

| Binärpaket              | Plattform und Toolchain                                                                                                      |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| aix-ppc64               | AIX 7.2 TL04 auf PPC64BE mit GCC 8                                                                                           |
| darwin-x64              | macOS 10.15, Xcode Kommandozeilenwerkzeuge 11 mit -mmacosx-version-min=10.13                                                 |
| darwin-arm64 (und .pkg) | macOS 11 (arm64), Xcode Kommandozeilenwerkzeuge 12 mit -mmacosx-version-min=10.13                                            |
| linux-arm64             | CentOS 7 mit devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                       |
| linux-armv7l            | Cross-kompiliert auf Ubuntu 18.04 x64 mit [benutzerdefinierten GCC-Toolchain](https://github.com/rvagg/rpi-newer-crosstools) |
| linux-ppc64le           | CentOS 7 mit devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                       |
| linux-s390x             | RHEL 7 mit devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                         |
| linux-x64               | CentOS 7 mit devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                       |
| win-x64 und win-x86     | Windows 2012 R2 (x64) mit Visual Studio 2019                                                                                 |

<em id="fn8">8</em>: Die Enterprise Linux devtoolset-8 erlaubt es uns, Binärdateien mit GCC 8 zu kompilieren, aber mit den glibc und libstdc++ Versionen der Host-Plattformen (CentOS 7 / RHEL 7). Daher sind auf diesen Systemen produzierte Binärdateien mit glibc >= 2.17 und libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). Diese sind auf Distributionen verfügbar, die nativ GCC 4.9 unterstützen, wie Ubuntu 14.04 und Debian 8.

#### OpenSSL asm Unterstützung

OpenSSL-1.1.1 benötigt die folgende Assembler-Version für die Verwendung von asm Unterstützung auf x86_64 und ia32.

Für die Verwendung von AVX-512

* gas (GNU Assembler) Version 2.26 oder höher
* nasm Version 2.11.8 oder höher unter Windows

AVX-512 ist für Skylake-X von OpenSSL-1.1.1 deaktiviert.

Für die Nutzung von AVX2

* gas (GNU Assembler) Version 2.23 oder höher
* Xcode Version 5.0 oder höher
* llvm Version 3.3 oder höher
* nasm Version 2.10 oder höher in Windows

Weitere Informationen finden Sie unter <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html>.

 Wenn Sie ohne eine der oben genannten kompilieren, verwenden Sie `configure` mit dem `--openssl-no-asm` Flag. Ansonsten wird `configure` fehlschlagen.

### Vorherige Versionen dieses Dokuments

Unterstützte Plattformen und Toolchains ändern sich mit jeder Hauptversion von Node.js. Dieses Dokument ist nur für die aktuelle Hauptversion von Node.js gültig. Frühere Versionen dieses Dokuments für ältere Versionen von Node.js:

* [Node.js 14](https://github.com/nodejs/node/blob/v14.x/BUILDING.md)
* [Node.js 12](https://github.com/nodejs/node/blob/v12.x/BUILDING.md)
* [Node.js 10](https://github.com/nodejs/node/blob/v10.x/BUILDING.md)

## Erstelle Node.js auf unterstützten Plattformen

### Hinweis über Python

Das Node.js Projekt unterstützt Python >= 3 für das Erstellen und Testen von Projekten.
### Unix und MacOS

#### Unix-Voraussetzungen

* `gcc` und `g++` >= 8.3 oder neuer, oder
* GNU Make 3.81 oder neuer
* Python 3.6, 3.7, 3.8 und 3.9 (siehe oben)

Installation über Linux Paket-Manager kann erreicht werden mit:

* Ubuntu, Debian: `sudo apt-get install python3 g++ make`
* Fedora: `sudo dnf install python3 gcc-c++ make`
* CentOS und RHEL: `sudo yum install python3 gcc-c++ make`
* OpenSUSE: `sudo zypper install python3 gcc-c++ make`
* Arch Linux, Manjaro: `sudo pacman -S python gcc make`

FreeBSD und OpenBSD Benutzer müssen möglicherweise auch `libexecinfo` installieren.

#### macOS prerequisites

* Xcode Befehlszeilenwerkzeuge >= 11 für macOS
* Python 3.6, 3.7, 3.8 und 3.9 (siehe oben)

macOS-Benutzer können die `Xcode Command Line Tools` installieren, indem Sie `xcode-select --install` ausführen. Alternativ, wenn Sie bereits den vollständigen Xcode installiert haben, Sie finden sie im Menü `Xcode -> Entwicklerwerkzeug öffnen ->
Weitere Entwicklerwerkzeuge. .`. Dieser Schritt wird `clang`, `clang++`und `make` installieren.

#### Erstelle Node.js

Wenn der Pfad zu Ihrem Build-Verzeichnis einen Leerzeichen enthält, wird der Build wahrscheinlich fehlschlagen.

Um Node.js zu bauen:

```console
$ ./configure
$ make -j4
```

Mit der Option `-j4` wird `make` 4 gleichzeitige Kompilierungsaufträge ausführen, was die Bauzeit reduzieren kann. Weitere Informationen finden Sie in der [GNU Make Documentation](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

Das obige erfordert, dass `python` mit einer unterstützten Version von Python auflöst. Siehe [Voraussetzungen](#prerequisites).

Nach dem Erstellen von [Firewall-Regeln](tools/macos-firewall.sh) können Popups, die eingehende Netzwerkverbindungen zulassen, beim Ausführen von Tests vermieden werden.

Das Ausführen des folgenden Skripts auf macOS fügt die Firewall-Regeln für den ausführbaren `Knoten` im `out` Verzeichnis und den symbolischen `Knoten` im Wurzelverzeichnis des Projekts hinzu.

```console
$ sudo ./tools/macos-firewall.sh
```

#### Installiere Node.js

Um diese Version von Node.js in ein Systemverzeichnis zu installieren:

```bash
[sudo] Installation erstellen
```

#### Führe Tests aus

Um das Build zu überprüfen:

```console
$make test-only
```

An dieser Stelle sind Sie bereit, Code-Änderungen vorzunehmen und die Tests erneut auszuführen.

Wenn Sie Tests ausführen, bevor Sie eine Pull Request einreichen, ist der empfohlene Befehl:

```console
$ make -j4 Test
```

`make -j4 test` führt eine vollständige Prüfung der Codebase durch, einschließlich der Durchführung von Linters und Dokumentationstests.

Stellen Sie sicher, dass der Linter keine Probleme meldet und dass alle Tests bestanden. Bitte senden Sie keine Patches, die entweder überprüft werden.

Wenn Sie den Linter ohne Tests ausführen wollen, verwenden Sie `make lint`/`vcbuild lint`. Es werden JavaScript, C++ und Markdown Dateien ausgegeben.

Wenn Sie Tests aktualisieren und Tests in einer einzelnen Testdatei ausführen möchten (z.B. `test/parallel/test-stream2-transform.js`):

```text
$ python tools/test.py test/parallel/test-stream2-transform.js
```

Sie können die gesamte Testreihe für ein bestimmtes Subsystem ausführen, indem Sie den Namen eines Subsystems angeben:

```text
$ python tools/test.py -J --mode=release Child-process
```

Wenn Sie die anderen Optionen überprüfen möchten, wenden Sie sich bitte an die Hilfe, indem Sie die `--help` Option verwenden:

```text
$ python tools/test.py --help
```

Sie können in der Regel Tests direkt mit Knoten ausführen:

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

Denken Sie daran, mit `make -j4` zwischen Testläufen neu zu kompilieren, wenn Sie Code in der `lib` oder `src` Verzeichnisse ändern.

Die Tests versuchen, die Unterstützung für IPv6 zu erkennen und IPv6 Tests gegebenenfalls auszuschließen. Wenn Ihre Haupt-Schnittstelle IPv6-Adressen hat, muss Ihre Loopback-Schnittstelle auch '::1' aktiviert sein. Für einige Standard-Installationen auf Ubuntu scheint dies nicht der Fall zu sein. Um '::1' auf dem Loopback-Interface auf Ubuntu zu aktivieren:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

Sie können [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) verwenden, um Tests auszuführen, falls Ihre IDE-Konfigurationen vorhanden sind.

#### Laufende Abdeckung

Es ist eine gute Praxis sicherzustellen, dass jeder Code, den Sie hinzufügen oder ändern, durch Tests abgedeckt wird. Sie können dies tun, indem Sie die Testsuite ausführen, bei der die Abdeckung aktiviert ist:

```console
$ ./configure --coverage
$ machen Deckung
```

Ein detaillierter Berichterstattungsbericht wird an `coverage/index.html` für die JavaScript-Berichterstattung und an `coverage/cxxcoverage.html` für C++-Berichterstattung geschrieben.

Wenn Sie nur die JavaScript-Tests ausführen wollen, müssen Sie nicht den ersten Befehl ausführen (`./configure --coverage`). Führe `coverage-run-js`aus, um JavaScript-Tests unabhängig von der C++ Testsuite auszuführen:

```text
$ make coverage-run-js
```

Wenn Sie Tests aktualisieren und eine einzelne Testdatei abdecken möchten (z.B. `test/parallel/test-stream2-transform.js`):

```text
$ make coverage-clean
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/parallel/test-stream2-transform.js
$ make coverage-report-js
```

Sie können die Abdeckung für die gesamte Testreihe für ein bestimmtes Subsystem erfassen, indem Sie den Namen eines Subsystems angeben:

```text
$ make coverage-clean
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py -J --mode=release child-process
$ make coverage-report-js
```

Der `erstellte Coverage` Befehl lädt einige Werkzeuge in das Projektverzeichnis herunter. Zur Bereinigung nach der Generierung der Berichte:

```console
$ Coverage-rein machen
```

#### Dokumentation erstellen

Um die Dokumentation zu erstellen:

Dies wird zuerst Node.js bauen (falls erforderlich) und dann verwenden, um die Dokumentation zu erstellen:

```bash
mach doc
```

Wenn du einen Node.js Build hast, kannst du nur die Dokumentation erstellen:

```bash
Knoten=/pfad/zu/knode nur doc-name erstellen
```

Um die Man-Seite zu lesen:

```bash
man doc/node.1
```

Wenn Sie die vollständige Dokumentation in einem Browser lesen möchten, führen Sie die folgende aus.

```bash
mach docserve
```

Dies wird einen statischen Dateiserver aufspucken und eine URL angeben, wo Sie die Dokumentation lokal durchsuchen können.

Wenn Sie sich die Dokumentation mit dem Programm ansehen, das Ihr Betriebssystem mit dem Standard-Webbrowser verknüpft hat, führen Sie Folgendes aus.

```bash
dokopen machen
```

Dies öffnet eine Datei-URL für eine einseitige Version aller durchsuchbaren HTML-Dokumente mit dem Standard-Browser.

Um zu testen, ob Node.js korrekt gebaut wurde:

```bash
./node -e "console.log('Hallo von Node.js ' + process.version)"
```

#### Debug-Build erstellen

Wenn Sie auf ein Problem stoßen, bei dem die Informationen des JS-Stack-Tracks nicht ausreichen oder wenn Sie vermuten, dass der Fehler außerhalb der JS VM passiert, können Sie versuchen, ein debug aktiviertes Binärprogramm zu erstellen:

```console
$ ./configure --debug
$ make -j4
```

`mache` mit `. configure --debug` erzeugt zwei Binärdateien, das reguläre Release eins in `out/Release/node` und ein Debug-Programm in `out/Debug/node`, nur die Version ist tatsächlich installiert, wenn Sie `make install` ausführen.

Um die Debug-Build mit allen normalen Abhängigkeiten zu verwenden, überschreiben Sie die Release-Version im Installationsverzeichnis:

``` console
$ make install PREFIX=/opt/node-debug/
$ cp -a -f out/Debug/node /opt/node-debug/node
```

Bei Verwendung der Debug-Binärdatei werden Kern-Dumps im Falle eines Absturzes erzeugt. Diese Kern-Dumps sind für das Debuggen nützlich, wenn sie mit der entsprechenden originalen Debug-Binärdatei und Systeminformationen zur Verfügung gestellt werden.

Beim Lesen des Core Dump benötigt `gdb` auf der gleichen Plattform, auf der der Core Dump erfasst wurde (z. 64-Bit `gdb` für `Knoten` auf einem 64-Bit-System erstellt Linux `gdb` für `Knoten` auf Linux gebaut) andernfalls werden Fehler wie `nicht im ausführbaren Format gefunden: Dateiformat nicht erkannt`.

Beispiel für die Erzeugung eines Backtrace aus dem Kerndump:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Bau eines ASAN-Builds

[ASAN](https://github.com/google/sanitizers) kann dabei helfen, verschiedene speicherbezogene Fehler zu erkennen. ASAN-Builds werden derzeit nur auf Linux unterstützt. Wenn Sie es unter Windows oder macOS überprüfen möchten oder eine konsistente Toolchain unter Linux wünschen, Sie können [Docker](https://www.docker.com/products/docker-desktop) ausprobieren (mit einem Bild wie `gengjiawen/node-build:2020-02-14`).

Die `--debug` ist nicht notwendig und wird Build und Testen verlangsamen, aber es kann Clear stacktrace anzeigen, wenn ASAN ein Problem trifft.

``` console
$ ./configure --debug --enable-asan && make -j4
$ make test-only
```

#### Häufige Umbauten bei der Entwicklung beschleunigen

Wenn Sie vorhaben, Node.js regelmäßig neu zu bauen, insbesondere wenn Sie mehrere Zweige verwenden, kann die Installation von `ccache` dazu beitragen, die Bauzeiten erheblich zu reduzieren. Einrichten mit:
```console
$ sudo apt install ccache # für Debian/Ubuntu, In den meisten Linux-Distributionen enthalten
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # fügen Sie zu Ihrer . rofile
$ export CXX="ccache g++" # zu Ihrem .profile hinzufügen
```
Dies ermöglicht nahezu sofortige Umbauten auch beim Wechsel von Zweigen.

Beim Ändern der JS Ebene in `lib`ist es möglich, sie extern zu laden, ohne die ausführbare Datei zu ändern:
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
Die resultierende Binärdatei enthält keine JS-Dateien und wird versuchen, sie aus dem angegebenen Verzeichnis zu laden. Der JS Debugger von Visual Studio Code unterstützt diese Konfiguration seit der November-2020-Version und erlaubt das Setzen von Haltepunkten.

#### Fehlerbehebung von Unix- und MacOS-Versionen

Veraltete Builds können manchmal dazu führen, dass `keine Fehler beim Erstellen gefunden wurden` haben. Dies und einige andere Probleme können mit `make distclean` gelöst werden. Das `misssaubere` Rezept entfernt aggressiv Artefakte. Du musst erneut bauen (`make -j4`). Da alle Build-Artefakte entfernt wurden, kann es viel mehr Zeit dauern als bisherige Builds. Außerdem entfernt `distclean` die Datei, die die Ergebnisse von `./configure` speichert. Wenn du `liefst.` mit nicht-Standard-Optionen konfigurieren (wie `--debug`), müssen Sie es erneut ausführen, bevor Sie `make -j4` aufrufen.

### Fenster

#### Voraussetzungen

##### Option 1: Manuelle Installation

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* Die "Desktop-Entwicklung mit C++"-Arbeitslast von [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) oder die "C++ Build-Tools"-Arbeitslast von [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), mit den voreingestellten optionalen Komponenten
* Grundlegende Unix-Werkzeuge, die für einige Tests benötigt werden, [Git für Windows](https://git-scm.com/download/win) enthält Git Bash und Werkzeuge, die im globalen `PATH` enthalten sein können.
* Der [NetWide Assembler](https://www.nasm.us/), für OpenSSL Assembler Module. Wenn nicht in der Standardposition installiert, muss es manuell zu `PATH` hinzugefügt werden. Ein Build mit der Option `openssl-no-asm` benötigt dies ebenso wenig wie ein Build-Targeting für ARM64 Windows.

Optionale Anforderungen, um das MSI-Installer-Paket zu erstellen:

* Das [WiX Toolset v3.11](https://wixtoolset.org/releases/) und die [Wix Toolset Visual Studio 2019 Erweiterung](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* Das [WiX Toolset v3.14](https://wixtoolset.org/releases/) wenn es für Windows 10 unter ARM (ARM64) erstellt wird

Optionale Voraussetzungen für das Kompilieren von Windows 10 auf ARM (ARM64):

* Visual Studio 15.9.0 oder neuer
* Visual Studio optionale Komponenten
  * Visual C++ Compiler und Bibliotheken für ARM64
  * Visual C++ ATL für ARM64
* Windows 10 SDK 10.0.17763.0 oder neuer

##### Option 2: Automatisierte Installation mit Boxstarter

Ein [Boxstarter](https://boxstarter.org/) Skript kann für das einfache Einrichten von Windows-Systemen mit allen erforderlichen Voraussetzungen für die Node.js Entwicklung verwendet werden. Dieses Skript installiert die folgenden [Chocolatey](https://chocolatey.org/) Pakete:

* [Git für Windows](https://chocolatey.org/packages/git) mit den `git` und Unix-Tools, die dem `PATH` hinzugefügt wurden
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) mit [Visual C++ Arbeitspensum](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [NetWide Assembler](https://chocolatey.org/packages/nasm)

Um die Node.js Voraussetzungen mit [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher)zu installieren, öffnen Sie <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> mit Internet Explorer oder Edge Browser auf dem Zielgerät.

Alternativ können Sie PowerShell verwenden. Führen Sie diese Befehle von einem erhöhten PowerShell-Terminal aus:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

Die gesamte Installation mit Boxstarter wird ca. 10 GB Festplattenplatz beanspruchen.

#### Erstelle Node.js

Wenn der Pfad zu Ihrem Build-Verzeichnis ein Leerzeichen oder ein Nicht-ASCII-Zeichen enthält, wird das Build wahrscheinlich fehlschlagen.

```console
> .\vcbuild
```

Um die Tests auszuführen:

```console
> .\vcbuild Test
```

Um zu testen, ob Node.js korrekt gebaut wurde:

```console
> Release\node -e "console.log('Hallo von Node.js', process.version)"
```

### Android/Android-basierte Geräte (z.B. Firefox-OS)

Android ist keine unterstützte Plattform. Patches zur Verbesserung des Android Builds sind willkommen. Es gibt keine Tests auf Android in der aktuellen kontinuierlichen Integrationsumgebung. Die Teilnahme von Menschen, die sich für die Verbesserung des Android Building, der Tests und der Unterstützung engagiert haben, wird gefördert.

Vergewissern Sie sich, dass Sie [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) zuvor in einem Ordner heruntergeladen und extrahiert haben. Dann ausführen:

```console
$ ./android-configure /path/zu/Ihr/android-ndk
$ make
```

## `Intl` (ECMA-402) Unterstützung

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) Unterstützung ist standardmäßig aktiviert.

### Build mit vollständiger ICU-Unterstützung (alle Locales werden von ICU unterstützt)

Dies ist die Standard-Option.

#### Unix/macOS

```console
$ ./configure --with-intl=full-icu
```

#### Fenster

```console
> .\vcbuild Full-icu
```

### Trimmed: `small icu` (nur Englisch) Unterstützung

 In dieser Konfiguration sind nur englische Daten enthalten, aber die `Intl` (ECMA-402) APIs.  Es muss keine Abhängigkeiten herunterladen, um zu funktionieren. Sie können zur Laufzeit vollständige Daten hinzufügen.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Fenster

```console
> .\vcbuild small-icu
```

### Gebäude ohne Intl Unterstützung

Das `Intl` Objekt wird nicht verfügbar sein, noch andere APIs wie `String.normalize`.

#### Unix/macOS

```console
$ ./configure --without-intl
```

#### Fenster

```console
> .\vcbuild ohne intl
```

### Vorhandene ICU verwenden (nur Unix/macOS)

```console
$ pkg-config --modversion icu-i18n && ./configure --with-intl=system-icu
```

Wenn Sie Cross-Compiler sind, muss Ihre `pkg-config` in der Lage sein, einen Pfad zu liefern, der sowohl für Ihre Host- als auch für Ihre Zielumgebungen funktioniert.

### Baue mit einer bestimmten ICU

Weitere ICU-Veröffentlichungen finden Sie unter [der ICU-Homepage](http://site.icu-project.org/download). Laden Sie die Datei mit dem Namen `icu4c-**##.#**-src.tgz` (oder `.zip`).

Um das Minimum empfohlene ICU zu überprüfen, führen Sie `./configure --help` aus und sehen Sie sich die Hilfe für die `--with-icu-source` Option an. Wenn die ICU-Version zu alt ist, wird während der Konfiguration eine Warnung ausgegeben.

#### Unix/macOS

Von einem bereits unverpackten ICU:

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/zu/icu
```

Von einem lokalen ICU-Tarball:

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/zu/icu.tgz
```

Von einer Ziel-URL:

```console
$ ./configure --with-intl=full-icu --with-icu-source=http://url/to/icu.tgz
```

#### Fenster

Neuste ICU nach `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (oder `. ip`) als `deps/icu` (Sie haben: `deps/icu/source/...`)

```console
> .\vcbuild Full-icu
```

## Erstelle Node.js mit FIPS-konformer OpenSSL

Die aktuelle Version von Node.js unterstützt keine FIPS, wenn statisch (die Standard) mit OpenSSL 1.1 verknüpft wird. aber für dynamisches Linken ist es möglich, FIPS mit dem Konfigurationsflag `--openssl-is-fips` zu aktivieren.

### Konfigurieren und Erstellen von Quictls/openssl für FIPS

Für quictls/openssl 3.0 ist es möglich, FIPS bei dynamischem Linking zu aktivieren. Node.js verwendet derzeit openssl-3.0.0+quic und kann wie folgt konfiguriert werden:
```console
$ git clone git@github.com:quictls/openssl.git
$ cd openssl
$ ./config --prefix=/path/to/install/dir/ shared enable-fips linux-x86_64
```
Dies kann mit den folgenden Befehlen kompiliert und installiert werden:
```console
$ make -j8
$ make install_ssldirs
$ make install_fips
```

Nachdem das FIPS-Modul und die Konfigurationsdatei durch die obige Anleitung installiert wurden, müssen wir auch `/path/to/install/dir/ssl/openssl aktualisieren. nf` um die generierte FIPS-Konfigurationsdatei zu verwenden (`fipsmodule.cnf`):
```text
.include fipsmodule. nf

# Liste der zu ladenden Provider,
[provider_sect]
default = default_sect
# Der Name der Fips-Sektion sollte mit dem Namen des Abschnitts im
# enthalten sein /path/to/install/dir/ssl/fipsmodule. nf.
fips = fips_sect

[default_sect]
aktivieren = 1
```

Im obigen Fall ist OpenSSL nicht im Standardverzeichnis installiert, deshalb müssen zwei Umgebungsvariablen gesetzt werden, `OPENSSL_CONF`, und `OPENSSL_MODULES` , die auf die OpenSSL-Konfigurationsdatei und das Verzeichnis verweisen, in dem sich OpenSSL-Module befinden:
```console
$ export OPENSSL_CONF=/path/to/install/dir/ssl/openssl.cnf
$ export OPENSSL_MODULES=/path/to/install/dir/lib/ossl-module
```

Node.js können dann konfiguriert werden, um FIPS zu aktivieren:
```console
$ ./configure --shared-openssl --shared-openssl-libpath=/path/to/install/dir/lib --shared-openssl-includes=/path/to/install/dir/include --shared-openssl-libname=crypto,ssl --openssl-is-fips
$ export LD_LIBRARY_PATH=/path/to/install/dir/lib
$ make -j8
```

Die erzeugte ausführbare Datei überprüfen:
```console
$ ldd ./node
    linux-vdso.so.1 (0x00007ffd7917b000)
    libcrypto.so.81. => /path/to/install/dir/lib/libcrypto.so.81.3 (0x00007fd911321000)
    libssl.so.81. => /path/to/install/dir/lib/libssl.so.81.3 (0x00007fd91125e000)
    libdl.so. => /usr/lib64/libdl.so.2 (0x00007fd911232000)
    libstdc++.so.6 => /usr/lib64/libstdc++.so. (0x00007fd911039000)
    libm.so.6 => /usr/lib64/libm.so.6 (0x00007fd910ef3000)
    libgcc_s. o.1 => /usr/lib64/libgcc_s.so.1 (0x00007fd910ed9000)
    libpthread. o.0 => /usr/lib64/libpthread.so.0 (0x00007fd910eb5000)
    libc.so.6 => /usr/lib64/libc.so.6 (0x00007fd910cec000)
    /lib64/ld-linux-x86-64.so.2 (0x0000007fd9117f2000)
```
Wenn der `ldd` Befehl besagt, dass `libcrypto` nicht gefunden werden kann, muss man `LD_LIBRARY_PATH` setzen, um auf das obige Verzeichnis für `--shared-openssl-libpath` zu verweisen (siehe vorheriger Schritt).

Überprüfen Sie die OpenSSL-Version:
```console
$ ./node -p process.versions.openssl
3.0.0-alpha16+quic
```

Überprüfen Sie, ob FIPS verfügbar ist:
```console
$ ./node -p 'process.config.variables.openssl_is_fips'
true
$ ./node --enable-fips -p 'crypto.getFips()'
1
```

FIPS-Unterstützung kann dann über die OpenSSL-Konfigurationsdatei aktiviert werden oder mit `--enable-fips` oder `--force-fips` Kommandozeilenoptionen für den Knoten. s ausführbar. Siehe Abschnitt [FIPS mit den Optionen Node.js](#enabling-fips-using-node.js-options) und [Aktivieren von FIPS mit OpenSSL config](#enabling-fips-using-openssl-config) unten.

### Aktiviere FIPS mit Node.js Optionen
Dies geschieht unter Verwendung einer der Optionen Node.js `--enable-fips` oder `--force-fips`, zum Beispiel:
```console
$-Knoten --enable-fips -p 'crypto.getFips()'
```

### Aktiviere FIPS mit OpenSSL-Konfiguration
Dieses Beispiel zeigt, dass die OpenSSL-Konfigurationsdatei verwendet wird FIPS kann ohne Angabe der `--enable-fips` oder `--force-fips` Optionen aktiviert werden, indem `default_properties = fips=yes gesetzt wird` in der FIPS Konfigurationsdatei gesetzt wird. Siehe [Link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) für Details.

Damit dies funktioniert, muss die OpenSSL-Konfigurationsdatei (Standard openssl.cnf) aktualisiert werden. Das folgende Beispiel zeigt ein Beispiel:
```console
openssl_conf = openssl_init

.include /path/to/install/dir/ssl/fipsmodule. nf

[openssl_init]
providers = prov
alg_section = algorithm_sect

[prov]
fips = fips_sect
default = default_sect

[default_sect]
activate = 1

[algorithm_sect]
default_properties = fips=yes
```
Nach dieser Änderung kann Node.js ohne die `--enable-fips` oder `--force-fips` Optionen ausgeführt werden.

## Erstelle Node.js mit externen Kernmodulen

Es ist möglich, eine oder mehrere JavaScript-Textdateien anzugeben, die beim Erstellen von Node.js als eingebaute Module im Binärprogramm gebündelt werden sollen.

### Unix/macOS

Dieser Befehl wird `/root/myModule.js` unter `require('/root/myModule')` und `./myModule2.js` über `require('myModule2')` verfügbar machen.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Fenster

Um `./myModule.js` verfügbar zu machen via `require('myModule')` und `./myModule2.js` über `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Hinweis für nachgelagerte Distributoren von Node.js

Das Ökosystem von Node.js ist abhängig von der ABI-Kompatibilität innerhalb einer Hauptversion. Zur Aufrechterhaltung der ABI-Kompatibilität ist es erforderlich, dass verteilte Versionen von Node installiert werden. -Versionen mit der gleichen Version von Abhängigkeiten oder ähnlichen Versionen, die ihre ABI-Kompatibilität nicht beeinträchtigen, wie sie von Node veröffentlicht wurden. s für alle angegebenen `NODE_MODULE_VERSION` (befindet sich in `src/node_version.h`).

Wenn Node.js mit einem ABI gebaut wird, der nicht mit den offiziellen Node.js Builds kompatibel ist (z. unter Verwendung einer ABI inkompatiblen Version einer Abhängigkeit), bitte reservieren und verwenden Sie eine benutzerdefinierte `NODE_MODULE_VERSION` indem Sie einen Pull-Request gegen die Registry unter [https://github. om/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
