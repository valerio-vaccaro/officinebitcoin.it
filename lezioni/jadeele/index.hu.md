---
layout: default
title: "Jade az Electrum Wallet használatával"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Fordítások

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade az Electrum Wallet használatával

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Miután Jade inicializálva lett, el lehet kezdeni a használatát, ehhez pedig ki kell választani egy megjelenítő walletet.

Jade olyan eszköz, amely több különböző wallettel, illetve companion app-pal használható, ahogyan ezeket Blockstream a weboldalán nevezi.

Ebben az útmutatóban az USB-n keresztüli használat lépéseit nézzük meg Electrum Wallet mellett.

Vegyük kézbe az inicializált Jade eszközt. Bekapcsolás után így jelenik meg:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Az Unlock Jade kiválasztásakor megjelenik a menü, ahol ki kell választani, hogyan csatlakozzon az eszköz a companion app-hoz.

Electrum használatával Jade csak USB-n keresztül csatlakoztatható, ezért ezt kell választani.

Indítsd el Electrumot, amely alapértelmezés szerint az utoljára használt wallet megnyitását ajánlja fel.

Ha ez az első alkalom, hogy Jade csatlakozik Electrumhoz, válaszd a Create New Wallet lehetőséget, majd a Finish gombot.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Adj nevet a walletnek, például Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Válaszd a Standard Wallet lehetőséget

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

A keystore kiválasztásánál alapvető fontosságú a Use a hardware device kiválasztása.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum elkezdi keresni a hardware eszközt

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

Amikor az USB-t csatlakoztatod a PC-hez (az USB C oldalon már Jade-hez csatlakoztatva), a hardware wallet megjeleníti a zárolási képernyőt. Jade a setup során beállított hatjegyű PIN megadásával oldható fel


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

A hardware eszköz feloldása után Electrum felismeri Jade-et. Folytasd a Next gombra kattintva.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

Ezen a ponton Electrum kéri a script policy beállítását; válaszd a Native Segwit lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Elkezdődik a nyilvános kulcs átvitele a Jade-en lévő walletből az Electrum megjelenítő walletbe.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

A nyilvános kulcs exportálásának végén a folyamat befejeződik.

A watch-only wallet készen áll, Electrum pedig a következő képernyővel jelzi a befejezést.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

A wallet ténylegesen létrejött, és el lehet kezdeni a felfedezését: láthatók az addresses, a wallet information, és ami különösen fontos, jobb alul látható az jelzés, hogy ez Blockstream Jade-ből létrehozott wallet. A Blockstream logó melletti zöld pont azt jelzi, hogy az eszköz be van kapcsolva és megfelelően csatlakozik.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Fogadási és költési tranzakciók

Electrum Receive menüjéből generálj egy scriptPubKey-t (címet) pénzek fogadásához. Mindig kis összeggel kezdj, és végezz fogadás+költés tesztet.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

A sats beérkezése után az érkezésük ellenőrizhető a History menüben.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Miután a tranzakció megerősítést kapott, el lehet költeni ezt az UTXO-t, és be lehet fejezni a tesztet.

A költéshez Jade használata szükséges az aláíráshoz.

Menj Electrum Send menüjébe, illessz be egy scriptPubKey-t, és gondosan ellenőrizd.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Ha elkészültél, nyomd meg a Pay gombot.

Megnyílik a tranzakciós ablak, ahol fontos beállítani a megfelelő tranzakciós fees értéket. Az összes beállítás elvégzése után kattints a jobb alsó Preview gombra.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

A tranzakciós ablak néhány fontos részletet mutat, mindenekelőtt a status értékét: Unsigned.

Ebben a fázisban látható a Sign parancs is, amely Jade-del helyezi el az aláírást.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum figyelmeztet, hogy kövesd az utasításokat a hardware eszközön, amely készen áll az aláírásra.

Előbb azonban jobb ellenőrizni, mit írsz alá: az imént beállított tranzakció összes paramétere Jade-en is megjelenik, és mind ellenőrizhető.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

A folytatáshoz győződj meg róla, hogy a kurzor mindig a nyílra → van állítva, amely a következő lépésekhez vezet, és soha nem az "X"-re, amely megszakítja a műveletet.

Az ellenőrzések megjelenítése akkor ér véget, amikor Jade megmutatja a fees értékét. Ezen a ponton a megerősítés az aláírás elhelyezésével egyenértékű.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Jade egy rövid pillanatig feldolgozza az aláírást.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Közben Electrumon ellenőrizhető a tranzakció status értéke, amely Unsigned állapotról Signed állapotra változott, és most már lehetséges a tranzakció terjesztése a Broadcast gombra kattintva.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

Az így tesztelt wallet használható biztonságosan tárolandó UTXO fogadására.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
