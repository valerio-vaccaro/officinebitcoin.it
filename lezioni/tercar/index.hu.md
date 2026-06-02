---
layout: default
title: "A karakteres terminál"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# A karakteres terminál

## Bevezetés
A Linux, pontosabban egy GNU Linux rendszer, mivel a Linux csak az a kernel, amely inicializálja a hardvert és biztosítja a használatához szükséges primitíveket, a fájl fogalmát rengeteg tevékenységhez használja. A fájlok adatfolyamok egy merevlemezen, konfigurációk, de nem csak ezek: léteznek speciális filesystems, amelyek információs fájlokat hoznak létre, ezekkel vezérelhető a számítógépünk működése, és sok eszköz is használható fájlként, például karakteres eszközként, amely bájtsorozatokat dolgoz fel különböző módokon.

A rendszer betöltési folyamata grafikus felülettel vagy a mi esetünkben shell prompttal zárul, vagyis azzal a karakteres felülettel, amelyet az óráinkon használni fogunk.

Az interfész ismerete lehetővé teszi, hogy a legtöbb Linux-eszközön sok műveletet elvégezzünk; a kurzusunkban a `bash`-t (bourne again shell) vesszük alapul, amely a Linux legelterjedtebb shellje. Login után a számítógépünk home könyvtárában találjuk magunkat, vagyis `\home\pippo` alatt, feltételezve, hogy a felhasználónevünk pippo, vagy `\root` alatt, ha a superuser fiókkal léptünk be (vagyis rootként).

SOHA NE HASZNÁLD a root fiókot úgy, ahogyan más operációs rendszerekben szokás.

A könyvtárak közötti mozgáshoz használhatod a `cd` (change directory) parancsot, emlékezve arra, hogy elfogad abszolút útvonalakat, amelyek `/` jellel kezdődnek, valamint relatív útvonalakat is az aktuális könyvtárból (amelyet `.` jelöl, vagy jelölés nélkül értendő), illetve más könyvtárakból, például home-ból (`~`). Ha listát szeretnél kapni a mappában lévő összes fájlról, használhatod az `ls` (list) parancsot, esetleg az ll argumentummal, vagyis `ls -ll`.

## Néhány hasznos parancs

Néhány hasznos parancs:

- `echo` kiírja a képernyőre az argumentumként átadott karakterlánc tartalmát,
- `man` megnyitja egy adott parancs kézikönyvét,
- `mc` konzolos fájlkezelő,
- `nano` minimális szövegszerkesztő,
- `rm` eltávolít egy fájlt,
- `mkdir` létrehoz egy könyvtárat,
- `rmdir` eltávolít egy könyvtárat (amelynek üresnek kell lennie),
- `touch` létrehoz egy üres fájlt vagy módosítja egy meglévő fájl dátumát,
- `cat` kiírja a képernyőre egy szövegfájl tartalmát,
- `ncdu` lehetővé teszi a filesystem böngészését a fájlok és könyvtárak mérete szerint rendezve,
- `wget` lehetővé teszi egy fájl letöltését a webről,
- `dd` információ átvitelét teszi lehetővé fájlok, eszközök, ... között
- `tail` kiírja a képernyőre egy fájl utolsó sorait (hasznos logokhoz a `-f` (follow) opcióval)
- `chmod` megváltoztatja egy fájl tulajdonságait (például a `+x` argumentum lehetővé teszi egy fájl végrehajtását)

Az aktuális mappában lévő végrehajtható fájlok a `./` előtaggal futtathatók, vagyis jelezzük, hogy az útvonal az aktuális könyvtárra vonatkozik.

## Input/output átirányítás
Az input és output átirányítása a `<` és `>` szimbólumokkal végezhető.

Egy fájlba íráshoz végrehajthatjuk

```
echo "pippo" > pippo.txt
```

Ez létrehoz egy pippo.txt nevű fájlt pippo tartalommal; ha ezután beírjuk

```
echo "pluto" > pippo.txt
```

a fájl tartalma pluto-ra cserélődik. Ha meg szeretnénk tartani az előző tartalmat, és az új tartalmat a végéhez szeretnénk hozzáfűzni, akkor `>>`-t kell használnunk `>` helyett.

A `<` szimbólum hasonlóan működik az inputoknál.

## Pipe
A pipe `|` lehetővé teszi, hogy egy program outputját egy másik program inputjával összekapcsoljuk.

```
cowsay "good evening" | lolcat
```

A cowsay outputja a lolcat parancs inputjaként kerül átadásra.

## Változók
A változók olyan nevek, amelyeket memóriahelyeknek adunk; ezek karakterláncokat, számokat és egyebeket tartalmazhatnak.

Egy változó beállításához a `=` parancsot használjuk; a használatához egyszerűen a `$` karaktert tesszük elé. Megállapodás szerint a változókat nagybetűvel írjuk.

```
VARIABLE="pippo"
echo $VARIABLE > pippo.txt
VARIABLE="pluto"
echo $VARIABLE >> pippo.txt
```

Létrehoz egy fájlt ezzel a tartalommal

```
pippo
pluto
```

Egy programot is elindíthatsz, és az outputját elmentheted egy változóba

```
VARIABLE=$(ls)
```

Az ls parancs outputja a VARIABLE nevű változóba kerül mentésre.

## Scripts
A scripts parancsok sorozatai, amelyek egymás után hajtódnak végre.

Az első parancs az interpreter, amelyet a parancs indítására használunk, általában `#!/bin/sh`, vagyis a `/bin/sh` futtatható fájl a `#!` előtaggal.

Futtatás előtt végrehajtási jogosultságra van szükségük a `chmod +x filename` paranccsal.

## Ismétlések
Ez az óra ismétlődő, és minden héten megismételjük. Alább a már megtartott ismétlések listája található.

| Dátum       | Jegyzetek                                      |
|-------------|------------------------------------------------|
| 240122-2230 | Első óra                                       |
| 240129-2230 | Bash script                                    |
| 240205-2230 | Bash script                                    |
