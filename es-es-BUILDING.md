# Construyendo Node.js

Dependiendo de qué plataforma o características necesitas, el proceso de construcción puede diferir. Después de haber construido un binario, ejecutando la suite de pruebas para confirmar que el binario funciona según lo previsto es un buen paso a continuación.

Si puede reproducir un fallo de prueba, busque en el [rastreador de problemas de Node.js](https://github.com/nodejs/node/issues) o presente un nuevo problema.

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

Esta lista de plataformas soportadas es actual a partir de la sucursal/liberación a la que pertenece.

### Input

Node.js depende de V8 y libuv. Adoptamos un subconjunto de sus plataformas soportadas.

### Estrategia

Hay tres niveles de apoyo:

* **Nivel 1**: Estas plataformas representan la mayoría de los usuarios de Node.js. El Grupo de Trabajo de Construcción Node.js mantiene infraestructura para una cobertura completa de pruebas. Los fallos de prueba en plataformas de nivel 1 bloquearán lanzamientos.
* **Nivel 2**: Estas plataformas representan segmentos más pequeños de la base de usuario de Node.js. El Grupo de Trabajo de Construcción Node.js mantiene infraestructura para una cobertura completa de pruebas. Los fallos de prueba en plataformas de nivel 2 bloquearán lanzamientos. Los problemas de infraestructura pueden retrasar la liberación de binarios para estas plataformas.
* **Experimental**: No se puede compilar o probar suite no puede pasar. El equipo central no crea versiones para estas plataformas. Los fallos de prueba en plataformas experimentales no bloquean lanzamientos. Acogemos con satisfacción las contribuciones para mejorar el apoyo a estas plataformas.

Las plataformas pueden moverse entre niveles entre las principales líneas de lanzamiento. La siguiente tabla reflejará esos cambios.

### Lista de plataformas

El soporte de compilación/ejecución de Node.js depende del sistema operativo, la arquitectura y la versión libc. La siguiente tabla muestra el nivel de soporte para cada combinación soportada. También se proporciona una lista de [herramientas de compilación soportadas](#supported-toolchains) para plataformas de nivel 1.

**Para aplicaciones de producción, ejecute Node.js sólo en plataformas soportadas.**

Node.js no soporta una versión de la plataforma si un proveedor ha expirado el soporte para ella. En otras palabras, Node.js no soporta la ejecución en plataformas de End-of-Life (EoL). Esto es cierto independientemente de las entradas en la tabla de abajo.

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

<em id="fn1">1</em>: GCC 8 no está disponible en la plataforma base. Los usuarios necesitarán la versión de prueba de [Toolchain PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) o similar para crear un compilador más reciente.

<em id="fn2">2</em>: GCC 8 no está disponible en la plataforma base. Los usuarios necesitarán el [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) o posterior para crear un compilador más reciente.

<em id="fn3">3</em>: Las versiones antiguas del núcleo pueden funcionar para ARM64. Sin embargo, la infraestructura de pruebas Node.js solo prueba >= 4.5.

<em id="fn4">4</em>: En Windows, ejecutando Node. s en emuladores de terminal de Windows como `mintty` requiere el uso de [winpty](https://github.com/rprichard/winpty) para que los canales tty funcionen (e. . `winpty node.exe script.js`). En "Git bash" si llama al alias del shell del nodo (`node` sin el `. xe` extension), `winpty` se utiliza automáticamente.

<em id="fn5">5</em>: El subsistema de Windows para Linux (WSL) no es compatible, pero el proceso de construcción de GNU/Linux y los binarios deberían funcionar. La comunidad sólo abordará los problemas que se reproducen en sistemas GNU/Linux nativos. Los problemas que solo se reproduzcan en WSL deben ser reportados en el [gestor de incidencias WSL](https://github.com/Microsoft/WSL/issues). No se recomienda ejecutar el binario de Windows (`node.exe`) en WSL. No funcionará sin la reorientación de stdio como por ejemplo.

<em id="fn6">6</em>: Ejecutar Node.js en x86 Windows debería funcionar y los binarios son proporcionados. Sin embargo, las pruebas en nuestra infraestructura sólo funcionan en WoW64. Además, la compilación en x86 Windows es Experimental y puede no ser posible.

<em id="fn7">7</em>: El compilador predeterminado de FreeBSD 12.0 es Clang 6.0.1, pero FreeBSD 12.1 se actualiza a 8.0.1. Otras versiones Clang/LLVM están disponibles a través del gestor de paquetes del sistema, incluyendo Clang 9.0.

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

<em id="fn8">8</em>: El Enterprise Linux devtoolset-8 nos permite compilar binarios con GCC 8 pero enlazados a las versiones glibc y libstdc++ de las plataformas host (CentOS 7 / RHEL 7). Por lo tanto, los binarios producidos en estos sistemas son compatibles con glibc >= 2.17 y libstdc++ >= 6.0.20 (`GLIBCX_3.4.20`). Estas están disponibles en distribuciones que soportan nativamente GCC 4.9, como Ubuntu 14.04 y Debian 8.

#### Soporte asm de OpenSSL

OpenSSL-1.1.1 requiere la siguiente versión de ensamblador para usar soporte asm en x86_64 e ia32.

Para uso de AVX-512,

* versión 2.26 o superior de gas (ensamblador GNU)
* nasm versión 2.11.8 o superior en Windows

AVX-512 está desactivado para Skylake-X por OpenSSL-1.1.1.

Para uso de AVX2,

* versión 2.23 o superior de gas (ensamblador GNU)
* Xcode versión 5.0 o superior
* llvm versión 3.3 o superior
* nasm versión 2.10 o superior en Windows

Consulte <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> para más detalles.

 Si se compila sin uno de los anteriores, use `configure` con el parámetro `--openssl-no-asm`. De lo contrario, `la configuración` fallará.

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

los usuarios de macOS pueden instalar `Xcode Command Line Tools` ejecutando `xcode-select --install`. Alternativamente, si ya tiene instalado el Xcode completo, puedes encontrarlos en el menú `Xcode -> Open Developer Tool ->
Más Herramientas para desarrolladores. .`. Este paso instalará `clang`, `clang++`y `make`.

#### Construyendo Node.js

Si la ruta a su directorio de compilación contiene un espacio, la construcción probablemente fallará.

Para construir Node.js:

```console
$ ./configure
$ make -j4
```

La opción `-j4` causará que `make` ejecute 4 trabajos de compilación simultáneos que pueden reducir el tiempo de construcción. Para más información, consulte la [Documentación de GNU Make](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

Lo anterior requiere que `python` resuelva una versión compatible de Python. Vea [Prerrequisitos](#prerequisites).

Después de construir, configurar [reglas de firewall](tools/macos-firewall.sh) puede evitar ventanas emergentes pidiendo aceptar conexiones de red entrantes cuando se ejecutan pruebas.

Ejecutar el siguiente script en macOS añadirá las reglas de cortafuegos para el `nodo ejecutable` en el directorio `out` y el enlace `nodo` simbólico en el directorio raíz del proyecto.

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

Si está ejecutando pruebas antes de enviar una Pull Request, el comando recomendado es:

```console
$ hacer prueba -j4
```

`make -j4 test` hace un chequeo completo en el código base, incluyendo ejecutando linters y pruebas de documentación.

Asegúrese de que el linter no reporte ningún problema y que todas las pruebas pasen. Por favor, no envíe parches que fallen en cualquiera de las dos comprobaciones.

Si quieres ejecutar el linter sin ejecutar pruebas, usa `make lint`/`vcbuild lint`. Enlintar archivos JavaScript, C++ y Markdown.

Si está actualizando pruebas y desea ejecutar pruebas en un solo archivo de prueba (por ejemplo, `test/parallel/test-stream2-transform.js`):

```text
$ python tools/test.py test/parallel/test-stream2-transform.js
```

Puede ejecutar todo el conjunto de pruebas para un subsistema dado proporcionando el nombre de un subsistema:

```text
$ python tools/test.py -J --mode=release child-process
```

Si desea comprobar las otras opciones, por favor consulte la ayuda usando la opción `--help`:

```text
$ python tools/test.py --help
```

Normalmente puede ejecutar pruebas directamente con node:

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

Recuerda recompilar con `make -j4` entre ejecuciones de prueba si cambias el código en los directorios `lib` o `src`.

Las pruebas intentan detectar el soporte para IPv6 y excluir las pruebas IPv6 si es apropiado. Si su interfaz principal tiene direcciones IPv6, entonces su interfaz de loopback también debe tener '::1' habilitado. Para algunas instalaciones por defecto en Ubuntu no parece ser el caso. Para habilitar '::1' en la interfaz de bucle en Ubuntu:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

Puede usar [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) para ejecutar/debug tests, si sus configuraciones IDE están presentes.

#### Cobertura en ejecución

Es una buena práctica asegurarse de que cualquier código que añadas o cambies está cubierto por pruebas. Puede hacerlo ejecutando la suite de pruebas con cobertura habilitada:

```console
$ ./configure --coverage
$ hacer cobertura
```

Un informe detallado de cobertura será escrito en `coverage/index.html` para cobertura JavaScript y en `coverage/cxxcoverage.html` para cobertura de C++.

Si solo desea ejecutar las pruebas de JavaScript, entonces no necesita ejecutar el primer comando (`./configure --coverage`). Ejecute `make coverage-run-js`, para ejecutar pruebas JavaScript independientemente del conjunto de pruebas C++:

```text
$ hacer cobertura-run-js
```

Si está actualizando las pruebas y desea recopilar la cobertura de un solo archivo de prueba (por ejemplo, `test/parallel/test-stream2-transform.js`):

```text
$ make coverage-clean
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/parallel/test-stream2-transform.js
$ make coverage-report-js
```

Puede recoger la cobertura de todo el conjunto de pruebas para un subsistema dado proporcionando el nombre de un subsistema:

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

Esto girará un servidor de archivos estáticos y proporcionará una URL a donde podrá navegar por la documentación localmente.

Si está cómodo viendo la documentación usando el programa que su sistema operativo ha asociado con el navegador web por defecto, ejecute lo siguiente.

```bash
hacer docopen
```

Esto abrirá una URL de archivo a una versión de una página de todos los documentos HTML navegables usando el navegador predeterminado.

Para probar si Node.js fue construido correctamente:

```bash
./node -e "console.log('Hola de Node.js ' + process.version)"
```

#### Construir una construcción de depuración

Si encuentras un problema en el que la información proporcionada por la stack trace JS no es suficiente, o si sospecha que el error ocurre fuera de la máquina virtual JS, puede intentar construir un binario habilitado para depuración:

```console
$ ./configure --debug
$ make -j4
```

`haz` con `. configure --debug` genera dos binarios, el lanzamiento regular uno en `out/Release/node` y un binario de depuración en `out/Debug/node`, sólo la versión de lanzamiento está instalada cuando ejecute `make install`.

Para usar la compilación de depuración con todas las dependencias normales sobreescribe la versión de lanzamiento en el directorio de instalación:

``` console
$ make install PREFIX=/opt/node-debug/
$ cp -a -f out/Debug/node /opt/node-debug/node
```

Cuando se utiliza el binario de depuración, los volcados de núcleo se generarán en caso de fallos. Estos volcados de núcleo son útiles para depurar cuando se les proporciona la correspondiente información original del binario de depuración e información del sistema.

La lectura del núcleo requiere `gdb` construido en la misma plataforma en la que fue capturado el núcleo (i.e. 64-bit `gdb` para `nodo` construido en un sistema de 64-bit Linux `gdb` para `nodo` construido en Linux) de lo contrario obtendrá errores como `no en formato ejecutable: formato de archivo no reconocido`.

Ejemplo de generar un backtrace desde el volcado del núcleo:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Construyendo una construcción ASAN

[ASAN](https://github.com/google/sanitizers) puede ayudar a detectar varios errores relacionados con la memoria. Las versiones de ASAN sólo están soportadas actualmente en linux. Si quieres marcarlo en Windows o macOS o quieres una toolchain consistente en Linux, puedes probar [Docker](https://www.docker.com/products/docker-desktop) (usando una imagen como `gengjiawen/node-build:2020-02-14`).

El `--debug` no es necesario y ralentizará la compilación y las pruebas, pero puede mostrar stacktrace claro si ASAN golpea un problema.

``` console
$ ./configure --debug --enable-asan && make -j4
$ make test-only
```

#### Acelera las reconstrucciones frecuentes al desarrollar

Si planeas reconstruir Node.js con frecuencia, especialmente si usas varias ramas, instalar `ccache` puede ayudar a reducir considerablemente los tiempos de compilación. Configurar con:
```console
$ sudo apt install ccache # para Debian/Ubuntu, incluido en la mayoría de distribuciones Linux
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # añade a tu . rofile
$ export CXX="ccache g++" # add to your .profile
```
Esto permitirá reconstruir casi al instante incluso cuando cambien ramas.

Al modificar solo la capa JS en `lib`, es posible cargarla externamente sin modificar el ejecutable:
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
El binario resultante no incluirá ningún archivo JS e intentará cargarlos desde el directorio especificado. El depurador JS de Visual Studio Code soporta esta configuración desde la versión Noviembre 2020 y permite establecer puntos de interrupción.

#### Solución de problemas para compilaciones Unix y macOS

Las compilaciones antiguas a veces pueden resultar en `archivos no encontrados` errores mientras se construyen. Este y algunos otros problemas pueden resolverse con `hacer distclean`. La receta `` distícula agresivamente elimina la construcción de artefactos. Necesitarás construir de nuevo (`make -j4`). Dado que todos los artefactos de construcción han sido eliminados, esta reconstrucción puede tomar mucho más tiempo que las versiones anteriores. Además, `distclean` elimina el archivo que almacena los resultados de `./configure`. Si corriste `. configure` con opciones no predeterminadas (como `--debug`), necesitará volver a ejecutarlo antes de invocar `make -j4`.

### Ventanas

#### Prerrequisitos

##### Opción 1: Instalación manual

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* La carga de trabajo "Desktop development with C++" de [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) o la carga de trabajo "C++ build tools" de [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), con los componentes opcionales por defecto
* Herramientas Unix básicas requeridas para algunas pruebas, [Git para Windows](https://git-scm.com/download/win) incluye Git Bash y herramientas que pueden ser incluidas en el global `PATH`.
* El ensamblador [NetWide](https://www.nasm.us/)para módulos de ensamblador OpenSL. Si no está instalado en la ubicación predeterminada, debe añadirse manualmente a `PATH`. Una compilación con la opción `openssl-no-asm` no necesita esto, ni una compilación orientada a ARM64 Windows.

Requisitos opcionales para construir el paquete del instalador MSI:

* [WiX Toolset v3.11](https://wixtoolset.org/releases/) y la extensión [Wix Toolset Visual Studio 2019](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* El [WiX Toolset v3.14](https://wixtoolset.org/releases/) si se construye para Windows 10 en ARM (ARM64)

Requisitos opcionales para la compilación de Windows 10 en ARM (ARM64):

* Visual Studio 15.9.0 o superior
* Componentes opcionales de Visual Studio
  * Compiladores y bibliotecas Visual C++ para ARM64
  * ATL Visual C++ para ARM64
* Windows 10 SDK 10.0.17763.0 o superior

##### Opción 2: Instalación automática con Boxstarter

Un script [Boxstarter](https://boxstarter.org/) puede utilizarse para una fácil configuración de sistemas Windows con todos los requisitos previos necesarios para el desarrollo de Node.js. Este script instalará los siguientes paquetes de [Chocolatey](https://chocolatey.org/):

* [Git para Windows](https://chocolatey.org/packages/git) con las herramientas `git` y Unix añadidas al `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Compilar Herramientas](https://chocolatey.org/packages/visualstudio2019buildtools) con [Visual C++ de carga de trabajo](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [Colmena Netwide](https://chocolatey.org/packages/nasm)

Para instalar los requisitos de Node.js usando [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), abre <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> con Internet Explorer o navegador Edge en la máquina de destino.

Alternativamente, puedes usar PowerShell. Ejecuta esos comandos desde un terminal de PowerShell elevado:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex (New-Object System. Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

La instalación completa con Boxstarter ocupará aproximadamente 10 GB de espacio en disco.

#### Construyendo Node.js

Si la ruta a su directorio de compilación contiene un espacio o un carácter no ASCII, la compilación probablemente fallará.

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

Android no es una plataforma compatible. Parches para mejorar la versión de Android son bienvenidos. No hay pruebas en Android en el entorno actual de integración continua. Se alienta la participación de personas dedicadas y decididas a mejorar la construcción de Android, las pruebas y el apoyo.

Asegúrese de que ha descargado y extraído [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) antes en una carpeta. Luego ejecutar:

```console
$ ./android-configure /path/to/su/android-ndk
$ make
```

## `Soporte Intl` (ECMA-402)

[El soporte de Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) está habilitado por defecto.

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

 En esta configuración, sólo se incluyen los datos en inglés, pero las APIs `Intl` (ECMA-402) completas.  No necesita descargar ninguna dependencia para funcionar. Puede añadir datos completos en tiempo de ejecución.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Ventanas

```console
> .\vcbuild small-icu
```

### Construyendo sin soporte Intl

El objeto `Intl` no estará disponible, ni alguna otra API como `String.normalize`.

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

Si está compilando entre sí, su `pkg-config` debe ser capaz de proporcionar una ruta que funcione tanto para su host como para entornos de destino.

### Construir con un ICU específico

Puede encontrar otros lanzamientos de ICU en [la página principal de ICU](http://site.icu-project.org/download). Descarga el archivo llamado algo como `icu4c-**##.#**-src.tgz` (o `.zip`).

Para comprobar el ICU mínimo recomendado, ejecute `./configure --help` y vea la ayuda para la opción `--with-icu-source`. Se imprimirá una advertencia durante la configuración si la versión de ICU es demasiado antigua.

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

Primero descomprima la última ICU a `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (o `. ip`) como `deps/icu` (Tendrás: `deps/icu/source/...`)

```console
> .\vcbuild full-icu
```

## Construyendo Node.js con OpenSSL compatible con FIPS

La versión actual de Node.js no soporta FIPS cuando se enlaza estáticamente (el valor por defecto) con OpenSSL 1.1. pero para enlazar dinámicamente es posible habilitar FIPS usando el indicador de configuración `--openssl-is-fips`.

### Configuración y construcción de quictls/openssl para FIPS

Para quictls/openssl 3.0 es posible activar FIPS al enlazar dinámicamente. Node.js actualmente usa openssl-3.0.0+quic que puede configurarse de la siguiente manera:
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

Después de que el módulo FIPS y el archivo de configuración hayan sido instalados por las instrucciones anteriores, también necesitamos actualizar `/path/to/install/dir/ssl/openssl. nf` para usar el archivo de configuración FIPS generado (`fipsmodule.cnf`):
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

En el caso anterior OpenSSL no está instalado en la ubicación predeterminada, por lo que deben establecerse dos variables de entorno, `OPENSSL_CONF`, y `OPENSSL_MODULES` que debería apuntar al archivo de configuración OpenSSL y al directorio donde se encuentran los módulos OpenSSL:
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
Si el comando `ldd` dice que `libcrypto` no se puede encontrar, uno necesita establecer `LD_LIBRARY_PATH` para apuntar al directorio usado anteriormente para `--shared-openssl-libpath` (ver paso anterior).

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

El soporte FIPS se puede habilitar a través del archivo de configuración OpenSSL o usando `--enable-fips` o `--force-fips` opciones de línea de comandos al Node. , ejecutable . Vea las secciones [Habilitando FIPS usando las opciones de Node.js](#enabling-fips-using-node.js-options) y [Habilitando FIPS usando la configuración OpenSSL](#enabling-fips-using-openssl-config) a continuación.

### Habilitando FIPS usando opciones de Node.js
Esto se hace usando una de las opciones de Node.js `--enable-fips` o `--force-fips`, por ejemplo:
```console
$ nodo --enable-fips -p 'crypto.getFips()'
```

### Habilitando FIPS usando configuración OpenSSL
Este ejemplo muestra que usando el archivo de configuración de OpenSSL, FIPS puede habilitarse sin especificar las opciones `--enable-fips` o `--force-fips` configurando `default_properties = fips=yes` en el archivo de configuración FIPS. Vea [enlace](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) para más detalles.

Para que esto funcione es necesario actualizar el archivo de configuración OpenSSL (por defecto openssl.cnf). A continuación se muestra un ejemplo:
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
Después de este cambio, Node.js puede ejecutarse sin las opciones `--enable-fips` o `--force-fips`.

## Construyendo Node.js con módulos principales externos

Es posible especificar uno o más archivos de texto JavaScript que serán empaquetados en el binario como módulos integrados al construir Node.js.

### Unix/macOS

Este comando hará que `/root/myModule.js` esté disponible vía `require('/root/myModule')` y `./myModule2.js` disponibles vía `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Ventanas

Para que `./myModule.js` esté disponible vía `require('myModule')` y `./myModule2.js` disponible vía `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Nota para los distribuidores downstream de Node.js

El ecosistema Node.js depende de la compatibilidad de ABI dentro de una versión importante. Para mantener la compatibilidad con ABI es necesario que las compilaciones distribuidas de Node. se construirán contra la misma versión de dependencias, o versiones similares que no rompan su compatibilidad con ABI, como las liberadas por Node. s para cualquier `NODE_MODULE_VERSION` dado (ubicado en `src/node_version.h`).

Cuando Node.js se construye (con la intención de distribuir) con un ABI incompatible con las compilaciones oficiales de Node.js (p. ej. usando una versión ABI incompatible de una dependencia), por favor reserva y usa un `NODE_MODULE_VERSION personalizado` abriendo una pull request contra el registro disponible en [https://github. om/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
