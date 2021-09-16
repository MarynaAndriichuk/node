# Construire Node.js

Depending on what platform or features you need, the build process may differ. After you've built a binary, running the test suite to confirm that the binary works as intended is a good next step.

If you can reproduce a test failure, search for it in the [Node.js issue tracker](https://github.com/nodejs/node/issues) or file a new issue.

## Table des matières

* [Plateformes prises en charge](#supported-platforms)
  * [Input](#input)
  * [Stratégie](#strategy)
  * [Liste des plateformes](#platform-list)
  * [Compilations prises en charge](#supported-toolchains)
  * [Plateformes binaires officielles et chaînes de compilation](#official-binary-platforms-and-toolchains)
    * [Prise en charge d'OpenSSL asm](#openssl-asm-support)
  * [Versions précédentes de ce document](#previous-versions-of-this-document)
* [Construire Node.js sur des plates-formes prises en charge](#building-nodejs-on-supported-platforms)
  * [Note à propos de Python](#note-about-python)
  * [Unix et macOS](#unix-and-macos)
    * [Prérequis Unix](#unix-prerequisites)
    * [macOS prerequisites](#macos-prerequisites)
    * [Construire Node.js](#building-nodejs-1)
    * [Installation de Node.js](#installing-nodejs)
    * [Tests en cours](#running-tests)
    * [Couverture en cours](#running-coverage)
    * [Construction de la documentation](#building-the-documentation)
    * [Construire une version de débogage](#building-a-debug-build)
    * [Construire une construction ASAN](#building-an-asan-build)
    * [Accélérer les reconstructions fréquentes lors du développement](#speeding-up-frequent-rebuilds-when-developing)
    * [Dépannage des versions Unix et macOS](#troubleshooting-unix-and-macos-builds)
  * [Fenêtres](#windows)
    * [Pré-requis](#prerequisites)
      * [Option 1 : installation manuelle](#option-1-manual-install)
      * [Option 2 : Installation automatique avec Boxstarter](#option-2-automated-install-with-boxstarter)
    * [Construire Node.js](#building-nodejs-2)
  * [Périphériques Android/Android (par exemple Firefox OS)](#androidandroid-based-devices-eg-firefox-os)
* [`Intl` (ECMA-402) support](#intl-ecma-402-support)
  * [Compilation avec support ICU complet (toutes les locales supportées par ICU)](#build-with-full-icu-support-all-locales-supported-by-icu)
    * [Unix/macOS](#unixmacos)
    * [Fenêtres](#windows-1)
  * [Prise en charge : `small-icu` (en anglais seulement)](#trimmed-small-icu-english-only-support)
    * [Unix/macOS](#unixmacos-1)
    * [Fenêtres](#windows-2)
  * [Construction sans support Intl](#building-without-intl-support)
    * [Unix/macOS](#unixmacos-2)
    * [Fenêtres](#windows-3)
  * [Utiliser l'ICU installée existante (Unix/macOS uniquement)](#use-existing-installed-icu-unixmacos-only)
  * [Construire avec une ICU spécifique](#build-with-a-specific-icu)
    * [Unix/macOS](#unixmacos-3)
    * [Fenêtres](#windows-4)
* [Construire Node.js avec OpenSSL conforme au FIPS](#building-nodejs-with-fips-compliant-openssl)
* [Construire Node.js avec des modules core externes](#building-nodejs-with-external-core-modules)
  * [Unix/macOS](#unixmacos-4)
  * [Fenêtres](#windows-5)
* [Note pour les distributeurs en aval de Node.js](#note-for-downstream-distributors-of-nodejs)

## Plateformes prises en charge

This list of supported platforms is current as of the branch/release to which it belongs.

### Input

Node.js repose sur V8 et libuv. Nous adoptons un sous-ensemble de leurs plates-formes supportées.

### Stratégie

Il y a trois paliers de support :

* **Tier 1**: Ces plateformes représentent la majorité des utilisateurs de Node.js. The Node.js Build Working Group maintains infrastructure for full test coverage. Les échecs de test sur les plateformes de niveau 1 bloqueront les versions.
* **Tier 2**: These platforms represent smaller segments of the Node.js user base. The Node.js Build Working Group maintains infrastructure for full test coverage. Les échecs de test sur les plateformes de niveau 2 bloqueront les versions. Les problèmes d'infrastructure peuvent retarder la publication de binaires pour ces plates-formes.
* **Expérimental**: Peut ne pas compiler ou tester suite peut ne pas passer. The core team does not create releases for these platforms. Test failures on experimental platforms do not block releases. Contributions to improve support for these platforms are welcome.

Les plateformes peuvent se déplacer entre les niveaux entre les lignes de publication majeures. The table below will reflect those changes.

### Liste des plateformes

Node.js compilation/execution support depends on operating system, architecture, and libc version. The table below lists the support tier for each supported combination. A list of [supported compile toolchains](#supported-toolchains) is also supplied for tier 1 platforms.

**Pour les applications de production, exécutez Node.js uniquement sur les plates-formes supportées.**

Node.js does not support a platform version if a vendor has expired support for it. In other words, Node.js does not support running on End-of-Life (EoL) platforms. Ceci est vrai indépendamment des entrées dans le tableau ci-dessous.

| Système d'exploitation | Architectures    | Versions                        | Type de support                                                     | Notes                                                                       |
| ---------------------- | ---------------- | ------------------------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| GNU/Linux              | x64              | noyau >= 3.10, glibc >= 2.17    | Niveau 1                                                            | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, Debian 9, EL 7 <sup>[2](#fn2)</sup> |
| GNU/Linux              | x64              | noyau >= 3.10, musl >= 1.1.19   | Expérimental                                                        | e.g. Alpine 3.8                                                             |
| GNU/Linux              | x86              | noyau >= 3.10, glibc >= 2.17    | Expérimental                                                        | Dégradé à partir de Node.js 10                                              |
| GNU/Linux              | arm64            | noyau >= 4.5, glibc >= 2.17     | Niveau 1                                                            | e.g. Ubuntu 16.04, Debian 9, EL 7 <sup>[3](#fn3)</sup>                      |
| GNU/Linux              | armv7            | noyau >= 4.14, glibc >= 2.24    | Niveau 1                                                            | e.g. Ubuntu 18.04, Debian 9                                                 |
| GNU/Linux              | armv6            | noyau >= 4.14, glibc >= 2.24    | Expérimental                                                        | Dégradé à partir de Node.js 12                                              |
| GNU/Linux              | ppc64le >=power8 | kernel >= 3.10.0, glibc >= 2.17 | Palier 2                                                            | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, EL 7  <sup>[2](#fn2)</sup>          |
| GNU/Linux              | s390x            | kernel >= 3.10.0, glibc >= 2.17 | Palier 2                                                            | e.g. EL 7 <sup>[2](#fn2)</sup>                                              |
| Fenêtres               | x64, x86 (WoW64) | >= Windows 8.1/2012 R2          | Niveau 1                                                            | <sup>[4](#fn4),[5](#fn5)</sup>                                              |
| Fenêtres               | x86 (natif)      | >= Windows 8.1/2012 R2          | Tier 1 (en cours) / Expérimental (compilation) <sup>[6](#fn6)</sup> |                                                                             |
| Fenêtres               | x64, x86         | Windows Server 2012 (pas R2)    | Expérimental                                                        |                                                                             |
| Fenêtres               | arm64            | >= Windows 10                   | Tier 2 (compilation) / Expérimental (en cours)                      |                                                                             |
| macOS                  | x64              | >= 10.13                        | Niveau 1                                                            |                                                                             |
| macOS                  | arm64            | >= 11                           | Expérimental                                                        |                                                                             |
| SmartOS                | x64              | >= 18                           | Palier 2                                                            |                                                                             |
| AIX                    | ppc64be >=power7 | >= 7.2 TL04                     | Palier 2                                                            |                                                                             |
| FreeBSD                | x64              | >= 11                           | Expérimental                                                        | Dégradé à partir de Node.js 12  <sup>[7](#fn7)</sup>                        |

<em id="fn1">1</em>: GCC 8 n'est pas fourni sur la plate-forme de base. Users will need the [Toolchain test builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) or similar to source a newer compiler.

<em id="fn2">2</em>: GCC 8 n'est pas fourni sur la plate-forme de base. Users will need the [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) or later to source a newer compiler.

<em id="fn3">3</em>: Les anciennes versions du noyau peuvent fonctionner pour ARM64. However the Node.js test infrastructure only tests >= 4.5.

<em id="fn4">4</em>: On Windows, running Node.js in Windows terminal emulators like `mintty` requires the usage of [winpty](https://github.com/rprichard/winpty) for the tty channels to work (e.g. `winpty node.exe script.js`). In "Git bash" if you call the node shell alias (`node` without the `.exe` extension), `winpty` is used automatically.

<em id="fn5">5</em>: The Windows Subsystem for Linux (WSL) is not supported, but the GNU/Linux build process and binaries should work. The community will only address issues that reproduce on native GNU/Linux systems. Issues that only reproduce on WSL should be reported in the [WSL issue tracker](https://github.com/Microsoft/WSL/issues). Running the Windows binary (`node.exe`) in WSL is not recommended. It will not work without workarounds such as stdio redirection.

<em id="fn6">6</em>: Running Node.js on x86 Windows should work and binaries are provided. Cependant, les tests dans notre infrastructure ne fonctionnent que sur WoW64. Furthermore, compiling on x86 Windows is Experimental and may not be possible.

<em id="fn7">7</em>: The default FreeBSD 12.0 compiler is Clang 6.0.1, but FreeBSD 12.1 upgrades to 8.0.1. Other Clang/LLVM versions are available via the system's package manager, including Clang 9.0.

### Compilations prises en charge

Selon la plate-forme hôte, la sélection des chaînes de compilation peut varier.

| Système d'exploitation | Versions du compilateur                                          |
| ---------------------- | ---------------------------------------------------------------- |
| Linux                  | GCC >= 8.3                                                       |
| Fenêtres               | Visual Studio >= 2019 avec le SDK Windows 10 sur un hôte 64 bits |
| macOS                  | Xcode >= 11 (Apple LLVM >= 11)                                   |

### Plateformes binaires officielles et chaînes de compilation

Les binaires à <https://nodejs.org/download/release/> sont produits sur:

| Paquet binaire         | Plateforme et Toolchain                                                                                                                 |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| aix-ppc64              | AIX 7.2 TL04 sur PPC64BE avec GCC 8                                                                                                     |
| darwin-x64             | macOS 10.15, Xcode Command Line Tools 11 avec -mmacosx-version-min=10.13                                                                |
| darwin-arm64 (et .pkg) | macOS 11 (arm64), Xcode Command Line Tools 12 avec -mmacosx-version-min=10.13                                                           |
| linux-arm64            | CentOS 7 avec devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                                 |
| linux-armv7l           | Cross-compilés sur Ubuntu 18,04 x64 avec [la chaîne de compilation personnalisée de GCC](https://github.com/rvagg/rpi-newer-crosstools) |
| linux-ppc64le          | CentOS 7 avec devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                                 |
| linux-s390x            | RHEL 7 avec devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                                   |
| linux-x64              | CentOS 7 avec devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                                                 |
| win-x64 et win-x86     | Windows 2012 R2 (x64) avec Visual Studio 2019                                                                                           |

<em id="fn8">8</em>: The Enterprise Linux devtoolset-8 allows us to compile binaries with GCC 8 but linked to the glibc and libstdc++ versions of the host platforms (CentOS 7 / RHEL 7). Therefore, binaries produced on these systems are compatible with glibc >= 2.17 and libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). These are available on distributions natively supporting GCC 4.9, such as Ubuntu 14.04 and Debian 8.

#### Prise en charge d'OpenSSL asm

OpenSSL-1.1.1 requires the following assembler version for use of asm support on x86_64 and ia32.

Pour l'utilisation de AVX-512,

* gas (assembleur GNU) version 2.26 ou supérieure
* nasm version 2.11.8 ou supérieure dans Windows

AVX-512 est désactivé pour Skylake-X par OpenSSL-1.1.1.

Pour l'utilisation de AVX2,

* gas (assembleur GNU) version 2.23 ou supérieure
* Xcode version 5.0 ou supérieure
* llvm version 3.3 ou supérieure
* nasm version 2.10 ou supérieure dans Windows

Please refer to <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> for details.

 If compiling without one of the above, use `configure` with the `--openssl-no-asm` flag. Sinon, `configure` échouera.

### Versions précédentes de ce document

Les plates-formes et les chaînes de compilation supportées changent avec chaque version majeure de Node.js. Ce document n'est valide que pour la version majeure actuelle de Node.js. Consulter les versions précédentes de ce document pour les anciennes versions de Node.js :

* [Node.js 14](https://github.com/nodejs/node/blob/v14.x/BUILDING.md)
* [Node.js 12](https://github.com/nodejs/node/blob/v12.x/BUILDING.md)
* [Node.js 10](https://github.com/nodejs/node/blob/v10.x/BUILDING.md)

## Construire Node.js sur des plates-formes prises en charge

### Note à propos de Python

Le projet Node.js supporte Python >= 3 pour la construction et les tests.
### Unix et macOS

#### Prérequis Unix

* `gcc` et `g++` >= 8.3 ou plus récent, ou
* GNU Make 3.81 ou plus récent
* Python 3.6, 3.7, 3.8 et 3.9 (voir note ci-dessus)

L'installation via le gestionnaire de paquets Linux peut être réalisée avec :

* Ubuntu, Debian: `sudo apt-get install python3 g++ make`
* Fedora: `sudo dnf install python3 gcc-c++ make`
* CentOS et RHEL: `sudo yum install python3 gcc-c++ make`
* OpenSUSE : `sudo zypper install python3 gcc-c++ make`
* Arch Linux, Manjaro: `sudo pacman -S python gcc make`

Les utilisateurs de FreeBSD et d'OpenBSD peuvent également avoir besoin d'installer `libexecinfo`.

#### macOS prerequisites

* Outils de ligne de commande Xcode >= 11 pour macOS
* Python 3.6, 3.7, 3.8 et 3.9 (voir note ci-dessus)

macOS users can install the `Xcode Command Line Tools` by running `xcode-select --install`. Alternatively, if you already have the full Xcode installed, you can find them under the menu `Xcode -> Open Developer Tool ->
More Developer Tools...`. This step will install `clang`, `clang++`, and `make`.

#### Construire Node.js

If the path to your build directory contains a space, the build will likely fail.

Pour construire Node.js :

```console
$ ./configure
$ make -j4
```

The `-j4` option will cause `make` to run 4 simultaneous compilation jobs which may reduce build time. For more information, see the [GNU Make Documentation](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

The above requires that `python` resolves to a supported version of Python. Voir [Prérequis](#prerequisites).

After building, setting up [firewall rules](tools/macos-firewall.sh) can avoid popups asking to accept incoming network connections when running tests.

Running the following script on macOS will add the firewall rules for the executable `node` in the `out` directory and the symbolic `node` link in the project's root directory.

```console
$ sudo ./tools/macos-firewall.sh
```

#### Installation de Node.js

Pour installer cette version de Node.js dans un répertoire système:

```bash
[sudo] faire installer
```

#### Exécution des tests

Pour vérifier la construction:

```console
$ rendre le test uniquement
```

À ce stade, vous êtes prêt à faire des changements de code et à relancer les tests.

If you are running tests before submitting a Pull Request, the recommended command is:

```console
$ faire -j4 test
```

`make -j4 test` does a full check on the codebase, including running linters and documentation tests.

Assurez-vous que le linter ne signale aucun problème et que tous les tests réussissent. Please do not submit patches that fail either check.

If you want to run the linter without running tests, use `make lint`/`vcbuild lint`. Il va linter les fichiers JavaScript, C++ et Markdown.

If you are updating tests and want to run tests in a single test file (e.g. `test/parallel/test-stream2-transform.js`):

```text
$ python tools/test.py test/parallel/test-stream2-transform.js
```

You can execute the entire suite of tests for a given subsystem by providing the name of a subsystem:

```text
$ python tools/test.py -J --mode=release child-process
```

If you want to check the other options, please refer to the help by using the `--help` option:

```text
$ python tools/test.py --help
```

Vous pouvez généralement exécuter des tests directement avec le noeud :

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

Remember to recompile with `make -j4` in between test runs if you change code in the `lib` or `src` directories.

The tests attempt to detect support for IPv6 and exclude IPv6 tests if appropriate. If your main interface has IPv6 addresses, then your loopback interface must also have '::1' enabled. For some default installations on Ubuntu that does not seem to be the case. To enable '::1' on the loopback interface on Ubuntu:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

You can use [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) to run/debug tests, if your IDE configs are present.

#### Couverture en cours

Il est bon de s'assurer que tout code que vous ajoutez ou modifiez est couvert par des tests. Vous pouvez le faire en exécutant la suite de tests avec l'activation de la couverture :

```console
$ ./configure --coverage
$ faire la couverture
```

A detailed coverage report will be written to `coverage/index.html` for JavaScript coverage and to `coverage/cxxcoverage.html` for C++ coverage.

If you only want to run the JavaScript tests then you do not need to run the first command (`./configure --coverage`). Run `make coverage-run-js`, to execute JavaScript tests independently of the C++ test suite:

```text
$ rendre coverage-run-js
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
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py -J --mode=release child process
$ make coverage-report-js
```

La commande `rendre la couverture` télécharge des outils au répertoire racine du projet. Pour nettoyer après avoir généré les rapports de couverture :

```console
$ nettoyer la couverture
```

#### Construction de la documentation

Pour compiler la documentation:

Cela va construire Node.js d'abord (si nécessaire) et ensuite l'utiliser pour construire les docs :

```bash
faire un doc
```

Si vous avez une version existante de Node.js, vous pouvez construire juste la documentation avec:

```bash
NOEUDE=/chemin/vers/noeud : doc-only
```

Pour lire la page de manuel :

```bash
man doc/node.1
```

Si vous préférez lire la documentation complète dans un navigateur, exécutez ce qui suit.

```bash
faire un service de doc
```

This will spin up a static file server and provide a URL to where you may browse the documentation locally.

If you're comfortable viewing the documentation using the program your operating system has associated with the default web browser, run the following.

```bash
faire du docopen
```

This will open a file URL to a one-page version of all the browsable HTML documents using the default browser.

Pour tester si Node.js a été construit correctement :

```bash
./node -e "console.log('Bonjour de Node.js ' + process.version)"
```

#### Construire une version de débogage

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

Lors de l'utilisation du binaire de débogage, les dumps de noyaux seront générés en cas de plantage. These core dumps are useful for debugging when provided with the corresponding original debug binary and system information.

Reading the core dump requires `gdb` built on the same platform the core dump was captured on (i.e. 64-bit `gdb` for `node` built on a 64-bit system, Linux `gdb` for `node` built on Linux) otherwise you will get errors like `not in executable format: File format not recognized`.

Exemple de génération d'une trace à partir de la décharge du noyau:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Construire une construction ASAN

[ASAN](https://github.com/google/sanitizers) can help detect various memory related bugs. Les versions ASAN ne sont actuellement prises en charge que sur linux. If you want to check it on Windows or macOS or you want a consistent toolchain on Linux, you can try [Docker](https://www.docker.com/products/docker-desktop) (using an image like `gengjiawen/node-build:2020-02-14`).

The `--debug` is not necessary and will slow down build and testing, but it can show clear stacktrace if ASAN hits an issue.

``` console
$ ./configure --debug --enable-asan && make -j4
$ rendre le test seulement
```

#### Accélérer les reconstructions fréquentes lors du développement

If you plan to frequently rebuild Node.js, especially if using several branches, installing `ccache` can help to greatly reduce build times. Configurer avec :
```console
$ sudo apt install ccache # pour Debian/Ubuntu, inclus dans la plupart des distributions Linux
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # ajoutez à votre . rofile
$ export CXX="ccache g++" # ajouter à votre .profile
```
Cela permettra des reconstructions quasi instantanées même lors du changement de branches.

When modifying only the JS layer in `lib`, it is possible to externally load it without modifying the executable:
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
The resulting binary won't include any JS files and will try to load them from the specified directory. The JS debugger of Visual Studio Code supports this configuration since the November 2020 version and allows for setting breakpoints.

#### Dépannage des versions Unix et macOS

Les builds de contes peuvent parfois entraîner des erreurs de `fichier non trouvé` lors de la construction. Ceci et d'autres problèmes peuvent être résolus avec `make distclean`. The `distclean` recipe aggressively removes build artifacts. You will need to build again (`make -j4`). Since all build artifacts have been removed, this rebuild may take a lot more time than previous builds. Additionally, `distclean` removes the file that stores the results of `./configure`. If you ran `./configure` with non-default options (such as `--debug`), you will need to run it again before invoking `make -j4`.

### Fenêtres

#### Pré-requis

##### Option 1 : installation manuelle

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* The "Desktop development with C++" workload from [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) or the "C++ build tools" workload from the [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), with the default optional components
* Basic Unix tools required for some tests, [Git for Windows](https://git-scm.com/download/win) includes Git Bash and tools which can be included in the global `PATH`.
* L' [Assembleur NetWide](https://www.nasm.us/), pour les modules d'assemblage OpenSSL. If not installed in the default location, it needs to be manually added to `PATH`. A build with the `openssl-no-asm` option does not need this, nor does a build targeting ARM64 Windows.

Exigences optionnelles pour construire le paquet d'installation MSI :

* The [WiX Toolset v3.11](https://wixtoolset.org/releases/) and the [Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* The [WiX Toolset v3.14](https://wixtoolset.org/releases/) if building for Windows 10 on ARM (ARM64)

Exigences optionnelles pour la compilation pour Windows 10 sur ARM (ARM64):

* Visual Studio 15.9.0 ou plus récent
* Composants optionnels pour Visual Studio
  * Compilateurs et bibliothèques Visual C++ pour ARM64
  * ATL C++ visuel pour ARM64
* Windows 10 SDK 10.0.17763.0 ou plus récent

##### Option 2 : Installation automatique avec Boxstarter

A [Boxstarter](https://boxstarter.org/) script can be used for easy setup of Windows systems with all the required prerequisites for Node.js development. This script will install the following [Chocolatey](https://chocolatey.org/) packages:

* [Git for Windows](https://chocolatey.org/packages/git) with the `git` and Unix tools added to the `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) with [Visual C++ workload](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [Assembleur NetWide](https://chocolatey.org/packages/nasm)

To install Node.js prerequisites using [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), open <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> with Internet Explorer or Edge browser on the target machine.

Vous pouvez également utiliser PowerShell. Run those commands from an elevated PowerShell terminal:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex (New-Object System.Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

The entire installation using Boxstarter will take up approximately 10 GB of disk space.

#### Construire Node.js

If the path to your build directory contains a space or a non-ASCII character, the build will likely fail.

```console
> .\vcbuild
```

Pour exécuter les tests :

```console
> .\vcbuild test
```

Pour tester si Node.js a été construit correctement :

```console
> Release\node -e "console.log('Bonjour de Node.js', process.version)"
```

### Périphériques Android/Android (par exemple Firefox OS)

Android n'est pas une plate-forme prise en charge. Patches to improve the Android build are welcome. There is no testing on Android in the current continuous integration environment. The participation of people dedicated and determined to improve Android building, testing, and support is encouraged.

Be sure you have downloaded and extracted [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) before in a folder. Puis exécutez :

```console
$ ./android-configure /chemin/vers/votre/android-ndk
$ faire
```

## `Intl` (ECMA-402) support

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) support is enabled by default.

### Compilation avec support ICU complet (toutes les locales supportées par ICU)

C'est l'option par défaut.

#### Unix/macOS

```console
$ ./configure --with-intl=full-icu
```

#### Fenêtres

```console
> .\vcbuild full-icu
```

### Prise en charge : `small-icu` (en anglais seulement)

 In this configuration, only English data is included, but the full `Intl` (ECMA-402) APIs.  It does not need to download any dependencies to function. Vous pouvez ajouter des données complètes à l'exécution.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Fenêtres

```console
> .\vcbuild small-icu
```

### Construction sans support Intl

The `Intl` object will not be available, nor some other APIs such as `String.normalize`.

#### Unix/macOS

```console
$ ./configure --without-intl
```

#### Fenêtres

```console
> .\vcbuild sans intl
```

### Utiliser l'ICU installée existante (Unix/macOS uniquement)

```console
$ pkg-config --modversion icu-i18n && ./configure --with-intl=system-icu
```

If you are cross-compiling, your `pkg-config` must be able to supply a path that works for both your host and target environments.

### Construire avec une ICU spécifique

You can find other ICU releases at [the ICU homepage](http://site.icu-project.org/download). Download the file named something like `icu4c-**##.#**-src.tgz` (or `.zip`).

To check the minimum recommended ICU, run `./configure --help` and see the help for the `--with-icu-source` option. A warning will be printed during configuration if the ICU version is too old.

#### Unix/macOS

À partir d'un ICU déjà décompressé :

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/to/icu
```

À partir d'une archive locale ICU :

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/to/icu.tgz
```

À partir d'une URL d'archive :

```console
$ ./configure --with-intl=full-icu --with-icu-source=http://url/to/icu.tgz
```

#### Fenêtres

First unpack latest ICU to `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (or `.zip`) as `deps/icu` (You'll have: `deps/icu/source/...`)

```console
> .\vcbuild full-icu
```

## Construire Node.js avec OpenSSL conforme au FIPS

The current version of Node.js does not support FIPS when statically linking (the default) with OpenSSL 1.1.1 but for dynamically linking it is possible to enable FIPS using the configuration flag `--openssl-is-fips`.

### Configuration et construction de quictls/openssl pour FIPS

Pour quictls/openssl 3.0, il est possible d'activer FIPS lors d'un lien dynamique. Node.js currently uses openssl-3.0.0+quic which can be configured as follows:
```console
$ git clone git@github.com:quictls/openssl.git
$ cd openssl
$ ./config --prefix=/path/to/install/dir/ shared enable-fips linux-x86_64
```
Ceci peut être compilé et installé en utilisant les commandes suivantes :
```console
$ make -j8
$ make install_ssldirs
$ make install_fips
```

After the FIPS module and configuration file have been installed by the above instructions we also need to update `/path/to/install/dir/ssl/openssl.cnf` to use the generated FIPS configuration file (`fipsmodule.cnf`):
```text
Module fips.inclus. nf

# Liste des fournisseurs à charger
[provider_sect]
default = default_sect
# Le nom de section de fips doit correspondre au nom de section à l'intérieur du
# inclus /path/to/install/dir/ssl/fipsmodule. Nf.
fips = fips_sect

[default_sect]
activer = 1
```

In the above case OpenSSL is not installed in the default location so two environment variables need to be set, `OPENSSL_CONF`, and `OPENSSL_MODULES` which should point to the OpenSSL configuration file and the directory where OpenSSL modules are located:
```console
$ export OPENSSL_CONF=/path/to/install/dir/ssl/openssl.cnf
$ export OPENSSL_MODULES=/path/to/install/dir/lib/ossl-modules
```

Node.js peut ensuite être configuré pour activer FIPS :
```console
$ ./configure --shared-openssl --shared-openssl-libpath=/path/to/install/dir/lib --shared-openssl-includes=/path/to/install/dir/include --shared-openssl-libname=crypto,ssl --openssl-is-fips
$ export LD_LIBRARY_PATH=/path/to/install/dir/lib
$ make -j8
```

Vérifier l'exécutable produit :
```console
$ ldd ./node
    linux-vdso.so.1 (0x00007ffd7917b000)
    libcrypto.so.81. => /path/to/install/dir/lib/lib/libcrypto.so.81.3 (0x00007fd911321000)
    libssl.so.81. => /path/to/install/dir/lib/lib/libssl.so.81.3 (0x00007fd91125e000)
    libdl.so. => /usr/lib64/libdl.so.2 (0x00007fd911232000)
    libstdc++.so.6 => /usr/lib64/libstdc++.so. (0x00007fd911039000)
    libm.so.6 => /usr/lib64/libm.so.6 (0x00007fd910ef3000)
    libgcc_s. o.1 => /usr/lib64/libgcc_s.so.1 (0x00007fd910ed9000)
    libpthread. o.0 => /usr/lib64/libpthread.so.0 (0x00007fd910eb5000)
    libc.so.6 => /usr/lib64/libc.so.6 (0x00007fd910cec000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fd9117f2000)
```
If the `ldd` command says that `libcrypto` cannot be found one needs to set `LD_LIBRARY_PATH` to point to the directory used above for `--shared-openssl-libpath` (see previous step).

Vérifier la version OpenSSL :
```console
$ ./node -p process.versions.openssl
3.0.0-alpha16+quic
```

Vérifiez que le FIPS est disponible :
```console
$ ./node -p 'process.config.variables.openssl_is_fips'
true
$ ./node --enable-fips -p 'crypto.getFips()'
1
```

FIPS support can then be enable via the OpenSSL configuration file or using `--enable-fips` or `--force-fips` command line options to the Node.js executable. See sections [Enabling FIPS using Node.js options](#enabling-fips-using-node.js-options) and [Enabling FIPS using OpenSSL config](#enabling-fips-using-openssl-config) below.

### Activation des FIPS en utilisant les options Node.js
This is done using one of the Node.js options `--enable-fips` or `--force-fips`, for example:
```console
$ node --enable-fips -p 'crypto.getFips()'
```

### Activer FIPS en utilisant la configuration OpenSSL
This example show that using OpenSSL's configuration file, FIPS can be enabled without specifying the `--enable-fips` or `--force-fips` options by setting `default_properties = fips=yes` in the FIPS configuration file. See [link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) for details.

For this to work the OpenSSL configuration file (default openssl.cnf) needs to be updated. Ce qui suit montre un exemple :
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

## Construire Node.js avec des modules core externes

It is possible to specify one or more JavaScript text files to be bundled in the binary as built-in modules when building Node.js.

### Unix/macOS

This command will make `/root/myModule.js` available via `require('/root/myModule')` and `./myModule2.js` available via `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Fenêtres

To make `./myModule.js` available via `require('myModule')` and `./myModule2.js` available via `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Note pour les distributeurs en aval de Node.js
Bonjour tout le monde!

L'écosystème Node.js dépend de la compatibilité ABI dans une version majeure. To maintain ABI compatibility it is required that distributed builds of Node.js be built against the same version of dependencies, or similar versions that do not break their ABI compatibility, as those released by Node.js for any given `NODE_MODULE_VERSION` (located in `src/node_version.h`).

When Node.js is built (with an intention to distribute) with an ABI incompatible with the official Node.js builds (e.g. using a ABI incompatible version of a dependency), please reserve and use a custom `NODE_MODULE_VERSION` by opening a pull request against the registry available at [https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
