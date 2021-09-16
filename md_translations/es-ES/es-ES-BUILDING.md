# Construyendo Node.js

Depending on what platform or features you need, the build process may differ. After you've built a binary, running the test suite to confirm that the binary works as intended is a good next step.

If you can reproduce a test failure, search for it in the [Node.js issue tracker](https://github.com/nodejs/node/issues) or file a new issue.

## Tabla de contenidos

* [Plataformas soportadas](#supported-platforms)
  * [Input](#input)
  * [Estrategia](#strategy)
  * [Lista de plataformas](#platform-list)
  * [Herramientas soportadas](#supported-toolchains)
  * [Plataformas binarias oficiales y cadenas de herramientas](#official-binary-platforms-and-toolchains)
    * [Soporte asm de OpenSSL](#openssl-asm-support)
  * [Versiones anteriores de este documento](#previous-versions-of-this-document)
* [Construyendo Node.js en plataformas soportadas](#building-nodejs-on-supported-platforms)
  * [Nota sobre Python](#note-about-python)
  * [Unix y macOS](#unix-and-macos)
    * [Prerrequisitos Unix](#unix-prerequisites)
    * [macOS prerequisites](#macos-prerequisites)
    * [Construyendo Node.js](#building-nodejs-1)
    * [Instalando Node.js](#installing-nodejs)
    * [Pruebas en ejecución](#running-tests)
    * [Cubo en ejecución](#running-coverage)
    * [Creando la documentación](#building-the-documentation)
    * [Construir una construcción de depuración](#building-a-debug-build)
    * [Construyendo una construcción ASAN](#building-an-asan-build)
    * [Acelera las reconstrucciones frecuentes al desarrollar](#speeding-up-frequent-rebuilds-when-developing)
    * [Solución de problemas para compilaciones Unix y macOS](#troubleshooting-unix-and-macos-builds)
  * [Ventanas](#windows)
    * [Prerrequisitos](#prerequisites)
      * [Opción 1: Instalación manual](#option-1-manual-install)
      * [Opción 2: Instalación automática con Boxstarter](#option-2-automated-install-with-boxstarter)
    * [Construyendo Node.js](#building-nodejs-2)
  * [Dispositivos basados en Android/Android (por ejemplo, Firefox OS)](#androidandroid-based-devices-eg-firefox-os)
* [`Soporte Intl` (ECMA-402)](#intl-ecma-402-support)
  * [Construir con soporte completo de ICU (todos los locales soportados por ICU)](#build-with-full-icu-support-all-locales-supported-by-icu)
    * [Unix/macOS](#unixmacos)
    * [Ventanas](#windows-1)
  * [Trimmed: `small-icu` (solo en inglés) soporte](#trimmed-small-icu-english-only-support)
    * [Unix/macOS](#unixmacos-1)
    * [Ventanas](#windows-2)
  * [Construyendo sin soporte Intl](#building-without-intl-support)
    * [Unix/macOS](#unixmacos-2)
    * [Ventanas](#windows-3)
  * [Usar ICU instalado (sólo Unix/macOS)](#use-existing-installed-icu-unixmacos-only)
  * [Construir con un ICU específico](#build-with-a-specific-icu)
    * [Unix/macOS](#unixmacos-3)
    * [Ventanas](#windows-4)
* [Construyendo Node.js con OpenSSL compatible con FIPS](#building-nodejs-with-fips-compliant-openssl)
* [Construyendo Node.js con módulos principales externos](#building-nodejs-with-external-core-modules)
  * [Unix/macOS](#unixmacos-4)
  * [Ventanas](#windows-5)
* [Nota para los distribuidores downstream de Node.js](#note-for-downstream-distributors-of-nodejs)

## Plataformas soportadas

This list of supported platforms is current as of the branch/release to which it belongs.

### Input

Node.js depende de V8 y libuv. Adoptamos un subconjunto de sus plataformas soportadas.

### Estrategia

Hay tres niveles de apoyo:

* **Nivel 1**: Estas plataformas representan la mayoría de los usuarios de Node.js. The Node.js Build Working Group maintains infrastructure for full test coverage. Los fallos de prueba en plataformas de nivel 1 bloquearán lanzamientos.
* **Tier 2**: These platforms represent smaller segments of the Node.js user base. The Node.js Build Working Group maintains infrastructure for full test coverage. Los fallos de prueba en plataformas de nivel 2 bloquearán lanzamientos. Los problemas de infraestructura pueden retrasar la liberación de binarios para estas plataformas.
* **Experimental**: No se puede compilar o probar suite no puede pasar. The core team does not create releases for these platforms. Test failures on experimental platforms do not block releases. Contributions to improve support for these platforms are welcome.

Las plataformas pueden moverse entre niveles entre las principales líneas de lanzamiento. The table below will reflect those changes.

### Lista de plataformas

Node.js compilation/execution support depends on operating system, architecture, and libc version. The table below lists the support tier for each supported combination. A list of [supported compile toolchains](#supported-toolchains) is also supplied for tier 1 platforms.

**Para aplicaciones de producción, ejecute Node.js sólo en plataformas soportadas.**

Node.js does not support a platform version if a vendor has expired support for it. In other words, Node.js does not support running on End-of-Life (EoL) platforms. Esto es cierto independientemente de las entradas en la tabla de abajo.

| Sistema operativo | Archivos         | Versiones                       | Tipo de Soporte                                                        | Notas                                                                       |
| ----------------- | ---------------- | ------------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| GNU/Linux         | x64              | kernel >= 3.10, glibc >= 2.17   | Nivel 1                                                                | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, Debian 9, EL 7 <sup>[2](#fn2)</sup> |
| GNU/Linux         | x64              | kernel >= 3.10, musl >= 1.1.19  | Experimental                                                           | e.g. Alpine 3.8                                                             |
| GNU/Linux         | x86              | kernel >= 3.10, glibc >= 2.17   | Experimental                                                           | Bajado a partir de Node.js 10                                               |
| GNU/Linux         | arm64            | kernel >= 4.5, glibc >= 2.17    | Nivel 1                                                                | e.g. Ubuntu 16.04, Debian 9, EL 7 <sup>[3](#fn3)</sup>                      |
| GNU/Linux         | armadura7        | kernel >= 4.14, glibc >= 2.24   | Nivel 1                                                                | e.g. Ubuntu 18.04, Debian 9                                                 |
| GNU/Linux         | armadura6        | kernel >= 4.14, glibc >= 2.24   | Experimental                                                           | Bajado a partir de Node.js 12                                               |
| GNU/Linux         | ppc64le >=power8 | kernel >= 3.10.0, glibc >= 2.17 | Nivel 2                                                                | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, EL 7  <sup>[2](#fn2)</sup>          |
| GNU/Linux         | s390x            | kernel >= 3.10.0, glibc >= 2.17 | Nivel 2                                                                | e.g. EL 7 <sup>[2](#fn2)</sup>                                              |
| Ventanas          | x64, x86 (WoW64) | >= Windows 8.1/2012 R2          | Nivel 1                                                                | <sup>[4](#fn4),[5](#fn5)</sup>                                              |
| Ventanas          | x86 (nativo)     | >= Windows 8.1/2012 R2          | Nivel 1 (ejecutando) / Experimental (compilación) <sup>[6](#fn6)</sup> |                                                                             |
| Ventanas          | x64, x86         | Windows Server 2012 (no R2)     | Experimental                                                           |                                                                             |
| Ventanas          | arm64            | >= Windows 10                   | Nivel 2 (compilación) / Experimental (ejecutando)                      |                                                                             |
| macOS             | x64              | >= 10.13                        | Nivel 1                                                                |                                                                             |
| macOS             | arm64            | >= 11                           | Experimental                                                           |                                                                             |
| SmartOS           | x64              | >= 18                           | Nivel 2                                                                |                                                                             |
| AIX               | ppc64be >=power7 | >= 7.2 TL04                     | Nivel 2                                                                |                                                                             |
| BSD               | x64              | >= 11                           | Experimental                                                           | Bajado a partir de Node.js 12  <sup>[7](#fn7)</sup>                         |

<em id="fn1">1</em>: GCC 8 no está disponible en la plataforma base. Users will need the [Toolchain test builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) or similar to source a newer compiler.

<em id="fn2">2</em>: GCC 8 no está disponible en la plataforma base. Users will need the [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) or later to source a newer compiler.

<em id="fn3">3</em>: Las versiones antiguas del núcleo pueden funcionar para ARM64. However the Node.js test infrastructure only tests >= 4.5.

<em id="fn4">4</em>: On Windows, running Node.js in Windows terminal emulators like `mintty` requires the usage of [winpty](https://github.com/rprichard/winpty) for the tty channels to work (e.g. `winpty node.exe script.js`). In "Git bash" if you call the node shell alias (`node` without the `.exe` extension), `winpty` is used automatically.

<em id="fn5">5</em>: The Windows Subsystem for Linux (WSL) is not supported, but the GNU/Linux build process and binaries should work. The community will only address issues that reproduce on native GNU/Linux systems. Issues that only reproduce on WSL should be reported in the [WSL issue tracker](https://github.com/Microsoft/WSL/issues). Running the Windows binary (`node.exe`) in WSL is not recommended. It will not work without workarounds such as stdio redirection.

<em id="fn6">6</em>: Running Node.js on x86 Windows should work and binaries are provided. Sin embargo, las pruebas en nuestra infraestructura sólo funcionan en WoW64. Furthermore, compiling on x86 Windows is Experimental and may not be possible.

<em id="fn7">7</em>: The default FreeBSD 12.0 compiler is Clang 6.0.1, but FreeBSD 12.1 upgrades to 8.0.1. Other Clang/LLVM versions are available via the system's package manager, including Clang 9.0.

### Herramientas soportadas

Dependiendo de la plataforma anfitriona, la selección de cadenas de herramientas puede variar.

| Sistema operativo | Versiones del compilador                                             |
| ----------------- | -------------------------------------------------------------------- |
| Linux             | GCC >= 8.3                                                           |
| Ventanas          | Visual Studio >= 2019 con el SDK de Windows 10 en un host de 64 bits |
| macOS             | Xcode >= 11 NLVM Excelente >= 11)                                    |

### Plataformas binarias oficiales y cadenas de herramientas

Los binarios en <https://nodejs.org/download/release/> se producen en:

| Paquete binario       | Plataforma y cadena de herramientas                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------------------- |
| aix-ppc64             | AIX 7.2 TL04 en PPC64BE con GCC 8                                                                             |
| darwin-x64            | macOS 10.15, Herramientas de línea de comandos Xcode 11 con -mmacosx-version-min=10.13                        |
| darwin-arm64 (y .pkg) | macOS 11 (arm64), Herramientas de línea de comandos Xcode 12 con -mmacosx-version-min=10.13                   |
| linux-arm64           | CentOS 7 con devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                        |
| linux-armv7l          | Cross-compilado en Ubuntu 18.04 x64 con [custom GCC toolchain](https://github.com/rvagg/rpi-newer-crosstools) |
| linux-ppc64le         | CentOS 7 con devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                        |
| linux-s390x           | RHEL 7 con devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                          |
| linux-x64             | CentOS 7 con devtoolset-8 / GCC 8 <sup>[8](#fn8)</sup>                                                        |
| win-x64 y win-x86     | Windows 2012 R2 (x64) con Visual Studio 2019                                                                  |

<em id="fn8">8</em>: The Enterprise Linux devtoolset-8 allows us to compile binaries with GCC 8 but linked to the glibc and libstdc++ versions of the host platforms (CentOS 7 / RHEL 7). Therefore, binaries produced on these systems are compatible with glibc >= 2.17 and libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). These are available on distributions natively supporting GCC 4.9, such as Ubuntu 14.04 and Debian 8.

#### Soporte asm de OpenSSL

OpenSSL-1.1.1 requires the following assembler version for use of asm support on x86_64 and ia32.

Para uso de AVX-512,

* versión 2.26 o superior de gas (ensamblador GNU)
* nasm versión 2.11.8 o superior en Windows

AVX-512 está desactivado para Skylake-X por OpenSSL-1.1.1.

Para uso de AVX2,

* versión 2.23 o superior de gas (ensamblador GNU)
* Xcode versión 5.0 o superior
* llvm versión 3.3 o superior
* nasm versión 2.10 o superior en Windows

Please refer to <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> for details.

 If compiling without one of the above, use `configure` with the `--openssl-no-asm` flag. De lo contrario, `la configuración` fallará.

### Versiones anteriores de este documento

Las plataformas y las cadenas de herramientas soportadas cambian con cada versión principal de Node.js. Este documento sólo es válido para la versión principal actual de Node.js. Consulte versiones anteriores de este documento para versiones anteriores de Node.js:

* [Node.js 14](https://github.com/nodejs/node/blob/v14.x/BUILDING.md)
* [Node.js 12](https://github.com/nodejs/node/blob/v12.x/BUILDING.md)
* [Node.js 10](https://github.com/nodejs/node/blob/v10.x/BUILDING.md)

## Construyendo Node.js en plataformas soportadas

### Nota sobre Python

El proyecto Node.js soporta Python >= 3 para compilar y probar.
### Unix y macOS

#### Prerrequisitos Unix

* `gcc` y `g++` >= 8.3 o superior, o
* GNU Make 3.81 o superior
* Python 3.6, 3.7, 3.8 y 3.9 (ver nota arriba)

La instalación a través del gestor de paquetes Linux se puede lograr con:

* Ubuntu, Debian: `sudo apt-get install python3 g++ make`
* Fedora: `sudo dnf install python3 gcc-c++ make`
* CentOS y RHEL: `sudo yum install python3 gcc-c++ make`
* OpenSUSE: `sudo zypper install python3 gcc-c++ make`
* Arch Linux, Manjaro: `sudo pacman -S python gcc make`

Los usuarios de FreeBSD y OpenBSD también pueden necesitar instalar `libexecinfo`.

#### macOS prerequisites

* Herramientas de línea de comandos Xcode >= 11 para macOS
* Python 3.6, 3.7, 3.8 y 3.9 (ver nota arriba)

macOS users can install the `Xcode Command Line Tools` by running `xcode-select --install`. Alternatively, if you already have the full Xcode installed, you can find them under the menu `Xcode -> Open Developer Tool ->
More Developer Tools...`. This step will install `clang`, `clang++`, and `make`.

#### Construyendo Node.js

If the path to your build directory contains a space, the build will likely fail.

Para construir Node.js:

```console
$ ./configure
$ make -j4
```

The `-j4` option will cause `make` to run 4 simultaneous compilation jobs which may reduce build time. For more information, see the [GNU Make Documentation](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

The above requires that `python` resolves to a supported version of Python. Vea [Prerrequisitos](#prerequisites).

After building, setting up [firewall rules](tools/macos-firewall.sh) can avoid popups asking to accept incoming network connections when running tests.

Running the following script on macOS will add the firewall rules for the executable `node` in the `out` directory and the symbolic `node` link in the project's root directory.

```console
$ sudo ./tools/macos-firewall.sh
```

#### Instalando Node.js

Para instalar esta versión de Node.js en un directorio del sistema:

```bash
[sudo] hacer instalación
```

#### Pruebas en ejecución

Para verificar la compilación:

```console
$ hacer test-only
```

En este punto, está listo para hacer cambios de código y volver a ejecutar las pruebas.

If you are running tests before submitting a Pull Request, the recommended command is:

```console
$ hacer prueba -j4
```

`make -j4 test` does a full check on the codebase, including running linters and documentation tests.

Asegúrese de que el linter no reporte ningún problema y que todas las pruebas pasen. Please do not submit patches that fail either check.

If you want to run the linter without running tests, use `make lint`/`vcbuild lint`. Enlintar archivos JavaScript, C++ y Markdown.

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

Normalmente puede ejecutar pruebas directamente con node:

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

Remember to recompile with `make -j4` in between test runs if you change code in the `lib` or `src` directories.

The tests attempt to detect support for IPv6 and exclude IPv6 tests if appropriate. If your main interface has IPv6 addresses, then your loopback interface must also have '::1' enabled. For some default installations on Ubuntu that does not seem to be the case. To enable '::1' on the loopback interface on Ubuntu:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

You can use [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) to run/debug tests, if your IDE configs are present.

#### Cobertura en ejecución

Es una buena práctica asegurarse de que cualquier código que añadas o cambies está cubierto por pruebas. Puede hacerlo ejecutando la suite de pruebas con cobertura habilitada:

```console
$ ./configure --coverage
$ hacer cobertura
```

A detailed coverage report will be written to `coverage/index.html` for JavaScript coverage and to `coverage/cxxcoverage.html` for C++ coverage.

If you only want to run the JavaScript tests then you do not need to run the first command (`./configure --coverage`). Run `make coverage-run-js`, to execute JavaScript tests independently of the C++ test suite:

```text
$ hacer cobertura-run-js
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

El comando `make coverage` descarga algunas herramientas al directorio raíz del proyecto. Para limpiar después de generar los informes de cobertura:

```console
$ limpiar la cobertura
```

#### Creando la documentación

Para compilar la documentación:

Esto construirá Node.js primero (si es necesario) y luego lo usará para compilar los documentos:

```bash
hacer documento
```

Si tiene una compilación existente de Node.js, puede compilar sólo los documentos con:

```bash
NOD=/ruta/a/nodo hacer sólo doc-only
```

Para leer la página del manual:

```bash
man doc/node.1
```

Si prefiere leer la documentación completa en un navegador, ejecute lo siguiente.

```bash
hacer docserve
```

This will spin up a static file server and provide a URL to where you may browse the documentation locally.

If you're comfortable viewing the documentation using the program your operating system has associated with the default web browser, run the following.

```bash
hacer docopen
```

This will open a file URL to a one-page version of all the browsable HTML documents using the default browser.

Para probar si Node.js fue construido correctamente:

```bash
./node -e "console.log('Hola de Node.js ' + process.version)"
```

#### Construir una construcción de depuración

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

Cuando se utiliza el binario de depuración, los volcados de núcleo se generarán en caso de fallos. These core dumps are useful for debugging when provided with the corresponding original debug binary and system information.

Reading the core dump requires `gdb` built on the same platform the core dump was captured on (i.e. 64-bit `gdb` for `node` built on a 64-bit system, Linux `gdb` for `node` built on Linux) otherwise you will get errors like `not in executable format: File format not recognized`.

Ejemplo de generar un backtrace desde el volcado del núcleo:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Construyendo una construcción ASAN

[ASAN](https://github.com/google/sanitizers) can help detect various memory related bugs. Las versiones de ASAN sólo están soportadas actualmente en linux. If you want to check it on Windows or macOS or you want a consistent toolchain on Linux, you can try [Docker](https://www.docker.com/products/docker-desktop) (using an image like `gengjiawen/node-build:2020-02-14`).

The `--debug` is not necessary and will slow down build and testing, but it can show clear stacktrace if ASAN hits an issue.

``` console
$ ./configure --debug --enable-asan && make -j4
$ make test-only
```

#### Acelera las reconstrucciones frecuentes al desarrollar

If you plan to frequently rebuild Node.js, especially if using several branches, installing `ccache` can help to greatly reduce build times. Configurar con:
```console
$ sudo apt install ccache # para Debian/Ubuntu, incluido en la mayoría de distribuciones Linux
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # añade a tu . rofile
$ export CXX="ccache g++" # add to your .profile
```
Esto permitirá reconstruir casi al instante incluso cuando cambien ramas.

When modifying only the JS layer in `lib`, it is possible to externally load it without modifying the executable:
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
The resulting binary won't include any JS files and will try to load them from the specified directory. The JS debugger of Visual Studio Code supports this configuration since the November 2020 version and allows for setting breakpoints.

#### Solución de problemas para compilaciones Unix y macOS

Las compilaciones antiguas a veces pueden resultar en `archivos no encontrados` errores mientras se construyen. Este y algunos otros problemas pueden resolverse con `hacer distclean`. The `distclean` recipe aggressively removes build artifacts. You will need to build again (`make -j4`). Since all build artifacts have been removed, this rebuild may take a lot more time than previous builds. Additionally, `distclean` removes the file that stores the results of `./configure`. If you ran `./configure` with non-default options (such as `--debug`), you will need to run it again before invoking `make -j4`.

### Ventanas

#### Prerrequisitos

##### Opción 1: Instalación manual

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* The "Desktop development with C++" workload from [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) or the "C++ build tools" workload from the [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), with the default optional components
* Basic Unix tools required for some tests, [Git for Windows](https://git-scm.com/download/win) includes Git Bash and tools which can be included in the global `PATH`.
* El ensamblador [NetWide](https://www.nasm.us/)para módulos de ensamblador OpenSL. If not installed in the default location, it needs to be manually added to `PATH`. A build with the `openssl-no-asm` option does not need this, nor does a build targeting ARM64 Windows.

Requisitos opcionales para construir el paquete del instalador MSI:

* The [WiX Toolset v3.11](https://wixtoolset.org/releases/) and the [Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* The [WiX Toolset v3.14](https://wixtoolset.org/releases/) if building for Windows 10 on ARM (ARM64)

Requisitos opcionales para la compilación de Windows 10 en ARM (ARM64):

* Visual Studio 15.9.0 o superior
* Componentes opcionales de Visual Studio
  * Compiladores y bibliotecas Visual C++ para ARM64
  * ATL Visual C++ para ARM64
* Windows 10 SDK 10.0.17763.0 o superior

##### Opción 2: Instalación automática con Boxstarter

A [Boxstarter](https://boxstarter.org/) script can be used for easy setup of Windows systems with all the required prerequisites for Node.js development. This script will install the following [Chocolatey](https://chocolatey.org/) packages:

* [Git for Windows](https://chocolatey.org/packages/git) with the `git` and Unix tools added to the `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) with [Visual C++ workload](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [Colmena Netwide](https://chocolatey.org/packages/nasm)

To install Node.js prerequisites using [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), open <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> with Internet Explorer or Edge browser on the target machine.

Alternativamente, puedes usar PowerShell. Run those commands from an elevated PowerShell terminal:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex ((New-Object System. Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

The entire installation using Boxstarter will take up approximately 10 GB of disk space.

#### Construyendo Node.js

If the path to your build directory contains a space or a non-ASCII character, the build will likely fail.

```console
> .\vcbuild
```

Para ejecutar las pruebas:

```console
> .\vcbuild prueba
```

Para probar si Node.js fue construido correctamente:

```console
> Lanzamiento\node -e "console.log('Hola de Node.js', process.version)"
```

### Dispositivos basados en Android/Android (por ejemplo, Firefox OS)

Android no es una plataforma compatible. Patches to improve the Android build are welcome. There is no testing on Android in the current continuous integration environment. The participation of people dedicated and determined to improve Android building, testing, and support is encouraged.

Be sure you have downloaded and extracted [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) before in a folder. Luego ejecutar:

```console
$ ./android-configure /path/to/su/android-ndk
$ make
```

## `Soporte Intl` (ECMA-402)

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) support is enabled by default.

### Construir con soporte completo de ICU (todos los locales soportados por ICU)

Esta es la opción por defecto.

#### Unix/macOS

```console
$ ./configure --with-intl=full-icu
```

#### Ventanas

```console
> .\vcbuild full-icu
```

### Trimmed: `small-icu` (solo en inglés) soporte

 In this configuration, only English data is included, but the full `Intl` (ECMA-402) APIs.  It does not need to download any dependencies to function. Puede añadir datos completos en tiempo de ejecución.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Ventanas

```console
> .\vcbuild small-icu
```

### Construyendo sin soporte Intl

The `Intl` object will not be available, nor some other APIs such as `String.normalize`.

#### Unix/macOS

```console
$ ./configure --without-intl
```

#### Ventanas

```console
> .\vcbuild sin intl
```

### Usar ICU instalado (sólo Unix/macOS)

```console
$ pkg-config --modversion icu-i18n && ./configure --with-intl=system-icu
```

If you are cross-compiling, your `pkg-config` must be able to supply a path that works for both your host and target environments.

### Construir con un ICU específico

You can find other ICU releases at [the ICU homepage](http://site.icu-project.org/download). Download the file named something like `icu4c-**##.#**-src.tgz` (or `.zip`).

To check the minimum recommended ICU, run `./configure --help` and see the help for the `--with-icu-source` option. A warning will be printed during configuration if the ICU version is too old.

#### Unix/macOS

Desde un ICU ya desempaquetado:

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/to/icu
```

Desde un tarball local de ICU:

```console
$ ./configure --with-intl=[small-icu,full-icu] --with-icu-source=/path/to/icu.tgz
```

Desde una URL de tarball:

```console
$ ./configure --with-intl=full-icu --with-icu-source=http://url/to/icu.tgz
```

#### Ventanas

First unpack latest ICU to `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (or `.zip`) as `deps/icu` (You'll have: `deps/icu/source/...`)

```console
> .\vcbuild full-icu
```

## Construyendo Node.js con OpenSSL compatible con FIPS

The current version of Node.js does not support FIPS when statically linking (the default) with OpenSSL 1.1.1 but for dynamically linking it is possible to enable FIPS using the configuration flag `--openssl-is-fips`.

### Configuración y construcción de quictls/openssl para FIPS

Para quictls/openssl 3.0 es posible activar FIPS al enlazar dinámicamente. Node.js currently uses openssl-3.0.0+quic which can be configured as follows:
```console
$ git clone git@github.com:quictls/openssl.git
$ cd openssl
$ ./config --prefix=/path/to/install/dir/ shared enable-fips linux-x86_64
```
Esto puede ser compilado e instalado usando los siguientes comandos:
```console
$ make -j8
$ make install_sldirs
$ make install_fips
```

After the FIPS module and configuration file have been installed by the above instructions we also need to update `/path/to/install/dir/ssl/openssl.cnf` to use the generated FIPS configuration file (`fipsmodule.cnf`):
```text
.include fipsmodule. nf

# Lista de proveedores a cargar
[provider_sect]
por defecto = default_sect
# El nombre de sección fips debe coincidir con el nombre de sección dentro del
# incluido /path/to/install/dir/ssl/fipsmodule. nf.
fips = fips_sect

[default_sect]
activar = 1
```

In the above case OpenSSL is not installed in the default location so two environment variables need to be set, `OPENSSL_CONF`, and `OPENSSL_MODULES` which should point to the OpenSSL configuration file and the directory where OpenSSL modules are located:
```console
$ export OPENSSL_CONF=/path/to/install/dir/ssl/openssl.cnf
$ export OPENSSL_MODULES=/path/to/install/dir/lib/ossl-modules
```

Node.js puede configurarse para habilitar FIPS:
```console
$ ./configure --shared-openssl --shared-openssl-libpath=/path/to/install/dir/lib --shared-openssl-includes=/path/to/install/dir/include --shared-openssl-libname=crypto,ssl --openssl-is-fips
$ export LD_LIBRARY_PATH=/path/to/install/dir/lib
$ make -j8
```

Verificar el ejecutable producido:
```console
$ ldd ./node
    linux-vdso.so.1 (0x00007ffd7917b000)
    libcrypto.so.81. => /ruta/to/install/dir/lib/libcrypto.so.81.3 (0x00007fd911321000)
    libssl.so.81. => /ruta/to/install/dir/lib/libssl.so.81.3 (0x00007fd91125e000)
    libdl.so. => /usr/lib64/libdl.so.2 (0x00007fd911232000)
    libstdc++.so.6 => /usr/lib64/libstdc++.so. (0x00007fd911039000)
    libm.so.6 => /usr/lib64/libm.so.6 (0x00007fd910ef3000)
    libgcc_s. o.1 => /usr/lib64/libgcc_s.so.1 (0x00007fd910ed9000)
    libpthread. o.0 => /usr/lib64/libpthread.so.0 (0x00007fd910eb5000)
    libc.so.6 => /usr/lib64/libc.so.6 (0x00007fd910cec000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fd9117f2000)
```
If the `ldd` command says that `libcrypto` cannot be found one needs to set `LD_LIBRARY_PATH` to point to the directory used above for `--shared-openssl-libpath` (see previous step).

Verificar la versión OpenSSL:
```console
$ ./node -p process.versions.openssl
3.0.0-alpha16+quic
```

Verificar que FIPS está disponible:
```console
$ ./node -p 'process.config.variables.openssl_is_fips'
true
$ ./node --enable-fips -p 'crypto.getFips()'
1
```

FIPS support can then be enable via the OpenSSL configuration file or using `--enable-fips` or `--force-fips` command line options to the Node.js executable. See sections [Enabling FIPS using Node.js options](#enabling-fips-using-node.js-options) and [Enabling FIPS using OpenSSL config](#enabling-fips-using-openssl-config) below.

### Habilitando FIPS usando opciones de Node.js
This is done using one of the Node.js options `--enable-fips` or `--force-fips`, for example:
```console
$ nodo --enable-fips -p 'crypto.getFips()'
```

### Habilitando FIPS usando configuración OpenSSL
This example show that using OpenSSL's configuration file, FIPS can be enabled without specifying the `--enable-fips` or `--force-fips` options by setting `default_properties = fips=yes` in the FIPS configuration file. See [link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) for details.

For this to work the OpenSSL configuration file (default openssl.cnf) needs to be updated. A continuación se muestra un ejemplo:
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

## Construyendo Node.js con módulos principales externos

It is possible to specify one or more JavaScript text files to be bundled in the binary as built-in modules when building Node.js.

### Unix/macOS

This command will make `/root/myModule.js` available via `require('/root/myModule')` and `./myModule2.js` available via `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Ventanas

To make `./myModule.js` available via `require('myModule')` and `./myModule2.js` available via `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Nota para los distribuidores downstream de Node.js
¡Hola mundo!

El ecosistema Node.js depende de la compatibilidad de ABI dentro de una versión importante. To maintain ABI compatibility it is required that distributed builds of Node.js be built against the same version of dependencies, or similar versions that do not break their ABI compatibility, as those released by Node.js for any given `NODE_MODULE_VERSION` (located in `src/node_version.h`).

When Node.js is built (with an intention to distribute) with an ABI incompatible with the official Node.js builds (e.g. using a ABI incompatible version of a dependency), please reserve and use a custom `NODE_MODULE_VERSION` by opening a pull request against the registry available at [https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
