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

Node.js是一个开源、跨平台的 JavaScript 运行环境。 它在浏览器之外执行 JavaScript 代码。 关于使用 Node.js的更多信息，请参阅 [Node.js网站][]。

Node.js项目使用 [开放治理模式](./GOVERNANCE.md)。 [OpenJS Foundation][] 为项目提供支持。

**此项目受 [行为准则][] 的约束。**

# 目录

* [支持](#support)
* [发布类型](#release-types)
  * [下载](#download)
    * [当前版本和 LTS](#current-and-lts-releases)
    * [每晚发布](#nightly-releases)
    * [API 文档](#api-documentation)
  * [正在验证二进制文件](#verifying-binaries)
* [Building Node.js](#building-nodejs)
* [安全](#security)
* [为 Node.js 贡献](#contributing-to-nodejs)
* [当前项目团队成员](#current-project-team-members)
  * [TSC（技术指导委员会）](#tsc-technical-steering-committee)
  * [协作者](#collaborators)
  * [释放密钥](#release-keys)
* [许可协议](#license)

## 支持

寻找帮助吗？ 查看 [关于获得支持](.github/SUPPORT.md) 的说明。

## 发布类型

* **当前**: 正在活动开发中。 当前版本的代码在其主要版本号的分支中 (例如， [v15.x](https://github.com/nodejs/node/tree/v15.x))。 Node.js每隔6个月发布一个新的主要版本，允许进行重大更改。 每年4月和10月都发生这种情况。 每年10月出现的释放都有8个月的支助寿命。 每年4月出现的释放将每年10月都转换为低地电信系统（见下文）。
* **LTS**: 获得长期支持的释放，侧重于稳定和安全。 每个偶数的主要版本都将成为LTS版本。 LTS 发布会得到 _活跃的 LTS_ 支持的12个月，以及另外18个月的 _维护_。 LTS 发行行有按字母顺序排序的代码名，从v4 Argon开始。 除某些特殊情况外，没有任何突破性变化或特征增添。
* **每晚**: 当前分支的代码在发生更改时每隔24小时构建一次。 谨慎使用。

当前版本和 LTS 版本遵循 [语义版本](https://semver.org)。 发布组成员 [签名](#release-keys) 当前发布和 LTS 发布。 欲了解更多信息，请参阅 [ReleADME](https://github.com/nodejs/Release#readme)。

### 下载

Binaries, installers, and source tarballs are available at <https://nodejs.org/en/download/>.

#### 当前版本和 LTS
<https://nodejs.org/download/release/>

[最新的](https://nodejs.org/download/release/latest/) 目录是当前版本的一个别名。 最新的 -_代号_ 目录是LTS 行最新版本的一个别名。 例如， [最新的 fermium](https://nodejs.org/download/release/latest-fermium/) 目录包含最新的 Fermium (Node.js 14)。

#### 每晚发布
<https://nodejs.org/download/nightly/>

每个目录名称和文件名都包含一个日期(UTC)，并在发布的HEAD中提交SHA。

#### API 文档

最新版本的文档是 <https://nodejs.org/api/>。 版本专用文档可在 _docs_ 子目录中的每个发布目录中查阅。 特定版本的文档也在 <https://nodejs.org/download/docs/>。

### 正在验证二进制文件

下载目录包含 `SHASUMS256.txt` 文件，其中包含 SHA 校验和文件.

要下载 `SHASUMS256.txt` 使用 `曲线`:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt
```

要检查下载的文件是否与校验总和匹配，请用 `sha256sum` 运行它，命令例如：

```console
$ grep node-vx.y.z.tar.gz SHASUMS256.txt | sha256sum -c -
```

对于当前的 LTS， `SHASUMS256.txt` 的 GPG 脱机签名在 `SHASUMS256.txt.sig` 中。 您可以使用 `gpg` 验证 `SHASUMS256.txt` 的完整性。 You will first need to import [the GPG keys of individuals authorized to create releases](#release-keys). 要导入密钥：

```console
$ gpg --keyserver pool.sks-keyservers.net --recv-keys DD8F2338BAE7501E3DDD5AC78C273792F7D83545D
```

请参阅此README底部以获取一个完整的脚本来导入活动释放密钥。

接下来，下载 `SHASUMS256.txt.sig` 版本：

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt.sig
```

然后使用 `gpg --验证SHASUMS256.txt.sig SHASUMS256.txt` 来验证文件的签名。

## Building Node.js

请参阅 [BUILDING.md](BUILDING.md) 关于如何从源代码构建Node.js的说明以及支持的平台列表。

## 安全

关于Node.js报告安全脆弱性的信息，请参阅 [SECURITY.md](./SECURITY.md)。

## 为 Node.js 贡献

* [为该项目做贡献][]
* [工 作 组][]
* [战略倡议][]
* [A. 技术价值和优先次序][]

## 当前项目团队成员

关于Node.js项目管理的信息，请参阅 [GOVERNANCE.md](./GOVERNANCE.md)。

### TSC（技术指导委员会）

<!--lint disable prohibited-strings-->
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (她/她)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (he/him)
* [ChALkeR](https://github.com/ChALkeR) - **cetcete 0.26 de la confirmes de la connection de la connectée de la connectée de la connectée de périque** &lt;chalkerx@gmail.com&gt; (he/him)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (he/him)
* [codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (he/her)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (he/him)
* [Danielleleleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (he/her)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (he/him)
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (he/him)
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (he/her)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (he/him)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (he/him)
* [marchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (她/她)
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (he/him)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [targos](https://github.com/targos) - **Michael Zasso** &lt;targos@protonmail.com&gt; (he/him)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [Trott](https://github.com/Trott) - **Rich Trott** &lt;rtrott@gmail.com&gt; (he/him)

### 海训方案

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (她/她)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (he/him)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt;  (he/they)
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (he/him)
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [imyller](https://github.com/imyller) - **Ilkka Myller** &lt;ilkka.myller@nodefield.com&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [nebrius](https://github.com/nebrius) - **Bryan Hughes** &lt;bryan@nebri.us&gt;
* [ofrobots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (he/him)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [rvagg](https://github.com/rvagg) - **Rod Vagg** &lt;r@va.gg&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (he/him)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (he/him)
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;

### 协作者

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (她/她)
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [ak239](https://github.com/ak239) - **Aleksei Koziatinskii** &lt;ak239spb@gmail.com&gt;
* [AndreasMadsen](https://github.com/AndreasMadsen) - **Andreas Madsen** &lt;amwebdk@gmail.com&gt; (he/him)
* [antsmartian](https://github.com/antsmartian) - **Anto Aravinth** &lt;anto.aravinth.cse@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [AshCripps](https://github.com/AshCripps) - **Ash Cripps** &lt;acripps@redhat.com&gt;
* [bcoe](https://github.com/bcoe) - **Ben Coe** &lt;bencoe@gmail.com&gt; (he/him)
* [Bengl](https://github.com/bengl) - **Bryan English** &lt;bryan@bryanenglish.com&gt; (he/him)
* [benjamingr](https://github.com/benjamingr) - **Benjamin Gruenbaum** &lt;benjamingr@gmail.com&gt;
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (她/她)
* [bmeck](https://github.com/bmeck) - **Bradley Farias** &lt;bradley.meck@gmail.com&gt;
* [bmeurer](https://github.com/bmeurer) - **Benedikt Meurer** &lt;benedikt.meurer@gmail.com&gt;
* [Boneskull](https://github.com/boneskull) - **Christopher Hiller** &lt;boneskull@boneskull.com&gt; (he/him)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (he/him)
* [bzoz](https://github.com/bzoz) - **Bartosz Sosnowski** &lt;bartosz@janeasystems.com&gt;
* [cclauss](https://github.com/cclauss) - **Christian Clauss** &lt;cclauss@me.com&gt; (he/him)
* [ChALkeR](https://github.com/ChALkeR) - **cetcete 0.26 de la confirmes de la connection de la connectée de la connectée de la connectée de périque** &lt;chalkerx@gmail.com&gt; (he/him)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (he/him)
* [codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (he/her)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (he/him)
* [Danielleleleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (he/her)
* [davisjam](https://github.com/davisjam) - **Jamie Davis** &lt;davisjam@vt.edu&gt; (he/him)
* [DerekNonGeneric](https://github.com/DerekNonGeneric) - **Derek Lewis** &lt;DerekNonGeneric@inf.is&gt; (he/him)
* [devnexen](https://github.com/devnexen) - **David Carlier** &lt;devnexen@gmail.com&gt;
* [devsnek](https://github.com/devsnek) - **Gus Caplan** &lt;me@gus.host&gt; (他们/他们)
* [dmabupt](https://github.com/dmabupt) - **Xu Meng** &lt;dmabupt@gmail.com&gt; (he/him)
* [dnlup](https://github.com/dnlup) **Daniele Belardi** &lt;dwon.dnl@gmail.com&gt; (he/him)
* [edsadr](https://github.com/edsadr) - **Adrian Estrada** &lt;edsadr@gmail.com&gt; (he/him)
* [eugeneo](https://github.com/eugeneo) - **Eugene Ostroukhov** &lt;eostroukhov@google.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (he/him)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt; (he/they)
* [Flarna](https://github.com/Flarna) - **Gerhard Stoubich** &lt;deb2001-github@yahoo.de&gt;  (he/they)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gdams](https://github.com/gdams) - **George Adams** &lt;george.adams@uk.ibm.com&gt; (he/him)
* [获取](https://github.com/geek) - **Wyatt Preul** &lt;wpreul@gmail.com&gt;
* [gengjiawen](https://github.com/gengjiawen) - **Jiawen Geng** &lt;technicalcute@gmail.com&gt;
* [GeoffreyBooth](https://github.com/geoffreybooth) - **Geoffrey Booth** &lt;webmaster@geoffreybooth.com&gt; (he/him)
* [gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (he/him)
* [guybedford](https://github.com/guybedford) - **Guy Bedford** &lt;guybedford@gmail.com&gt; (he/him)
* [HarshithaKP](https://github.com/HarshithaKP) - **Harshitha K P** &lt;harshitha014@gmail.com&gt; (她/她)
* [hashseed](https://github.com/hashseed) - **Yang Guo** &lt;yangguo@chromium.org&gt; (he/him)
* [他自己65](https://github.com/himself65) - **Zeyu Yang** &lt;himself65@outlook.com&gt; (he/him)
* [hiroppy](https://github.com/hiroppy) - **Yuta Hiroto** &lt;hello@hiroppy.me&gt; (he/him)
* [iansu](https://github.com/iansu) - **Ian Sutherland** &lt;ian@iansutherland.ca&gt;
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [JacksonTian](https://github.com/JacksonTian) - **Jackson Tian** &lt;shyvo1987@gmail.com&gt;
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (he/him)
* [jdalton](https://github.com/jdalton) - **John-David Dalton** &lt;john.david.dalton@gmail.com&gt;
* [jkrems](https://github.com/jkrems) - **Jan Krems** &lt;jan.krems@gmail.com&gt; (he/him)
* [joaocgreis](https://github.com/joaocgreis) - **João Reis** &lt;reis@janeasystems.com&gt;
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (he/her)
* [juanarbol](https://github.com/juanarbol) - **Juan Joseassociated Arboleda** &lt;soyjuanarbol@gmail.com&gt; (he/him)
* [JungMinu](https://github.com/JungMinu) - **Minwoo Jung** &lt;nodecorelab@gmail.com&gt; (he/him)
* [lance](https://github.com/lance) - **Lance Ball** &lt;lball@redhat.com&gt; (he/him)
* [传说](https://github.com/legendecas) - **Chengzhong Wu** &lt;legendecas@gmail.com&gt; (he/him)
* [Leko](https://github.com/Leko) - **Shingo Inoue** &lt;leko.noor@gmail.com&gt; (he/him)
* [linkgoron](https://github.com/linkgoron) - **Nitzan Uziely** &lt;linkgoron@gmail.com&gt;
* [lpinca](https://github.com/lpinca) - **Luigi Pinca** &lt;luigipinca@gmail.com&gt; (he/him)
* [lundibundi](https://github.com/lundibundi) - **Denys Otrishko** &lt;shishugi@gmail.com&gt; (he/him)
* [Lxxyx](https://github.com/Lxxyx) - **Zijian Liu** &lt;lxxyxzj@gmail.com&gt; (he/him)
* [mfintosh](https://github.com/mafintosh) - **Mathias Buus** &lt;mathiasbuus@gmail.com&gt; (he/him)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (he/him)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (he/him)
* [miladfarca](https://github.com/miladfarca) - **Milad Fa** &lt;mfarazma@redhat.com&gt; (he/him)
* [mildsunrise](https://github.com/mildsunrise) - **Alba Mendez** &lt;me@alba.sh&gt; (she/her)
* [misterdjules](https://github.com/misterdjules) - **Julien Gilli** &lt;jgilli@nodejs.org&gt;
* [marchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (她/她)
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (he/him)
* [ofrobots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (he/him)
* [oyyd](https://github.com/oyyd) - **Ouyang Yadong** &lt;oyydoibh@gmail.com&gt; (he/him)
* [panva](https://github.com/panva) - **Filip Skokan** &lt;panva.ip@gmail.com&gt;
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja D P** &lt;Pooja.D.P@ibm.com&gt; (she/her)
* [puzpuzpuz](https://github.com/puzpuzpuz) - **Andrey Pechkurov** &lt;apechkurov@gmail.com&gt; (he/him)
* [Qard](https://github.com/Qard) - **Stephen Belanger** &lt;admin@stephenbelanger.com&gt; (he/him)
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt; (he/him)
* [refack](https://github.com/refack) - **Refael Ackermann (attributed civiliates, Bruximately)** &lt;refack@gmail.com&gt; (he/him/searcticma/maximum diff)
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
* [targos](https://github.com/targos) - **Michael Zasso** &lt;targos@protonmail.com&gt; (he/him)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (he/him)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [Trivikr](https://github.com/trivikr) - **Trivikram Kamat** &lt;trivikr.dev@gmail.com&gt;
* [Trott](https://github.com/Trott) - **Rich Trott** &lt;rtrott@gmail.com&gt; (he/him)
* [vdeturckheim](https://github.com/vdeturckheim) - **Vladimir de Turckheim** &lt;vlad2t@hotmail.com&gt; (he/him)
* [watilde](https://github.com/watilde) - **Daijiro Wachi** &lt;daijiro.wachi@gmail.com&gt; (he/him)
* [watson](https://github.com/watson) - **Thomas Watson** &lt;w@tson.dk&gt;
* [XadillaX](https://github.com/XadillaX) - **Khaidi Chu** &lt;i@2333.moe&gt; (he/him)
* [yashLadha](https://github.com/yashLadha) - **Yash Ladha** &lt;yash@yashladha.in&gt; (he/him)
* [yhwang](https://github.com/yhwang) - **Yihong Wang** &lt;yh.wang@ibm.com&gt;
* [yorkie](https://github.com/yorkie) - **Yorkie Liu** &lt;yorkiefixer@gmail.com&gt;
* [yosuke-furukawa](https://github.com/yosuke-furukawa) - **Yosuke Furukawa** &lt;yosuke.furukawa@gmail.com&gt;
* [ZYSzys](https://github.com/ZYSzys) - **Yongsheng Zhang** &lt;zyszys98@gmail.com&gt; (he/him)

### 合作者荣誉勋章

* [andrasq](https://github.com/andrasq) - **Andras** &lt;andras@kinvey.com&gt;
* [AnnaMag](https://github.com/AnnaMag) - **Anna M. Kedzierska** &lt;anna.m.kedzierska@gmail.com&gt;
* [aqrn](https://github.com/aqrln) - **Alexey Orlenko** &lt;eaglexrlnk@gmail.com&gt; (he/him)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [brendanashworth](https://github.com/brendanashworth) - **Brendan Ashworth** &lt;brendan.ashworth@me.com&gt;
* [calvinmetcalf](https://github.com/calvinmetcalf) - **Calvin Metcalf** &lt;calvin.metcalf@gmail.com&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [claudiorodriguez](https://github.com/claudiorodriguez) - **Claudio Rodriguez** &lt;cjrodr@yahoo.com&gt;
* [DavidCai1993](https://github.com/DavidCai1993) - **David Cai** &lt;davidcai1993@yahoo.com&gt; (he/him)
* [数字无限](https://github.com/digitalinfinity) - **Hitesh Kanwathirtha** &lt;digitalinfinity@gmail.com&gt; (he/him)
* [eljefedelrodeodeljefe](https://github.com/eljefedelrodeodeljefe) - **Robert Jefe Lindstaedt** &lt;robert.lindstaedt@gmail.com&gt;
* [estliberitas](https://github.com/estliberitas) - **Alexander Makarenko** &lt;estliberitas@gmail.com&gt;
* [fireedfox](https://github.com/firedfox) - **Daniel Wang** &lt;wangyang0123@gmail.com&gt;
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (he/him)
* [glentiki](https://github.com/glentiki) - **Glen Keane** &lt;glenkeane.94@gmail.com&gt; (he/him)
* [iarna](https://github.com/iarna) - **Rebecca Turner** &lt;me@re-becca.org&gt;
* [imran-iq](https://github.com/imran-iq) - **Imran Iqbal** &lt;imran@imraniqbal.org&gt;
* [Olegas](https://github.com/Olegas) - **Oleg Elifantiev** &lt;oleg@elifantiev.ru&gt;
* [lxe](https://github.com/lxe) - **Aleksey Smolenchuk** &lt;lxe@lxe.co&gt;
* [thlorenz](https://github.com/thlorenz) - **Thorsten Lorenz** &lt;thlorenz@gmx.de&gt;
* [jasongin](https://github.com/jasongin) - **Jason Ginchereau** &lt;jasongin@microsoft.com&gt;
* [jbergstroem](https://github.com/jbergstroem) - **Johan Bergström** &lt;bugs@bergstroem.nu&gt;
* [jhamhader](https://github.com/jhamhader) - **Yuval Brik** &lt;yuval@brik.org.il&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [julianduque](https://github.com/julianduque) - **Julian Duque** &lt;julianduquej@gmail.com&gt; (he/him)
* [kfarnung](https://github.com/kfarnung) - **Kyle Farnung** &lt;kfarnung@microsoft.com&gt; (he/him)
* [kunalspathak](https://github.com/kunalspathak) - **Kunal Pathak** &lt;kunal.pathak@microsoft.com&gt;
* [lucamaraschi](https://github.com/lucamaraschi) - **Luca Maraschi** &lt;luca.maraschi@gmail.com&gt; (he/him)
* [rlidwka](https://github.com/rlidwka) - **Alex Kocharin** &lt;alex@kocharin.ru&gt;
* [maclover7](https://github.com/maclover7) - **Jon Moss** &lt;me@jonathanmoss.me&gt; (he/him)
* [配对](https://github.com/matthewloring) - **Matthew Loring** &lt;mattloring@google.com&gt;
* [微米](https://github.com/micnic) - **Nicu Micleusclusanu** &lt;micnic90@gmail.com&gt; (he/him)
* [mikeal](https://github.com/mikeal) - **Mikeal Rogers** &lt;mikeal.rogers@gmail.com&gt;
* [怪物](https://github.com/monsanto) - **Christopher Monsanto** &lt;chris@monsan.to&gt;
* [MoonBall](https://github.com/MoonBall) - **陈刚** &lt;gangc.cxy@foxmail.com&gt;
* [不是别人aardvark](https://github.com/not-an-aardvark) - **Teddy Katz** &lt;teddy.katz@gmail.com&gt; (he/him)
* [othiym23](https://github.com/othiym23) - **Forest L Norvell** &lt;ogd@aoaioxxysz.net&gt; (he/him)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;
* [petkaantonov](https://github.com/petkaantonov) - **Petka Antonov** &lt;petka_antonov@hotmail.com&gt;
* [phillipj](https://github.com/phillipj) - **Phillip Johnsen** &lt;johphi@gmail.com&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [pmq20](https://github.com/pmq20) - **Minqi Pan** &lt;pmq2001@gmail.com&gt;
* [princejwesley](https://github.com/princejwesley) - **Prince John Wesley** &lt;princejohnwesley@gmail.com&gt;
* [psmarshall](https://github.com/psmarshall) - **Peter Marshall** &lt;petermarshall@chromium.org&gt; (he/him)
* [robertkowalski](https://github.com/robertkowalski) - **Robert Kowalski** &lt;rok@kowalski.gd&gt;
* [rmg](https://github.com/rmg) - **Ryan Graham** &lt;r.m.graham@gmail.com&gt;
* [龙卷风](https://github.com/ronkorving) - **Ron Korving** &lt;ron@ronkorving.nl&gt;
* [romankl](https://github.com/romankl) - **Roman Klauke** &lt;romaaan.git@gmail.com&gt;
* [RReverser](https://github.com/RReverser) - **Ingvar Stepanyan** &lt;me@rreverser.com&gt;
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [sebdeckers](https://github.com/sebdeckers) - **Sebastiaan Deckers** &lt;sebdeckers83@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [stefanmb](https://github.com/stefanmb) - **Stefan Budeanu** &lt;stefan@budeanu.com&gt;
* [推文](https://github.com/tellnes) - **Christian Tellnes** &lt;christian@tellnes.no&gt;
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (he/him)
* [marsonya](https://github.com/marsonya) - **Akhil Marsonya** &lt;akhil.marsonya27@gmail.com&gt; (he/him)
* [tunniclm](https://github.com/tunniclm) - **Mike Tunnicliffe** &lt;m.j.tunnicliffe@gmail.com&gt;
* [vsemozhetbyt](https://github.com/vsemozhetbyt) - **Vse Mozhet Byt** &lt;vsemozhetbyt@gmail.com&gt; (he/him)
* [vkurchatkin](https://github.com/vkurchatkin) - **Vladimir Kurchatkin** &lt;vladimir.kurchatkin@gmail.com&gt;
* [Ayase-252](https://github.com/Ayase-252) - **Qingyu Deng** &lt;i@ayase-lab.com&gt;
* [whitlockjc](https://github.com/whitlockjc) - **Jeremy Whitlock** &lt;jwhitlock@apache.org&gt;
<!--lint enable prohibited-strings-->

协作者按照 [协作者指南](./doc/guides/collaborator-guide.md) 来维持Node.js项目。

### 三角龙座

* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja Durgad** &lt;Pooja.D.P@ibm.com&gt;
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `74F12602B6F1C4E913FAA37AD3A89613643B6201`
* **Rod Vagg** &lt;rod@vagg.org&gt; `DD8F2338BAE7501E3DD5AC78C273792F7D83545D`
* **Colin Ihrig** &lt;cjihrig@gmail.com&gt; `94AE36675C464D64BAFA68DD7434390BDBE9B9C5`

### 释放密钥

Node.js 发布器的主要GPG 密钥(一些发行者用子密钥签名)：

* **Beth Griggs** &lt;bgriggs@redhat.com&gt; `4ED778F539E3634C779C87C6D7062848A1AB005C`
* **Shelley Vohr** &lt;shelley.vohr@gmail.com&gt; `B9E2F5981AA6E0CD28160D9FF13993A75599653C`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `1C050899334244A8AF75E53792EF661D867B9DFA`
* **James M Snell** &lt;jasnell@keybase.io&gt; `71DCFD284A79C3B38668286BC97EC7A07EDE3FC1`
* **Michaël Zasso** &lt;targos@protonmail.com&gt; `8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600`
* **Myles Borins** &lt;myles.borins@gmail.com&gt; `C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8`
* **Richard Lau** &lt;rlau@redhat.com&gt; `C82FA3AE1CBEDC6BE46B9360C43C45C17AB93C`
* **Ruy Adorno** &lt;ruyadorno@hotmail.com&gt; `108F52B48DB57BB0CC439B2997B01419BD92F80A`
* **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; `A48C2BE680E841632CD4E44F07496B3EB3C1762`
* **Evan Lucas** &lt;evanlucas@me.com&gt; `B9AE9905FFD7803F25714661B63B535A4C206CA9`
* **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; `77984 A986EBC2AA786BC0F66B01FB92821C587A`

导入完整的信任释放密钥(包括可能用于签署释放的子密钥)：

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

请参阅上面关于 [验证二进制](#verifying-binaries) 的章节，以了解如何使用这些密钥来验证已下载的文件。

用于签署先前发布版本的其他密钥：

* **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt; `9554F04D7259F04124DE6B476D5A82AC7E37093B`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Isaac Z. Schlueter** &lt;i@izs.me&gt; `93C7E9E91B49E432C2F75674B0A78B0A6C481CF6`
* **Italo A. Casas** &lt;me@italoacasas.com&gt; `56730D5401028683275BD23C23EFEFE93C4CFFFE`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`

## 许可协议

Node.js是在 [MIT 许可证](https://opensource.org/licenses/MIT) 下可用的。 Node.js还包括外部图书馆，这些图书馆可以使用各种许可证。  关于许可证全文，请参阅 [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE)。

[行为准则]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[为该项目做贡献]: CONTRIBUTING.md
[Node.js网站]: https://nodejs.org/
[OpenJS Foundation]: https://openjsf.org/
[战略倡议]: https://github.com/nodejs/TSC/blob/HEAD/Strategic-Initiatives.md
[A. 技术价值和优先次序]: doc/guides/technical-values.md
[工 作 组]: https://github.com/nodejs/TSC/blob/HEAD/WORKING_GROUPS.md
