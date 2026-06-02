---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Az Acinq Phoenix egy natív Lightning Network wallet, non-custodial, amely hatékony, BIP39-szabványú, jól kapcsolódó walletet kínál, és a teljes irányítást a felhasználóknál hagyja.

Hamarosan látni fogod, hogy a Phoenix egy LN-csatornát nyit, amelynek egyenlegéért 100%-ban te vagy felelős.
A Phoenix megfelelő használatához csak minimális odafigyelésre és a Lightning Network alapvető ismeretére van szükség. Megtanulod például ellenőrzés alatt tartani a csatornád likviditását, a saját igényeid szerint egyensúlyban tartani, és gondoskodni arról, hogy az Acinq online lásson, hogy a csatorna nyitva maradjon és az LN-infrastruktúra fennmaradjon.

# Alapműveletek
A [Phoenix apk letöltése és ellenőrzése](https://officinebitcoin.it/lezioni/verifica/index.html) után telepítheted az appot a telefonodra.

A Phoenix megnyitáskor megkérdezi, hogy új walletet szeretnél-e létrehozni, vagy egy korábbit visszaállítani. Ha ez az első tapasztalatod a Phoenixszel, válaszd a `Create new wallet` lehetőséget. Ezután üdvözlő képernyők sorozata következik, amely ott zárul, ahol megnyomod a `Get started` gombot.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Miután a Phoenix megnyílt, **az első elvégzendő művelet, mint mindig, a wallet backupja**.

A Phoenix a BIP39 szabványt használja, m/84'/0'/0' derivációs útvonallal, és 12 szó sorozatát adja, amelyet papírra kell leírni és biztonságos helyen kell tárolni.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Lépj be a menükbe, és kérd meg a Phoenixet, hogy mutassa meg a *Recovery phrase*-t a `Display seed` gombra kattintva.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Ha elkészültél, ne felejts el teljesen legörgetni a képernyő aljára, hogy megerősítsd a backup elvégzését, és többé ne lásd az értesítést és a figyelmeztetést.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

A Phoenix lényegében használatra kész. Az új walleted egyenlege nulla, és konfigurálható. Bal alsó sarokban találod a parancsot, amellyel újra beléphetsz a beállításokba, és hasznos opciókat állíthatsz be a napi használathoz.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Használat Torral
A Phoenix több verziója óta az Acinq letiltotta a beépített Tor-motort. Ha Tor-védelemmel szeretnéd használni a Phoenixet, két lépés szükséges:
- engedélyezd a Tort a Phoenix beállításaiban
- használj egy harmadik féltől származó appot, amely a wallet forgalmát az onion hálózaton keresztül irányítja.

Nyisd meg a beállításokat, válaszd a Tort, majd engedélyezd az `Enable Tor` opciót, végül irányítsd a forgalmat azon az appon keresztül, amelyet általában használsz (Orbot, Invizible Pro stb.). E harmadik féltől származó appok egyike nélkül, de a Phoenix beállításaiban engedélyezett Torral, a wallet nem fog tudni csatlakozni az internethez.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Egyéb beállítások
Több funkciót is módosíthatsz vagy beállíthatsz:
- a wallet nevét, a felül látható `Wallet` szóra kattintva;
- a referencia pénznemet a `Display` almenüből.
- állítsd be a díjakat a `Channel management` menüben; ez fontos beállítás, mert a túl alacsony díjérték veszélyeztetheti a csatorna megnyitását: alapértelmezés szerint 5,000 sats, emeld 15,000-re; a Phoenix úgyis az adott pillanatban megfelelő értéket fogja használni;
- az `Access control` almenüben állíts be minden olyan biztonsági óvintézkedést, amelyet kezelni tudsz: PIN költéshez, PIN vagy biometrikus ellenőrzés az app eléréséhez;
- állítsd be a saját `Electrum server` szerveredet az ilyen nevű menüben, figyelembe véve, hogy a Phoenix érvényes SSL-tanúsítványt igényel (például Let's Encrypt);
- engedélyezd az `Experimental features` opciót egy újrahasználható Bolt12 LN-cím igényléséhez
- kezeld az esetleges csatornazárásokat vagy több wallet létrehozását/törlését.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# LN-csatorna megnyitása ⚡️

A Phoenix főképernyőjén válaszd a `Receive` parancsot

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

A wallet két fogadási módot kínál, mindkettőt QR-kóddal: Lightning és Onchain.

## Lightning számla kifizetése

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Az LN-csatornád gyors megnyitásának egyik módja, hogy számlát hozol létre Phoenixben, és kifizeted egy másik LN-wallettel.

Az első bejövő fizetés határozza meg egy csatorna megnyitását, amelynek likviditását az imént létrehozott számla összege adja meg (az onchain csatornanyitási tranzakció díjait leszámítva).

Előfordulhat, hogy a pénz azonnal elérhető, még akkor is, ha ideiglenes várakozási értesítés jelenik meg az onchain megerősítésekről. Vagy lehet, hogy várnod kell, mielőtt használhatod.

## Onchain tranzakció
Egy LN-csatorna megnyitása mindig onchain tranzakció, 2-of-2 multisig: te és az ellenoldal (Acinq) a saját pénzeddel határozzátok meg a feltételeket.

Ha nincs lehetőséged Lightning számlát fizetni vagy fogadni, de vannak onchain forrásaid, használhatod azt az onchain címet, amelyet a Phoenix megjelenít neked.

A tranzakció után a Phoenix így néz ki:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

Az app figyelmeztet, hogy 3 blockchain megerősítést kell megvárnod, mielőtt használhatod a pénzt.

# Csatornalikviditás kezelése
Amint megkapod a 3 megerősítést, az LN-walleted készen áll a használatra.

Kezdetben az összes likviditása kimenő, és csak költeni tudsz; ezt itt láthatod: `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Bejövő likviditást úgy hozhatsz létre, hogy kifizetsz egy vagy több Lightning Network számlát.

# A wallet használata

A Phoenix wallet használata kellemes és nagyon egyszerű élmény.

Csak ezeket kell észben tartani:
1. az imént létrehozott csatorna egy smart contract közted és az Acinq között, a te pénzeddel finanszírozva;
2. a csatornaállapotok backupjának és az infrastruktúra karbantartásának nehéz munkáját az Acinq végzi, amely néhány extra sat díjat számít fel az általad végrehajtott fizetési műveletekért;
3. rendszeresen nyisd meg a walletedet, és időnként végezz műveleteket, mert ha az ellenoldal észreveszi a hiányodat és "zombie"-nak tekint, dönthet úgy, hogy lezárja a csatornát. Az Acinq azért zár csatornákat, hogy ne költsön erőforrást és időt backupok és alvó csatornák fenntartására;
4. te is dönthetsz úgy, hogy lezárod ezt a csatornát, ha már nincs szükséged a használatára.
5. csatornazárás esetén a `cooperative closure` eljárás a legjobb, mert sok problémát elkerül.

## Splicing
Külön említést érdemel az Acinq által megvalósított `Splicing` technika, amely lehetővé teszi a teljes csatornakapacitás növelését vagy csökkentését.

A Splicing érdekes: ha van egy `tot` kapacitású csatornád, bővítheted vagy csökkentheted. Úgy tűnhet, hogy ezek a műveletek mindenki saját igényeitől függnek, **de ez nem ilyen egyszerű**.

Mindig tartsd szem előtt, hogy **a Phoenix egy Lightning Network wallet**, és bár támogatja a Bitcoin Layer1-et, kis összegű Layer2 fizetésekre kellene használni.

**Valójában minden onchain műveletet az Acinq a csatornakapacitás módosításának okaként fog értelmezni**:
- `xsats` összeg fogadása Phoenixre egy onchain walletből: az Acinq bővíti a csatornát, a kapacitást `tot` értékről `tot + xsats` értékre emelve
- `ysats` összeg fizetése Phoenixből egy onchain címre: az Acinq csökkenti a csatornát, a kapacitást `tot` értékről `tot - ysats` értékre csökkentve.

A `Splicing` egy onchain tranzakció (2-of-2 multisig), amely díjakkal jár. Bár ezek alacsonyabbak, mint a csatornanyitás/-zárás költségei, ezeknek a műveleteknek a gondatlanul vagy rossz időben történő elvégzése szükségtelenül magas költségeket eredményezhet.

LN-ről Onchainre és vissza történő mozgatáshoz próbálj megfelelő `swap` eszközöket használni, és ne erre használd a Phoenix Walletet.

# Pénz visszaszerzése
Végül, de mindennél fontosabbként, itt lép be a képbe a **non-custodial** eszközök jelentősége.

Ha és amikor a csatorna lezárul, visszaszerezheted az onchain pénzedet **úgy, hogy importálod a 12 backup szót egy olyan walletbe, amely támogatja a BIP39 szabványt**.

Többek között az Electrum wallet egy olyan lehetőség, amely ezt a műveletet egyszerűvé és intuitívvá teszi.

Ha a wallet ehelyett *custodial*, és nem birtoklod a kulcsokat, problémákba ütközhetsz: a *személytelen ügyfélszolgálattal* való nehézkes kapcsolattartástól kezdve a visszaszerzéshez szükséges, terhes `kyc` folyamaton át **egészen addig, hogy lehetetlenné válik a pénzed visszaszerzése (bármekkora is a teljes összeg)**.

Megéri?

# Tanulási támogatás
Ha részt vettél a Telegram élő bemutatóján, ezt tekintheted egy újabb lépésnek a személyes szuverenitásod felé (nem csak pénzügyi értelemben).
Ha lemaradtál róla, **ne ess kétségbe**: ezek a jegyzetek pontosan a felzárkózást szolgálják, ráadásul tudnod kell, hogy az Officine-nél újra meg fogjuk tartani.

Hogy ne maradj le a következő bemutatóról, csatlakozz a [Telegram csoporthoz](https://t.me/officinebitcoin), hogy folyamatosan naprakész maradj.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Megkeresheted a hozzád legközelebbi [Satoshi Spritz](https://satoshispritz.it/) eseményt is. A Satoshi Spritz egy helyi meetup, ahol kizárólag Bitcoinról beszélgetnek, ahová elviheted a kérdéseidet, és válaszokat kaphatsz más tapasztalt bitcoinerektől. A linken megtalálod a félsziget térképét.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Végül, ha nem találsz meetupot a közeledben, kihasználhatod a [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) heti élő közvetítéseit, egy virtuális meetupot, amelyet azoknak hoztak létre, akik nem tudnak részt venni a Satoshi Spritzen, vagy hogy segítsen a kisebb meetupoknak jegyzetelni és inspirációt találni saját bemutatóikhoz.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
