# Erstelle Node.js

Depending on what platform or features you need, the build process may differ. After you've built a binary, running the test suite to confirm that the binary works as intended is a good next step.

If you can reproduce a test failure, search for it in the [Node.js issue tracker](https://github.com/nodejs/node/issues) or file a new issue.

## Inhaltsverzeichnis

* [Unterstützte Plattformen](#supported-platforms)
  * [Input](#input)
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

## Unterstützte Plattformen

This list of supported platforms is current as of the branch/release to which it belongs.

### Input

Node.js setzt auf V8 und libuv. Wir nehmen eine Teilmenge ihrer unterstützten Plattformen an.

### Strategie

Es gibt drei Unterstützungsstufen:

* **Stufe 1**: Diese Plattformen repräsentieren die Mehrheit der Benutzer von Node.js. The Node.js Build Working Group maintains infrastructure for full test coverage. Testfehler auf den Plattformen Stufe 1 blockieren Releases.
* **Tier 2**: These platforms represent smaller segments of the Node.js user base. The Node.js Build Working Group maintains infrastructure for full test coverage. Testfehler auf Ebene 2 Plattformen blockieren Releases. Infrastrukturprobleme könnten die Veröffentlichung von Binärdateien für diese Plattformen verzögern.
* **Experimentell**: Kann nicht kompilieren oder Testsuite nicht bestehen. The core team does not create releases for these platforms. Test failures on experimental platforms do not block releases. Contributions to improve support for these platforms are welcome.

Plattformen können sich zwischen den Stufen zwischen den Hauptauslöserlinien bewegen. The table below will reflect those changes.

### Plattformliste

Node.js compilation/execution support depends on operating system, architecture, and libc version. The table below lists the support tier for each supported combination. A list of [supported compile toolchains](#supported-toolchains) is also supplied for tier 1 platforms.

**Führen Sie für Produktionsanwendungen nur Node.js auf unterstützten Plattformen aus.**

Node.js does not support a platform version if a vendor has expired support for it. In other words, Node.js does not support running on End-of-Life (EoL) platforms. Dies gilt unabhängig von den Einträgen in der nachstehenden Tabelle.

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

<em id="fn1">1</em>: GCC 8 wird nicht auf der Basisplattform bereitgestellt. Users will need the [Toolchain test builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) or similar to source a newer compiler.

<em id="fn2">2</em>: GCC 8 wird nicht auf der Basisplattform bereitgestellt. Users will need the [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) or later to source a newer compiler.

<em id="fn3">3</em>: Ältere Kernel-Versionen können für ARM64 funktionieren. However the Node.js test infrastructure only tests >= 4.5.

<em id="fn4">4</em>: On Windows, running Node.js in Windows terminal emulators like `mintty` requires the usage of [winpty](https://github.com/rprichard/winpty) for the tty channels to work (e.g. `winpty node.exe script.js`). In "Git bash" if you call the node shell alias (`node` without the `.exe` extension), `winpty` is used automatically.

<em id="fn5">5</em>: The Windows Subsystem for Linux (WSL) is not supported, but the GNU/Linux build process and binaries should work. The community will only address issues that reproduce on native GNU/Linux systems. Issues that only reproduce on WSL should be reported in the [WSL issue tracker](https://github.com/Microsoft/WSL/issues). Running the Windows binary (`node.exe`) in WSL is not recommended. It will not work without workarounds such as stdio redirection.

<em id="fn6">6</em>: Running Node.js on x86 Windows should work and binaries are provided. Allerdings laufen Tests in unserer Infrastruktur nur auf WoW64. Furthermore, compiling on x86 Windows is Experimental and may not be possible.

<em id="fn7">7</em>: The default FreeBSD 12.0 compiler is Clang 6.0.1, but FreeBSD 12.1 upgrades to 8.0.1. Other Clang/LLVM versions are available via the system's package manager, including Clang 9.0.

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

<em id="fn8">8</em>: The Enterprise Linux devtoolset-8 allows us to compile binaries with GCC 8 but linked to the glibc and libstdc++ versions of the host platforms (CentOS 7 / RHEL 7). Therefore, binaries produced on these systems are compatible with glibc >= 2.17 and libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). These are available on distributions natively supporting GCC 4.9, such as Ubuntu 14.04 and Debian 8.

#### OpenSSL asm Unterstützung

OpenSSL-1.1.1 requires the following assembler version for use of asm support on x86_64 and ia32.

Für die Verwendung von AVX-512

* gas (GNU Assembler) Version 2.26 oder höher
* nasm Version 2.11.8 oder höher unter Windows

AVX-512 ist für Skylake-X von OpenSSL-1.1.1 deaktiviert.

Für die Nutzung von AVX2

* gas (GNU Assembler) Version 2.23 oder höher
* Xcode Version 5.0 oder höher
* llvm Version 3.3 oder höher
* nasm Version 2.10 oder höher in Windows

Please refer to <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> for details.

 If compiling without one of the above, use `configure` with the `--openssl-no-asm` flag. Ansonsten wird `configure` fehlschlagen.

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

macOS users can install the `Xcode Command Line Tools` by running `xcode-select --install`. Alternatively, if you already have the full Xcode installed, you can find them under the menu `Xcode -> Open Developer Tool ->
More Developer Tools...`. This step will install `clang`, `clang++`, and `make`.

#### Erstelle Node.js

If the path to your build directory contains a space, the build will likely fail.

Um Node.js zu bauen:

```console
$ ./configure
$ make -j4
```

The `-j4` option will cause `make` to run 4 simultaneous compilation jobs which may reduce build time. For more information, see the [GNU Make Documentation](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

The above requires that `python` resolves to a supported version of Python. Siehe [Voraussetzungen](#prerequisites).

After building, setting up [firewall rules](tools/macos-firewall.sh) can avoid popups asking to accept incoming network connections when running tests.

Running the following script on macOS will add the firewall rules for the executable `node` in the `out` directory and the symbolic `node` link in the project's root directory.

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

If you are running tests before submitting a Pull Request, the recommended command is:

```console
$ make -j4 Test
```

`make -j4 test` does a full check on the codebase, including running linters and documentation tests.

Stellen Sie sicher, dass der Linter keine Probleme meldet und dass alle Tests bestanden. Please do not submit patches that fail either check.

If you want to run the linter without running tests, use `make lint`/`vcbuild lint`. Es werden JavaScript, C++ und Markdown Dateien ausgegeben.

If you are updating tests and want to run tests in a single test file (e.g. `test/parallel/test-stream2-transform.js`):

```text
$ python tools/test.py test/parallel/test-stream2-transform.js
```

You can execute the entire suite of tests for a given subsystem by providing the name of a subsystem:

```text
$ python tools/test.py -J --mode=release Child-process
```

If you want to check the other options, please refer to the help by using the `--help` option:

```text
$ python tools/test.py --help
```

Sie können in der Regel Tests direkt mit Knoten ausführen:

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

Remember to recompile with `make -j4` in between test runs if you change code in the `lib` or `src` directories.

The tests attempt to detect support for IPv6 and exclude IPv6 tests if appropriate. If your main interface has IPv6 addresses, then your loopback interface must also have '::1' enabled. For some default installations on Ubuntu that does not seem to be the case. To enable '::1' on the loopback interface on Ubuntu:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

You can use [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) to run/debug tests, if your IDE configs are present.

#### Laufende Abdeckung

Es ist eine gute Praxis sicherzustellen, dass jeder Code, den Sie hinzufügen oder ändern, durch Tests abgedeckt wird. Sie können dies tun, indem Sie die Testsuite ausführen, bei der die Abdeckung aktiviert ist:

```console
$ ./configure --coverage
$ machen Deckung
```

A detailed coverage report will be written to `coverage/index.html` for JavaScript coverage and to `coverage/cxxcoverage.html` for C++ coverage.

If you only want to run the JavaScript tests then you do not need to run the first command (`./configure --coverage`). Run `make coverage-run-js`, to execute JavaScript tests independently of the C++ test suite:

```text
$ make coverage-run-js
```

If you are updating tests and want to collect coverage for a single test file (e.g. `test/parallel/test-stream2-transform.js`):

```text
$ make coverage-clean
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/parallel/test-stream2-transform.js
$ make coverage-report-js
```

You can collect coverage for the entire suite of tests for a given subsystem by providing the name of a subsystem:

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

This will spin up a static file server and provide a URL to where you may browse the documentation locally.

If you're comfortable viewing the documentation using the program your operating system has associated with the default web browser, run the following.

```bash
dokopen machen
```

This will open a file URL to a one-page version of all the browsable HTML documents using the default browser.

Um zu testen, ob Node.js korrekt gebaut wurde:

```bash
./node -e "console.log('Hallo von Node.js ' + process.version)"
```

#### Debug-Build erstellen

If you run into an issue where the information provided by the JS stack trace is not enough, or if you suspect the error happens outside of the JS VM, you can try to build a debug enabled binary:

```console
$ ./configure --debug
$ make -j4
```

`make` with `./configure --debug` generates two binaries, the regular release one in `out/Release/node` and a debug binary in `out/Debug/node`, only the release version is actually installed when you run `make install`.

To use the debug build with all the normal dependencies overwrite the release version in the install directory:

``` console
$ make install PREFIX=/opt/node-debug/
$ cp -a -f out/Debug/node /opt/node-debug/node
```

Bei Verwendung der Debug-Binärdatei werden Kern-Dumps im Falle eines Absturzes erzeugt. These core dumps are useful for debugging when provided with the corresponding original debug binary and system information.

Reading the core dump requires `gdb` built on the same platform the core dump was captured on (i.e. 64-bit `gdb` for `node` built on a 64-bit system, Linux `gdb` for `node` built on Linux) otherwise you will get errors like `not in executable format: File format not recognized`.

Beispiel für die Erzeugung eines Backtrace aus dem Kerndump:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Bau eines ASAN-Builds

[ASAN](https://github.com/google/sanitizers) can help detect various memory related bugs. ASAN-Builds werden derzeit nur auf Linux unterstützt. If you want to check it on Windows or macOS or you want a consistent toolchain on Linux, you can try [Docker](https://www.docker.com/products/docker-desktop) (using an image like `gengjiawen/node-build:2020-02-14`).

The `--debug` is not necessary and will slow down build and testing, but it can show clear stacktrace if ASAN hits an issue.

``` console
$ ./configure --debug --enable-asan && make -j4
$ make test-only
```

#### Häufige Umbauten bei der Entwicklung beschleunigen

If you plan to frequently rebuild Node.js, especially if using several branches, installing `ccache` can help to greatly reduce build times. Einrichten mit:
```console
$ sudo apt install ccache # für Debian/Ubuntu, In den meisten Linux-Distributionen enthalten
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # fügen Sie zu Ihrer . rofile
$ export CXX="ccache g++" # zu Ihrem .profile hinzufügen
```
Dies ermöglicht nahezu sofortige Umbauten auch beim Wechsel von Zweigen.

When modifying only the JS layer in `lib`, it is possible to externally load it without modifying the executable:
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
The resulting binary won't include any JS files and will try to load them from the specified directory. The JS debugger of Visual Studio Code supports this configuration since the November 2020 version and allows for setting breakpoints.

#### Fehlerbehebung von Unix- und MacOS-Versionen

Veraltete Builds können manchmal dazu führen, dass `keine Fehler beim Erstellen gefunden wurden` haben. Dies und einige andere Probleme können mit `make distclean` gelöst werden. The `distclean` recipe aggressively removes build artifacts. You will need to build again (`make -j4`). Since all build artifacts have been removed, this rebuild may take a lot more time than previous builds. Additionally, `distclean` removes the file that stores the results of `./configure`. If you ran `./configure` with non-default options (such as `--debug`), you will need to run it again before invoking `make -j4`.

### Fenster

#### Voraussetzungen

##### Option 1: Manuelle Installation

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* The "Desktop development with C++" workload from [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) or the "C++ build tools" workload from the [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), with the default optional components
* Basic Unix tools required for some tests, [Git for Windows](https://git-scm.com/download/win) includes Git Bash and tools which can be included in the global `PATH`.
* Der [NetWide Assembler](https://www.nasm.us/), für OpenSSL Assembler Module. If not installed in the default location, it needs to be manually added to `PATH`. A build with the `openssl-no-asm` option does not need this, nor does a build targeting ARM64 Windows.

Optionale Anforderungen, um das MSI-Installer-Paket zu erstellen:

* The [WiX Toolset v3.11](https://wixtoolset.org/releases/) and the [Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* The [WiX Toolset v3.14](https://wixtoolset.org/releases/) if building for Windows 10 on ARM (ARM64)

Optionale Voraussetzungen für das Kompilieren von Windows 10 auf ARM (ARM64):

* Visual Studio 15.9.0 oder neuer
* Visual Studio optionale Komponenten
  * Visual C++ Compiler und Bibliotheken für ARM64
  * Visual C++ ATL für ARM64
* Windows 10 SDK 10.0.17763.0 oder neuer

##### Option 2: Automatisierte Installation mit Boxstarter

A [Boxstarter](https://boxstarter.org/) script can be used for easy setup of Windows systems with all the required prerequisites for Node.js development. This script will install the following [Chocolatey](https://chocolatey.org/) packages:

* [Git for Windows](https://chocolatey.org/packages/git) with the `git` and Unix tools added to the `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) with [Visual C++ workload](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [NetWide Assembler](https://chocolatey.org/packages/nasm)

To install Node.js prerequisites using [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), open <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> with Internet Explorer or Edge browser on the target machine.

Alternativ können Sie PowerShell verwenden. Run those commands from an elevated PowerShell terminal:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

The entire installation using Boxstarter will take up approximately 10 GB of disk space.

#### Erstelle Node.js

If the path to your build directory contains a space or a non-ASCII character, the build will likely fail.

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

Android ist keine unterstützte Plattform. Patches to improve the Android build are welcome. There is no testing on Android in the current continuous integration environment. The participation of people dedicated and determined to improve Android building, testing, and support is encouraged.

Be sure you have downloaded and extracted [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) before in a folder. Dann ausführen:

```console
$ ./android-configure /path/zu/Ihr/android-ndk
$ make
```

## `Intl` (ECMA-402) Unterstützung

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) support is enabled by default.

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

 In this configuration, only English data is included, but the full `Intl` (ECMA-402) APIs.  It does not need to download any dependencies to function. Sie können zur Laufzeit vollständige Daten hinzufügen.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Fenster

```console
> .\vcbuild small-icu
```

### Gebäude ohne Intl Unterstützung

The `Intl` object will not be available, nor some other APIs such as `String.normalize`.

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

If you are cross-compiling, your `pkg-config` must be able to supply a path that works for both your host and target environments.

### Baue mit einer bestimmten ICU

You can find other ICU releases at [the ICU homepage](http://site.icu-project.org/download). Download the file named something like `icu4c-**##.#**-src.tgz` (or `.zip`).

To check the minimum recommended ICU, run `./configure --help` and see the help for the `--with-icu-source` option. A warning will be printed during configuration if the ICU version is too old.

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

First unpack latest ICU to `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (or `.zip`) as `deps/icu` (You'll have: `deps/icu/source/...`)

```console
> .\vcbuild Full-icu
```

## Erstelle Node.js mit FIPS-konformer OpenSSL

The current version of Node.js does not support FIPS when statically linking (the default) with OpenSSL 1.1.1 but for dynamically linking it is possible to enable FIPS using the configuration flag `--openssl-is-fips`.

### Konfigurieren und Erstellen von Quictls/openssl für FIPS

Für quictls/openssl 3.0 ist es möglich, FIPS bei dynamischem Linking zu aktivieren. Node.js currently uses openssl-3.0.0+quic which can be configured as follows:
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

After the FIPS module and configuration file have been installed by the above instructions we also need to update `/path/to/install/dir/ssl/openssl.cnf` to use the generated FIPS configuration file (`fipsmodule.cnf`):
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

In the above case OpenSSL is not installed in the default location so two environment variables need to be set, `OPENSSL_CONF`, and `OPENSSL_MODULES` which should point to the OpenSSL configuration file and the directory where OpenSSL modules are located:
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
If the `ldd` command says that `libcrypto` cannot be found one needs to set `LD_LIBRARY_PATH` to point to the directory used above for `--shared-openssl-libpath` (see previous step).

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

FIPS support can then be enable via the OpenSSL configuration file or using `--enable-fips` or `--force-fips` command line options to the Node.js executable. See sections [Enabling FIPS using Node.js options](#enabling-fips-using-node.js-options) and [Enabling FIPS using OpenSSL config](#enabling-fips-using-openssl-config) below.

### Aktiviere FIPS mit Node.js Optionen
This is done using one of the Node.js options `--enable-fips` or `--force-fips`, for example:
```console
$-Knoten --enable-fips -p 'crypto.getFips()'
```

### Aktiviere FIPS mit OpenSSL-Konfiguration
This example show that using OpenSSL's configuration file, FIPS can be enabled without specifying the `--enable-fips` or `--force-fips` options by setting `default_properties = fips=yes` in the FIPS configuration file. See [link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) for details.

For this to work the OpenSSL configuration file (default openssl.cnf) needs to be updated. Das folgende Beispiel zeigt ein Beispiel:
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
After this change Node.js can be run without the `--enable-fips` or `--force-fips` options.

## Erstelle Node.js mit externen Kernmodulen

It is possible to specify one or more JavaScript text files to be bundled in the binary as built-in modules when building Node.js.

### Unix/macOS

This command will make `/root/myModule.js` available via `require('/root/myModule')` and `./myModule2.js` available via `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Fenster

To make `./myModule.js` available via `require('myModule')` and `./myModule2.js` available via `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Hinweis für nachgelagerte Distributoren von Node.js
Hallo Welt!

Das Ökosystem von Node.js ist abhängig von der ABI-Kompatibilität innerhalb einer Hauptversion. To maintain ABI compatibility it is required that distributed builds of Node.js be built against the same version of dependencies, or similar versions that do not break their ABI compatibility, as those released by Node.js for any given `NODE_MODULE_VERSION` (located in `src/node_version.h`).

When Node.js is built (with an intention to distribute) with an ABI incompatible with the official Node.js builds (e.g. using a ABI incompatible version of a dependency), please reserve and use a custom `NODE_MODULE_VERSION` by opening a pull request against the registry available at [https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
