---
layout: default
title: "MemPush: Bitcoin-tranzakciók egyszerű küldése és kezelése a mempoolban"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# MemPush: Bitcoin-tranzakciók egyszerű küldése és kezelése a mempoolban

A MemPush (https://mempush.com/) egy innovatív platform, amely egyszerűvé, biztonságossá és hozzáférhetővé teszi a Bitcoin-tranzakciók küldését és kezelését a mempoolban. A mempool, vagyis a blockchainen megerősítésre váró Bitcoin-tranzakciók ideiglenes "tárolója", ennek a szolgáltatásnak a központi eleme, amely megszünteti a felhasználók és fejlesztők számára a technikai bonyodalmakat.

## Mi az a MemPush?

A MemPush olyan webszolgáltatás, amely lehetővé teszi raw Bitcoin transactions (hexadecimális formátumban) közvetlen küldését a mempoolba, fejlett konfigurációk vagy saját Bitcoin nodes nélkül. A Valerio Vaccaro által tervezett MemPush a Tor hálózatot is támogatja, hogy nagyobb adatvédelmet biztosítson a felhasználóknak.

![alt text](https://officinebitcoin.it/lezioni/mempush/front.png)

A GitHubon (https://github.com/valerio-vaccaro/mempush) open-source licenc alatt elérhető forráskód lehetővé teszi, hogy bárki ellenőrizze a projekt biztonságát, hozzájáruljon a fejlesztéséhez, vagy saját, személyre szabott példányt futtasson a szolgáltatásból.

## Hogyan működik a MemPush?

A MemPush felülete intuitív és könnyen használható:

1. **A webhely megnyitása**: látogass el a https://mempush.com/ címre.
2. **A raw transaction megadása**: illeszd be a Bitcoin-tranzakciót hexadecimális formátumban a kijelölt mezőbe.
3. **A tranzakció elküldése**: kattints a "Submit Raw Transaction" gombra, hogy a tranzakció Bitcoin nodes segítségével továbbításra kerüljön a mempoolba.
4. **Az állapot figyelése**: ellenőrizd a tranzakció előrehaladását egy blockchain explorerrel.
5. **Automatikus újraküldés**: a MemPush szükség esetén automatikusan újraküldi a tranzakciókat, hogy biztosítsa a mempoolban maradásukat.

![alt text](https://officinebitcoin.it/lezioni/mempush/list.png)

Nincs szükség regisztrációra, az open-source megközelítés pedig kiküszöböli a rejtett kockázatokat, így a MemPush a kevésbé tapasztalt felhasználók számára is ideális.

## Kinek szól a MemPush?

A MemPush különböző igények kielégítésére készült:
1. **Alacsony díjak**: az alacsony díjú tranzakciókat a rendszer automatikusan újraküldi, hogy forgalmi csúcsok idején ne kerüljenek ki a mempoolból.
2. **Timelocked tranzakciók**: támogatja az időbeli korlátozásokkal rendelkező tranzakciók figyelését és újraküldését, biztosítva azok hatékony kezelését.
3. **Fejlett figyelés**: a MemPush rendszeresen ellenőrzi a tranzakciók állapotát, és csak a megerősített vagy érvénytelenített tranzakciók eltávolítását teszi lehetővé (például double-spends esetén).
4. **Fokozott adatvédelem**: a Tor hálózat támogatásának köszönhetően a MemPush védi a felhasználó anonimitását a tranzakciók küldésekor.

## Technikai jellemzők

A GitHub repository (https://github.com/valerio-vaccaro/mempush) elegáns Python-megvalósítást mutat be, amely a Flask frameworkre épül, és adatbázissal van integrálva a tranzakciók kezeléséhez. A MemPush olyan szolgáltatásokra támaszkodik, mint a blockstream.info és a mempool.space a tranzakciók figyeléséhez és továbbításához, a jövőbeni tervek között pedig szerepel egy helyi Bitcoin node integrálása.

Fő erősségek:
- **Biztonság**: nem tárol érzékeny adatokat vagy privát kulcsokat, így teljes védelmet biztosít.
- **Skálázhatóság**: a Bitcoin-hálózathoz való közvetlen kapcsolódásnak köszönhetően nagy tranzakciómennyiséget támogat.
- **Open-source**: a nyilvános kód lehetővé teszi az ellenőrzést, a közösségi hozzájárulásokat és a testreszabást.

## Következtetés

A MemPush hatékony és hozzáférhető megoldás mindazok számára, akik bonyodalmak nélkül szeretnének Bitcoin-tranzakciókat küldeni és kezelni a mempoolban. Átláthatóságával, adatvédelmi támogatásával és egyszerű használatával értékes kiegészítést jelent a Bitcoin-ökoszisztémához. Látogass el a https://mempush.com/ oldalra, hogy kipróbáld, vagy nézd meg a kódot itt: https://github.com/valerio-vaccaro/mempush.
