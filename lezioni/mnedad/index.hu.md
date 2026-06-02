---
layout: default
title: "Mnemonics & Dice: tanuld meg létrehozni a mnemonikodat"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Mnemonics & Dice: tanuld meg létrehozni a mnemonikodat

## Bevezetés
A mnemonika saját entrópiaforrással történő létrehozása csökkenti egy Bitcoin wallet támadási felületét; ugyanakkor néhány tényezőt figyelembe kell venni:

- a folyamatnak a lehető legegyszerűbbnek és leggyorsabbnak kell lennie, sallangok és felesleges ismétlések nélkül,
- az entrópiát nem szabad szükségtelen eszközökre másolni, és a számítások vagy feldolgozások szükségességét a minimumon kell tartani,
- a szoftverek/szkriptek/programok használatát kerülni kell, kivéve, ha pontos kódellenőrzést és az összes függőség ellenőrzését elvégezted,
- különböző setupok kissé eltérő folyamatokat igényelhetnek.

## A szavak létrehozása
Az első lépés a mnemonika 12 vagy 24 szavának kiszámítása; 12 szó általában bőven elegendő egy Bitcoin wallet biztonságához.

A szavak létrehozásához használhatod a [TRGM](https://github.com/valerio-vaccaro/TRMG) által leírt módszert, 3 dobókockával: ezek közül 1 nyolcoldalú, 2 pedig tizenhatoldalú. MINDEN kockadobás EGY ÉS CSAK EGY szónak felel meg; ennek megtalálásához egyszerűen végig kell görgetni a webhely táblázatát, és megkeresni a dobásokhoz tartozó kockaeredmények megfelelését (az első kocka MINDIG a 8 oldalú). A szó oszlopa tartalmazza a keresett szót.

Az ajánlás az, hogy hozd létre mind a 12 vagy 24 szót, és szükség esetén javítsd az utolsót, vagy mindenképpen használd a kockákat az utolsó szóhoz tartozó entrópia létrehozására.

## A checksum kiszámítása
Az utolsó szót nem teljesen mi döntjük el, mert tartalmaz egy ellenőrző részt; vagyis nem választhatjuk meg teljesen az azt alkotó mind a 11 entrópiabitet. Ehelyett 12 szavas mnemonika esetén az első 7-et, 24 szavas mnemonika esetén pedig az első 3-at választhatjuk meg.

Tegyük fel, hogy az utolsó szavunk BACON, amely az 1, 9 és 11 dobásoknak felel meg (ne feledd, hogy az első kocka MINDIG a 8 oldalú). A táblázat a Group 12 és Group 24 értékeket is tartalmazza, amelyek lehetővé teszik a szavak csoportosítását úgy, hogy csak az első két dobás entrópiáját (group 12), illetve csak az első dobást (group 24) vesszük figyelembe.

Tegyük fel, hogy 12 szavas mnemonikát szeretnénk létrehozni; ez azt jelenti, hogy a checksum a 16 lehetséges szó egyike lesz, amelyeknek ugyanaz a group 12 értékük, mint a bacon szónak, azaz 0001000. A lehetséges szavak:

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

Hogyan találjuk meg a különböző lehetőségek közül az egyetlen helyes szót? Ez a setupodtól függ; nézzünk néhány példát:

- bruteforce, vagyis mindegyiket sorban kipróbálni, amíg meg nem találod a helyeset (24 szavas mnemonikáknál nagyon fáradságos); ezt a módszert kell használni Ledgerrel vagy Electrummal (ügyelve arra, hogy a BIP39 opció ki legyen választva),
- kiszámítani az összes lehetséges szót az első 11 vagy 23 szóval, és megkeresni azt az egyet, amely ebbe a halmazba esik; ez a módszer használható Jade-del és más olyan hardware walletokkal, amelyek képesek kiszámítani egy mnemonika összes lehetséges utolsó szavát,
- beírni a teljes mnemonikát, és hagyni, hogy a hardware wallet kijavítsa helyettünk, ahogyan például a Specter-DIY nagyon elegánsan teszi.

## Backup (egy másik lecke témája)
Alapvető fontosságú a jó backup irányelv, ezért:
- több backup,
- több adathordozón és
- lehetőség szerint titkosítva vagy felosztva (de tudni kell jól megcsinálni).

## Bibliográfia

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Ismétlések
Ez a lecke ismétlődő, és minden hónapban meg lesz ismételve. Alább található a már megtartott ismétlések listája.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   |
