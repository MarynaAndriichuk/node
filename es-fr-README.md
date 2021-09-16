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

Node.js es un entorno de ejecución de código abierto, multiplataforma y JavaScript. Ejecuta código JavaScript fuera de un navegador. Para más información sobre el uso de Node.js, vea el [sitio web de Node.js][].

El proyecto Node.js utiliza un [modelo de gobernanza abierto](./GOVERNANCE.md). La [Fundación OpenJS][] proporciona soporte para el proyecto.

**Este proyecto está vinculado por un [Código de Conducta][].**

# Tabla de contenidos

* [Soporte](#support)
* [Tipos de lanzamiento](#release-types)
  * [Descargar](#download)
    * [Versiones actuales y LTS](#current-and-lts-releases)
    * [Versiones nocturnas](#nightly-releases)
    * [Documentación de la API](#api-documentation)
  * [Verificando binarios](#verifying-binaries)
* [Construyendo Node.js](#building-nodejs)
* [Seguridad](#security)
* [Contribuir a Node.js](#contributing-to-nodejs)
* [Miembros actuales del equipo del proyecto](#current-project-team-members)
  * [TSC (Dirección Técnica)](#tsc-technical-steering-committee)
  * [Colaboradores](#collaborators)
  * [Lanzamiento de claves](#release-keys)
* [Licencia](#license)

## Soporte

¿Buscando ayuda? Echa un vistazo a las instrucciones [para obtener soporte](.github/SUPPORT.md).

## Tipos de lanzamiento

* **Actual**: En desarrollo activo. El código para la versión actual está en la rama para su número de versión mayor (por ejemplo, [v15.x](https://github.com/nodejs/node/tree/v15.x)). Node.js lanza una nueva versión principal cada 6 meses, permitiendo cambios de ruptura. Esto ocurre en abril y octubre de cada año. Los lanzamientos que aparecen cada octubre tienen una vida de apoyo de 8 meses. Lanzamientos que aparecen cada abril se convierten en LTS (ver abajo) cada octubre.
* **LTS**: Lanzamientos que reciben soporte a largo plazo, centrados en la estabilidad y la seguridad. Cada versión mayor numerada se convertirá en una versión LTS. Los lanzamientos LTS reciben 12 meses de soporte _Active LTS_ y otros 18 meses de _mantenimiento_. Las líneas de lanzamiento de LTS tienen nombres de código ordenados alfabéticamente, comenzando por v4 Argon. No hay cambios de ruptura ni adiciones de características, excepto en algunas circunstancias especiales.
* **Noche**: Código de la rama actual construido cada 24 horas cuando hay cambios. Usar con precaución.

Los lanzamientos actuales y LTS siguen [Versionado semántico](https://semver.org). Un miembro del Equipo de Lanzamiento [firma](#release-keys) cada lanzamiento Actual y LTS. Para obtener más información, consulte el [Release README](https://github.com/nodejs/Release#readme).

### Descargar

Binarios, instaladores y tarballs fuente están disponibles en <https://nodejs.org/en/download/>.

#### Versiones actuales y LTS
<https://nodejs.org/download/release/>

El directorio [último](https://nodejs.org/download/release/latest/) es un alias para la última versión actual. El directorio último-_nombre en clave_ es un alias para la última versión de una línea LTS. Por ejemplo, el directorio [latest-fermium](https://nodejs.org/download/release/latest-fermium/) contiene la última versión de Fermium (Node.js 14).

#### Versiones nocturnas
<https://nodejs.org/download/nightly/>

Cada nombre de directorio y nombre de archivo contiene una fecha (en UTC) y el commit SHA en el HEAD de la versión.

#### Documentación de la API

La documentación para la última versión actual está en <https://nodejs.org/api/>. La documentación específica de la versión está disponible en cada directorio de publicación en el subdirectorio _docs_. La documentación específica de la versión también está en <https://nodejs.org/download/docs/>.

### Verificando binarios

Los directorios de descarga contienen un archivo `SHASUMS256.txt` con sumas de verificación SHA para los archivos.

Para descargar `SHASUMS256.txt` usando `curl`:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt
```

Para comprobar que un archivo descargado coincide con la suma de comprobación, ejecutalo a través de `sha256sum` con un comando como:

```console
$ grep node-vx.y.z.tar.gz SHASUMS256.txt | sha256sum -c -
```

Para Current y LTS, la firma independiente de GPG de `SHASUMS256.txt` está en `SHASUMS256.txt.sig`. Puedes usarlo con `gpg` para verificar la integridad de `SHASUMS256.txt`. Primero tendrá que importar [las claves GPG de individuos autorizados a crear versiones](#release-keys). Para importar las claves:

```console
$ gpg --keyserver pool.sks-keyservers.net --recv-keys DD8F2338BAE7501E3DD5AC78C273792F7D83545D
```

Vea en la parte inferior de este README un script completo para importar las claves de liberación activas.

A continuación, descargue el `SHASUMS256.txt.sig` para la versión:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt.sig
```

Luego use `gpg --verify SHASUMS256.txt.sig SHASUMS256.txt` para verificar la firma del archivo.

## Construyendo Node.js

Vea [BUILDING.md](BUILDING.md) para instrucciones sobre cómo construir Node.js desde el código fuente y una lista de plataformas soportadas.

## Seguridad

Para obtener información sobre reportar vulnerabilidades de seguridad en Node.js, consulte [SECURITY.md](./SECURITY.md).

## Contribuir a Node.js

* [Contribuyendo al proyecto][]
* [Grupos de Trabajo][]
* [Iniciativas estratégicas][]
* [Valores técnicos y priorización][]

## Miembros actuales del equipo del proyecto

Para obtener información sobre la gobernanza del proyecto Node.js, consulte [GOVERNANCE.md](./GOVERNANCE.md).

### TSC (Dirección Técnica)

<!--lint disable prohibited-strings-->
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (ella)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (él/él)
* [Chaleco](https://github.com/ChALkeR) - **Сковорода Никита Андреевиichard** &lt;chalkerx@gmail.com&gt; (él/él)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (él/él)
* [codificación](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (ella/ell)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (él/él)
* [danielleadams](https://github.com/danielleadams) - **enella Adams** &lt;adamzdanielle@gmail.com&gt; (ella/ell)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gigreeshpunathil](https://github.com/gireeshpunathil) - **Punatil de Gireesh** &lt;gpunathi@in.ibm.com&gt; (él/él)
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (él/él)
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (ella/ell)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (él/él)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (él/él)
* [mmarchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (ella)
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (él/él)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [targos](https://github.com/targos) - **Michaeunque l Zasso** &lt;targos@protonmail.com&gt; (él/él)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [Trott](https://github.com/Trott) - **Trott rico** &lt;rtrott@gmail.com&gt; (él/él)

### emérito del TSC

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (she/her)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (él/él)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt;  (él/ella)
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnë** &lt;gibfahn@gmail.com&gt; (él/él)
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [imyller](https://github.com/imyller) - **Ilkka Myller** &lt;ilkka.myller@nodefield.com&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [nebrius](https://github.com/nebrius) - **Bryan Hughes** &lt;bryan@nebri.us&gt;
* [ofrobots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (él/él)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [rvagg](https://github.com/rvagg) - **Vagón de caña** &lt;r@va.gg&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (él/él)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (él/él)
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;

### Colaboradores

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (she/her)
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [ak239](https://github.com/ak239) - **Aleksei Koziatinskii** &lt;ak239spb@gmail.com&gt;
* [AndreasMadsen](https://github.com/AndreasMadsen) - **Andreas Madsen** &lt;amwebdk@gmail.com&gt; (he/him)
* [antsmartian](https://github.com/antsmartian) - **Anto Aravinth** &lt;anto.aravinth.cse@gmail.com&gt; (él/él)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [AshCripps](https://github.com/AshCripps) - **Ash Cripps** &lt;acripps@redhat.com&gt;
* [bcoe](https://github.com/bcoe) - **Ben Coe** &lt;bencoe@gmail.com&gt; (he/him)
* [bengl](https://github.com/bengl) - **Bryan English** &lt;bryan@bryanenglish.com&gt; (él/él)
* [benjamingr](https://github.com/benjamingr) - **Benjamin Gruenbaum** &lt;benjamingr@gmail.com&gt;
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (ella)
* [bmeck](https://github.com/bmeck) - **Bradley Farias** &lt;bradley.meck@gmail.com&gt;
* [bmeurer](https://github.com/bmeurer) - **Benedikt Meurer** &lt;benedikt.meurer@gmail.com&gt;
* [boneskull](https://github.com/boneskull) - **Christopher Hiller** &lt;boneskull@boneskull.com&gt; (él/él)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (él/él)
* [bzoz](https://github.com/bzoz) - **Bartosz Sosnowski** &lt;bartosz@janeasystems.com&gt;
* [cláusulas](https://github.com/cclauss) - **Claus cristiano** &lt;cclauss@me.com&gt; (él/él)
* [Chaleco](https://github.com/ChALkeR) - **Сковорода Никита Андреевиichard** &lt;chalkerx@gmail.com&gt; (él/él)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (él/él)
* [codificación](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (ella/ell)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (él/él)
* [danielleadams](https://github.com/danielleadams) - **enella Adams** &lt;adamzdanielle@gmail.com&gt; (ella/ell)
* [davisjam](https://github.com/davisjam) - **Jamie Davis** &lt;davisjam@vt.edu&gt; (él/él)
* [DerekNonGeneric](https://github.com/DerekNonGeneric) - **Derek Lewis** &lt;DerekNonGeneric@inf.is&gt; (he/him)
* [devnexen](https://github.com/devnexen) - **David Carlier** &lt;devnexen@gmail.com&gt;
* [devsnek](https://github.com/devsnek) - **Gus Caplan** &lt;me@gus.host&gt; (el/ellos)
* [dmabupt](https://github.com/dmabupt) - **Xu Meng** &lt;dmabupt@gmail.com&gt; (él/él)
* [dnlup](https://github.com/dnlup) **Daniele Belardi** &lt;dwon.dnl@gmail.com&gt; (he/him)
* [edsadr](https://github.com/edsadr) - **Adrian Estrada** &lt;edsadr@gmail.com&gt; (él/él)
* [eugeneo](https://github.com/eugeneo) - **Eugene Ostroukhov** &lt;eostroukhov@google.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (él/él)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [Fishrock123](https://github.com/Fishrock123) - **Jeremiah Senkpiel** &lt;fishrock123@rocketmail.com&gt; (él/ella)
* [Flarna](https://github.com/Flarna) - **Gerhard Stockich** &lt;deb2001-github@yahoo.de&gt;  (él)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gdams](https://github.com/gdams) - **George Adams** &lt;george.adams@uk.ibm.com&gt; (él/él)
* [geek](https://github.com/geek) - **Wyatt Preul** &lt;wpreul@gmail.com&gt;
* [gengjiawen](https://github.com/gengjiawen) - **Jiawen Geng** &lt;technicalcute@gmail.com&gt;
* [GeoffreyBooth](https://github.com/geoffreybooth) - **Cabina de Geoffrey** &lt;webmaster@geoffreybooth.com&gt; (él/él)
* [gigreeshpunathil](https://github.com/gireeshpunathil) - **Punatil de Gireesh** &lt;gpunathi@in.ibm.com&gt; (él/él)
* [guybedford](https://github.com/guybedford) - **Guy Bedford** &lt;guybedford@gmail.com&gt; (él/él)
* [HarshithaKP](https://github.com/HarshithaKP) - **Harshitha K P** &lt;harshitha014@gmail.com&gt; (ella/ell)
* [hashseed](https://github.com/hashseed) - **Yang Guo** &lt;yangguo@chromium.org&gt; (he/him)
* [él mismo 65](https://github.com/himself65) - **Zeyu Yang** &lt;himself65@outlook.com&gt; (él/él)
* [hiroppy](https://github.com/hiroppy) - **Yuta Hiroto** &lt;hello@hiroppy.me&gt; (he/him)
* [iansu](https://github.com/iansu) - **Ian Sutherland** &lt;ian@iansutherland.ca&gt;
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [JacksonTian](https://github.com/JacksonTian) - **Jackson Tian** &lt;shyvo1987@gmail.com&gt;
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (él/él)
* [jdalton](https://github.com/jdalton) - **John-David Dalton** &lt;john.david.dalton@gmail.com&gt;
* [jkrems](https://github.com/jkrems) - **Jan Krems** &lt;jan.krems@gmail.com&gt; (él/él)
* [joaocgreis](https://github.com/joaocgreis) - **João Reis** &lt;reis@janeasystems.com&gt;
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (ella/ell)
* [juanarbol](https://github.com/juanarbol) - **Juan José Arboleda** &lt;soyjuanarbol@gmail.com&gt; (él/él)
* [JungMinu](https://github.com/JungMinu) - **Minwoo Jung** &lt;nodecorelab@gmail.com&gt; (he/him)
* [lance](https://github.com/lance) - **Bala de Lanza** &lt;lball@redhat.com&gt; (él/él)
* [legendecas](https://github.com/legendecas) - **Chengzhong Wu** &lt;legendecas@gmail.com&gt; (él/él)
* [Leko](https://github.com/Leko) - **Shingo Inoue** &lt;leko.noor@gmail.com&gt; (he/him)
* [linkgoron](https://github.com/linkgoron) - **Nitzan Uziely** &lt;linkgoron@gmail.com&gt;
* [lpinca](https://github.com/lpinca) - **Luigi Pinca** &lt;luigipinca@gmail.com&gt; (él/él)
* [lundibundi](https://github.com/lundibundi) - **Denys Otrishko** &lt;shishugi@gmail.com&gt; (he/him)
* [Lxxyx](https://github.com/Lxxyx) - **Liu Zijian** &lt;lxxyxzj@gmail.com&gt; (él/él)
* [mafintosh](https://github.com/mafintosh) - **Mathias Buus** &lt;mathiasbuus@gmail.com&gt; (él/él)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (él/él)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (él/él)
* [miladfarca](https://github.com/miladfarca) - **Milad Fa** &lt;mfarazma@redhat.com&gt; (él/él)
* [levemente amanecer](https://github.com/mildsunrise) - **Alba Mendez** &lt;me@alba.sh&gt; (ella/ell)
* [misterdjules](https://github.com/misterdjules) - **Julien Gilli** &lt;jgilli@nodejs.org&gt;
* [mmarchini](https://github.com/mmarchini) - **Mary Marchini** &lt;oss@mmarchini.me&gt; (ella)
* [mscdex](https://github.com/mscdex) - **Brian White** &lt;mscdex@mscdex.net&gt;
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (él/él)
* [ofrobots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (él/él)
* [oyyd](https://github.com/oyyd) - **Ouyang Yadong** &lt;oyydoibh@gmail.com&gt; (he/him)
* [panva](https://github.com/panva) - **Filip Skokan** &lt;panva.ip@gmail.com&gt;
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja D P** &lt;Pooja.D.P@ibm.com&gt; (ella/ell)
* [puzpuzpuz](https://github.com/puzpuzpuz) - **Andrey Pechkurov** &lt;apechkurov@gmail.com&gt; (he/him)
* [Qard](https://github.com/Qard) - **Stephen Belanger** &lt;admin@stephenbelanger.com&gt; (él/él)
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt; (él/él)
* [refack](https://github.com/refack) - **Refael Ackermann (diálogo)** &lt;refack@gmail.com&gt; (él/él/producto/producto/producto)
* [rexagod](https://github.com/rexagod) - **Pranshu mañivastava** &lt;rexagod@gmail.com&gt; (él/él)
* [richardlau](https://github.com/richardlau) - **Richard Lau** &lt;rlau@redhat.com&gt;
* [rickyes](https://github.com/rickyes) - **Ricky Zhou** &lt;0x19951125@gmail.com&gt; (él/él)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [rubys](https://github.com/rubys) - **Sam Ruby** &lt;rubys@intertwingly.net&gt;
* [ruyadorno](https://github.com/ruyadorno) - **Ruy Adorno** &lt;ruyadorno@github.com&gt; (él/él)
* [rvagg](https://github.com/rvagg) - **Vagón de caña** &lt;rod@vagg.org&gt;
* [ryzokuken](https://github.com/ryzokuken) - **Ujjwal Sharma** &lt;ryzokuken@disroot.org&gt; (él/él)
* [saghul](https://github.com/saghul) - **Saúl Ibarra Corretgé** &lt;saghul@gmail.com&gt;
* [santigimeno](https://github.com/santigimeno) - **Santiago Gimeno** &lt;santiago.gimeno@gmail.com&gt;
* [seishun](https://github.com/seishun) - **Nikolai Vavilov** &lt;vvnicholas@gmail.com&gt;
* [shisama](https://github.com/shisama) - **Masashi Hirano** &lt;shisama07@gmail.com&gt; (he/him)
* [silverwind](https://github.com/silverwind) - **Roman Reiss** &lt;me@silverwind.io&gt;
* [srl295](https://github.com/srl295) - **Steven R Loomis** &lt;srloomis@us.ibm.com&gt;
* [starkwang](https://github.com/starkwang) - **Weijia Wang** &lt;starkwang@126.com&gt;
* [sxa](https://github.com/sxa) - **Stewart X Addison** &lt;sxa@redhat.com&gt; (él/él)
* [targos](https://github.com/targos) - **Michaeunque l Zasso** &lt;targos@protonmail.com&gt; (él/él)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (él/él)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [trivikr](https://github.com/trivikr) - **Kamat Trivikram** &lt;trivikr.dev@gmail.com&gt;
* [Trott](https://github.com/Trott) - **Trott rico** &lt;rtrott@gmail.com&gt; (él/él)
* [vdeturckheim](https://github.com/vdeturckheim) - **Vladimir de Turckheim** &lt;vlad2t@hotmail.com&gt; (he/him)
* [watilde](https://github.com/watilde) - **Daijiro Wachi** &lt;daijiro.wachi@gmail.com&gt; (he/him)
* [watson](https://github.com/watson) - **Thomas Watson** &lt;w@tson.dk&gt;
* [XadillaX](https://github.com/XadillaX) - **Khaidi Chu** &lt;i@2333.moe&gt; (él/él)
* [yashLadha](https://github.com/yashLadha) - **Yash Ladha** &lt;yash@yashladha.in&gt; (he/him)
* [yhwang](https://github.com/yhwang) - **Yihong Wang** &lt;yh.wang@ibm.com&gt;
* [yorkie](https://github.com/yorkie) - **Yorkie Liu** &lt;yorkiefixer@gmail.com&gt;
* [yosuke-furukawa](https://github.com/yosuke-furukawa) - **Yosuke Furukawa** &lt;yosuke.furukawa@gmail.com&gt;
* [ZYSzys](https://github.com/ZYSzys) - **Yongsheng Zhang** &lt;zyszys98@gmail.com&gt; (él/él)

### Colaborador emérito

* [andrasq](https://github.com/andrasq) - **Andras** &lt;andras@kinvey.com&gt;
* [AnnaMag](https://github.com/AnnaMag) - **Anna M. Kedzierska** &lt;anna.m.kedzierska@gmail.com&gt;
* [aqrln](https://github.com/aqrln) - **Alexey Orlenko** &lt;eaglexrlnk@gmail.com&gt; (él/él)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [brendanashworth](https://github.com/brendanashworth) - **Brendan Ashworth** &lt;brendan.ashworth@me.com&gt;
* [calvinmetcalf](https://github.com/calvinmetcalf) - **Calvin Metcalf** &lt;calvin.metcalf@gmail.com&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [claudiorodriguez](https://github.com/claudiorodriguez) - **Claudio Rodriguez** &lt;cjrodr@yahoo.com&gt;
* [DavidCai1993](https://github.com/DavidCai1993) - **David Cai** &lt;davidcai1993@yahoo.com&gt; (él/él)
* [digitalinfinidad](https://github.com/digitalinfinity) - **Kanwathirtha golpeada** &lt;digitalinfinity@gmail.com&gt; (él/él)
* [elJefedelrodeodeljefe](https://github.com/eljefedelrodeodeljefe) - **Robert Jefe Lindstaedt** &lt;robert.lindstaedt@gmail.com&gt;
* [estliberitas](https://github.com/estliberitas) - **Alexander Makarenko** &lt;estliberitas@gmail.com&gt;
* [zorro de fuego](https://github.com/firedfox) - **Daniel Wang** &lt;wangyang0123@gmail.com&gt;
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnë** &lt;gibfahn@gmail.com&gt; (él/él)
* [glentiki](https://github.com/glentiki) - **Glen Keane** &lt;glenkeane.94@gmail.com&gt; (él/él)
* [iarna](https://github.com/iarna) - **Rebecca Turner** &lt;me@re-becca.org&gt;
* [imran-iq](https://github.com/imran-iq) - **Imran Iqbal** &lt;imran@imraniqbal.org&gt;
* [Olegas](https://github.com/Olegas) - **Oleg Elifantiev** &lt;oleg@elifantiev.ru&gt;
* [lxe](https://github.com/lxe) - **Aleksey Smolenchuk** &lt;lxe@lxe.co&gt;
* [thlorenz](https://github.com/thlorenz) - **Thorsten Lorenz** &lt;thlorenz@gmx.de&gt;
* [jasongin](https://github.com/jasongin) - **Jason Ginchereau** &lt;jasongin@microsoft.com&gt;
* [jbergstroem](https://github.com/jbergstroem) - **Johan Bergström** &lt;bugs@bergstroem.nu&gt;
* [jhamhader](https://github.com/jhamhader) - **Yuval Brik** &lt;yuval@brik.org.il&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [Navegación](https://github.com/julianduque) - **Julian Duque** &lt;julianduquej@gmail.com&gt; (él/él)
* [kfarnung](https://github.com/kfarnung) - **Kyle Farnung** &lt;kfarnung@microsoft.com&gt; (él/él)
* [kunalspathak](https://github.com/kunalspathak) - **Kunal Pathak** &lt;kunal.pathak@microsoft.com&gt;
* [lucamaraschi](https://github.com/lucamaraschi) - **Luca Maraschi** &lt;luca.maraschi@gmail.com&gt; (he/him)
* [rlidwka](https://github.com/rlidwka) - **Alex Kocharin** &lt;alex@kocharin.ru&gt;
* [maclover7](https://github.com/maclover7) - **Jon Moss** &lt;me@jonathanmoss.me&gt; (él/él)
* [matthewloring](https://github.com/matthewloring) - **Matthew Loring** &lt;mattloring@google.com&gt;
* [micrófono](https://github.com/micnic) - **Nicu Micleus** &lt;micnic90@gmail.com&gt; (él/él)
* [mikeal](https://github.com/mikeal) - **Mikeal Rogers** &lt;mikeal.rogers@gmail.com&gt;
* [monsanto](https://github.com/monsanto) - **Christopher Monsanto** &lt;chris@monsan.to&gt;
* [Bola lunar](https://github.com/MoonBall) - **Colmillo chino** &lt;gangc.cxy@foxmail.com&gt;
* [no-an-aardvark](https://github.com/not-an-aardvark) - **Teddy Katz** &lt;teddy.katz@gmail.com&gt; (él/él)
* [othiym23](https://github.com/othiym23) - **Forrest L Norvell** &lt;ogd@aoaioxxysz.net&gt; (él/él)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;
* [petkaantonov](https://github.com/petkaantonov) - **Petka Antonov** &lt;petka_antonov@hotmail.com&gt;
* [Phillipj](https://github.com/phillipj) - **Phillip Johnsen** &lt;johphi@gmail.com&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [pmq20](https://github.com/pmq20) - **Minqi Pan** &lt;pmq2001@gmail.com&gt;
* [princejwesley](https://github.com/princejwesley) - **Prince John Wesley** &lt;princejohnwesley@gmail.com&gt;
* [psmarshall](https://github.com/psmarshall) - **Peter Marshall** &lt;petermarshall@chromium.org&gt; (él/él)
* [robertkowalski](https://github.com/robertkowalski) - **Robert Kowalski** &lt;rok@kowalski.gd&gt;
* [rmg](https://github.com/rmg) - **Ryan Graham** &lt;r.m.graham@gmail.com&gt;
* [ronkorving](https://github.com/ronkorving) - **Corvando Ron** &lt;ron@ronkorving.nl&gt;
* [romankl](https://github.com/romankl) - **Roman Klauke** &lt;romaaan.git@gmail.com&gt;
* [RReverser](https://github.com/RReverser) - **Ingvar Stepanyan** &lt;me@rreverser.com&gt;
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [sebdeckers](https://github.com/sebdeckers) - **Sebastiaan Deckers** &lt;sebdeckers83@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [stefanmb](https://github.com/stefanmb) - **Stefan Budeanu** &lt;stefan@budeanu.com&gt;
* [relatos](https://github.com/tellnes) - **Christian Tellnes** &lt;christian@tellnes.no&gt;
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (él/él)
* [marsonya](https://github.com/marsonya) - **Akhil Marsonya** &lt;akhil.marsonya27@gmail.com&gt; (he/him)
* [tunniclm](https://github.com/tunniclm) - **Mike Tunnicliffe** &lt;m.j.tunnicliffe@gmail.com&gt;
* [vsemozhetbyt](https://github.com/vsemozhetbyt) - **Vse Mozhet Byt** &lt;vsemozhetbyt@gmail.com&gt; (he/him)
* [vkurchatkin](https://github.com/vkurchatkin) - **Vladimir Kurchatkin** &lt;vladimir.kurchatkin@gmail.com&gt;
* [Ayase-252](https://github.com/Ayase-252) - **Qingyu Deng** &lt;i@ayase-lab.com&gt;
* [whitlockjc](https://github.com/whitlockjc) - **Jeremy Whitlock** &lt;jwhitlock@apache.org&gt;
<!--lint enable prohibited-strings-->

Los colaboradores siguen la [Guía del Colaborador](./doc/guides/collaborator-guide.md) en el mantenimiento del proyecto Node.js.

### Triagers

* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja Durgad** &lt;Pooja.D.P@ibm.com&gt;
* **Ella Adams** &lt;adamzdanielle@gmail.com&gt; `74F12602B6F1C4E913FAA37AD3A89613643B6201`
* **Rod Vagg** &lt;rod@vagg.org&gt; `DD8F2338BAE7501E3DD5AC78C273792F7D83545D`
* **Colin Ihrig** &lt;cjihrig@gmail.com&gt; `94AE36675C464D64BAFA68DD7434390BDBE9B9C5`

### Lanzamiento de claves

Claves GPG primarias para los lanzadores de Node.js (algunos lanzadores firman con subclaves):

* **Beth Griggs** &lt;bgriggs@redhat.com&gt; `4ED778F539E3634C779C87C6D7062848A1AB005C`
* **Shelley Vohr** &lt;shelley.vohr@gmail.com&gt; `B9E2F5981AA6E0CD28160D9FF13993A75599653C`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `1C050899334244A8AF75E53792EF661D867B9DFA`
* **James M Snell** &lt;jasnell@keybase.io&gt; `71DCFD284A79C3B38668286BC97EC7A07EDE3FC1`
* **Michaël Zasso** &lt;targos@protonmail.com&gt; `8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600`
* **Myles Borins** &lt;myles.borins@gmail.com&gt; `C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8`
* **Richard Lau** &lt;rlau@redhat.com&gt; `C82FA3AE1CBEDC6BE46B9360C43CEC45C17AB93C`
* **Ruy Adorno** &lt;ruyadorno@hotmail.com&gt; `108F52B48DB57BB0CC439B2997B01419BD92F80A`
* **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; `A48C2BEE680E841632CD4E44F07496B3EB3C1762`
* **Evan Lucas** &lt;evanlucas@me.com&gt; `B9AE9905FFD7803F25714661B63B535A4C206CA9`
* **Gibson Fahnä** &lt;gibfahn@gmail.com&gt; `77984A986EBC2AA786BC0F66B01FBB92821C587A`

Para importar el conjunto completo de claves de liberación de confianza (incluyendo subclaves posiblemente utilizadas para firmar lanzamientos):

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

Consulte la sección anterior en [Verificación de Binarios](#verifying-binaries) para ver cómo utilizar estas claves para verificar un archivo descargado.

Otras claves utilizadas para firmar algunas versiones anteriores:

* **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt; `9554F04D7259F04124DE6B476D5A82AC7E37093B`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Isaac Z. Schlueter** &lt;i@izs.me&gt; `93C7E9E91B49E432C2F75674B0A78B0A6C481CF6`
* **Italo A. Casas** &lt;me@italoacasas.com&gt; `56730D5401028683275BD23C23EFEFE93C4CFFFE`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`

## Licencia

Node.js está disponible bajo la [licencia MIT](https://opensource.org/licenses/MIT). Node.js también incluye bibliotecas externas que están disponibles bajo una variedad de licencias.  Consulte [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE) para ver el texto completo de la licencia.

[Código de Conducta]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Contribuyendo al proyecto]: CONTRIBUTING.md
[sitio web de Node.js]: https://nodejs.org/
[Fundación OpenJS]: https://openjsf.org/
[Iniciativas estratégicas]: https://github.com/nodejs/TSC/blob/HEAD/Strategic-Initiatives.md
[Valores técnicos y priorización]: doc/guides/technical-values.md
[Grupos de Trabajo]: https://github.com/nodejs/TSC/blob/HEAD/WORKING_GROUPS.md
