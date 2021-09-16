# Building Node.js

取决于您需要什么平台或功能，构建过程可能 不同。 Depending on what platform or features you need, the build process may differ. After you've built a binary, running the test suite to confirm that the binary works as intended is a good next step.

If you can reproduce a test failure, search for it in the [Node.js issue tracker](https://github.com/nodejs/node/issues) or file a new issue.

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

This list of supported platforms is current as of the branch/release to which it belongs.

### Input

Node.js依赖于V8和libuv。 我们采纳了他们支持的平台的子集。

### 战略

有三个支持级别：

* **Tier 1**: These platforms represent the majority of Node.js users. The Node.js Build Working Group maintains infrastructure for full test coverage. Test failures on tier 1 platforms will block releases. Node.js 构建工作组维护全面测试覆盖的基础设施。 第1级平台测试失败将阻止发布。
* **Tier 2**: These platforms represent smaller segments of the Node.js user base. The Node.js Build Working Group maintains infrastructure for full test coverage. Test failures on tier 2 platforms will block releases. Infrastructure issues may delay the release of binaries for these platforms. Node.js 构建工作组维护完整测试 覆盖范围的基础设施。 第二级平台上的测试失败将阻止发布。 基础设施问题可能会推迟为这些平台释放二维码。
* **Experimental**: May not compile or test suite may not pass. The core team does not create releases for these platforms. Test failures on experimental platforms do not block releases. Contributions to improve support for these platforms are welcome. 核心团队 没有为这些平台创建发布。 实验性的 平台测试失败不会阻止释放。 欢迎为改善这些 平台的支持作出贡献。

平台可能会在主要发布线之间的层级间移动。 下面的表 将会反映这些变化。

### 平台列表

Node.js 编译/执行支持取决于操作系统，架构， 和 libc 版本。 下表列出每个支持 组合的支持级别。 Node.js compilation/execution support depends on operating system, architecture, and libc version. The table below lists the support tier for each supported combination. A list of [supported compile toolchains](#supported-toolchains) is also supplied for tier 1 platforms.

**仅在支持的平台上运行Node.js生产应用程序。**

Node.js does not support a platform version if a vendor has expired support for it. In other words, Node.js does not support running on End-of-Life (EoL) platforms. This is true regardless of entries in the table below. 换言之，Node.js不支持运行于终身生命(EOL) 平台。 无论下表中的条目如何，情况都是如此。

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

<em id="fn1">1</em>: 海合会8 未在基础平台上提供。 <em id="fn1">1</em>: GCC 8 is not provided on the base platform. Users will need the [Toolchain test builds PPA](https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/test?field.series_filter=xenial) or similar to source a newer compiler.

<em id="fn2">2</em>: 海合会8 未在基础平台上提供。 用户需要 [devtoolset-8](https://www.softwarecollections.org/en/scls/rhscl/devtoolset-8/) 或更高版本才能提供更新的编译器。

<em id="fn3">3</em>: 更早的内核版本可能适用于 ARM64 。 然而， Node.js 仅测试基础结构测试 >= 4.5。

<em id="fn4">4</em>: On Windows, running Node.js in Windows terminal emulators like `mintty` requires the usage of [winpty](https://github.com/rprichard/winpty) for the tty channels to work (e.g. `winpty node.exe script.js`). In "Git bash" if you call the node shell alias (`node` without the `.exe` extension), `winpty` is used automatically. 在“Git bash”中，如果您调用节点外壳别名(`节点` 没有 `xe` 扩展 ), `winpty` 被自动使用

<em id="fn5">5</em>: The Windows Subsystem for Linux (WSL) is not supported, but the GNU/Linux build process and binaries should work. The community will only address issues that reproduce on native GNU/Linux systems. Issues that only reproduce on WSL should be reported in the [WSL issue tracker](https://github.com/Microsoft/WSL/issues). Running the Windows binary (`node.exe`) in WSL is not recommended. It will not work without workarounds such as stdio redirection. 只能解决在本机的 GNU/Linux 系统上复制的问题。 只在 WSL 上复制的问题应该在 [WSL issue Tracker](https://github.com/Microsoft/WSL/issues) 中报告。 不建议在 WSL 中运行 Windows 二进制(`node.exe`)。 如果没有工作区，如立体重定向，它将无法工作 。

<em id="fn6">6</em>: Running Node.js on x86 Windows should work and binaries are provided. However, tests in our infrastructure only run on WoW64. Furthermore, compiling on x86 Windows is Experimental and may not be possible. 然而，我们的基础设施试验只在WoW64上进行。 此外，在 x86 Windows 上编译是实验性的， 可能是不可能的。

<em id="fn7">7</em>: The default FreeBSD 12.0 compiler is Clang 6.0.1, but FreeBSD 12.1 upgrades to 8.0.1. Other Clang/LLVM versions are available via the system's package manager, including Clang 9.0. 其它的 Clang/LLVM 版本可通过系统包管理器获取 ，包括Clang 9.0。

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

<em id="fn8">8</em>: The Enterprise Linux devtoolset-8 allows us to compile binaries with GCC 8 but linked to the glibc and libstdc++ versions of the host platforms (CentOS 7 / RHEL 7). Therefore, binaries produced on these systems are compatible with glibc >= 2.17 and libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20`). These are available on distributions natively supporting GCC 4.9, such as Ubuntu 14.04 and Debian 8. 因此，在这些系统 生成的二进制文件与 glibc >= 2.17 和 libstdc++ >= 6.0.20 (`GLIBCXX_3.4.20` ) 兼容。 这些文件可在本质上支持海湾合作委员会4.9版的分发，例如 Ubuntu 14.04和Debian 8。

#### OpenSSL 支持

OpenSSL-1.1.1 requires the following assembler version for use of asm support on x86_64 and ia32.

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

 If compiling without one of the above, use `configure` with the `--openssl-no-asm` flag. Otherwise, `configure` will fail. 否则， `配置` 将失败。

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

macOS users can install the `Xcode Command Line Tools` by running `xcode-select --install`. Alternatively, if you already have the full Xcode installed, you can find them under the menu `Xcode -> Open Developer Tool ->
More Developer Tools...`. This step will install `clang`, `clang++`, and `make`. 或者，如果您已经安装了完整的 Xcode ， 您可以在菜单 `Xcode -> 打开开发者工具 ->
更多开发者工具。 。` 此步骤将安装 `clang`, `clang++`, `make`。

#### Building Node.js

If the path to your build directory contains a space, the build will likely fail.

要生成Node.js：

```console
$ ./configure
make -j4
```

The `-j4` option will cause `make` to run 4 simultaneous compilation jobs which may reduce build time. For more information, see the [GNU Make Documentation](https://www.gnu.org/software/make/manual/html_node/Parallel.html). 欲了解更多信息，请参阅 [GNU Make 文档](https://www.gnu.org/software/make/manual/html_node/Parallel.html)。

The above requires that `python` resolves to a supported version of Python. See [Prerequisites](#prerequisites). 查看 [前提条件](#prerequisites)。

After building, setting up [firewall rules](tools/macos-firewall.sh) can avoid popups asking to accept incoming network connections when running tests.

Running the following script on macOS will add the firewall rules for the executable `node` in the `out` directory and the symbolic `node` link in the project's root directory.

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

If you are running tests before submitting a Pull Request, the recommended command is:

```console
$ make -j4 测试
```

`make -j4 test` does a full check on the codebase, including running linters and documentation tests.

请确保班轮没有报告任何问题，并确保所有测试通过。 请 不要提交检查失败的补丁。

If you want to run the linter without running tests, use `make lint`/`vcbuild lint`. It will lint JavaScript, C++, and Markdown files. 它会lint JavaScript, C++, and Markdown文件。

If you are updating tests and want to run tests in a single test file (e.g. `test/parallel/test-stream2-transform.js`):

```text
$ python tools/test.py test/paradel/test-stream2-transform.js
```

You can execute the entire suite of tests for a given subsystem by providing the name of a subsystem:

```text
$ python tools/test.py -J --mode=release child-process
```

If you want to check the other options, please refer to the help by using the `--help` option:

```text
$ python tools/test.py --help
```

您通常可以使用节点直接运行测试：

```text
$ .节点./test/paradel/test-stream2-transform.js
```

Remember to recompile with `make -j4` in between test runs if you change code in the `lib` or `src` directories.

The tests attempt to detect support for IPv6 and exclude IPv6 tests if appropriate. If your main interface has IPv6 addresses, then your loopback interface must also have '::1' enabled. For some default installations on Ubuntu that does not seem to be the case. To enable '::1' on the loopback interface on Ubuntu: 如果您的主接口有IPv6地址，那么您的 循环接口也必须启用 ':1' 。 对于Ubuntu上的一些默认安装 似乎没有。 要启用 '::1' 在 Ubuntu 的 循环接口上：

```bash
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```

You can use [node-code-ide-configs](https://github.com/nodejs/node-code-ide-configs) to run/debug tests, if your IDE configs are present.

#### 正在运行的范围

确保您添加或更改的任何代码都包含在测试范围内是好的做法。 您可以通过运行带有覆盖面的测试套件来这样做：

```console
$ ./configure --coverage
$ make coverage
```

A detailed coverage report will be written to `coverage/index.html` for JavaScript coverage and to `coverage/cxxcoverage.html` for C++ coverage.

If you only want to run the JavaScript tests then you do not need to run the first command (`./configure --coverage`). Run `make coverage-run-js`, to execute JavaScript tests independently of the C++ test suite: 运行 `make coverage-run-js`, 来执行 JavaScript 测试，独立于 C++ 测试套件：

```text
美元制作封面运行js
```

If you are updating tests and want to collect coverage for a single test file (e.g. `test/parallel/test-stream2-transform.js`):

```text
$做覆盖清洁
$NODE_V8_COVERAGE=coverage/tmp python tools/test.py test/paradel/test-stream2-transform.js
$做覆盖报告-js
```

You can collect coverage for the entire suite of tests for a given subsystem by providing the name of a subsystem:

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

This will spin up a static file server and provide a URL to where you may browse the documentation locally.

If you're comfortable viewing the documentation using the program your operating system has associated with the default web browser, run the following.

```bash
打开文档
```

This will open a file URL to a one-page version of all the browsable HTML documents using the default browser.

测试Node.js是否正确构建：

```bash
./node -e "console.log('Hello from Node.js ' + process.version)"
```

#### 构建调试版本

If you run into an issue where the information provided by the JS stack trace is not enough, or if you suspect the error happens outside of the JS VM, you can try to build a debug enabled binary:

```console
$ ./configure --debug
$make -j4
```

`make` with `./configure --debug` generates two binaries, the regular release one in `out/Release/node` and a debug binary in `out/Debug/node`, only the release version is actually installed when you run `make install`.

To use the debug build with all the normal dependencies overwrite the release version in the install directory:

``` console
$ make installation PREFIX=/opt/node-debug/
$ cp -f out/debug/节点 /opt/node-debug/节点
```

当使用调试二进制时，在发生崩溃时将生成核心转储。 When using the debug binary, core dumps will be generated in case of crashes. These core dumps are useful for debugging when provided with the corresponding original debug binary and system information.

Reading the core dump requires `gdb` built on the same platform the core dump was captured on (i.e. 64-bit `gdb` for `node` built on a 64-bit system, Linux `gdb` for `node` built on Linux) otherwise you will get errors like `not in executable format: File format not recognized`.

从核心倾销生成回溯跟踪的示例：

``` console
$ gdb /opt/node-debug/节点core.node.8.153559906
$ backtrack
```

#### 构建一个ASAN建筑

[ASAN](https://github.com/google/sanitizers) can help detect various memory related bugs. ASAN builds are currently only supported on linux. If you want to check it on Windows or macOS or you want a consistent toolchain on Linux, you can try [Docker](https://www.docker.com/products/docker-desktop) (using an image like `gengjiawen/node-build:2020-02-14`). ASAN构建当前仅在线上支持。 如果您想要在 Windows 或 macOS 上检查，或者您想在 Linux 上找到一个一致的工具链 ， 您可以尝试 [Docker](https://www.docker.com/products/docker-desktop) (使用类似于 `gengjiawen/node-build:2020-02-14` 的图像)。

The `--debug` is not necessary and will slow down build and testing, but it can show clear stacktrace if ASAN hits an issue.

``` console
$ ./configuring --enable-asan && make -j4
$ make test-only
```

#### 开发时加速频繁的重建

If you plan to frequently rebuild Node.js, especially if using several branches, installing `ccache` can help to greatly reduce build times. Set up with: 设置于：
```console
$ sudo apt install ccache # for Debian/Ubuntu, 包含在大部分Linux distros
$ccache -o cache_dir=<tmp_dir>
ccache -o max_size=5。 G
$ 导出 CC="ccache gcc" # 添加到您的. rofile
$ 导出 CXX="ccache g++" # 添加到您的 .profile
```
这将允许在切换分支时进行近瞬间重建。

When modifying only the JS layer in `lib`, it is possible to externally load it without modifying the executable:
```console
$ ./configure --node-build-modules-path $(pwd)
```
由此产生的二进制文件不会包含任何JS文件，并尝试从 指定目录加载它们。 The resulting binary won't include any JS files and will try to load them from the specified directory. The JS debugger of Visual Studio Code supports this configuration since the November 2020 version and allows for setting breakpoints.

#### 疑难解答Unix 和 macOS 版本

旧版本的构建有时会导致 `文件在构建时找不到` 个错误。 这个问题和其他一些问题可以通过 `进行远程` 解决。 `远程` 配方主动移除构建工艺品。 您将需要 重新构建(`make -j4`)。 既然所有建筑物已被移除，此 重建可能比以前的建筑需要更多的时间。 此外， `远程` 删除了存储 `./configuration` 结果的文件。 如果你的 运行 `。 配置` 有非默认选项 (例如 `--debug`), 您需要 才能重新运行 `make -j4`

### 窗口

#### 必备条件

##### 选项1：手动安装

* [Python 3.9](https://www.microsoft.com/en-us/p/python-39/9p7qfqmjrfp7)
* The "Desktop development with C++" workload from [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/) or the "C++ build tools" workload from the [Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019), with the default optional components
* Basic Unix tools required for some tests, [Git for Windows](https://git-scm.com/download/win) includes Git Bash and tools which can be included in the global `PATH`.
* [NetWassembler](https://www.nasm.us/), 用于 OpenSSL 集成模块。 如果未安装在默认位置，需要手动将 添加到 `PATH` 中。 The [NetWide Assembler](https://www.nasm.us/), for OpenSSL assembler modules. If not installed in the default location, it needs to be manually added to `PATH`. A build with the `openssl-no-asm` option does not need this, nor does a build targeting ARM64 Windows.

构建MSI安装程序包的可选要求：

* The [WiX Toolset v3.11](https://wixtoolset.org/releases/) and the [Wix Toolset Visual Studio 2019 Extension](https://marketplace.visualstudio.com/items?itemName=WixToolset.WixToolsetVisualStudio2019Extension)
* The [WiX Toolset v3.14](https://wixtoolset.org/releases/) if building for Windows 10 on ARM (ARM64)

在ARM上编译Windows 10的可选要求 (ARM64)：

* Visual Studio 15.9.0 或更新版本
* Visual Studio 可选组件
  * ARM64 的Visual C++ 编译器和库
  * ARM64 的Visual C++ ATL
* Windows 10 SDK 10.0.17763.0 或更新版本

##### 备选办法2：自动使用 Boxstarter 安装

A [Boxstarter](https://boxstarter.org/) script can be used for easy setup of Windows systems with all the required prerequisites for Node.js development. This script will install the following [Chocolatey](https://chocolatey.org/) packages: 此脚本将安装以下 [Chocolatey](https://chocolatey.org/) 软件包：

* [Git for Windows](https://chocolatey.org/packages/git) with the `git` and Unix tools added to the `PATH`
* [Python 3.x](https://chocolatey.org/packages/python)
* [Visual Studio 2019 Build Tools](https://chocolatey.org/packages/visualstudio2019buildtools) with [Visual C++ workload](https://chocolatey.org/packages/visualstudio2019-workload-vctools)
* [NetWide Assembler](https://chocolatey.org/packages/nasm)

To install Node.js prerequisites using [Boxstarter WebLauncher](https://boxstarter.org/WebLauncher), open <https://boxstarter.org/package/nr/url?https://raw.githubusercontent.com/nodejs/node/HEAD/tools/bootstrap/windows_boxstarter> with Internet Explorer or Edge browser on the target machine.

或者，您可以使用 PowerShell。 Alternatively, you can use PowerShell. Run those commands from an elevated PowerShell terminal:

```powershell
Set-ExecutionPolicy Unrestricted -Force
iex (New-Object System.Net.WebClient).DownloadString('https://boxstarter.org/bootstraper.ps1'))
get-boxstarter -Force
Install-BoxstarterPackage https://raw.githubusercontent.com/nodejs/node/HEAD工具s/bootstrap/windows_boxstarter -disableReboots
```

The entire installation using Boxstarter will take up approximately 10 GB of disk space.

#### Building Node.js

If the path to your build directory contains a space or a non-ASCII character, the build will likely fail.

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

Android 不支持该平台。 Android is not a supported platform. Patches to improve the Android build are welcome. There is no testing on Android in the current continuous integration environment. The participation of people dedicated and determined to improve Android building, testing, and support is encouraged. 在当前的连续集成 环境中没有测试安卓系统。 鼓励那些致力于并决心改进 Android 建筑、测试和支持的人参与。

Be sure you have downloaded and extracted [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html) before in a folder. Then run: 然后运行：

```console
$ ./android-configure /path/to/your/android-ndk
$make
```

## `Intl` (ECMA-402) 支持

[Intl](https://github.com/nodejs/node/blob/HEAD/doc/api/intl.md) support is enabled by default.

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

 In this configuration, only English data is included, but the full `Intl` (ECMA-402) APIs.  It does not need to download any dependencies to function. You can add full data at runtime.  它不需要下载 任何依赖方才能起作用。 您可以在运行时添加完整数据。

#### Unix/macOS

```console
$ ./configure --with-intl=smallicu
```

#### 窗口

```console
> \vcbuild小图标
```

### 构建时不支持 Intl

The `Intl` object will not be available, nor some other APIs such as `String.normalize`.

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

If you are cross-compiling, your `pkg-config` must be able to supply a path that works for both your host and target environments.

### 使用 ICU 构建特定的

You can find other ICU releases at [the ICU homepage](http://site.icu-project.org/download). Download the file named something like `icu4c-**##.#**-src.tgz` (or `.zip`). 下载命名的文件 `icu4c-**##。#**-src.tgz` (或 `.zip`).

To check the minimum recommended ICU, run `./configure --help` and see the help for the `--with-icu-source` option. A warning will be printed during configuration if the ICU version is too old. 如果在 ICU 版本过旧，配置过程中将打印 个警告。

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

First unpack latest ICU to `deps/icu` [icu4c-**##.#**-src.tgz](http://site.icu-project.org/download) (or `.zip`) as `deps/icu` (You'll have: `deps/icu/source/...`)

```console
> \vcbuild完整图标
```

## 使用 FIPS 兼容的 OpenSSL 构建Node.js

The current version of Node.js does not support FIPS when statically linking (the default) with OpenSSL 1.1.1 but for dynamically linking it is possible to enable FIPS using the configuration flag `--openssl-is-fips`.

### 配置和构建FIPS的 quictls/openssl

对于quictls/openssl 3.0 ，动态链接时可以启用 FIPS。 For quictls/openssl 3.0 it is possible to enable FIPS when dynamically linking. Node.js currently uses openssl-3.0.0+quic which can be configured as follows:
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

After the FIPS module and configuration file have been installed by the above instructions we also need to update `/path/to/install/dir/ssl/openssl.cnf` to use the generated FIPS configuration file (`fipsmodule.cnf`):
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

In the above case OpenSSL is not installed in the default location so two environment variables need to be set, `OPENSSL_CONF`, and `OPENSSL_MODULES` which should point to the OpenSSL configuration file and the directory where OpenSSL modules are located:
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
If the `ldd` command says that `libcrypto` cannot be found one needs to set `LD_LIBRARY_PATH` to point to the directory used above for `--shared-openssl-libpath` (see previous step).

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

FIPS support can then be enable via the OpenSSL configuration file or using `--enable-fips` or `--force-fips` command line options to the Node.js executable. FIPS support can then be enable via the OpenSSL configuration file or using `--enable-fips` or `--force-fips` command line options to the Node.js executable. See sections [Enabling FIPS using Node.js options](#enabling-fips-using-node.js-options) and [Enabling FIPS using OpenSSL config](#enabling-fips-using-openssl-config) below.

### 使用 Node.js 选项启用 FIPS
This is done using one of the Node.js options `--enable-fips` or `--force-fips`, for example:
```console
$ 节点 --enable-fips -p 'crypto.getFips()'
```

### 使用 OpenSSL 配置启用 FIPS
This example show that using OpenSSL's configuration file, FIPS can be enabled without specifying the `--enable-fips` or `--force-fips` options by setting `default_properties = fips=yes` in the FIPS configuration file. See [link](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers) for details. 详情请参阅 [链接](https://github.com/openssl/openssl/blob/master/README-FIPS.md#loading-the-fips-module-at-the-same-time-as-other-providers)

For this to work the OpenSSL configuration file (default openssl.cnf) needs to be updated. The following shows an example: 下面显示一个示例：
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
After this change Node.js can be run without the `--enable-fips` or `--force-fips` options.

## 使用外部核心模块构建Node.js

It is possible to specify one or more JavaScript text files to be bundled in the binary as built-in modules when building Node.js.

### Unix/macOS

This command will make `/root/myModule.js` available via `require('/root/myModule')` and `./myModule2.js` available via `require('myModule2')`.

```console
$ ./configure --link-module '/root/myModule.js' --link-module './myModule2.js'
```

### 窗口

To make `./myModule.js` available via `require('myModule')` and `./myModule2.js` available via `require('myModule2')`:

```console
> .\vcbuild link-module './myModule.js' link-module './myModule2.js'
```

## Node.js下游发行商的说明
The Node.js ecosystem is reliant on ABI compatibility within a major release. To maintain ABI compatibility it is required that distributed builds of Node.js be built against the same version of dependencies, or similar versions that do not break their ABI compatibility, as those released by Node.js for any given `NODE_MODULE_VERSION` (located in `src/node_version.h`).

Node.js生态系统依赖于一个主要版本内的 ABI 兼容性。 The Node.js ecosystem is reliant on ABI compatibility within a major release. To maintain ABI compatibility it is required that distributed builds of Node.js be built against the same version of dependencies, or similar versions that do not break their ABI compatibility, as those released by Node.js for any given `NODE_MODULE_VERSION` (located in `src/node_version.h`).

When Node.js is built (with an intention to distribute) with an ABI incompatible with the official Node.js builds (e.g. using a ABI incompatible version of a dependency), please reserve and use a custom `NODE_MODULE_VERSION` by opening a pull request against the registry available at [https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json](https://github.com/nodejs/node/blob/HEAD/doc/abi_version_registry.json).
