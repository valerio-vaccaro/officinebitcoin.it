---
layout: default
name: "Bitcoin kezdőcsomag"
description: "Egyszerűen bevezethető kezdőcsomag a Bitcoin helyes használatához. Tanuld meg, hogyan tölts le és telepíts mobil walletet, hogyan állíts be POS-t fizetési kérésekhez, és hogyan ismerd meg a wallet haladó beállításait."
title: "Kezdeti fogalomtár"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Fordítások

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

Ez egy jó módja annak, hogy a lehető leghelyesebben kezdd el használni a Bitcoint. Az alábbiakban egy nagyon karcsú, könnyen megvalósítható *starter kit* javaslat következik, amelyet önállóan is beállíthatsz.

Akár kíváncsi felhasználó vagy, akár olyan szakember, aki Bitcoint szeretne elfogadni fizetési módként, akár tapasztalt felhasználó, aki barátoknak és családtagoknak keres megoldást, ez az útmutató segít:
- letölteni és telepíteni egy mobil walletet a Bitcoin minden szintű használatához (onchain hosszú távú tárolásra; vagy Liquid és Lightning azonnali fizetésekhez);
- beállítani egy POS-t, amely euróban megadott árakból fizetési kéréseket hoz létre;
- megismerni a wallet haladó beállításait. Ezt a részt a végére tettük, hogy az első lépéseket egyszerűbbé tegyük, de mindig nézd meg, mert fontos.

Először tisztázzuk, mit értünk azon, hogy a Bitcoint *helyes módon* használjuk.

# Kezdeti fogalomtár
- `Not your keys, not your coins`
  Ha először találkozol Bitcoinnal, a `Not your keys, not your coins` mondat új lehet, és elsőre csak a szó szerinti fordítása érthető. A Bitcoin az aszimmetrikus kriptográfia elvén működik, nyilvános és privát kulcspárok alapján. Csak a privát kulcsok **kizárólagos** birtoklásával és saját kezelésével mondhatod, hogy irányítod a Bitcoinjaidat.
  
  Ezért csak te ismerheted a privát kulcsokat, azt a titkot, amellyel birtokolhatod és később elköltheted az ezekhez a kulcsokhoz tartozó bitcoint. A `Not your keys, not your coins` a világ bitcoinerei számára szinte _mantra_, és számodra is az lesz.

- `Recovery phrase`
  Rövid története során a Bitcoin protokoll úgy fejlődött, hogy egyszerűbbé tegye a titkok, vagyis a privát kulcsok kezelését. Ma ezek 12 vagy 24 angol szó sorozataként jelennek meg, így könnyebb leírni és ellenőrizni őket. Ezek a szavak jelentik a legfontosabb titkot. Papírra kell írni és nagyon biztonságos helyen, például széfben kell tartani. Soha nem szabad lefotózni, számítógépre másolni vagy másokkal megosztani.

- `Wallet`
  A wallet az az eszköz, amellyel láthatod az egyenlegedet, illetve Bitcoint fogadhatsz vagy költhetsz. Ebben az útmutatóban egyet letöltünk a telefonodra. A telefonos wallet neve `hot wallet`, mert mindig internethez kapcsolódó eszközön fut. Kezdésnek ez teljesen megfelelő; tanulással később más módszereket is megismersz a wallet használatának finomítására.

- `Non Custodial`
  Alapvetően fontos, hogy Bitcoint `non-custodial` walletekkel kezdj használni, vagyis olyanokkal, amelyek **teljes ellenőrzést adnak a privát kulcsok felett**. Mindig légy óvatos azokkal, akik más, úgynevezett custodial eszközök használatára ösztönöznek. A custodial walletek olyan eszközök, amelyek kulcsai nem a tieid. Nem az a kérdés, **hogy**, hanem **mikor** akadályoznak meg végleg abban, hogy hozzáférj a pénzedhez.

# Blockstream App (ex Green Wallet)
A starter kithez a Blockstream Appot töltjük le, egy `open source` walletet, amelynek kódját ellenőrizheted. Az alkalmazásnak hosszú fejlesztési múltja és megfelelő története van; a wallet korábban megbízhatónak bizonyult.

---
⚠️ Az alábbi utasítások az Android app letöltésére és telepítésére vonatkoznak. iOS esetén a hivatalos áruházat kell használnod.

---

## 🌍 Fordítások

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

Nyisd meg a https://github.com/Blockstream/green_android linket, amely a fejlesztő hivatalos Github tárolója.

![img](assets/01.webp)

Az oldal közepén, jobb oldalon válaszd a *Releases* résznél a `Latest` elemet, hogy a legfrissebb verziót töltsd le.

Egy oldalra jutsz, amely a legújabb release-t mutatja; e tutorial írásakor, 2025 decemberében ez az 5.1.4. Ugyanezen az oldalon válaszd ki, mit tölthetsz le:

![img](assets/02.webp)

Töltsd le a `.apk` fájlt a Play Store használata nélkül, és telepítsd az Android telefonodra.

![img](assets/03.webp)

---
⚠️ A telefonod külön engedélyeket kérhet nem tanúsított forrásból származó appok letöltéséhez. Add meg ezeket az engedélyeket a folytatáshoz.

---
Amikor az Android a Blockstream App telepítését kéri, kattints az `Install` gombra.

![img](assets/04.webp)

A telepítés végén válaszd az `Open` lehetőséget.

![img](assets/05.webp)

Megnyílik a Blockstream App; a wallet használatának megkezdéséhez válaszd a `Get Started` lehetőséget.

![img](assets/07.webp)

A Blockstream megkérdezi, részt vennél-e adatgyűjtésben az app fejlesztésének segítésére. Utasítsd el a meghívást.

![img](assets/08.webp)

# Az első walleted
Elkezdheted létrehozni az első walletedet. Kattints a `Set Up Mobile Wallet` gombra.

![img](assets/09.webp)

Elindul a wallet létrehozási folyamata.

![img](assets/10.webp)

Néhány másodperc alatt befejeződik. A wallet készen áll; a használathoz kattints a `Continue` gombra.

![img](assets/11.webp)

A wallet a `Home` nevű képernyőn nyílik meg. Egyelőre nézd meg, de azonnal figyelj az alsó `Security` menüre.

# A te kulcsaid, a te érméid

![img](assets/12.webp)

Ebben a menüben a wallet biztonsági mentésére kérnek. Ez nem más, mint annak a 12 szónak a megjelenítése, amelyre a jövőbeli visszaállításhoz szükséged lesz. Ez a 12 szó maga a walleted: **győződj meg róla, hogy biztonságos környezetben vagy, távol kíváncsi szemektől, és legyen nálad jegyzetfüzet vagy papír a szavak leírásához, mielőtt biztonságos helyre teszed őket** (például széfbe). Kattints a `Back Up Now` gombra, és nézd meg a 12 szót.

**Írd le a szavak pontos sorrendjét is: 1, 2, 3 stb.; a jobb későbbi olvashatóságért írd nagybetűkkel, de ne feledd, hogy ha később kézzel kell beírnod őket, kisbetűket kell használnod**.

![img](assets/13.webp)

Miután leírtad és biztonságos helyre tetted a szavakat, folytasd a starter kitet. Minden további beállítás az útmutató végén található.

# TRANSACT menü
A wallet használata nagyon egyszerű:
- menj a `Transact` menübe
- két fő parancs van: `Send` és `Receive` (**hagyd figyelmen kívül a `Buy` elemet**).

![img](assets/17.webp)

Ha már lesznek tranzakcióid, azok a parancsok alatti részen jelennek meg. Mivel még nincs pénzed, első fogadáshoz válaszd a `Receive` lehetőséget.

Több *Assets* jelenik meg, de csak a Bitcoinra figyelj. Választhatsz Bitcoin onchain (narancssárga ikon) és Liquid (kék ikon) között; utóbbi azonnali fizetéseket tesz lehetővé, a Lightning Networkhöz hasonlóan, de egy később bemutatott mechanizmussal.

Kezdésként válaszd a Bitcoin Onchain lehetőséget, a narancssárga ikont.

![img](assets/18.webp)

Megjelenik egy QR-kód, amely az egyik Bitcoin címedet jelöli; alul `bc1q` előtaggal és további karakterekkel is látod. Megmutathatod a QR-kódot annak, aki fizetni szeretne neked, hogy megkapd az első összegeket, ésszerűen kis Bitcoin-részeket, más néven `Satoshi`-kat.

![img](assets/19.webp)

Ha visszalépsz és a Liquidet választod, a menü ⚡️**Lightning Ready** jelzést ad. Tudnod kell, hogy egy `SWAP` szolgáltatással a Blockstream App szinte azonnali fizetések fogadását, Lightning Network fizetési kérések kiállítását vagy LN számlák fizetését teszi lehetővé, ugyanazon wallet Liquid számlájára történő befizetéssel/kifizetéssel.

![img](assets/20.webp)

A választás után megnyíló menüben válaszd ki, hogyan szeretnél pénzt fogadni: Liquid vagy Lightning. Liquid esetén a Bitcoin Onchainnél látotthoz hasonló QR-kód jelenik meg, egy `lq1q` előtagú címmel.

Lightning választásakor meg kell adnod a fogadni kívánt összeget, majd a `Confirm` gombra kell kattintanod.

![img](assets/21.webp)

A Blockstream App megmutatja az LN számlát jelölő QR-kódot, amely bármely Lightning Network wallettel kifizethető.

![img](assets/22.webp)

---
⚠️ A szimulációban 210 sats fogadását kértük, de a létrejött QR-kód arra figyelmeztet, hogy 160 sats érkezik. A swapoknak ugyanis költségük van, körülbelül 50 satoshis minden fogadott fizetésnél. **Ezt fontos szem előtt tartani, különösen mikrofizetések fogadásakor**. A fizető fél számára semmi sem változik: a beállításkor kért 210 satoshis összeget látja levonva.

---

# Kereskedő vagy? Használd a POS-t
Ahhoz, hogy ez az útmutató valódi **starter kit** legyen, a wallet Bitcoin bevételeit külső POS-szal kapcsolhatjuk össze.

Néhány egyszerű lépésben beállíthatod közvetlenül itt: https://btcpos.cash/.

![img](assets/23.webp)

Így Lightning fizetéseket fogadhatsz közvetlenül a Blockstream Appban létrehozott walletedre, megoszthatod a linket munkatársakkal, és ehhez csak a következő lépéseket kell követned: hozz létre egy linket, amelyet kéznél tartasz a telefon kezdőképernyőjén. A walleted `Descriptor` értékét kell kimásolnod és beillesztened a linken található nagy középső mezőbe.

# 1. Első pénzek fogadása a Liquid hálózaton
Engedélyezni kell az *Assets* megjelenítését a wallet kezdőképernyőjén. Ha most jött létre, kapnod kell egy LN számla kifizetését, vagy pénzt kell fogadnod egy Liquid címre.

Pénz fogadása után kiválaszthatod a Liquidet a `Home` menüben látható `Assets` között.

![img](assets/24.webp)

# 2. A szükséges paraméterek elérése
Most megvan, ami kell azokhoz a paraméterekhez, amelyekkel a walletet „átviheted” a POS-ba. Technikailag ez *nyilvános kulcs exportálása*, egy részlet, amelyet későbbi tanulással értesz meg. Most elég, ha a jobb felső menüt választod:

![img](assets/25.webp)

Majd a megjelenő legördülő menüben a `Watch-only` elemet.
![img](assets/26.webp)

Megjelenik az `Output Descriptors`, pontosan az a paraméter, amelyet keresünk. Másold ki a megfelelő paranccsal, és térj vissza a POS beállítási oldalára.

![img](assets/27.webp)

# 3. A POS beállítása
Illeszd be a descriptort a megfelelő mezőbe, és kattints a `GENERATE POS LINK` gombra. A rendszer egy egyedi URL-t hoz létre, amely csak rád és a walletedre érvényes.

![img](assets/28.webp)

Előbb beállíthatod a referencia pénznemet is, az `Currency` legördülő menüben USD, CHF és EUR közül választva.
![img](assets/29.webp)

# 4. Beszedés fizetési kérések létrehozásával a POS-ban
A `GENERATE POS LINK` megnyomása után az oldal mutatja az eredményt: **a link sikeresen létrejött**. Kimásolhatod, mert a link a létrehozott URL-en mindig **csak a te walletedhez** marad elérhető.

![img](assets/30.webp)

Megnyithatod a POS-t és elkezdheted használni:
![img](assets/31.webp)

Tegyük fel például, hogy 3.351 sats összegű számlát szeretnél létrehozni leírással.

![img](assets/32.webp)

A `CREATE INVOICE` gombra kattintva a POS megjeleníti a QR-kódot vagy szöveges számlát, amelyet egy ügyfélnek mutathatsz.

![img](assets/33.webp)

Amikor az ügyfél kifizette a számlát, amelyen helyesen olvassa a *description* mezőt (ebben az esetben Coppa del Nonno), a POS jelzi a beérkezett fizetést.

![img](assets/34.webp)

Ez a walletben is helyesen látható.
![img](assets/35.webp)

Most már csak meg kell jegyezned és kéznél tartanod a POS linket, hogy szükség esetén használd, akár azon a telefonon is, amelyre a walletet telepítetted.

![img](assets/36.webp)

Hozzáadás linkként/appként a kezdőképernyőhöz

![img](assets/37.webp)

# ⚠️ FONTOS MEGJEGYZÉS
Ha újraolvasod az utolsó példában éppen elvégzett számlabeszedési lépéseket, két fontos dolgot látunk:
1. az ügyfélnek 3.351 sats összegű számla jelent meg
2. a walletünk 3.293 sats összeget kapott.

Mielőtt botrányt kiáltanánk, vissza kell térni a POS kezdőképernyőjére, amely az alábbi képen látható szöveget mutatja:

![img](assets/38.webp)

A 3.351 (ügyfélnek bemutatott számla) és a 3.293 (a te bevételed) közötti különbség pontosan ebből adódik:
- 50 sats minden létrehozott számláért
- 0,25% szolgáltatási díj (8 sats = 3.351 0,25%-a)
- Összesen beérkezett: 3.293

#### Most kezded, és ez egy starter kit. Egy kis díj a kompromisszum azért, hogy a Bitcoint self-custody módon, közvetítők nélkül használd, és élvezd a lehetőségeket, beleértve a kis azonnali fizetéseket is.

#### Tanulással más eszközöket is megismersz majd, amelyek nem igényelnek más díjakat azokon túl, amelyek a tapasztalt felhasználók számára is várhatók.

---
# Egyéb beállítások

Ideje jól megismerni az első walletedet. A beállítások fontosak, mert segítenek a mindennapi használatban.

## Menü
A Blockstream App menüi alul találhatók:
- Home
- Transact
- Security
- Settings

Folytasd a wallet beállítását a `Security` menüből. A `Recovery phrase` szavainak megtekintése és leírása mellett ez a menü más fontos funkciókat is kínál.

Beállíthatod például a biometrikus belépést (ha a telefonodon be van állítva), vagy hozzáadhatsz egy hatjegyű PIN-t a wallet eléréséhez. Ezek nagyon fontosak, mert megakadályozzák, hogy idegenek hozzáférjenek és megnézzék a walletedet, ha náluk van a telefonod.

![img](assets/14.webp)

Ebben a menüben a *Logout* idejét is meghatározhatod, vagyis hogy a wallet hány perc inaktivitás után lépjen ki. Alapértelmezés szerint *5 minutes*, de igényeid szerint hosszabbra vagy rövidebbre állíthatod.
![img](assets/15.webp)
# SETTINGS menü
Nagyon fontos menü, mert a wallet összes beállítását tartalmazza. Itt például átnevezheted a walletet: a példában *Starter Kit* lett a neve. A walletek átnevezése fontos, ha ugyanazon az eszközön többet használsz.

![img](assets/39.webp)

Ha a `Denomination` almenübe lépsz, nagyon hasznos pénznemmel kapcsolatos beállításokat találsz.
![img](assets/40.webp)

A Bitcoin összegek egységeként a `satoshi/sats` használatát ajánlom. A Satoshi a BTC legkisebb egysége, a Bitcoin százmilliomod része. Emellett megjelenik az átváltáshoz használt referencia exchange választása is. Olyat használj, amely EUR összegek megjelenítését és beállítását engedi.

![img](assets/41.webp)

Végül a `Settings` menüben ellenőrizheted a Blockstream App aktuális verzióját, megnézheted, szükséges-e frissítés, és közvetlenül *in-app* támogatást kérhetsz.
![img](assets/42.webp)

# HOME menü
A Blockstream App `Home` menüje az a képernyő, ahol a wallet minden új belépéskor megnyílik. Lefelé görgetve találsz egy lehetőséget Bitcoin vásárlására integrált exchange-en keresztül. **Ne használd**.

![img](assets/16.webp)

# Wallet visszaállítása
Ha használat közben rájössz, hogy telefont kell cserélned, vagy a *Starter Kit* walletet több eszközön kell használnod, ezt a Blockstream Appal megteheted.

Ehhez meg kell tanulnod a wallet visszaállítási eljárását, amelyet alább ismertetünk, beleértve azokat a lépéseket is, ha elveszíted a hozzáférést ahhoz a telefonhoz, amelyen elkezdted használni a walletet.

A pénzed valójában nincs „az eszközön” vagy „a walletben”. A pénz a Bitcoin hálózaton van, legyen az Onchain, Lightning vagy Liquid. A wallet, pontosabban a wallet nyilvános és privát kulcsai azok az eszközök, amelyekkel hozzáférsz a használt címekhez és a kapcsolódó egyenleghez.

Ezért írtad le a 12 szót és tetted biztonságos helyre... **Ugye megtetted?** Mert ezek nélkül a szavak nélkül többé nem férsz hozzá a pénzedhez.

# a. A Blockstream App új telepítése
Először telepítsd újra a Blockstream Appot az elején bemutatott eljárással. Közben megjelenhetett új release, ezért a legfrissebbet használd.

Indítsd el a Blockstream Appot az új eszközön, kattints a `Get Started` gombra, és utasítsd el az adatgyűjtést.

# b. Visszaállítás biztonsági mentésből
A hasonlóságok az első telepítéssel itt véget érnek. Amikor megjelenik a wallet létrehozási képernyője, ne a `Set Up Mobile Wallet` lehetőséget válaszd, mint először, hanem a `Restore from backup` elemet.

![img](assets/43.webp)

Ha a Bitcoin fő hálózatát használod, vagyis azt, amely valódi pénzeket használ, a következő képernyőn válaszd a `Mainnet` lehetőséget.

![img](assets/43.webp)

Megjelenik a képernyő a `Recovery phrase` szavainak mezőivel. Írd be őket sorrendben és helyesen, majd válaszd a `Continue` gombot, hogy újra létrejöjjön a wallet az új eszközön.

![img](assets/45.webp)

A wallet visszaállítása néhány percig tarthat; várj türelmesen, amíg sikeresen befejeződik. A folyamat végén újra megtalálod a walletedet az egyenleggel és a tranzakciós előzményekkel.

![img](assets/46.webp)

---
⚠️ Az új eszközön újra létrehozott wallet 100%-ban aktív. Ez azt jelenti, hogy a költéshez szükséges privát kulcsok is benne vannak. Ezt tartsd észben, ha egy munkatársnak adnád az üzletedhez.

**Munkatársaknak inkább a POS linket használd, mert az csak a nyilvános kulccsal (a `descriptor` értékkel) készült**.

---

# Hogyan folytasd a tanulást?

![img](assets/47.webp)
![img](assets/48.webp)
