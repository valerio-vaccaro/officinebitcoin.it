---
layout: default
title: "Jade airgapped a Sparrow Wallet használatával"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade airgapped a Sparrow Wallet használatával

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

A Jade teljesen airgapped kommunikációra is használható, a firmware és a hardver sajátosságainak köszönhetően.

A beépített kamera és kijelző ugyanis pontosan azt a feladatot látja el, hogy üzeneteket fogadjon és küldjön a watch-only wallet felé, illetve onnan vissza.

Ez az útmutató bemutatja, hogyan használható a Jade airgapped módon a Sparrow Wallet használatával.

Az eljárás először a beállítást, majd a kiterjesztett nyilvános kulcs exportálását foglalja magában Jade-ről a Sparrow watch-only walletbe, végül pedig egy költési tranzakciót.

Oktatási megfontolásból úgy döntöttünk, hogy a műveletsort a Jade oldaláról indulva mutatjuk be.

## Haladó beállítás

Az eszköz airgapped használata valódi beállítást igényel, vagyis ezt a Jade inicializálásakor kell elvégezni (1), ezért az eszköznek inicializálatlan állapotban kell lennie.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Megjelenik egy figyelmeztetés, hogy ellenőrizd a beállítási útmutatót a https://blockstream.com/jade/ weboldalon.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

A Jade airgapped használatra történő konfigurálása csak az Advanced Setup kiválasztásával végezhető el.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

A Jade figyelmeztet, hogy ez a beállítás néhány haladó technikai funkciót tartalmaz. Elég a lehető legnagyobb figyelemmel eljárni, majd megnyomni a megerősítő gombot.

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

A dobókocka-entrópiával létrehozott mnemonic megadásához válaszd a Restore Wallet lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Most be kell állítani a mnemonic hosszát: 12 vagy 24 szó. A menü azt is felkínálja, hogy a wallet egy QR-kód beolvasásával legyen visszaállítva: ez a SeedQr, amelyet a külön Setup útmutató tárgyalt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Tisztán oktatási és gyorsasági okokból ez az útmutató 12 szavas mnemonic használatával mutatja be a beállítást.

A következő lépést a leírtak szerint kell követni, hogy elérhető legyen az airgapped funkció. Valóban azt kell választani, hogy a recovery phrase CompactSeedQR formátumban legyen exportálva, a Yes kiválasztásával.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

A választás után figyelmeztetést kapsz, hogy a QR-kódot a dobozban található sablonra kell felrajzolni, ahogyan az a Setupnak szentelt lecke "Extra" szakaszában látható.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Az eljárás végén ellenőrizni kell az egyezést a felrajzolt kód és az eszköz által mutatott CompactSeedQR között. Ekkor ugyanis aktiválódik a Jade beépített kamerája, amellyel be kell keretezni az imént felrajzolt SeedQR-t.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Ha a rajz megfelel annak, amit az eszköz az imént befejezett eljárásban javasolt, megjelenik egy megerősítő jelzés.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Most a Jade megmutatja az eszköz companion apphoz való csatlakoztatásának lehetőségeit: válaszd a QR lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

A következő lépés szintén választást igényel a felhasználótól: az encrypted keys mentése az eszközön, vagy betöltésük minden munkamenetben az imént felrajzolt SeedQR beolvasásával.

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

Megjegyzés:

Hasznos megérteni ezt a két hozzáférési lehetőséget:

- QR PIN Unlock: az inicializálás során a Jade az eszközön titkosítva menti a wallet adatait; ezek mindig elérhetők lesznek a Jade feloldásával a QR PIN eljáráson keresztül.
- SeedQR: a SeedQR-t minden alkalommal be kell olvastatni a Jade-del, amikor be akarod tölteni a kulcsokat az eszközre.

Oktatási megfontolásból az előző opciónál a SeedQR lett kiválasztva, ezért az eszköz stateless módon lesz használva: a Jade figyelmeztet, hogy a munkamenet ideiglenes, és a kulcsokat az eszköz kikapcsoláskor "elfelejti".

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Nyilvános kulcs exportálása

Most, hogy a Jade kifejezetten teljesen airgapped működésre van konfigurálva, áttérünk a nyilvános kulcs exportálásának kényes szakaszára.
 
Mindig a Jade-ből kiindulva, amely visszatért a kezdő menükhöz, válaszd az Options lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

Megjegyzés: az, hogy a Jade Temporary Signer módban van, az Active jelzés melletti órát ábrázoló ikonból látható.

Az Options menüben válaszd a Wallet lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Ezután válaszd az Export Xpub lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

Ezen a ponton a Jade kijelzője egy dinamikus QR-kódot mutat, amely a kiterjesztett nyilvános kulcsot képviseli. Ennek az almenünek az Options részében kiválasztható a multisig/singlesig export és a derivation path.

Ehhez az útmutatóhoz egy full segwit singlesig exportálását választottuk.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

Ebben a szakaszban lép be a képbe a Sparrow. Indítsd el a programot, és hozz létre egy új walletet a New Wallet kiválasztásával.

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Adj nevet a walletnek, majd kattints a Create Wallet gombra.

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

A következő beállítási képernyőn kattints az Airgapped Hardware Wallet lehetőségre.

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Megnyílik egy Sparrow ablak, amely a támogatott hardware walleteket mutatja. Válaszd a Jade-et.

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

Ekkor aktiválódik annak a PC-nek a kamerája, amellyel dolgozol.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Ha egynél több webkamera érhető el, válaszd ki a legjobbat abból a legördülő menüből, ahol a Default Camera látható.

Most vedd kézbe a Jade-et, amely közben továbbra is az Xpubot képviselő dinamikus QR-kódot mutatja, és helyezd a kijelzőt a PC kamerája elé úgy, hogy a QR-kód a szaggatott területen belül maradjon.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

A kamerakép alatt van egy görgetősáv, amely kékre vált.

Ez jelzi az Xpub Sparrow általi beolvasásának előrehaladását: 0-100%.

Ebben a szakaszban szükség lehet néhány finomhangolásra: a Jade kijelző fényerejének növelésére vagy csökkentésére, az elülső megvilágítás módosítására, vagy a Use HD Capture kiválasztására, illetve a felbontás csökkentésére a Sparrow legördülő menüjében.

Ne ijedj meg ezektől a részletektől: ha egyszer kialakítottad a saját munkakörnyezetedet, ezek a lépések teljes kényelemmel és könnyedséggel fognak menni. (2)

Az exportálás akkor történt meg, amikor a kameraablak bezárul, és a Sparrow Settings képernyőjére visszatérve megjelenik a watch-only wallet összes adata.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

A Sparrow felépítése miatt most alkalmazni kell a script policyt az Apply gombra kattintva.

A wallet létrehozása a wallet fájljának titkosításához használt jelszó megadásával és megerősítésével folytatódik.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

És akkor zárul le, amikor a jobb alsó görgetősáv 100%-ra kitöltötte a mezőt.

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Költési tranzakció

Ha feltételezzük, hogy a Jade a személyes hardware wallet szerepét tölti be, akkor abból kell kiindulni, hogy vannak rajta összegek, és ezeket a jövőben el kell majd költeni.

Miután a Sparrow lett kiválasztva watch-only walletként, a Jade pedig aláíró eszközként, nézzük meg, hogyan lehet ezzel a két eszközzel tranzakciót összeállítani, aláírni és továbbítani.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

A példában összesen 56,598 sats egyenleg áll rendelkezésre.

A Sparrow bal oldali menüjében válaszd a Send lehetőséget, és kezdd el felépíteni a költési tranzakciót. Miután mindent beállítottál, kattints jobb alul a Create transaction gombra.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Megjelenik egy haladó tranzakciós ablak, ahol látható, hogy a Sparrow a Jade-et ismeri fel aláíró eszközként (Signing Wallet).

Ha a beállítások megfelelőek, kattints a Finalize Transaction gombra.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Megjelenik az aláírási képernyő. Egy airgapped rendszerben a .psbt export QR-kódon keresztül történik, ezért a Sparrow-ban kattints bal alul a Show QR gombra.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Megjelenik egy ablak egy dinamikus QR-kóddal, amely a psbt-t képviseli, és amelyet ezután a Jade kamerájával kell beolvasni.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Vedd kézbe a Jade-et, és a főmenükből válaszd a Scan QR lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Keretezd be a Sparrow által generált dinamikus QR-kódot a Jade időközben aktiválódott kamerájával. A hardware wallet kijelzőjén egy kék görgetősáv jelzi a beolvasás készültségi százalékát.

Amikor a psbt importálása befejeződött, a Jade megjeleníti a tranzakció részleteit ellenőrzésre: az első képernyőn a célcímet és az összeget,

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

a második képernyőn pedig a díjakat. Ez utóbbi megerősítésével a Jade alkalmazza az aláírást.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

A Jade kijelzője automatikusan egy újabb dinamikus QR-kódot mutat: ez az aláírt tranzakció.

Ezen a képernyőn az opciók között növelhető vagy csökkenthető a sűrűség, hogy jobb legyen a kommunikáció a wallet appal.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Közben a Sparrow-t, amelyet egy dinamikus QR-kód megjelenítésénél hagytunk, át kell állítani az aláírt tranzakció fogadására és továbbítására.

Ezért a PC webkamerájának újbóli aktiválásához a Scan QR gombra kell kattintani.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Helyezd a Jade kijelzőjét a webkamera elé, és hagyd, hogy a Sparrow importálja az aláírt tranzakciót.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

A kép alatti görgetősávnak 100%-ig kell haladnia, amíg az importálás megtörténik; ezt a Sparrow a következőképpen mutatja.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Most a teljes tranzakció ismét ellenőrizhető, és ha minden rendben van, a Broadcast Transaction gombra kattintva továbbítható.

A Transactions menüben megjelenik a kimenő tranzakció.

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Megjegyzések

- (1) - Ha a Jade már inicializálva van, elég az Options menübe lépni → Settings → Factory reset
- (2) - A Jade Original kijelzője nagyon kicsi, és ahhoz, hogy a dinamikus QR-kódot be lehessen keretezni a Sparrow által mutatott szaggatott területen belül, a kijelzőt néhány centiméterre kell közel vinni. Ezért szükség lehet egy nagyon nagy felbontású, megfelelő gyújtótávolságú webkamerára, vagy olyan appokra, mint az Iriun, amelyekkel egy telefon a PC kamerájává "alakítható". A telefonoknak ugyanis közelről jobb a fókuszálási képességük.
