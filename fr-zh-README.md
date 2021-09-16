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

Node.js est un environnement d'exécution JavaScript open-source, multi-plate-forme. Il exécute du code JavaScript en dehors d'un navigateur. Pour plus d'informations sur l'utilisation de Node.js, voir le [site Web Node.js][]. Il exécute du code JavaScript en dehors d'un navigateur. Pour plus d'informations sur l'utilisation de Node.js, voir le [site Web Node.js][].

Le projet Node.js utilise un [modèle de gouvernance ouverte](./GOVERNANCE.md). La [Fondation OpenJS][] fournit un support pour le projet. La [Fondation OpenJS][] fournit un support pour le projet.

**Ce projet est lié par un [Code de Conduite][].**

# Table des matières

* [Soutien](#support)
* [Types de version](#release-types)
  * [Télécharger](#download)
    * [Versions actuelles et LTS](#current-and-lts-releases)
    * [Versions nocturnes](#nightly-releases)
    * [Documentation de l'API](#api-documentation)
  * [Vérification des binaires](#verifying-binaries)
* [Construire Node.js](#building-nodejs)
* [Sécurité](#security)
* [Contribuer à Node.js](#contributing-to-nodejs)
* [Membres actuels de l'équipe du projet](#current-project-team-members)
  * [TSC (comité de pilotage technique)](#tsc-technical-steering-committee)
  * [Collaborateurs](#collaborators)
  * [Touches de libération](#release-keys)
* [Licence](#license)

## Soutien

Vous cherchez de l'aide? Vous cherchez de l'aide? Consultez les instructions [pour obtenir de l'aide](.github/SUPPORT.md).

## Types de version

* **Courant**: Sous-développement actif. **Courant**: Sous-développement actif. Le code pour la version actuelle est dans la branche pour son numéro de version principale (par exemple, [v15.x](https://github.com/nodejs/node/tree/v15.x)). Node.js publie une nouvelle version majeure tous les 6 mois, ce qui permet de briser les changements. Cela se produit chaque année en avril et en octobre. Les parutions qui apparaissent chaque octobre ont une durée de vie de 8 mois. Les versions paraissant chaque avril convertissent en LTS (voir ci-dessous) chaque octobre. Node.js publie une nouvelle version majeure tous les 6 mois, ce qui permet de briser les changements. Cela se produit chaque année en avril et en octobre. Les parutions qui apparaissent chaque octobre ont une durée de vie de 8 mois. Les versions paraissant chaque avril convertissent en LTS (voir ci-dessous) chaque octobre.
* **LTS**: Les versions qui reçoivent un support à long terme, avec un accent sur la stabilité et la sécurité. Chaque version majeure au nombre pair deviendra une version LTS. Les versions de LTS reçoivent 12 mois de support _Active LTS_ et 18 mois supplémentaires de _Maintenance_. Les lignes de publication de LTS ont des noms de code classés par ordre alphabétique, en commençant par la version 4 Argon. Il n'y a aucun changement ou ajout de fonctionnalités, sauf dans certaines circonstances particulières. Chaque version majeure au nombre pair deviendra une version LTS. Les versions de LTS reçoivent 12 mois de support _Active LTS_ et 18 mois supplémentaires de _Maintenance_. Les lignes de publication de LTS ont des noms de code classés par ordre alphabétique, en commençant par la version 4 Argon. Il n'y a aucun changement ou ajout de fonctionnalités, sauf dans certaines circonstances particulières.
* **Nightly**: Code de la branche actuelle construit toutes les 24 heures quand il y a des changements. Utiliser avec précaution. Utiliser avec précaution.

Les versions actuelles et LTS suivent [Versioning sémantique](https://semver.org). Un membre de l'équipe de publication [signe](#release-keys) chaque version actuelle et LTS. Pour plus d'informations, voir la [Release README](https://github.com/nodejs/Release#readme). Un membre de l'équipe de publication [signe](#release-keys) chaque version actuelle et LTS. Pour plus d'informations, voir la [Release README](https://github.com/nodejs/Release#readme).

### Télécharger

Les binaires, les installateurs et les archives sources sont disponibles sur <https://nodejs.org/en/download/>.

#### Versions actuelles et LTS
<https://nodejs.org/download/release/>

Le répertoire [latest](https://nodejs.org/download/release/latest/) est un alias pour la dernière version actuelle. Le répertoire latest-_nom de code_ est un alias pour la dernière version d'une ligne LTS. Par exemple, le répertoire [latest-fermium](https://nodejs.org/download/release/latest-fermium/) contient la dernière version de Fermium (Node.js 14). Le répertoire latest-_nom de code_ est un alias pour la dernière version d'une ligne LTS. Par exemple, le répertoire [latest-fermium](https://nodejs.org/download/release/latest-fermium/) contient la dernière version de Fermium (Node.js 14).

#### Versions nocturnes
<https://nodejs.org/download/nightly/>

Chaque nom de répertoire et nom de fichier contient une date (en UTC) et la SHA de la livraison à la HEAD de la version.

#### Documentation de l'API

La documentation pour la dernière version actuelle est à <https://nodejs.org/api/>. La documentation spécifique à la version est disponible dans chaque répertoire de publication dans le sous-répertoire _docs_. La documentation spécifique à la version est également à <https://nodejs.org/download/docs/>. La documentation spécifique à la version est disponible dans chaque répertoire de publication dans le sous-répertoire _docs_. La documentation spécifique à la version est également à <https://nodejs.org/download/docs/>.

### Vérification des binaires

Les répertoires de téléchargement contiennent un fichier `SHASUMS256.txt` avec des sommes de contrôle SHA pour les fichiers.

Pour télécharger `SHASUMS256.txt` en utilisant `curl`:

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt
```

Pour vérifier qu'un fichier téléchargé correspond à la somme de contrôle, exécutez-la à travers `sha256sum` avec une commande telle que :

```console
$ grep node-vx.y.z.tar.gz SHASUMS256.txt | sha256sum -c -
```

Pour Current et LTS, la signature détachée GPG de `SHASUMS256.txt` est dans `SHASUMS256.txt.sig`. Vous pouvez l'utiliser avec `gpg` pour vérifier l'intégrité de `SHASUMS256.txt`. Vous devrez d'abord importer [les clés GPG des individus autorisés à créer des versions](#release-keys). Pour importer les clés : Vous pouvez l'utiliser avec `gpg` pour vérifier l'intégrité de `SHASUMS256.txt`. Vous devrez d'abord importer [les clés GPG des individus autorisés à créer des versions](#release-keys). Pour importer les clés :

```console
$ gpg --keyserver pool.sks-keyservers.net --recv-keys DDD8F2338BAE7501E3DD5AC78C273792F7D83545D
```

Voir le bas de ce README pour un script complet d'importer les clés de version actives.

Ensuite, téléchargez le `SHASUMS256.txt.sig` pour la version :

```console
$ curl -O https://nodejs.org/dist/vx.y.z/SHASUMS256.txt.sig
```

Ensuite, utilisez `gpg --verify SHASUMS256.txt.sig SHASUMS256.txt` pour vérifier la signature du fichier.

## Construire Node.js

Voir [BUILDING.md](BUILDING.md) pour des instructions sur la façon de construire Node.js à partir des sources et une liste des plates-formes supportées.

## Sécurité

Pour des informations sur les vulnérabilités de sécurité dans Node.js, voir [SECURITY.md](./SECURITY.md).

## Contribuer à Node.js

* [Contribuer au projet][]
* [Groupes de travail][]
* [Initiatives stratégiques][]
* [Valeurs techniques et priorisation][]

## Membres actuels de l'équipe du projet

Pour des informations sur la gouvernance du projet Node.js, voir [GOVERNANCE.md](./GOVERNANCE.md).

### TSC (comité de pilotage technique)

<!--lint disable prohibited-strings-->
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (elle)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (il/elle)
* [ChALkeR](https://github.com/ChALkeR) - **Сковорода Никита Андрееви<unk>** &lt;chalkerx@gmail.com&gt; (il/elle)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (il/elle)
* [codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (elle)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (il/elle)
* [Danielleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (elle)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (il/elle)
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (il/elle)
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (il/elle)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (il/elle)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (il/elle)
* [mmarchini](https://github.com/mmarchini) - **Marie Marchini** &lt;oss@mmarchini.me&gt; (elle)
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (il/elle)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [targos](https://github.com/targos) - **Michae<unk> l Zasso** &lt;targos@protonmail.com&gt; (il/elle)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [Trott](https://github.com/Trott) - **Trott riche** &lt;rtrott@gmail.com&gt; (il/lui)

### TSC emeriti

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (elle)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (il/elle)
* [Fishrock123](https://github.com/Fishrock123) - **Jérémie Senkpiel** &lt;fishrock123@rocketmail.com&gt;  (ils/ils)
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (il/elle)
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [isaacs](https://github.com/isaacs) - **Isaac Z. Schlueter** &lt;i@izs.me&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [mscdex](https://github.com/mscdex) - **Blanc Brian** &lt;mscdex@mscdex.net&gt;
* [nebrius](https://github.com/nebrius) - **Bryan Hughes** &lt;bryan@nebri.us&gt;
* [des robots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (il/elle)
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [rvagg](https://github.com/rvagg) - **Vagg de baguette** &lt;r@va.gg&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (il/elle)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (il/lui)
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;

### Collaborateurs

* [addaleax](https://github.com/addaleax) - **Anna Henningsen** &lt;anna@addaleax.net&gt; (elle)
* [aduh95](https://github.com/aduh95) - **Antoine du Hamel** &lt;duhamelantoine1995@gmail.com&gt; (he/him)
* [ak239](https://github.com/ak239) - **Aleksei Koziatinskii** &lt;ak239spb@gmail.com&gt;
* [AndreasMadsen](https://github.com/AndreasMadsen) - **Andreas Madsen** &lt;amwebdk@gmail.com&gt; (he/him)
* [antsmartian](https://github.com/antsmartian) - **Anto Aravinth** &lt;anto.aravinth.cse@gmail.com&gt; (il/elle)
* [apapirovski](https://github.com/apapirovski) - **Anatoli Papirovski** &lt;apapirovski@mac.com&gt; (he/him)
* [AshCripps](https://github.com/AshCripps) - **Ash Cripps** &lt;acripps@redhat.com&gt;
* [bcoe](https://github.com/bcoe) - **Ben Coe** &lt;bencoe@gmail.com&gt; (he/him)
* [bengl](https://github.com/bengl) - **Bryan Français** &lt;bryan@bryanenglish.com&gt; (il/elle)
* [benjamingr](https://github.com/benjamingr) - **Benjamin Gruenbaum** &lt;benjamingr@gmail.com&gt;
* [BethGriggs](https://github.com/BethGriggs) - **Beth Griggs** &lt;bgriggs@redhat.com&gt; (elle)
* [bmeck](https://github.com/bmeck) - **Bradley Farias** &lt;bradley.meck@gmail.com&gt;
* [bmeurer](https://github.com/bmeurer) - **Benedikt Meurer** &lt;benedikt.meurer@gmail.com&gt;
* [kull osseux](https://github.com/boneskull) - **Christopher Hiller** &lt;boneskull@boneskull.com&gt; (il/elle)
* [BridgeAR](https://github.com/BridgeAR) - **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; (il/elle)
* [bzoz](https://github.com/bzoz) - **Bartosz Sosnowski** &lt;bartosz@janeasystems.com&gt;
* [cclauss](https://github.com/cclauss) - **Christian Clauss** &lt;cclauss@me.com&gt; (il/elle)
* [ChALkeR](https://github.com/ChALkeR) - **Сковорода Никита Андрееви<unk>** &lt;chalkerx@gmail.com&gt; (il/elle)
* [cjihrig](https://github.com/cjihrig) - **Colin Ihrig** &lt;cjihrig@gmail.com&gt; (il/elle)
* [codebytere](https://github.com/codebytere) - **Shelley Vohr** &lt;codebytere@gmail.com&gt; (elle)
* [danbev](https://github.com/danbev) - **Daniel Bevenius** &lt;daniel.bevenius@gmail.com&gt; (il/elle)
* [Danielleadams](https://github.com/danielleadams) - **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; (elle)
* [davisjam](https://github.com/davisjam) - **Jamie Davis** &lt;davisjam@vt.edu&gt; (il/elle)
* [DerekNonGeneric](https://github.com/DerekNonGeneric) - **Derek Lewis** &lt;DerekNonGeneric@inf.is&gt; (he/him)
* [devnexen](https://github.com/devnexen) - **David Carlier** &lt;devnexen@gmail.com&gt;
* [devsnek](https://github.com/devsnek) - **Gus Caplan** &lt;me@gus.host&gt; (ils/ils)
* [dmabupt](https://github.com/dmabupt) - **Xu Meng** &lt;dmabupt@gmail.com&gt; (il/elle)
* [dnlup](https://github.com/dnlup) **Daniele Belardi** &lt;dwon.dnl@gmail.com&gt; (he/him)
* [edsadr](https://github.com/edsadr) - **Adrian Estrada** &lt;edsadr@gmail.com&gt; (il/elle)
* [eugénéo](https://github.com/eugeneo) - **Eugène Ostroukhov** &lt;eostroukhov@google.com&gt;
* [evanlucas](https://github.com/evanlucas) - **Evan Lucas** &lt;evanlucas@me.com&gt; (il/elle)
* [fhinkel](https://github.com/fhinkel) - **Franziska Hinkelmann** &lt;franziska.hinkelmann@gmail.com&gt; (she/her)
* [Fishrock123](https://github.com/Fishrock123) - **Jérémie Senkpiel** &lt;fishrock123@rocketmail.com&gt; (ils/ils)
* [Flarna](https://github.com/Flarna) - **Gerhard Sto<unk> bich** &lt;deb2001-github@yahoo.de&gt;  (ils/ils)
* [gabrielschulhof](https://github.com/gabrielschulhof) - **Gabriel Schulhof** &lt;gabrielschulhof@gmail.com&gt;
* [gdams](https://github.com/gdams) - **George Adams** &lt;george.adams@uk.ibm.com&gt; (il/elle)
* [geek](https://github.com/geek) - **Wyatt Preul** &lt;wpreul@gmail.com&gt;
* [gengjiawen](https://github.com/gengjiawen) - **Jiawen Geng** &lt;technicalcute@gmail.com&gt;
* [GeoffreyBooth](https://github.com/geoffreybooth) - **Stand Geoffrey** &lt;webmaster@geoffreybooth.com&gt; (il/elle)
* [gireeshpunathil](https://github.com/gireeshpunathil) - **Gireesh Punathil** &lt;gpunathi@in.ibm.com&gt; (il/elle)
* [guybedford](https://github.com/guybedford) - **Guy Bedford** &lt;guybedford@gmail.com&gt; (il/elle)
* [HarshithaKP](https://github.com/HarshithaKP) - **Harshitha K P** &lt;harshitha014@gmail.com&gt; (elle)
* [hashseed](https://github.com/hashseed) - **Yang Guo** &lt;yangguo@chromium.org&gt; (he/him)
* [lui-même65](https://github.com/himself65) - **Zeyu Yang** &lt;himself65@outlook.com&gt; (il/elle)
* [hiroppy](https://github.com/hiroppy) - **Yuta Hiroto** &lt;hello@hiroppy.me&gt; (he/him)
* [iansu](https://github.com/iansu) - **Ian Sutherland** &lt;ian@iansutherland.ca&gt;
* [indutny](https://github.com/indutny) - **Fedor Indutny** &lt;fedor.indutny@gmail.com&gt;
* [JacksonTian](https://github.com/JacksonTian) - **Jackson Tian** &lt;shyvo1987@gmail.com&gt;
* [jasnell](https://github.com/jasnell) - **James M Snell** &lt;jasnell@gmail.com&gt; (il/elle)
* [jdalton](https://github.com/jdalton) - **John-David Dalton** &lt;john.david.dalton@gmail.com&gt;
* [jkrems](https://github.com/jkrems) - **Jan Krems** &lt;jan.krems@gmail.com&gt; (il/elle)
* [joaocgreis](https://github.com/joaocgreis) - **João Reis** &lt;reis@janeasystems.com&gt;
* [joyeecheung](https://github.com/joyeecheung) - **Joyee Cheung** &lt;joyeec9h3@gmail.com&gt; (il/elle)
* [juanarbol](https://github.com/juanarbol) - **Juan Joseph Arboleda** &lt;soyjuanarbol@gmail.com&gt; (il/elle)
* [JungMinu](https://github.com/JungMinu) - **Minwoo Jung** &lt;nodecorelab@gmail.com&gt; (he/him)
* [lance](https://github.com/lance) - **Boule de Lance** &lt;lball@redhat.com&gt; (il/elle)
* [légendes](https://github.com/legendecas) - **Chengzhong Wu** &lt;legendecas@gmail.com&gt; (il/elle)
* [Leko](https://github.com/Leko) - **Shingo Inoue** &lt;leko.noor@gmail.com&gt; (he/him)
* [linkgoron](https://github.com/linkgoron) - **Nitzan Uziely** &lt;linkgoron@gmail.com&gt;
* [lpinca](https://github.com/lpinca) - **Luigi Pinca** &lt;luigipinca@gmail.com&gt; (il/elle)
* [lundibundi](https://github.com/lundibundi) - **Denys Otrishko** &lt;shishugi@gmail.com&gt; (he/him)
* [Lxxyx](https://github.com/Lxxyx) - **Liu de Zijian** &lt;lxxyxzj@gmail.com&gt; (il/elle)
* [mafintosh](https://github.com/mafintosh) - **Mathias Buus** &lt;mathiasbuus@gmail.com&gt; (il/elle)
* [mcollina](https://github.com/mcollina) - **Matteo Collina** &lt;matteo.collina@gmail.com&gt; (il/elle)
* [mhdawson](https://github.com/mhdawson) - **Michael Dawson** &lt;midawson@redhat.com&gt; (il/elle)
* [miladfarca](https://github.com/miladfarca) - **Milad Fa** &lt;mfarazma@redhat.com&gt; (il/elle)
* [mildsunrise](https://github.com/mildsunrise) - **Alba Mendez** &lt;me@alba.sh&gt; (elle)
* [misterdjules](https://github.com/misterdjules) - **Julien Gilli** &lt;jgilli@nodejs.org&gt;
* [mmarchini](https://github.com/mmarchini) - **Marie Marchini** &lt;oss@mmarchini.me&gt; (elle)
* [mscdex](https://github.com/mscdex) - **Blanc Brian** &lt;mscdex@mscdex.net&gt;
* [MylesBorins](https://github.com/MylesBorins) - **Myles Borins** &lt;myles.borins@gmail.com&gt; (il/elle)
* [des robots](https://github.com/ofrobots) - **Ali Ijaz Sheikh** &lt;ofrobots@google.com&gt; (il/elle)
* [oyyd](https://github.com/oyyd) - **Ouyang Yadong** &lt;oyydoibh@gmail.com&gt; (he/him)
* [panva](https://github.com/panva) - **Filip Skokan** &lt;panva.ip@gmail.com&gt;
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja D P** &lt;Pooja.D.P@ibm.com&gt; (elle)
* [puzpuzpuz](https://github.com/puzpuzpuz) - **Andrey Pechkurov** &lt;apechkurov@gmail.com&gt; (he/him)
* [Qard](https://github.com/Qard) - **Stephen Belanger** &lt;admin@stephenbelanger.com&gt; (il/lui)
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt; (il/elle)
* [refack](https://github.com/refack) - **Refael Ackermann (<unk> <unk> <unk> <unk> <unk> 文** &lt;refack@gmail.com&gt; (lui/lui/)
* [rexagod](https://github.com/rexagod) - **Pranshu Srivastava** &lt;rexagod@gmail.com&gt; (il/elle)
* [richardlau](https://github.com/richardlau) - **Richard Lau** &lt;rlau@redhat.com&gt;
* [rickyes](https://github.com/rickyes) - **Ricky Zhou** &lt;0x19951125@gmail.com&gt; (il/lui)
* [ronag](https://github.com/ronag) - **Robert Nagy** &lt;ronagy@icloud.com&gt;
* [rubys](https://github.com/rubys) - **Sam Ruby** &lt;rubys@intertwingly.net&gt;
* [ruyadorno](https://github.com/ruyadorno) - **Ruy Adorno** &lt;ruyadorno@github.com&gt; (il/elle)
* [rvagg](https://github.com/rvagg) - **Vagg de baguette** &lt;rod@vagg.org&gt;
* [ryzokuken](https://github.com/ryzokuken) - **Ujwal Sharma** &lt;ryzokuken@disroot.org&gt; (il/elle)
* [saghul](https://github.com/saghul) - **Saúl Ibarra Corretgé** &lt;saghul@gmail.com&gt;
* [santigimeno](https://github.com/santigimeno) - **Santiago Gimeno** &lt;santiago.gimeno@gmail.com&gt;
* [seishun](https://github.com/seishun) - **Nikolai Vavilov** &lt;vvnicholas@gmail.com&gt;
* [shisama](https://github.com/shisama) - **Masashi Hirano** &lt;shisama07@gmail.com&gt; (he/him)
* [silverwind](https://github.com/silverwind) - **Roman Reiss** &lt;me@silverwind.io&gt;
* [srl295](https://github.com/srl295) - **Steven R Loomis** &lt;srloomis@us.ibm.com&gt;
* [starkwang](https://github.com/starkwang) - **Weijia Wang** &lt;starkwang@126.com&gt;
* [sxa](https://github.com/sxa) - **Stewart X Addison** &lt;sxa@redhat.com&gt; (il/elle)
* [targos](https://github.com/targos) - **Michae<unk> l Zasso** &lt;targos@protonmail.com&gt; (il/elle)
* [TimothyGu](https://github.com/TimothyGu) - **Tiancheng "Timothy" Gu** &lt;timothygu99@gmail.com&gt; (il/lui)
* [tniessen](https://github.com/tniessen) - **Tobias Nießen** &lt;tniessen@tnie.de&gt;
* [trivikr](https://github.com/trivikr) - **Trivikram Kamat** &lt;trivikr.dev@gmail.com&gt;
* [Trott](https://github.com/Trott) - **Trott riche** &lt;rtrott@gmail.com&gt; (il/lui)
* [vdeturckheim](https://github.com/vdeturckheim) - **Vladimir de Turckheim** &lt;vlad2t@hotmail.com&gt; (he/him)
* [watilde](https://github.com/watilde) - **Daijiro Wachi** &lt;daijiro.wachi@gmail.com&gt; (he/him)
* [watson](https://github.com/watson) - **Thomas Watson** &lt;w@tson.dk&gt;
* [XadillaX](https://github.com/XadillaX) - **Khaidi Chu** &lt;i@2333.moe&gt; (il/elle)
* [yashLadha](https://github.com/yashLadha) - **Yash Ladha** &lt;yash@yashladha.in&gt; (he/him)
* [yhwang](https://github.com/yhwang) - **Yihong Wang** &lt;yh.wang@ibm.com&gt;
* [yorkie](https://github.com/yorkie) - **Yorkie Liu** &lt;yorkiefixer@gmail.com&gt;
* [yosuke-furukawa](https://github.com/yosuke-furukawa) - **Yosuke Furukawa** &lt;yosuke.furukawa@gmail.com&gt;
* [ZYSzys](https://github.com/ZYSzys) - **Yongsheng Zhang** &lt;zyszys98@gmail.com&gt; (il/elle)

### Collaborateur émérite

* [andrasq](https://github.com/andrasq) - **Andras** &lt;andras@kinvey.com&gt;
* [AnnaMag](https://github.com/AnnaMag) - **Anna M. Kedzierska** &lt;anna.m.kedzierska@gmail.com&gt;
* [aqrln](https://github.com/aqrln) - **Alexey Orlenko** &lt;eaglexrlnk@gmail.com&gt; (il/elle)
* [bnoordhuis](https://github.com/bnoordhuis) - **Ben Noordhuis** &lt;info@bnoordhuis.nl&gt;
* [brendanashworth](https://github.com/brendanashworth) - **Brendan Ashworth** &lt;brendan.ashworth@me.com&gt;
* [calvinmetcalf](https://github.com/calvinmetcalf) - **Calvin Metcalf** &lt;calvin.metcalf@gmail.com&gt;
* [chrisdickinson](https://github.com/chrisdickinson) - **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt;
* [claudiorodriguez](https://github.com/claudiorodriguez) - **Claudio Rodriguez** &lt;cjrodr@yahoo.com&gt;
* [DavidCai1993](https://github.com/DavidCai1993) - **David Cai** &lt;davidcai1993@yahoo.com&gt; (il/elle)
* [digitalinfinité](https://github.com/digitalinfinity) - **Hitesh Kanwathirtha** &lt;digitalinfinity@gmail.com&gt; (il/elle)
* [eljefedelrodeodeljefe](https://github.com/eljefedelrodeodeljefe) - **Robert Jefe Lindstaedt** &lt;robert.lindstaedt@gmail.com&gt;
* [estliberitas](https://github.com/estliberitas) - **Alexander Makarenko** &lt;estliberitas@gmail.com&gt;
* [firedfox](https://github.com/firedfox) - **Daniel Wang** &lt;wangyang0123@gmail.com&gt;
* [gibfahn](https://github.com/gibfahn) - **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; (il/elle)
* [glentiki](https://github.com/glentiki) - **Glen Keane** &lt;glenkeane.94@gmail.com&gt; (il/elle)
* [iarna](https://github.com/iarna) - **Rebecca Turner** &lt;me@re-becca.org&gt;
* [imran-iq](https://github.com/imran-iq) - **Imran Iqbal** &lt;imran@imraniqbal.org&gt;
* [imyller](https://github.com/imyller) - **Ilkka Myller** &lt;ilkka.myller@nodefield.com&gt;
* [isaacs](https://github.com/isaacs) - **Isaac Z. Schlueter** &lt;i@izs.me&gt;
* [italoacasas](https://github.com/italoacasas) - **Italo A. Casas** &lt;me@italoacasas.com&gt; (il/elle)
* [jasongin](https://github.com/jasongin) - **Jason Ginchereau** &lt;jasongin@microsoft.com&gt;
* [jbergstroem](https://github.com/jbergstroem) - **Johan Bergström** &lt;bugs@bergstroem.nu&gt;
* [jhamhader](https://github.com/jhamhader) - **Yuval Brik** &lt;yuval@brik.org.il&gt;
* [joshgav](https://github.com/joshgav) - **Josh Gavant** &lt;josh.gavant@outlook.com&gt;
* [julianduque](https://github.com/julianduque) - **Julian Duque** &lt;julianduquej@gmail.com&gt; (il/elle)
* [kfarnung](https://github.com/kfarnung) - **Kyle Farnung** &lt;kfarnung@microsoft.com&gt; (il/elle)
* [kunalspathak](https://github.com/kunalspathak) - **Kunal Pathak** &lt;kunal.pathak@microsoft.com&gt;
* [lucamaraschi](https://github.com/lucamaraschi) - **Luca Maraschi** &lt;luca.maraschi@gmail.com&gt; (he/him)
* [lxe](https://github.com/lxe) - **Aleksey Smolenchuk** &lt;lxe@lxe.co&gt;
* [maclover7](https://github.com/maclover7) - **Jon Moss** &lt;me@jonathanmoss.me&gt; (il/elle)
* [matthewloring](https://github.com/matthewloring) - **Lore Matthew** &lt;mattloring@google.com&gt;
* [micnic](https://github.com/micnic) - **Nicu Micleus<unk> anu** &lt;micnic90@gmail.com&gt; (il/elle)
* [mikeal](https://github.com/mikeal) - **Mikeal Rogers** &lt;mikeal.rogers@gmail.com&gt;
* [monsanto](https://github.com/monsanto) - **Christopher Monsanto** &lt;chris@monsan.to&gt;
* [MoonBall](https://github.com/MoonBall) - **Chen Gang** &lt;gangc.cxy@foxmail.com&gt;
* [not-an-aardvark](https://github.com/not-an-aardvark) - **Teddy Katz** &lt;teddy.katz@gmail.com&gt; (il/elle)
* [Olegas](https://github.com/Olegas) - **Oleg Elifantiev** &lt;oleg@elifantiev.ru&gt;
* [orangemocha](https://github.com/orangemocha) - **Alexis Campailla** &lt;orangemocha@nodejs.org&gt;
* [othiym23](https://github.com/othiym23) - **Forrest L Norvell** &lt;ogd@aoaioxxysz.net&gt; (il/elle)
* [petkaantonov](https://github.com/petkaantonov) - **Petka Antonov** &lt;petka_antonov@hotmail.com&gt;
* [phillipj](https://github.com/phillipj) - **Phillip Johnsen** &lt;johphi@gmail.com&gt;
* [piscisaureus](https://github.com/piscisaureus) - **Bert Belder** &lt;bertbelder@gmail.com&gt;
* [pmq20](https://github.com/pmq20) - **Minqi Pan** &lt;pmq2001@gmail.com&gt;
* [princejwesley](https://github.com/princejwesley) - **Prince John Wesley** &lt;princejohnwesley@gmail.com&gt;
* [psmarshall](https://github.com/psmarshall) - **Peter Marshall** &lt;petermarshall@chromium.org&gt; (il/elle)
* [rlidwka](https://github.com/rlidwka) - **Alex Kocharin** &lt;alex@kocharin.ru&gt;
* [rmg](https://github.com/rmg) - **Ryan Graham** &lt;r.m.graham@gmail.com&gt;
* [robertkowalski](https://github.com/robertkowalski) - **Robert Kowalski** &lt;rok@kowalski.gd&gt;
* [romankl](https://github.com/romankl) - **Roman Klauke** &lt;romaaan.git@gmail.com&gt;
* [ronkorving](https://github.com/ronkorving) - **Ron Korving** &lt;ron@ronkorving.nl&gt;
* [RReverser](https://github.com/RReverser) - **Ingvar Stepanyan** &lt;me@rreverser.com&gt;
* [sam-github](https://github.com/sam-github) - **Sam Roberts** &lt;vieuxtech@gmail.com&gt;
* [sebdeckers](https://github.com/sebdeckers) - **Sebastiaan Deckers** &lt;sebdeckers83@gmail.com&gt;
* [shigeki](https://github.com/shigeki) - **Shigeki Ohtsu** &lt;ohtsu@ohtsu.org&gt; (he/him)
* [stefanmb](https://github.com/stefanmb) - **Stefan Budeanu** &lt;stefan@budeanu.com&gt;
* [tellnes](https://github.com/tellnes) - **Christian Tellnes** &lt;christian@tellnes.no&gt;
* [thefourtheye](https://github.com/thefourtheye) - **Sakthipriyan Vairamani** &lt;thechargingvolcano@gmail.com&gt; (il/elle)
* [thlorenz](https://github.com/thlorenz) - **Thorsten Lorenz** &lt;thlorenz@gmx.de&gt;
* [trevnorris](https://github.com/trevnorris) - **Trevor Norris** &lt;trev.norris@gmail.com&gt;
* [tunniclm](https://github.com/tunniclm) - **Mike Tunnicliffe** &lt;m.j.tunnicliffe@gmail.com&gt;
* [vkurchatkin](https://github.com/vkurchatkin) - **Vladimir Kurchatkin** &lt;vladimir.kurchatkin@gmail.com&gt;
* [vsemozhetbyt](https://github.com/vsemozhetbyt) - **Vse Mozhet Byt** &lt;vsemozhetbyt@gmail.com&gt; (he/him)
* [whitlockjc](https://github.com/whitlockjc) - **Jeremy Whitlock** &lt;jwhitlock@apache.org&gt;
<!--lint enable prohibited-strings-->

Les collaborateurs suivent le [Guide de Collaborateur](./doc/guides/collaborator-guide.md) pour maintenir le projet Node.js.

### Triageurs

* [Ayase-252](https://github.com/Ayase-252) - **Qingyu Deng** &lt;i@ayase-lab.com&gt;
* [marsonya](https://github.com/marsonya) - **Akhil Marsonya** &lt;akhil.marsonya27@gmail.com&gt; (he/him)
* [PoojaDurgad](https://github.com/PoojaDurgad) - **Pooja Durgad** &lt;Pooja.D.P@ibm.com&gt;
* [RaisinTen](https://github.com/RaisinTen) - **Darshan Sen** &lt;raisinten@gmail.com&gt;

### Touches de libération

Clés GPG primaires pour les Releasers Node.js (certains Releasers signent avec des clés secondaires) :

* **Beth Griggs** &lt;bgriggs@redhat.com&gt; `4ED778F539E3634C779C87C6D7062848A1AB005C`
* **Colin Ihrig** &lt;cjihrig@gmail.com&gt; `94AE36675C464D64BAFA68DD7434390BDBE9B9C5`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `74F12602B6F1C4E913FAA37AD3A89613643B6201`
* **James M Snell** &lt;jasnell@keybase.io&gt; `71DCFD284A79C3B38668286BC97EC7A07EDE3FC1`
* **Michaël Zasso** &lt;targos@protonmail.com&gt; `8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600`
* **Myles Borins** &lt;myles.borins@gmail.com&gt; `C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8`
* **Richard Lau** &lt;rlau@redhat.com&gt; `C82FA3AE1CBEDC6BE46B9360C43CEC45C17AB93C`
* **Rod Vagg** &lt;rod@vagg.org&gt; `DD8F2338BAE7501E3DD5AC78C273792F7D83545D`
* **Ruben Bridgewater** &lt;ruben@bridgewater.de&gt; `A48C2BEE680E841632CD4E44F07496B3EB3C1762`
* **Ruy Adorno** &lt;ruyadorno@hotmail.com&gt; `108F52B48DB57BB0CC439B2997B01419BD92F80A`
* **Shelley Vohr** &lt;shelley.vohr@gmail.com&gt; `B9E2F5981AA6E0CD28160D9FF13993A75599653C`

Pour importer l'ensemble des clés de version de confiance (y compris les sous-clés éventuellement utilisées pour signer les versions):

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

Voir la section ci-dessus sur [Vérifier les binaires](#verifying-binaries) pour savoir comment utiliser ces clés pour vérifier un fichier téléchargé.

Autres clés utilisées pour signer des versions précédentes :

* **Chris Dickinson** &lt;christopher.s.dickinson@gmail.com&gt; `9554F04D7259F04124DE6B476D5A82AC7E37093B`
* **Danielle Adams** &lt;adamzdanielle@gmail.com&gt; `1C050899334244A8AF75E53792EF661D867B9DFA`
* **Evan Lucas** &lt;evanlucas@me.com&gt; `B9AE9905FFD7803F25714661B63B535A4C206CA9`
* **Gibson Fahnestock** &lt;gibfahn@gmail.com&gt; `77984A986EBC2AA786BC0F66B01FBB92821C587A`
* **Isaac Z. Schlueter** &lt;i@izs.me&gt; `93C7E9E91B49E432C2F75674B0A78B0A6C481CF6`
* **Italo A. Casas** &lt;me@italoacasas.com&gt; `56730D5401028683275BD23C23EFEFE93C4CFFFE`
* **Jeremiah Senkpiel** &lt;fishrock@keybase.io&gt; `FD3A5288F042B6850C66B31F09FE44734EB7990E`
* **Julien Gilli** &lt;jgilli@fastmail.fm&gt; `114F43EE0176B71C7BC219DD50A3051F888C628D`
* **Timothy J Fontaine** &lt;tjfontaine@gmail.com&gt; `7937DFD2AB06298B2293C3187D33FF9D0246406D`

## Licence

Node.js est disponible sous la [licence MIT](https://opensource.org/licenses/MIT). Node.js inclut également des bibliothèques externes qui sont disponibles sous une variété de licences.  Voir [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE) pour le texte complet de la licence. Node.js inclut également des bibliothèques externes qui sont disponibles sous une variété de licences.  Voir [LICENSE](https://github.com/nodejs/node/blob/HEAD/LICENSE) pour le texte complet de la licence.

[Code de Conduite]: https://github.com/nodejs/admin/blob/HEAD/CODE_OF_CONDUCT.md
[Contribuer au projet]: CONTRIBUTING.md
[site Web Node.js]: https://nodejs.org/
[Fondation OpenJS]: https://openjsf.org/
[Initiatives stratégiques]: https://github.com/nodejs/TSC/blob/HEAD/Strategic-Initiatives.md
[Valeurs techniques et priorisation]: doc/guides/technical-values.md
[Groupes de travail]: https://github.com/nodejs/TSC/blob/HEAD/WORKING_GROUPS.md
