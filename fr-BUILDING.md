# Construire Node.js

Selon la plate-forme ou les fonctionnalités dont vous avez besoin, le processus de compilation peut être différent. Après avoir compilé un binaire, exécuter la suite de tests pour confirmer que le binaire fonctionne comme prévu est une bonne étape suivante.

Si vous pouvez reproduire un échec de test, recherchez le dans le [suivi de tickets Node.js](https://github.com/nodejs/node/issues) ou remplissez un nouveau ticket.

## Table des matières!

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

Cette liste des plates-formes supportées est à jour à partir de la branche/version à laquelle elle appartient.

### Input

Node.js repose sur V8 et libuv. Nous adoptons un sous-ensemble de leurs plates-formes supportées.

### Stratégie

Il y a trois paliers de support :

* **Tier 1**: Ces plateformes représentent la majorité des utilisateurs de Node.js. Le groupe de travail Node.js Build maintient l'infrastructure pour une couverture complète des tests. Les échecs de test sur les plateformes de niveau 1 bloqueront les versions.
* **Tier 2**: Ces plateformes représentent des segments plus petits de la base d'utilisateurs de Node.js. Le groupe de travail Node.js Build maintient l'infrastructure pour une couverture complète des tests. Les échecs de test sur les plateformes de niveau 2 bloqueront les versions. Les problèmes d'infrastructure peuvent retarder la publication de binaires pour ces plates-formes.
* **Expérimental**: Peut ne pas compiler ou tester suite peut ne pas passer. L'équipe principale ne crée pas de versions pour ces plates-formes. Les échecs de test sur les plates-formes expérimentales ne bloquent pas les versions. Les contributions destinées à améliorer le support de ces plateformes sont les bienvenues.

Les plateformes peuvent se déplacer entre les niveaux entre les lignes de publication majeures. Le tableau ci-dessous reflétera ces changements.

### Liste des plateformes

Le support de la compilation/exécution de Node.js dépend du système d'exploitation, de l'architecture et de la version libc. Le tableau ci-dessous liste le niveau de support pour chaque combinaison supportée. Une liste de [chaînes de compilation supportées](#supported-toolchains) est également fournie pour les plates-formes de niveau 1.

**Pour les applications de production, exécutez Node.js uniquement sur les plates-formes supportées.**

Node.js ne prend pas en charge une version de plate-forme si un fournisseur a expiré le support pour elle. En d'autres termes, Node.js ne prend pas en charge l'exécution sur les plates-formes de fin de vie (EoL). Ceci est vrai indépendamment des entrées dans le tableau ci-dessous.

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

<em id="fn1">1</em>: GCC 8 n'est pas fourni sur la plate-forme de base. Les utilisateurs auront besoin du test [Toolchain builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) ou similaire à la source d'un compilateur plus récent.

<em id="fn2">2</em>: GCC 8 n'est pas fourni sur la plate-forme de base. Les utilisateurs auront besoin du [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) ou ultérieur pour source un compilateur plus récent.

<em id="fn3">3</em>: Les anciennes versions du noyau peuvent fonctionner pour ARM64. Cependant l'infrastructure de test Node.js ne teste que >= 4.5.

<em id="fn4">4</em>: On Windows, running Node.js in Windows terminal emulators like `mintty` requires the usage of [winpty](https://github.com/rprichard/winpty) for the tty channels to work (e.g. `winpty node.exe script.js`). Dans "Git bash" si vous appelez l'alias du shell du noeud (`node` sans le `. extension xe` ), `winpty` est utilisé automatiquement.

<em id="fn5">5</em>: Le sous-système Windows pour Linux (WSL) n'est pas pris en charge, mais le processus de compilation et les binaires GNU/Linux devraient fonctionner. La communauté ne traitera que les problèmes qui se reproduisent sur les systèmes natifs GNU/Linux. Les problèmes qui ne se reproduisent que sur WSL doivent être signalés dans le [suiveur de problèmes WSL](https://github.com/Microsoft/WSL/issues). L'exécution du binaire Windows (`node.exe`) dans WSL n'est pas recommandée. Il ne fonctionnera pas sans contournements tels que la redirection stdio.

<em id="fn6">6</em>: L'exécution de Node.js sur Windows x86 devrait fonctionner et les binaires sont fournis. Cependant, les tests dans notre infrastructure ne fonctionnent que sur WoW64. De plus, la compilation sur x86 Windows est expérimentale et peut ne pas être possible.

<em id="fn7">7</em>: Le compilateur par défaut FreeBSD 12.0 est Clang 6.0.1, or FreeBSD 12.1 passe à 8.0.1. D'autres versions de Clang/LLVM sont disponibles via le gestionnaire de paquets du système, y compris Clang 9.0.

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

<em id="fn8">8</em>: Le devtoolset-8 Enterprise Linux nous permet de compiler des binaires avec GCC 8 mais liés aux versions glibc et libstdc++ des plates-formes hôtes (CentOS 7 / RHEL 7). Par conséquent, les binaires produits sur ces systèmes sont compatibles avec glibc >= 2.17 et libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). Ceux-ci sont disponibles sur les distributions prenant en charge nativement GCC 4.9, comme Ubuntu 14.04 et Debian 8.

#### Prise en charge d'OpenSSL asm

OpenSSL-1.1.1 requiert la version assembleur suivante pour utiliser le support asm sur x86_64 et ia32.

Pour l'utilisation de AVX-512,

* gas (assembleur GNU) version 2.26 ou supérieure
* nasm version 2.11.8 ou supérieure dans Windows

AVX-512 est désactivé pour Skylake-X par OpenSSL-1.1.1.

Pour l'utilisation de AVX2,

* gas (assembleur GNU) version 2.23 ou supérieure
* Xcode version 5.0 ou supérieure
* llvm version 3.3 ou supérieure
* nasm version 2.10 ou supérieure dans Windows

Veuillez vous référer à <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> pour plus de détails.

 Si vous compilez sans l'un des éléments ci-dessus, utilisez `configure` avec l'option `--openssl-no-asm`. Sinon, `configure` échouera.

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

Les utilisateurs de macOS peuvent installer les `Outils de ligne de commande Xcode` en exécutant `xcode-select --install`. Alternativement, si vous avez déjà installé le Xcode complet, vous pouvez les trouver dans le menu `Xcode -> Open Developer Tool ->
Plus d'outils développeurs. .`. Cette étape installera `clang`, `clang++`et `fera`.

#### Construire Node.js

Si le chemin d'accès à votre répertoire de compilation contient un espace, la compilation échouera probablement.

Pour construire Node.js :

```console
$ ./configure
$ make -j4
```

L'option `-j4` fera que `make` exécutera 4 tâches de compilation simultanée qui peuvent réduire le temps de compilation. Pour plus d'informations, voir la [documentation GNU Make](https://www.gnu.org/software/make/manual/html_node/Parallel.html).

Ce qui précède nécessite que `python` se résout à une version supportée de Python. Voir [Prérequis](#prerequisites).

Après la construction, la configuration des [règles de pare-feu](tools/macos-firewall.sh) peut éviter les popups demandant d'accepter les connexions réseau entrantes lors de l'exécution des tests.

Exécuter le script suivant sur macOS ajoutera les règles de pare-feu pour le nœud exécutable `` dans le répertoire `out` et le lien symbolique `node` dans le répertoire racine du projet.

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

Si vous exécutez des tests avant de soumettre une Pull Request, la commande recommandée est :

```console
$ faire -j4 test
```

`faire un test -j4` fait une vérification complète sur la base de code, y compris l'exécution de linters et des tests de documentation.

Assurez-vous que le linter ne signale aucun problème et que tous les tests réussissent. Veuillez ne pas soumettre de correctifs qui échouent dans l'une ou l'autre des vérifications.

Si vous voulez exécuter le linter sans exécuter de tests, utilisez `make lint`/`vcbuild lint`. Il va linter les fichiers JavaScript, C++ et Markdown.

Si vous mettez à jour les tests et que vous voulez exécuter les tests dans un seul fichier de test (par exemple `test/parallel/test-stream2-transform.js` ) :

```text
$ python tools/test.py test/parallel/test-stream2-transform.js
```

Vous pouvez exécuter toute la suite de tests pour un sous-système donné en fournissant le nom d'un sous-système :

```text
$ python tools/test.py -J --mode=release child-process
```

Si vous voulez vérifier les autres options, veuillez vous référer à l'aide en utilisant l'option `--help`:

```text
$ python tools/test.py --help
```

Vous pouvez généralement exécuter des tests directement avec le noeud :

```text
$ ./node ./test/parallel/test-stream2-transform.js
```

N'oubliez pas de recompiler avec `make -j4` entre les exécutions de test si vous changez de code dans les répertoires `lib` ou `src`.

Les tests tentent de détecter le support d'IPv6 et d'exclure les tests IPv6 si nécessaire. Si votre interface principale a des adresses IPv6, alors votre interface de bouclage doit aussi avoir '::1' activé. Pour certaines installations par défaut sur Ubuntu qui ne semble pas être le cas. Pour activer '::1' sur l'interface de bouclage sur Ubuntu:

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

Vous pouvez utiliser [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) pour exécuter/déboguer des tests, si vos configurations IDE sont présentes.

#### Couverture en cours

Il est bon de s'assurer que tout code que vous ajoutez ou modifiez est couvert par des tests. Vous pouvez le faire en exécutant la suite de tests avec l'activation de la couverture :

```console
$ ./configure --coverage
$ faire la couverture
```

Un rapport de couverture détaillé sera écrit à `coverage/index.html` pour la couverture JavaScript et à `coverage/cxxcoverage.html` pour la couverture C++.

Si vous voulez seulement exécuter les tests JavaScript, vous n'avez pas besoin d'exécuter la première commande (`./configure --coverage`). Exécutez `make coverage-run-js`, pour exécuter des tests JavaScript indépendamment de la suite de test C++ :

```text
$ rendre coverage-run-js
```

Si vous mettez à jour les tests et que vous voulez collecter la couverture pour un seul fichier de test (par exemple `test/parallel/test-stream2-transform.js` ) :

```text
$ make coverage-clean
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/parallel/test-stream2-transform.js
$ make coverage-report-js
```

Vous pouvez collecter une couverture pour toute la suite de tests pour un sous-système donné en fournissant le nom d'un sous-système :

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

Cela va faire tourner un serveur de fichiers statique et fournir une URL à l'endroit où vous pouvez parcourir la documentation localement.

Si vous êtes à l'aise de consulter la documentation en utilisant le programme que votre système d'exploitation a associé au navigateur Web par défaut, exécutez ce qui suit.

```bash
faire du docopen
```

Ceci ouvrira une URL de fichier vers une version d'une page de tous les documents HTML navigables à l'aide du navigateur par défaut.

Pour tester si Node.js a été construit correctement :

```bash
./node -e "console.log('Bonjour de Node.js ' + process.version)"
```

#### Construire une version de débogage

Si vous rencontrez un problème où les informations fournies par la trace de la pile JS ne suffisent pas, ou si vous soupçonnez que l'erreur se produit en dehors de la machine virtuelle JS, vous pouvez essayer de construire un binaire de débogage activé :

```console
$ ./configure --debug
$ make -j4
```

`faire` avec `. configure --debug` génère deux binaires, la version régulière dans `out/Release/node` et un binaire de débogage dans `out/Debug/node`, seule la version release est réellement installée lorsque vous exécutez `make install`.

Pour utiliser la version de débogage avec toutes les dépendances normales écraser la version de version dans le répertoire d'installation:

``` console
$ make install PREFIX=/opt/node-debug/
$ cp -a -f out/Debug/node /opt/node-debug/node
```

Lors de l'utilisation du binaire de débogage, les dumps de noyaux seront générés en cas de plantage. Ces noyaux sont utiles pour le débogage lorsqu'ils sont fournis avec le binaire de débogage original correspondant et les informations du système.

La lecture du dump core nécessite `gdb` construit sur la même plate-forme que celle sur laquelle le dump core a été capturé (i.e. 64 bits `gdb` pour `node` construit sur un système 64 bits Linux `gdb` pour `noeud` construit sur Linux) sinon vous obtiendrez des erreurs comme `au format exécutable : format de fichier non reconnu`.

Exemple de génération d'une trace à partir de la décharge du noyau:

``` console
$ gdb /opt/node-debug/node core.node.8.1535359906
$ backtrace
```

#### Construire une construction ASAN

[ASAN](https://github.com/google/sanitizers) peut aider à détecter divers bogues liés à la mémoire. Les versions ASAN ne sont actuellement prises en charge que sur linux. Si vous voulez le vérifier sous Windows ou macOS ou si vous voulez une chaîne de compilation cohérente sous Linux, vous pouvez essayer [Docker](https://www.docker.com/products/docker-desktop) (en utilisant une image comme `gengjiawen/node-build:2020-02-14`).

Le `--debug` n'est pas nécessaire et ralentira la compilation et les tests, mais il peut afficher la trace de pile si ASAN heurte un problème.

``` console
$ ./configure --debug --enable-asan && make -j4
$ rendre le test seulement
```

#### Accélérer les reconstructions fréquentes lors du développement

Si vous prévoyez de reconstruire fréquemment Node.js, surtout si vous utilisez plusieurs branches, l'installation de `ccache` peut aider à réduire considérablement le temps de construction. Configurer avec :
```console
$ sudo apt install ccache # pour Debian/Ubuntu, inclus dans la plupart des distributions Linux
$ ccache -o cache_dir=<tmp_dir>
$ ccache -o max_size=5. G
$ export CC="ccache gcc" # ajoutez à votre . rofile
$ export CXX="ccache g++" # ajouter à votre .profile
```
Cela permettra des reconstructions quasi instantanées même lors du changement de branches.

Lors de la modification de la couche JS dans `lib`, il est possible de la charger externalement sans modifier l'exécutable :
```console
$ ./configure --node-builtin-modules-path $(pwd)
```
Le binaire résultant n'inclura aucun fichier JavaScript et tentera de les charger depuis le répertoire spécifié. Le débogueur JS de Visual Studio Code prend en charge cette configuration depuis la version de Novembre 2020 et permet de régler les points d'arrêt.

#### Dépannage des versions Unix et macOS

Les builds de contes peuvent parfois entraîner des erreurs de `fichier non trouvé` lors de la construction. Ceci et d'autres problèmes peuvent être résolus avec `make distclean`. La recette `distclean` supprime agressivement la construction d'artefacts. Vous devrez reconstruire (`make -j4`). Puisque tous les artefacts de construction ont été supprimés, cette reconstruction peut prendre beaucoup plus de temps que les versions précédentes. De plus, `distclean` supprime le fichier qui stocke les résultats de `./configure`. Si vous avez couru `. configure` avec des options non par défaut (telles que `--debug`), vous devrez l'exécuter à nouveau avant d'appeler `make -j4`.

### Fenêtres

#### Pré-requis

##### Option 1 : installation manuelle

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* La charge de travail "Desktop development with C++" de [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) ou la charge de travail "C++ tools" de la [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), avec les composants optionnels par défaut
* Outils Unix de base requis pour certains tests, [Git pour Windows](https://git-scm.com/download/win) inclut Git Bash et des outils qui peuvent être inclus dans le `PATH global`.
* L' [Assembleur NetWide](https://www.nasm.us/), pour les modules d'assemblage OpenSSL. Si non installé dans l'emplacement par défaut, il doit être ajouté manuellement à `PATH`. Une version avec l'option `openssl-no-asm` n'a pas besoin de cela, pas plus qu'une version ciblant la version ARM64 Windows.

Exigences optionnelles pour construire le paquet d'installation MSI :

* [WiX Toolset v3.11](https://wixtoolset.org/releases/) et [Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* Le [WiX Toolset v3.14](https://wixtoolset.org/releases/) si vous construisez pour Windows 10 sur ARM (ARM64)

Exigences optionnelles pour la compilation pour Windows 10 sur ARM (ARM64):

* Visual Studio 15.9.0 ou plus récent
* Composants optionnels pour Visual Studio
  * Compilateurs et bibliothèques Visual C++ pour ARM64
  * ATL C++ visuel pour ARM64
* Windows 10 SDK 10.0.17763.0 ou plus récent

##### Option 2 : Installation automatique avec Boxstarter

Un script [Boxstarter](https://boxstarter.org/) peut être utilisé pour une configuration facile des systèmes Windows avec toutes les conditions requises pour le développement de Node.js. Ce script installera les paquets [Chocolatey](https://chocolatey.org/) suivants :

* [Git pour Windows](https://chocolatey.org/packages/git) avec les outils `git` et Unix ajoutés au PATH ``
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) avec [Visual C++ charge de travail](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [Assembleur NetWide](https://chocolatey.org/packages/nasm)

Pour installer les conditions préalables de Node.js en utilisant [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), ouvrez <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> avec le navigateur Internet Explorer ou Edge sur la machine cible.

Vous pouvez également utiliser PowerShell. Exécutez ces commandes depuis un terminal PowerShell élevé :

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex (New-Object System.Net.WebClient).DownloadString('https://boxstarter.org/bootstrapper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

L'installation entière à l'aide de Boxstarter prendra environ 10 Go d'espace disque.

#### Construire Node.js

Si le chemin d'accès à votre répertoire de compilation contient un espace ou un caractère non ASCII, la compilation échouera probablement.

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

Android n'est pas une plate-forme prise en charge. Les correctifs pour améliorer la version d'Android sont les bienvenus. Il n'y a pas de test sur Android dans l'environnement actuel d'intégration continue. La participation de personnes dévouées et déterminées à améliorer la construction d'Android, les tests et le soutien est encouragé.

Assurez-vous d'avoir téléchargé et extrait [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) avant dans un dossier. Puis exécutez :

```console
$ ./android-configure /chemin/vers/votre/android-ndk
$ faire
```

## `Intl` (ECMA-402) support

Le support [Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) est activé par défaut.

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

 Dans cette configuration, seules les données en anglais sont incluses, mais toutes les API `Intl` (ECMA-402).  Il n'a pas besoin de télécharger des dépendances pour fonctionner. Vous pouvez ajouter des données complètes à l'exécution.

#### Unix/macOS

```console
$ ./configure --with-intl=small-icu
```

#### Fenêtres

```console
> .\vcbuild small-icu
```

### Construction sans support Intl

L'objet `Intl` ne sera pas disponible, ni aucune autre API comme `String.normalize`.

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

Si vous compilez croix, votre `pkg-config` doit être en mesure de fournir un chemin qui fonctionne à la fois pour votre hôte et pour vos environnements cibles.

### Construire avec une ICU spécifique

Vous pouvez trouver d'autres versions de la ICU sur [la page d'accueil ICU](http://site.icu-project.org/download). Téléchargez le fichier nommé quelque chose comme `icu4c-**##.#**-src.tgz` (ou `.zip`).

Pour vérifier la ICU minimale recommandée, exécutez `./configure --help` et consultez l'aide pour l'option `--with-icu-source`. Un avertissement sera affiché lors de la configuration si la version ICU est trop ancienne.

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

Premier dépack la dernière ICU vers `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (ou `. ip`) comme `deps/icu` (Vous aurez : `deps/icu/source/...`)

```console
> .\vcbuild full-icu
```

## Construire Node.js avec OpenSSL conforme au FIPS

La version actuelle de Node.js ne prend pas en charge FIPS en liaison statique (par défaut) avec OpenSSL 1.1. mais pour un lien dynamique, il est possible d'activer FIPS en utilisant le drapeau de configuration `--openssl-is-fips`.

### Configuration et construction de quictls/openssl pour FIPS

Pour quictls/openssl 3.0, il est possible d'activer FIPS lors d'un lien dynamique. Node.js utilise actuellement openssl-3.0.0+quic qui peut être configuré comme suit:
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

Une fois que le module FIPS et le fichier de configuration ont été installés par les instructions ci-dessus, nous devons également mettre à jour `/path/to/install/dir/ssl/openssl. nf` pour utiliser le fichier de configuration FIPS généré (`fipsmodule.cnf` ) :
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

Dans le cas ci-dessus OpenSSL n'est pas installé dans l'emplacement par défaut, donc deux variables d'environnement doivent être définies, `OPENSSL_CONF`, et `OPENSSL_MODULES` qui doivent pointer vers le fichier de configuration OpenSSL et le répertoire où se trouvent les modules OpenSSL :
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
Si la commande `ldd` dit que `libcrypto` ne peut pas être trouvée on a besoin de définir `LD_LIBRARY_PATH` pour pointer vers le répertoire utilisé ci-dessus pour `--shared-openssl-libpath` (voir l'étape précédente).

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

Le support FIPS peut alors être activé via le fichier de configuration OpenSSL ou en utilisant `--enable-fips` ou `--force-fips` options de ligne de commande au noeud. s exécutable. Voir les sections [Activer FIPS en utilisant les options Node.js](#enabling-fips-using-node.js-options) et [activer FIPS en utilisant la configuration OpenSSL](#enabling-fips-using-openssl-config) ci-dessous.

### Activation des FIPS en utilisant les options Node.js
Ceci est fait en utilisant l'une des options de Node.js `--enable-fips` ou `--force-fips`, par exemple :
```console
$ node --enable-fips -p 'crypto.getFips()'
```

### Activer FIPS en utilisant la configuration OpenSSL
Cet exemple montre que l'utilisation du fichier de configuration d'OpenSSL, FIPS peut être activé sans spécifier les options `--enable-fips` ou `--force-fips` en définissant `default_properties = fips=yes` dans le fichier de configuration FIPS. Voir le lien [](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) pour plus de détails.

Pour que cela fonctionne, le fichier de configuration OpenSSL (par défaut openssl.cnf) doit être mis à jour. Ce qui suit montre un exemple :
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
Après cette modification, Node.js peut être exécuté sans les options `--enable-fips` ou `--force-fips`.

## Construire Node.js avec des modules core externes

Il est possible de spécifier un ou plusieurs fichiers texte JavaScript à inclure dans le binaire en tant que modules intégrés lors de la construction de Node.js.

### Unix/macOS

Cette commande rendra `/root/myModule.js` disponible via `require('/root/myModule')` et `./myModule2.js` disponibles via `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### Fenêtres

Pour rendre `./myModule.js` disponible via `require('myModule')` et `./myModule2.js` disponibles via `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Note pour les distributeurs en aval de Node.js

L'écosystème Node.js dépend de la compatibilité ABI dans une version majeure. Pour maintenir la compatibilité ABI, il est nécessaire que les versions distribuées de Node. sont construits avec la même version des dépendances, ou des versions similaires qui ne rompent pas leur compatibilité ABI, comme celles publiées par Node. s pour toute donnée `NODE_MODULE_VERSION` (située dans `src/node_version.h`).

Quand Node.js est construit (avec l'intention de distribuer) avec un ABI incompatible avec les versions officielles de Node.js (par ex. en utilisant une version de dépendance incompatible avec ABI), veuillez réserver et utiliser un `NODE_MODULE_VERSION personnalisé` en ouvrant une demande d'ajout sur le registre disponible sur [https://github. om/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
