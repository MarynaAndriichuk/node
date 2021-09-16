# Building Node.js

根据您需要什么平台或特征，构建过程可能不同。 在你构建了一个二进制文件后，运行测试套件以确认二进制文件是一个良好的下一步。

如果您可以复制测试失败，请在 [Node.js issue Tracker](https://github.com/nodejs/node/issues) 中搜索或提交一个新问题。

## 目录

* [支持的平台](#supported-platforms)
  * [Input](#input)
  * [战略](#strategy)
  * [平台列表](#platform-list)
  * [支持的刀具](#supported-toolchains)
  * [官方二进制平台和工具链：](#official-binary-platforms-and-toolchains)
    * [OpenSSL 支持](#openssl-asm-support)
  * [此文档的先前版本](#previous-versions-of-this-document)
* [建立支持的平台 Node.js](#building-nodejs-on-supported-platforms)
  * [关于 Python 的注释](#note-about-python)
  * [Unix 和 macOS](#unix-and-macos)
    * [唯一的前提条件](#unix-prerequisites)
    * [macOS prerequisites](#macos-prerequisites)
    * [Building Node.js](#building-nodejs-1)
    * [安装 Node.js](#installing-nodejs)
    * [正在运行测试](#running-tests)
    * [正在运行封面](#running-coverage)
    * [构建文档](#building-the-documentation)
    * [构建调试版本](#building-a-debug-build)
    * [构建一个ASAN建筑](#building-an-asan-build)
    * [开发时加速频繁的重建](#speeding-up-frequent-rebuilds-when-developing)
    * [疑难解答Unix 和 macOS 版本](#troubleshooting-unix-and-macos-builds)
  * [窗口](#windows)
    * [必备条件](#prerequisites)
      * [选项1：手动安装](#option-1-manual-install)
      * [备选办法2：自动使用 Boxstarter 安装](#option-2-automated-install-with-boxstarter)
    * [Building Node.js](#building-nodejs-2)
  * [Android/Android设备(例如，Firefox OS)](#androidandroid-based-devices-eg-firefox-os)
* [`Intl` (ECMA-402) 支持](#intl-ecma-402-support)
  * [使用 ICU 完全支持 (所有支持 ICU 的本地化)](#build-with-full-icu-support-all-locales-supported-by-icu)
    * [Unix/macOS](#unixmacos)
    * [窗口](#windows-1)
  * [Trimed: `small-icu` (只有英文版)](#trimmed-small-icu-english-only-support)
    * [Unix/macOS](#unixmacos-1)
    * [窗口](#windows-2)
  * [构建时不支持 Intl](#building-without-intl-support)
    * [Unix/macOS](#unixmacos-2)
    * [窗口](#windows-3)
  * [使用已安装的 ICU (仅限Unix/macOS )](#use-existing-installed-icu-unixmacos-only)
  * [使用 ICU 构建特定的](#build-with-a-specific-icu)
    * [Unix/macOS](#unixmacos-3)
    * [窗口](#windows-4)
* [使用 FIPS 兼容的 OpenSSL 构建Node.js](#building-nodejs-with-fips-compliant-openssl)
* [使用外部核心模块构建Node.js](#building-nodejs-with-external-core-modules)
  * [Unix/macOS](#unixmacos-4)
  * [窗口](#windows-5)
* [Node.js下游发行商的说明](#note-for-downstream-distributors-of-nodejs)

## 支持的平台

这个支持的平台列表是它所属的分支/版本的当前列表。

### Input

Node.js依赖于V8和libuv。 我们采纳了他们支持的平台的子集。

### 战略

有三个支持级别：

* **一级**: 这些平台代表了Node.js用户的大多数。 Node.js 建筑工作组维持全面测试覆盖的基础设施。 第1级平台测试失败将阻止发布。
* **级别2**: 这些平台代表了Node.js用户基础中的较小的部分。 Node.js 建筑工作组维持全面测试覆盖的基础设施。 第二级平台上的测试失败将阻止发布。 基础设施问题可能会推迟为这些平台释放二维码。
* **实验**: 可能不编译或测试套件可能无法通过。 核心小组没有为这些平台创建释放。 实验平台上的测试失败不会阻止释放。 欢迎为改善对这些平台的支持作出贡献。

平台可能会在主要发布线之间的层级间移动。 下表将反映这些变化。

### 平台列表

Node.js 编译/执行支持取决于操作系统、架构和 libc 版本。 下表列出每一种支持组合的支持级别。 还为第1级平台提供了一个 [支持的编译工具链](#supported-toolchains) 列表。

**仅在支持的平台上运行Node.js生产应用程序。**

Node.js不支持平台版本，如果供应商已过期支持的话。 换言之，Node.js不支持在生命终点平台上运行。 无论下表中的条目如何，情况都是如此。

| 操作系统      | 结构               | 版本                              | 支持类型                                   | 注                                                                           |
| --------- | ---------------- | ------------------------------- | -------------------------------------- | --------------------------------------------------------------------------- |
| GNU/Linux | x64              | 内核 >= 310, glibc >= 2.17        | 第1级                                    | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, Debian 9, EL 7 <sup>[2](#fn2)</sup> |
| GNU/Linux | x64              | 内核 >= 310，必须 >= 1.1.19          | 实验性                                    | e.g. Alpine 3.8                                                             |
| GNU/Linux | x86              | 内核 >= 310, glibc >= 2.17        | 实验性                                    | 降级为 Node.js 10                                                              |
| GNU/Linux | arm64            | 内核 >= 4.5, glibc >= 2.17        | 第1级                                    | e.g. Ubuntu 16.04, Debian 9, EL 7 <sup>[3](#fn3)</sup>                      |
| GNU/Linux | 护甲7              | 内核 >= 4.14, glibc >= 2.24       | 第1级                                    | e.g. Ubuntu 18.04, Debian 9                                                 |
| GNU/Linux | 护甲6              | 内核 >= 4.14, glibc >= 2.24       | 实验性                                    | 降级至 Node.js 12                                                              |
| GNU/Linux | ppc64le >=power8 | kernel >= 3.10.0, glibc >= 2.17 | 第 2 级                                  | e.g. Ubuntu 16.04 <sup>[1](#fn1)</sup>, EL 7  <sup>[2](#fn2)</sup>          |
| GNU/Linux | s390x            | kernel >= 3.10.0, glibc >= 2.17 | 第 2 级                                  | e.g. EL 7 <sup>[2](#fn2)</sup>                                              |
| 窗口        | x64, x86 (WoW64) | >= Windows 8.1/2012 R2          | 第1级                                    | <sup>[4](#fn4),[5](#fn5)</sup>                                              |
| 窗口        | x86 (原始)         | >= Windows 8.1/2012 R2          | 第1级(运行) / 实验性(编译) <sup>[6](#fn6)</sup> |                                                                             |
| 窗口        | x64, x86         | Windows Server 2012 (不是 R2)     | 实验性                                    |                                                                             |
| 窗口        | arm64            | >= Windows 10                   | 第2层 (编译) / 实验性(运行)                     |                                                                             |
| macOS     | x64              | >= 10.13                        | 第1级                                    |                                                                             |
| macOS     | arm64            | >= 11                           | 实验性                                    |                                                                             |
| SmartOS   | x64              | >= 18                           | 第 2 级                                  |                                                                             |
| AIX       | ppc64be >=power7 | >= 7.2 TL04                     | 第 2 级                                  |                                                                             |
| FreeBSD   | x64              | >= 11                           | 实验性                                    | 降级为 Node.js 12  <sup>[7](#fn7)</sup>                                        |

<em id="fn1">1</em>: 海合会8 未在基础平台上提供。 用户将需要 [工具链测试版本 PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) 或类似于源代码更新的编译器。

<em id="fn2">2</em>: 海合会8 未在基础平台上提供。 用户将需要 [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) 或稍后才能提供一个更新的编译器。

<em id="fn3">3</em>: 更早的内核版本可能适用于 ARM64 。 然而，Node.js只测试基础结构测试 >= 4.5。

<em id="fn4">4</em>: 在 Windows 上，运行节点。 s 在 Windows 终端模拟器中，例如 `迷你` 需要使用 [winpty](https://github.com/rprichard/winpty) 才能正常工作 (e). 。 `winpty node.exe script.js`)。 在“Git bash”中，如果您调用节点外壳别名(`节点` 没有 `xe` 扩展), `winpty` 被自动使用

<em id="fn5">5</em>: 不支持用于 Linux 的 Windows 子系统, 但GNU/Linux 构建进程和二进制程序应该正常工作。 社区只能解决在本机GNU/Linux系统上复制的问题。 只能在WSL上复制的问题应该在 [WSL Issue Tracker](https://github.com/Microsoft/WSL/issues) 中报告。 不建议在 WSL 中运行 Windows 二进制(`node.exe`)。 如果没有工作条件，例如立刻重定向，它就无法发挥作用。

<em id="fn6">6</em>: 在 x86 Windows 上运行Node.js 应该能够工作，并提供二进制文件。 然而，我们的基础设施试验只在WoW64上进行。 此外，在 x86 Windows 上编译是实验性的，可能是不可能的。

<em id="fn7">7</em>: 默认 FreeBSD 12.0 编译器是 Clang 6.0.1, 但FreeBSD 12.1 升级到 8.0.1。 其他Clang/LLVM版本可通过系统包管理器获取，包括Clang 9.0。

### 支持的刀具

根据主机平台，工具链的选择可能各不相同。

| 操作系统  | 编译版本                                             |
| ----- | ------------------------------------------------ |
| Linux | 海合会 >= 8.3                                       |
| 窗口    | Visual Studio >= 2019 与 Windows 10 SDK 在一个64位主机上 |
| macOS | Xcode >= 11 (Apple LLLVM >= 11)                  |

### 官方二进制平台和工具链：

在 <https://nodejs.org/download/release/> 上生成双脚：

| 二进制包                  | 平台和工具链接                                                                                |
| --------------------- | -------------------------------------------------------------------------------------- |
| aix-ppc64             | AIX 7.2 TL04 on PPC64BE with CCC 8                                                     |
| 暗-x64                 | macOS 10.15, Xcode Command Line Tools 11 with -mmacosx-version-min=10.13               |
| darwin-arm64 (和 .pkg) | macOS 11 (arm64), Xcode Command Line Tools 12 with -mmacosx-version-min=10.13          |
| linux-arm64           | 中心OS 7 与 devtoolset-8 / GC 8 <sup>[8](#fn8)</sup>                                      |
| linux-armv7l          | 在 Ubuntu 18.04 x64 上使用 [个自定义海湾合作委员会工具链](https://github.com/rvagg/rpi-newer-crosstools) |
| linux-ppc64le         | 中心OS 7 与 devtoolset-8 / GC 8 <sup>[8](#fn8)</sup>                                      |
| linux-s390x           | 带有devtoolset-8 / GC 8 <sup>[8](#fn8)</sup>                                             |
| linux-x64             | 中心OS 7 与 devtoolset-8 / GC 8 <sup>[8](#fn8)</sup>                                      |
| 双英-x64 和 win-x86      | Windows 2012 R2 (x64) 与 Visual Studio 2019                                             |

<em id="fn8">8</em>: Enterprise Linux devtoolset-8 允许我们编译海合会8但链接到主机平台的 glibc 和 libstdc++ 版本(CentOS 7 / RHEL 7)。 因此，在这些系统上生成的二进制文件与glibc >= 2.17 和 libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20` ) 兼容。 如Ubuntu 14.04和Debian 8等本质上支持海湾合作委员会4.9份的分发文件。

#### OpenSSL 支持

OpenSSL-1.1.1 需要以下集合版本才能在 x86_64 和 ia32 上使用 asm 支持。

a. 使用AVX-512；

* 气体(GNU 装配器) 版本 2.26 或以上
* Windows 中的nasm 版本 2.1.8或更高版本

OpenSSL-1.1.1在 Skylake-X 禁用AVX-512

对于AVX2的使用

* 气体(GNU 装配器) 版本 2.23 或以上
* Xcode 5.0 或更高版本
* llvm 版本 3.3 或更高版本
* Windows 中的nasm 版本 2.10 或更高版本

Please refer to <https://www.openssl.org/docs/man1.1.1/man3/OPENSSL_ia32cap.html> for details.

 如果编译时没有上述任何一个，请使用 `配置` 与 `--openssl-no-asm` 标记。 否则， `配置` 将失败。

### 此文档的先前版本

支持的平台和工具链随着每个主要版本Node.js而变化。 此文档仅适用于当前主要版本的 Node.js。 查阅旧版本Node.js的此文档：

* [Node.js 14](https://github.com/nodejs/node/blob/v14.x/BUILDING.md)
* [Node.js 12](https://github.com/nodejs/node/blob/v12.x/BUILDING.md)
* [Node.js 10](https://github.com/nodejs/node/blob/v10.x/BUILDING.md)

## 建立支持的平台 Node.js

### 关于 Python 的注释

Node.js项目支持 Python >= 3 建造和测试。
### Unix 和 macOS

#### 唯一的前提条件

* `gcc` and `g++` >= 8.3 或更高版本，或
* GNU Make 3.81 或更新
* Python 3.6、3.7、3.8和3.9（见上文注）

通过 Linux 软件包管理器安装可以实现：

* Ubuntu, Debian: `sudo apt-get install python3 g++ make`
* Fedora: `sudo dnf install python3 gcc-c++ make`
* CentOS 和 RHEL: `sudo yum install python3 gcc-c++ make`
* OpenSUSE: `sudo zypper install python3 gcc-c++ make`
* Arch Linux, Manjaro: `sudo pacman -S python gcc make`

FreeBSD 和 OpenBSD 用户可能也需要安装 `libexecinfo`。

#### macOS prerequisites

* Xcode 命令行工具 >= 11 for macOS
* Python 3.6、3.7、3.8和3.9（见上文注）

macOS 用户可以通过运行 `xcode-select --install` 来安装 `Xcode 命令行工具`。 或者，如果您已经安装了完整的 Xcode 你可以在菜单 `Xcode -> 打开开发者工具 ->
更多开发者工具 。`. 此步骤将安装 `clang`, `clang++`, 并 `make`。

#### Building Node.js

如果您的构建目录的路径包含一个空格，构建可能会失败。

要生成Node.js：

```console
$ ./configure
make -j4
```

`-j4` 选项将导致 `让` 同时运行 4 个编译任务，这可能会缩短构建时间。 欲了解更多信息，请参阅 [GNU Make 文档](https://www.gnu.org/software/make/manual/html_node/Parallel.html)。

以上要求 `python` 解决到 Python 支持的版本。 查看 [前提条件](#prerequisites)。

在构建后，设置 [防火墙规则](tools/macos-firewall.sh) 可以避免在运行测试时请求接受传入网络的连接。

在 macOS 上运行下面的脚本将在 `外围中为可执行的 <code>节点` 添加防火墙规则。</code> 目录和符号 `节点` 链接在项目的根目录中。

```console
$ sudo ./tools/macos-firewall.sh
```

#### 安装 Node.js

要将此版本的 Node.js 安装到系统目录：

```bash
[sudo] 进行安装
```

#### 运行测试

要验证构建：

```console
$只进行测试
```

此刻，您准备修改代码并重新运行测试。

如果您在提交Pull Request之前正在运行测试，推荐命令是：

```console
$ make -j4 测试
```

`让-j4测试` 对代码片段进行全面检查，包括运行linters和文档测试。

请确保班轮没有报告任何问题，并确保所有测试通过。 请不要提交检查失败的补丁。

如果你想要运行直线器而不运行测试，请使用 `制作直线`/`vcbuild直线`。 它会lint JavaScript, C++, and Markdown文件。

如果您正在更新测试并想要在单个测试文件中运行测试(例如， `test/paradel/test-stream2-transform.js`):

```text
$ python tools/test.py test/paradel/test-stream2-transform.js
```

您可以通过提供子系统的名称来执行给定子系统的整套测试：

```text
$ python tools/test.py -J --mode=release child-process
```

如果您想要检查其他选项，请通过使用 `--help` 选项查看帮助：

```text
$ python tools/test.py --help
```

您通常可以使用节点直接运行测试：

```text
$ .节点./test/paradel/test-stream2-transform.js
```

如果您在 `lib` 或 `src` 目录中更改代码，请记住用 `在测试运行之间重新编译-j4`。

测试试图检测IPv6支持，并酌情排除IPv6测试。 如果您的主接口有IPv6地址，那么您的循环接口也必须启用 ':1' 。 对于Ubuntu上似乎没有的一些默认安装。 要启用 '::1' 在 Ubuntu 上的循环接口：

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

如果您的 IDE 配置存在，您可以使用 [节点代码-IDe-configs](https://github.com/nodejs/node-code-ide-configs) 来运行/调试测试。

#### 正在运行的范围

确保您添加或更改的任何代码都包含在测试范围内是好的做法。 您可以通过运行带有覆盖面的测试套件来这样做：

```console
$ ./configure --coverage
$ make coverage
```

详细的覆盖率报告将被写入JavaScript覆盖率为 `coverage/index.html` 和 `cxxcoverage.html` C++ 覆盖率。

如果你只想运行JavaScript测试，那么你不需要运行第一个命令(`./configure --covery`)。 运行 `make coverage-run-js`, 独立于 C++ 测试套件执行JavaScript 测试：

```text
美元制作封面运行js
```

如果您正在更新测试并想要收集一个测试文件的覆盖面(例如 `test/paradel/test-stream2-transform.js`)：

```text
$做覆盖清洁
$NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/paradel/test-stream2-transform.js
$做覆盖报告-js
```

您可以通过提供子系统的名称来收集给定子系统的整个测试套件的覆盖范围：

```text
$ coverage-clearing
$ NODE_V8_COVERAGE=coverage/tmp python tools/test.py -J --mode=release child-process
$ make coverage-report-js
```

`覆盖` 命令下载一些工具到项目根目录。 在生成覆盖报告后进行清理：

```console
美元进行覆盖清理
```

#### 构建文档

编写文件：

这将首先构建Node.js(如果有必要)，然后使用它构建文档：

```bash
制作doc
```

如果你有一个现有的 Node.js 构建，你可以只构建文档：

```bash
NODE=/path/to/节点只制作文档
```

阅读这个人页面：

```bash
man doc/node.1
```

如果您希望在浏览器中阅读完整文档，请执行以下操作。

```bash
制作docservice
```

这将会旋转一个静态文件服务器，并提供一个 URL 到您可以在本地浏览文档。

如果您很舒服地使用程序查看文档，您的操作系统与默认的 web 浏览器相关联，请执行以下操作。

```bash
打开文档
```

这将使用默认浏览器打开一个文件URL到所有可浏览的 HTML 文档的一页版本。

测试Node.js是否正确构建：

```bash
./node -e "console.log('Hello from Node.js ' + process.version)"
```

#### 构建调试版本

如果你遇到了JS 堆栈跟踪提供的信息不够的问题。 或者如果您怀疑在JS VM之外发生了错误，您可以尝试构建一个启用调试的二进制：

```console
$ ./configure --debug
$make -j4
```

`用 <code>制作` 配置 --debug</code> 生成两个二进制文件 常规发布一次在 `场外/发布/节点` 和 调试二进制的 `场外/调试/节点`, 当您运行 `进行安装` 时，仅安装版本才真正安装。

要使用所有正常依赖关系的调试构建，请覆盖安装目录中的发行版本：

``` console
$ make installation PREFIX=/opt/node-debug/
$ cp -f out/debug/节点 /opt/node-debug/节点
```

当使用调试二进制时，在发生崩溃时将生成核心转储。 当提供相应的原始调试二进制和系统信息时，这些核心转储对调试非常有用。

读取核心转储需要 `gdb` 建立在抓取核心转储的同一个平台上(即) 64 位 `gdb` 用于 `节点` 建立在一个64 位系统上 Linux `gdb` 用于 `节点` 建立在 Linux上的节点，否则您将会遇到类似于 `无法执行格式的错误：文件格式无法识别`。

从核心倾销生成回溯跟踪的示例：

``` console
$ gdb /opt/node-debug/节点core.node.8.153559906
$ backtrack
```

#### 构建一个ASAN建筑

[ASAN](https://github.com/google/sanitizers) 可以帮助检测到各种与内存相关的错误。 ASAN构建当前仅在线上支持。 如果您想要在 Windows 或 macOS 上检查，或者您想在 Linux 上找到一个一致的工具链， 您可以尝试 [Docker](https://www.docker.com/products/docker-desktop) (使用类似于 `gengjiawen/node-build:2020-02-14` 的图像)。

`--debug` 不是必要的，将会减慢构建和测试，但如果ASAN遇到问题，它可以显示清晰的堆栈跟踪。

``` console
$ ./configuring --enable-asan && make -j4
$ make test-only
```

#### 开发时加速频繁的重建

如果您打算经常重建 Node.js，特别是如果使用几个分支，安装 `ccache` 可以帮助大大缩短构建时间。 设置于：
```console
$ sudo apt install ccache # for Debian/Ubuntu, 包含在大部分Linux distros
$ccache -o cache_dir=<tmp_dir>
ccache -o max_size=5。 G
$ 导出 CC="ccache gcc" # 添加到您的. rofile
$ 导出 CXX="ccache g++" # 添加到您的 .profile
```
这将允许在切换分支时进行近瞬间重建。

当只修改 `lib`中的 JS 层时，可以在外部加载它而不修改可执行文件：
```console
$ ./configure --node-build-modules-path $(pwd)
```
生成的二进制文件不会包含任何JS文件，并将尝试从指定的目录加载。 Visual Studio 代码的 JS 调试器支持自2020年11月版本以来的配置，并允许设置断点。

#### 疑难解答Unix 和 macOS 版本

旧版本的构建有时会导致 `文件在构建时找不到` 个错误。 这个问题和其他一些问题可以通过 `进行远程` 解决。 `远程` 配方主动移除构造工艺品。 您将需要重新构建(`make -j4`)。 由于所有建筑物已被拆除，这次重建可能需要比以前的建筑更多的时间。 此外， `远程` 移除储存 `结果的文件。/configure`。 如果您运行了 `。 使用非默认选项配置` (例如 `--debug`), 您需要重新运行它才能使用 `make -j4`。

### 窗口

#### 必备条件

##### 选项1：手动安装

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* 来自 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) 的“使用 C++” 的桌面开发”或来自 [构建工具](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019)的 “C++ 构建工具”的工作量， 默认可选组件
* 某些测试所需基本的 Unix 工具 [Windows Git](https://git-scm.com/download/win) 包括Git Bash 和可以包含在全局 `PATH` 的工具。
* [NetWassembler](https://www.nasm.us/), 用于 OpenSSL 集成模块。 如果未安装在默认位置，它需要手动添加到 `PATH`。 使用 `openssl-no-asm` 选项的构建不需要这样做，目标的 ARM64 Windows也不需要这么做。

构建MSI安装程序包的可选要求：

* [WiX 工具集 v3.11](https://wixtoolset.org/releases/) and [Wix 工具集 Visual Studio 2019 扩展](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* [WiX 工具集 v3.14](https://wixtoolset.org/releases/) 如果构建在 ARM 上 Windows 10 (ARM64)

在ARM上编译Windows 10的可选要求 (ARM64)：

* Visual Studio 15.9.0 或更新版本
* Visual Studio 可选组件
  * ARM64 的Visual C++ 编译器和库
  * ARM64 的Visual C++ ATL
* Windows 10 SDK 10.0.17763.0 或更新版本

##### 备选办法2：自动使用 Boxstarter 安装

[Boxstarter](https://boxstarter.org/) 脚本可以用于轻松安装Windows系统，并且为 Node.js 开发所需的所有先决条件。 此脚本将安装以下 [Chocolatey](https://chocolatey.org/) 软件包：

* [Git for Windows](https://chocolatey.org/packages/git) with `git` and Unix tools 添加到 `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Building Tools](https://chocolatey.org/packages/visualstudio2019buildtools) with [Visual C++ mandate](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [NetWide Assembler](https://chocolatey.org/packages/nasm)

要使用 [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher)安装Node.js 前提条件, 请打开 <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> 与Internet Explorer 或 Edge 浏览器在目标机器上.

或者，您可以使用 PowerShell。 从 PowerShell 高阶终端运行这些命令：

```powershell
设置执行政策不受限制 -Force
iex (新对象系统)。 Net.WebClient).DownloadString('https://boxstarter.org/bootstraper.ps1').
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter -DisableReboots
```

使用 Boxstarter 的整个安装将占用大约10GB 的磁盘空间。

#### Building Node.js

如果到您的构建目录的路径包含空格或非ASCII字符，构建可能会失败。

```console
> 。\vcbuild
```

要运行测试：

```console
> \vcbuild测试
```

测试Node.js是否正确构建：

```console
> 版本\node -e "console.log('Hello from Node.js', process.version)"
```

### Android/Android设备(例如，Firefox OS)

Android 不支持该平台。 改进安卓构建的补丁是受欢迎的。 在当前连续集成环境中没有测试安卓系统。 鼓励那些致力于和决心改进安卓建设、测试和支持的人参与。

请确保您在文件夹中下载并提取了 [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) 然后运行：

```console
$ ./android-configure /path/to/your/android-ndk
$make
```

## `Intl` (ECMA-402) 支持

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) 支持是默认启用的。

### 使用 ICU 完全支持 (所有支持 ICU 的本地化)

这是默认选项。

#### Unix/macOS

```console
$ ./configure --with-intl=fullicu
```

#### 窗口

```console
> \vcbuild完整图标
```

### Trimed: `small-icu` (只有英文版)

 在这个配置中，只包含英文数据，但是完整的 `Intl` (ECMA-402) API。  它不需要下载任何依赖才能运行。 您可以在运行时添加完整数据。

#### Unix/macOS

```console
$ ./configure --with-intl=smallicu
```

#### 窗口

```console
> \vcbuild小图标
```

### 构建时不支持 Intl

`Intl` 对象将不可用，或其他一些API，如 `String.normalize`。

#### Unix/macOS

```console
$ ./configure --without out-intl
```

#### 窗口

```console
> 。\vcbuild时不再提示
```

### 使用已安装的 ICU (仅限Unix/macOS )

```console
$ pkg-config --modversion icu-i18n && ./config--with-intl=system-icu
```

如果您正在交叉编译，您的 `pkg-config` 必须能够提供一个既适合您的主机又适合目标环境的路径。

### 使用 ICU 构建特定的

您可以在 [的 ICU 主页](http://site.icu-project.org/download) 找到其他的 ICU 版本。 下载命名的文件 `icu4c-**##。#**-src.tgz` (或 `.zip`)。

若要检查建议的最低数量的 ICU，运行 `./configure --help` 并查看 `--with-icu-source` 选项的帮助。 如果ICU 版本太旧，将在配置期间打印警告。

#### Unix/macOS

已经从一个已经解包的 ICU：

```console
$ ./configure --with-intl=[smallicu,fullicu] --with-icu-source=/path/to/icu
```

来自本地ICU tarball：

```console
$ ./configure --with-intl=[smallicu,fullicu] --with-icu-source=/path/to/icu.tgz
```

从 tarball URL：

```console
$ ./configure --with-intl=full icu --with-icu-source=http://url/to/icu.tgz
```

#### 窗口

首先解包最新的 ICU 到 `deps/icu` [icu4c-**###**-src.tgz](http://site.icu-project.org/download) (或 `. ip`as `deps/icu` (您将拥有： `deps/icu/source/...`)

```console
> \vcbuild完整图标
```

## 使用 FIPS 兼容的 OpenSSL 构建Node.js

当前版本的 Node.js 不支持 FIPS 时静态链接 (默认) 和 OpenSSL 1.1。 但对于动态链接，可以使用配置标志 `--openssl-is-fips` 启用 FIPS。

### 配置和构建FIPS的 quictls/openssl

对于quictls/openssl 3.0 ，动态链接时可以启用 FIPS。 Node.js 当前使用 openssl-3.0.0.0+quic 可以配置如下：
```console
$ git clone git@github.com:quictls/openssl.git
$ cd openssl
$ ./config --prefix=/path/to/install/dir/shared enable-fips linux-x86_64
```
这可以通过以下命令进行编译和安装：
```console
$make -j8
make install_ssldirs
$make install_fips
```

在上述说明安装了FIPS模块和配置文件后，我们也需要更新 `/path/to/install/dir/sl/openssl。 nf` 可使用生成的 FIPS 配置文件(`fipsomudule.cnf`):
```text
.include fipsmobule。 nf

# 要加载
[provider_sect]
默认 = 默认值
# fips 部分名称应该匹配在
# 中包含/path/to/install/dir/sl/fipsmobule。 页：1
fips = fips_sect

[default_sect]
激活 = 1
```

在上述情况下，OpenSSL未安装在默认位置，因此需要设置两个环境变量。 `OPENSSL_CONF`， 和 `OPENSSL_MODULES` 应该指向OpenSSL 配置文件和OpenSSL 模块所在的目录：
```console
$ 导出 OPENSSL_CONF=/path/to/install/dir/ssl/openssl.cnf
$ 导出 OPENSSL_MODULES=/path/to/install/dir/lib/ossl-modules
```

Node.js可以配置为启用 FIPS：
```console
$ ./configure --shared-openssl --shared-openssl-libath=/path/to/install/dir/lib --shared-openssl-includes=/path/to/install/dir/include --shared-openssl-libname=crypto,ssl --openssl-is-fips
$ export LD_LIBRARY_PATH=/path/to/install/dir/lib
$ make -j8
```

验证已生成的可执行文件：
```console
$ ld./节点
    linux-vdso.so.1 (0x00007ffd7917b000)
    libcrypto.so.81。 => /path/to/install/dir/lib/libcrypto.so.81.3 (0x00007fd911321000)
    libssl.so.81. => /path/to/install/dir/libs/libssl.so.81.3 (0x00007fd91125e000)
    libdl.so. => /usr/lib64/libdl.so.2 (0x00007fd911232000)
    libstdc++.so.6 => /usr/lib64/libstdc++.so. (0x00007fd911039000)
    libm.so.6 => /usr/lib64/libm.so.6 (0x00007fd910ef3000)
    libgcc_s. o.1 => /usr/lib64/libgcc_s.so.1 (0x00007fd910ed9000)
    libpthread o.0 => /usr/lib64/libpthread.so.0 (0x00007fd910eb500)
    libc.so.6 => /usr/lib64/libc.so.6 (0x007fd910cec000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fd9117f2000)
```
如果 `ld` 命令表示 `libcrypto` 无法找到一个需要设置 `LD_LIBRARY_PATH` 指向上面用于 `--shared-openssl-libpath` (见前一步)。

验证 OpenSSL 版本：
```console
$ ./节点 -p process.versions.openssl
3.0.0-alpha16+quic
```

验证 FIPS 可用：
```console
$ ./note -p 'process.config.variables.openssl_is_fips'
true
$ ./node --enable-fips -p 'crypto.getFips()'
1
```

然后可以通过 OpenSSL 配置文件启用FIPS 支持，或使用 `--enable-fips` 或 `--force-fips` 对节点的命令行选项。 s 可执行性。 查看 [节使用 Node.js 选项](#enabling-fips-using-node.js-options) 和 [使用 OpenSSL 配置启用 FIPS](#enabling-fips-using-openssl-config)

### 使用 Node.js 选项启用 FIPS
这是使用 Node.js 选项 `--enable-fips` or `--force-fips`等, 例如:
```console
$ 节点 --enable-fips -p 'crypto.getFips()'
```

### 使用 OpenSSL 配置启用 FIPS
此示例显示使用 OpenSSL 的配置文件， FIPS 可以在不指定 `--enable-fips` 或 `--force-fips` 选项通过设置 `default_properties = fips=yes` 在 FIPS 配置文件中。 详情请访问 [link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers)

要使它正常工作，OpenSSL 配置文件 (默认 openssl.cnf) 需要更新。 下面显示一个示例：
```console
openssl_conf = openssl_init

.include /path/to/install/dir/ssl/fipsmobule。 nf

[openssl_init]
providers = prov
alg_section = algorithm_sect

[prov]
fips = fips_sect
default = default_sect

[default_sect]
激活 = 1

[algorithm_sect]
default_properties = fips=yes
```
此更改后，Node.js可以在没有 `--enable-fips` 或 `--force-fips` 选项的情况下运行。

## 使用外部核心模块构建Node.js

可以在构建Node.js时指定一个或多个要捆绑在二进制文件中的JavaScript文本文件。

### Unix/macOS

此命令将通过 `/root/myModule.js` 可用到 `require('/root/myModule')` 和 `.myModule2.js` 可通过 `require('myModule2')` 获取。

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### 窗口

若要通过 `./myModule.js` 通过 `require('myModule')` 和 `./myModule2.js` 通过 `required ('myModule2')` 提供：

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Node.js下游发行商的说明

Node.js生态系统依赖于一个主要版本内的 ABI 兼容性。 要保持ABI兼容性，需要分发的节点构建。 s 可以根据相同版本的依赖或类似的版本进行构建，这些版本不会与Node发布的版本相抵触。 s 针对任一指定 `NODE_MODULE_VERSION` (位于 `src/node_version.h` 中)。

当Node.js是与官方版本Node.js不兼容的 ABI 构建时(例如，打算发行版) 使用 ABI 不兼容的依赖版本， 请保留并使用自定义 `NODE_MODULE_VERSION` 通过在 [https://github上打开注册表的拉取请求。 om/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
