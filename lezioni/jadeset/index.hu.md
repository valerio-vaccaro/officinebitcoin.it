---
layout: default
title: "Jade beállítása"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade beállítása

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

A Jade olyan csomagolásban érkezik, amelynek sértetlenségét ellenőrizni kell: nézd meg a doboz (alsó rész) és a fedél (felső rész) közé helyezett két holografikus, manipuláció elleni matricát.

A csomag egy kis felhasználói kézikönyvet, két CompactSeedQR sablont és magát a hardware walletet tartalmazza.

A Jade az alsó gomb nyomva tartásával kapcsol be, majd a 3 menüt jeleníti meg:

- Setup Jade
- Scan QR
- Options

Az Options menüben több paraméter is beállítható a személyes igények szerint, de először az inicializálást kell elvégezni.

A görgetőgombbal válaszd ki a __Setup Jade__ menüt, majd erősítsd meg az előlapi gombbal.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Megjelenik egy figyelmeztetés, hogy ellenőrizd a beállítási útmutatót a https://blockstream.com/jade/ oldalon.

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

A helyes végrehajtáshoz ajánlott a mnemonikot kockadobásokkal létrehozni, és ezt az entrópiát használni a wallet létrehozásához. Ezért válaszd az __Advanced Setup__ lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

A Jade figyelmeztet, hogy ez a beállítás néhány haladó technikai funkciót tartalmaz. Elég a maximális figyelem, majd a megerősítő gomb megnyomása.

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

A kockaentrópiával generált mnemonik beírásához válaszd a __Restore Wallet__ lehetőséget.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Most be kell állítani a mnemonik hosszát: 12 vagy 24 szó. A menü azt is felkínálja, hogy QR-kód beolvasásával állítsd vissza a walletet: ez a SeedQr, amelyet máshol tárgyalunk.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Tisztán oktatási és gyorsasági okokból ez az útmutató 12 szavas mnemonikkal mutatja be a beállítást.

Elkezdődik az első szó beírásának folyamata, és a Jade megjeleníti a billentyűzetet a megfelelő betűk beviteléhez. A görgetőgombbal állj ← → a megfelelő pozícióra.

Ebben a példában az 1. szó: "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Az első 3-4 betű beírása után a Jade szavakat választ a BIP39 szótárból, és javaslatokat kezd megjeleníteni. A görgetőgombbal lépj előre vagy hátra, amíg meg nem találod a helyes szót.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Folytasd a szavak beírását, amíg el nem érsz az utolsó szóhoz: a checksumhoz.

Ekkor a Jade két lehetőséget mutat: meglévő szó beírását, vagy egy érvényes checksum kiszámítását a saját szoftverével.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Megjegyzés:

- Ha a beállítás kockadobásokkal létrehozott 12 szavas mnemonikból indul, ajánlott az Existing lehetőséget választani, majd a szó első betűit beírni, a kockadobás által javasolt tartományból kiválasztva őket.
- Ha a beállítás ehelyett kockadobásokkal generált 24 szavas mnemonikból indul, megkérheted a Jade-et, hogy számolja ki az összes lehetséges checksumot, majd választhatsz egyet. Igaz, hogy így valamennyi entrópia elveszik, de csak az utolsó szóban. Ha úgy döntöttél, hogy a pénzedet a Jade-re bízod, ez elfogadható kompromisszum.
- Meglévő wallet visszaállítása esetén: add meg a helyes checksumot az Existing kiválasztásával.

A kockadobásokkal generált mnemonikból történő beállítás példáját folytatva az előző menüben az Existing lehetőséget választjuk, azzal a céllal, hogy beírjuk a betűket és megtaláljuk a megfelelő checksumot.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

Ekkor a Jade felajánlja a recovery phrase exportálását _CompactSeedQR_ formájában.

A _CompactSeedQR_ olyan kódolás, amely a mnemonic phrase-t QR-kóddá alakítja, amelyet a wallet Jade-en történő visszaállításához lehet beolvasni.

Ha ki szeretnéd próbálni, nézd meg az útmutató alján található részt, amely elmagyarázza, hogyan kell megcsinálni.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Ha az előző menüben a "No" lehetőséget választod, folytathatod a beállítás végéig.

Az eszköz készen áll arra, hogy a watch-only wallethez csatlakozzon.

A következő menü a csatlakozási lehetőségeket mutatja:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Válaszd az USB-t, majd erősítsd meg a megerősítő gombbal.

Ekkor a Jade kéri, hogy csatlakoztasd egy companion apphoz.

A következő példában az eszközt USB-n keresztül a Blockstream Greenhez csatlakoztatjuk; ez a wallet ugyanis lehetővé teszi a Jade firmware-frissítéseinek ellenőrzését, és az USB-n keresztül figyelt eszközzel vezetett beállítást kínál.

Nyisd meg a Greent, és ellenőrizd a hálózati és biztonsági beállításokat.

Ha van firmware-frissítés, a Green azonnal jelzi, és ajánlott elvégezni a frissítést.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

A firmware-frissítés befejezése után a Green elkezd kommunikálni a Jade-del.

Az aláíróeszköz ekkor kéri a duress PIN beállítását, amely titkosítja a privát kulcsokat a Jade-en, így azok mindenki számára hozzáférhetetlenné válnak, kivéve azt, aki rendelkezik a hatjegyű PIN-nel.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Miközben a Green a fent látható képernyővel várakozik, a Jade-en megjelenik a 6 jegyű PIN beállításának lehetősége, majd annak megerősítése a helyes újbóli beírással.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

A Jade perzisztens adatokat hoz létre úgy, hogy titkosítja őket az eszközön.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

A művelet végén, amely néhány pillanatig tarthat, a Green megnyitja a használatra kész walletet.

Ha kikapcsolod, majd újra bekapcsolod a Jade-et, az eszköz inicializáltként jelenik meg, frissített firmware-rel, és készen áll a feloldásra (Unlock Jade), hogy a companion appal használható legyen.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: CompactSeedQR létrehozása

A mnemonik beírásának végén kihagytuk a kulcsok QR-kód formátumú exportálását, hogy a beállítási szakaszra összpontosítsunk. Ez az exportálási mód később bármikor elvégezhető.

Kapcsold be a Jade-et, és az Options → Temporary Signer → Continue → 12/24 Words menüből visszatérsz a recovery phrase beviteli menüjéhez, amelynek végén megjelenik a SeedQR formátumba történő exportálás választóképernyője.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

A Yes kiválasztásakor figyelmeztetést kapsz, hogy a QR-kódot a dobozban található sablonra kell lerajzolnod.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

A folyamat azzal kezdődik, hogy áttekintést mutat arról, milyen lesz a lerajzolandó QR-kód (egyes részek adatvédelmi okokból ki vannak törölve).

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

Ezután a rács összes mezője egyenként megjelenik, A1-től C3-ig vagy E5-ig, a recovery phrase hosszától függően.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

A rács utolsó mezőjének lerajzolása után a Jade ismét megjeleníti az áttekintést az első ellenőrzéshez. Folytasd a Done megerősítésével.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Bekapcsol a Jade beépített kamerája, amellyel be kell keretezned az imént lerajzolt SeedQR-t.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Ha a rajz megfelel annak, amit a Jade az imént befejezett folyamatban javasolt, megerősítő jelzés jelenik meg.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

A Continue megerősítésére kattintva a Jade a főmenükből működő állapotban jelenik meg.

A CompactSeedQR egy eszköz a wallet Jade-en történő visszaállításához.
