---
layout: default
name: "A kézi Coin Control megértése"
description: "Átfogó útmutató a kézi UTXO-kiválasztáshoz. Értsd meg, miért fontos, és tanuld meg használni különböző software walletekkel (asztali és mobil)"
title: "A kézi Coin Control megértése"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# A kézi Coin Control megértése

## Bevezetés

A Bitcoin protokoll robusztusságát egyszerű alapfogalmak garantálják. Ezek közül kiemelkedik az átláthatóság: minden Bitcoin-tranzakció nyilvános, és bárki könnyen ellenőrizheti. Bár ez a tulajdonság a protokoll egyik alappillére, mert megakadályozza a csalást és biztosítja a pénzeszközök valódiságát, a bizalmasság szempontjából kihívást is jelenthet. **Elgondolkodtál már azon, hogy ennyi átláthatóság hatással lehet-e a magánszférádra?**

Érdemes. Bár non-KYC satoshik gyűjtése meglehetősen egyszerű, a magánszférád leginkább a költési szakaszban van veszélyben.

## Mi történik, amikor elköltesz egy UTXO-t
Bitcoint költeni nem pusztán érték átadása valaki másnak.

Amikor felhasználod az egyik UTXO-dat, teljesítened kell a protokoll átláthatósága által megkövetelt feltételeket, mert bizonyítanod kell az adott pénzeszközök tulajdonjogát. Ezért:
- fel kell fedned a nyilvános kulcsodat;
- digitális aláírást kell létrehoznod.

A költés pillanata tehát a legkritikusabb: **bitcoint költeni olyan cselekedet, amelyet tudatosan és a lehető legnagyobb kontroll mellett kell elvégezni**.

## Coin Control
A Bitcoin protokollban nem léteznek olyan elemek, mint a "számla" vagy a "pénzegység". Az UTXO fogalma nem ennek a leckének a fő témája, de arra biztatlak, hogy kérdezz a megbízható Satoshi Spritzeden, vagy kérj egy leckét itt az Officine Bitcoinon.
Amit tudnod kell: Bitcoin esetén amit felhalmozol, majd később elköltesz, az satoshikban mért kisebb vagy nagyobb könyvelési egység, amelyet `unspent transaction outputs`, azaz **UTXOs** képviselnek, más néven `coins`.
Amikor UTXO-kat használsz egy tranzakció létrehozásához, azok teljesen megsemmisülnek, és a helyükön új UTXO-k jönnek létre.

A software walleteket úgy fejlesztik, hogy ezt a választást automatikusan végezzék el, "véletlenszerűen" kiválasztott coins használatával, egyetlen szempont alapján: fedezzék a szükséges költési összeget.

`Coin Control`, más néven `Coin Selection`, egyes software walletek olyan funkciója, amely lehetővé teszi, hogy **manuálisan kiválaszd a tranzakció építésekor elkölteni kívánt UTXO-kat**.

Tegyük fel, hogy van egy walleted 3 UTXO-val, rendre 21,000, 42,000 és 63,000 satoshi értékben.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Ha 24,000 sats elköltésére van szükséged, és hagyod, hogy a software automatikusan válasszon, egy jó wallet dönthet úgy, hogy UTXO1 + UTXO2 kombinációját használja a 24k sats és a bányászdíjak kifizetésére, miközben visszajárót hoz létre, amely az eredeti wallet egy belső címére tér vissza.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

A tranzakció után az új helyzet a walletben, csak az UTXO-kat számolva, így foglalható össze.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

A megfelelő software-rel és tudatossággal azonban más, helyesebb döntést is hozhattál volna. Például úgy, hogy csak az UTXO2-t választod ki (42,000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Így a walleted végső UTXO-helyzete másképp nézne ki.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Miért válasszunk UTXO-kat manuálisan?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

A példánkban az egyenleg valójában ugyanaz: `108,280 sats`. 24,000 sats elköltése után coin control nélkül 2 UTXO lenne a walletben; kézi coin control mellett összesen 3.

**Miért kell mindezt megtenni?**

Több oka van, vagy lehet annak, hogy nem használtuk az `UTXO1`-et, **és ezek mind annak a gyökerénél vannak, hogy költéskor miért jó gyakorlat a kézi coin control aktiválása**.

## Adatvédelem
A fő előny, amikor kézi coin-kiválasztásról beszélünk, **a költő nagyobb adatvédelme**.

Vegyük újra a példánkat: 24,000 satoshi elköltése _coin control nélkül_. Mivel a Bitcoin blockchain nyilvános főkönyv, egy külső megfigyelő kétséget kizáróan kijelentheti, hogy az `UTXO1 of 21,000 sats` és `UTXO2 of 42,000 sats` inputs, valamint a visszajáró, `UTXO5 of 38,280 sats`, **mind ugyanahhoz a felhasználóhoz tartoznak**.

Ha ehelyett manuálisan választod ki az `UTXO2`-t, az `UTXO1` teljesen privát marad az UTXO setben, és várhat arra, hogy megfelelőbb időpontban költsék el.

Az `UTXO1` származhat KYC-forrásból, például árukért vagy szolgáltatásokért kapott fizetésből, míg a többi UTXO nem.

**Ha ez a te walleted lenne, szeretnéd, hogy egy külső megfigyelő ilyen bizonyossággal vissza tudja követni a személyazonosságodat?** A kézi UTXO-kiválasztást megvalósító walletek lehetővé teszik például **egy vagy több UTXO elkülönítését**, ezt a funkciót ilyen helyzetekben érdemes használni.

Bár úgy gondolom, hogy a KYC-pénzeket külön walletben kell tartani a non-KYC bitcointól, ha ez a te eseted, néhány címed elkülönítése alapvető segítség, amelyet úgy érhetsz el, hogy megtanulod manuálisan kiválasztani a költési inputjaidat.

## Díjmegtakarítás
A megfelelő UTXO kiválasztása egy költéshez lehetővé teszi a díjak optimalizálását. A példánkban is a software wallet két UTXO-t választott ki a költés fedezésére. Két UTXO két aláírást jelent, amelyet meg kell mutatni a hálózatnak, tehát nagyobb tranzakciós súlyt vBytes-ban.

Kézi coin control használatával kiválaszthatsz csak egyet, amely elegendő az összeg fedezésére, így díjat takarítasz meg, mert a tranzakció "súlya" csökken.

Amikor magasak a díjak, de kénytelen vagy bitcoint on-chain költeni (például Lightning Network csatorna nyitásához), a coin control használata megfelelő gazdasági ösztönzővé válik.

## Visszajárók összevonása
Amikor fizetést végzel és on-chain Bitcoint használsz, a visszajáró fogadásának lehetősége szinte mindig bizonyossággá válik. Minden visszajáró önmagában is kis adatvédelmi veszteség, mivel felfed a hálózatnak egy címedet, amely összekapcsolható az eredeti inputoddal.

Mivel a legjobb HD walletek speciális címeket generálnak a visszajáróhoz, könnyen felismerheted őket, és "elkülönítheted" a különböző tranzakciókból származó összes visszajárót; amikor ezek elérnek egy bizonyos összeget, manuálisan kiválaszthatod és konszolidálhatod őket, vagy átválthatod őket a Lightning Networkön (ez a kedvenc módszerem), hogy visszaszerezd a költés során elvesztett adatvédelmet.

## Költés cold walletből
Egy cold wallet olyan eszköz, amellyel ésszerűen jó biztonsági szintet érhetsz el, hogy bármilyen mennyiségű pénzeszközt hosszú időre félretegyél. Előfordulhatnak azonban váratlan események, amelyek miatt hozzá kell férned a megtakarításaidhoz, és fedezned kell váratlan kiadásokat.

A tanácsom: **soha ne költs közvetlenül a cold walletből, hogy elkerüld, hogy visszajárót kapj ugyanannak a walletnek a címei közé**. Tanuld meg manuálisan kiválasztani a kiadás fedezéséhez szükséges UTXO-kat, utald át őket egy hot walletbe, és onnan készítsd el a tranzakciódat. A visszajárót ezután visszaküldheted egy cold wallet címre (ha az összeg megfelelő), vagy más célra használhatod.

## Gyakorlati bemutató
E hosszú bevezető után nézzük meg, hogyan lehet a coin controlt a gyakorlatban használni különböző desktop és mobile software-ekkel. Mindig ugyanazt a HD walletet fogjuk használni, importálva mindegyik választott eszközbe, hogy megmutassuk a köztük lévő kisebb különbségeket.

## Desktop Wallets

## Sparrow
Ha Sparrow-t használsz, nyisd meg a walletedet, és válaszd ki az _UTXOs_ menüpontot a bal oldali menüben. Látni fogod a walletedhez tartozó összes UTXO listáját.

Egyszerűen kattints az egyikre, majd válaszd a _Send Selected_ lehetőséget. Sparrow a parancs mellett azt is megmutatja, összesen mennyit választottál ki költésre.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Többet is kiválaszthatsz. Használd a _CTRL_ billentyűt a listában nem egymás melletti UTXO-k kiválasztásához.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Az UTXO-k manuális kiválasztása után Sparrow grafikusan, egyértelműen megmutatja, hogyan épül fel a tranzakciód, amelyet ezután véglegesíthetsz és befejezhetsz.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### UTXO elkülönítés
Pénzeszközök elkülönítése azt jelenti, hogy "lezárod" őket a walletben, így nem használhatók tranzakciós inputként.

Sparrow lehetővé teszi ezt a funkciót, amely az _UTXOs_ menüből érhető el. Vidd az egeret a "lezárni" kívánt UTXO fölé, és kattints jobb gombbal. Az opciók között megtalálod a _Freeze_ lehetőséget. Így különíthetsz el egy UTXO-t Sparrow Walletben.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Ha a desktop walleted Electrum, manuálisan választhatsz UTXO-kat mind az _Addresses_, mind a _Coins_ menüből.
Mindkét menüben a kiválasztás úgy történik, hogy az egeret az UTXO-ra irányítod, majd jobb kattintás után kiválasztod az _Add to coin control_ lehetőséget.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Egynél több UTXO-t is kiválaszthatsz, a _CTRL_ billentyűvel, ha nem egymás mellett vannak.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum zölddel grafikusan kiemeli a kiválasztott UTXO-kat, alul pedig egy ugyanilyen színnel kiemelt sáv mutatja a coin control utáni elérhető egyenleget.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Miután az output(s) ki vannak választva, a tranzakciót a megszokott módon, a _Send_ menüből építheted fel.

### UTXO elkülönítés
Electrum ezt az opciót a _Coins_ menüben kínálja: válassz ki egy adott UTXO-t, majd jobb egérgombbal válaszd a _Freeze_ lehetőséget. Az _Addresses_ menüből "befagyaszthatsz" egy pénz nélküli címet is, vagy a "coin"-t, hogy megakadályozd a költést.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk megnyitás után a főmenüből teszi lehetővé az UTXO-k kiválasztását.
Indítsd el a Nunchukot, és kattints a _View coins_ lehetőségre.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Megnyílik egy ablak a walleted összes UTXO-jával, ahol egyet vagy többet kiválaszthatsz az egyes összegek melletti négyzet bejelölésével. A kiválasztás után folytasd a _Create transaction_ paranccsal.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Ezután megadhatod a célcímet, beállíthatod az összeget és a díjakat.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
A Blockstream App desktop, korábbi nevén Green, akkor engedi a coin-kiválasztást, miután elkezdted felépíteni a tranzakciót. Nyisd meg a walletedet, és kattints a _Send_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Illeszd be a célcímet a megfelelő mezőbe, majd válaszd a _Manual coin selection_ lehetőséget.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Megnyílik egy ablak, ahol egy vagy több UTXO-t választhatsz ki. A következő példában két coint választottunk ki. Ezután erősítsd meg a választást a _Confirm Coin Selection_ gombra kattintva.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Állítsd be az összeget és a díjakat, majd folytasd a tranzakciódat a megszokott módon.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Megjegyzés: A Green _Coins_ menüjében vannak _Lock_/_Unlock_ opciók, amelyek UTXO-k elkülönítésének lehetőségét sugallják. Ez csak az úgynevezett multisig számlákban érhető el; a funkció csak nagyon kicsi UTXO-khoz aktiválódik, a `Dust` küszöb közelében.

## Mobile Wallets

## Blue Wallet
Mobilon is választhatsz olyan walleteket, amelyek lehetővé teszik a kézi UTXO-kiválasztást. Először nézzük a Blue Walletet.

Ha ezt a software-t használod, nyisd meg a walletedet, és kattints, hogy belépj az egyik walleted parancsképernyőire. A coin control eléréséhez be kell lépned a költési szakaszba, ezért kattints a _Send_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

A következő képernyőn válaszd a jobb felső sarokban lévő három ponttal jelzett menüt. Megnyílik egy lenyíló ablak több paranccsal. Válaszd az utolsót: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

Ekkor a Blue Wallet megjeleníti az összes UTXO-dat. Az összegeken kívül grafikusan különböző színekkel is meg vannak különböztetve.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Válaszd ki az UTXO-t, majd válaszd a _Use Coin_ lehetőséget.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

A Blue Wallet visszavisz a _Send_ ablakba, hogy folytasd a tranzakció építését. Állítsd be az összeget és a díjakat, majd válaszd a _Next_ gombot.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Most a megszokott módon befejezheted a tranzakciót.

### UTXO elkülönítés
A Blue Wallet azt is lehetővé teszi, hogy UTXO-kat elkülöníts, így azok nem lesznek elérhetők költésre, ami jó funkció egy mobile wallet esetében.

Lépj be a coin controlba a fent leírt módon, majd az UTXO kiválasztása után a _Use Coin_ helyett válaszd a _Freeze_ lehetőséget.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
A Nunchuk mobilverziója is lehetővé teszi a felhasználók számára a coin control használatát. Ha ezt az appot mobilon használod, nyisd meg, és lépj a _Wallet_ menübe. Innen válaszd a _View coins_ lehetőséget.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Az UTXO-k listáját tartalmazó ablakban kattints a _Select_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Minden UTXO mellett megjelenik a kiválasztási funkció. Akárcsak a desktop verzióban, Nunchuk mobile esetén a kézi kiválasztás az összeg melletti négyzet bejelölésével történik. A képernyő mutatja a kiválasztott UTXO-k számát és a teljes elérhető összeget. Ha végeztél, a bal alsó sarokban lévő ₿ szimbólum a tranzakció építésének indítására szolgáló parancs.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Most befejezheted a tranzakciót, kiválasztva az összeget és a _Continue_ gombra kattintva.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Folytasd a megszokott módon: illessz be egy célcímet, egy leírást, és testreszabhatod a díjbeállításokat.

## Bitcoin Keeper
A Bitcoin Keeper az utolsó wallet, amelyet ebben az útmutatóban megnézünk. Nézzük meg a coin control funkcióját egy single-sig wallettel, még ha az ilyen használat nem is ennek a konkrét appnak a fő célja.

Miután beállítottad a Keepert a telefonodon, indítsd el, és nyiss meg egy walletet, amely tartalmaz néhány UTXO-t. A főképernyő közepén kattints a _View All Coins_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper áttekintést mutat az UTXO-król. A kiválasztási képernyő eléréséhez kattints a _Select To Control_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Coins kiválasztásához jelöld be őket, a megfelelő parancsra kattintva. Ha kész vagy, kattints a _Send_ gombra.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

A Bitcoin Keeper közvetlenül a _Send_ menübe visz, ahol a kiválasztott UTXO-kkal felépítheted a tranzakciót.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Az ebben az útmutatóban látott software walletek mindegyike lehet a hardware walleted watch-only felülete. Ez azt jelenti, hogy egy offline aláíró eszköz coin controlja az eddig látott lépésekkel történik.

## Általános ajánlások
A coin control nagyon hatékony gyakorlat a tranzakciós inputjaid kiválasztására. A kézi kiválasztás még hatékonyabb, ha a pénzeszközeid fogadásakor jól felcímkézted satoshijaid eredetét. Ha el szeretnéd sajátítani ezt a technikát, ajánlom ezt az oktatóanyagot:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
