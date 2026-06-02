---
layout: default
title: "Ghostinbox.it: email használata email fiók nélkül"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Ghostinbox.it: email használata email fiók nélkül

A Ghostinbox egy webes platform, amely lehetővé teszi, hogy a felhasználók ideiglenes email-címeket hozzanak létre üzenetek fogadására anélkül, hogy felfednék valódi email-címüket. A szolgáltatás ideális gyors regisztrációkhoz, fiókellenőrzésekhez, email-kézbesíthetőségi tesztekhez, illetve minden olyan helyzethez, amikor el akarod kerülni a spamet vagy védeni szeretnéd az identitásodat.

A hagyományos email-szolgáltatásokkal ellentétben a Ghostinbox nem igényel regisztrációt és nem tárol személyes adatokat, ezért kiváló választás azoknak, akik számára elsődleges a privacy. Emellett a Tor hálózat támogatása anonim hozzáférést tesz lehetővé a szolgáltatáshoz, elrejtve a felhasználó IP-címét. A projekt open-source jellege átláthatóságot biztosít, és lehetővé teszi a fejlesztők számára, hogy megvizsgálják a kódot lehetséges sérülékenységek vagy testreszabási lehetőségek után kutatva.

## Hogyan működik a Ghostinbox?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

A Ghostinbox használata rendkívül intuitív, és nem igényel technikai ismereteket:

1. **Nyisd meg a webhelyet**: Látogasd meg a https://ghostinbox.it/ címet (vagy használd Toron keresztül a nagyobb anonimitásért).
2. **Hozz létre egy ideiglenes email-címet**: Kattints a gombra egy új ideiglenes email-cím létrehozásához (például random@ghostinbox.it). A cím azonnal aktív és használatra kész.
3. **Fogadj üzeneteket**: Használd a létrehozott címet emailek fogadására, például online szolgáltatások regisztrációjához, fiókellenőrzéshez vagy teszteléshez. Az üzenetek valós időben jelennek meg a webhely bejövő üzenetei között.
4. **Figyeld az üzeneteket**: A kapott üzenetek megtekintéséhez nyisd meg az ideiglenes bejövő fiókot közvetlenül a Ghostinboxon. Nincs szükség külső email-kliensre.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

A szolgáltatást gyorsra és súrlódásmentesre tervezték: nincs szükség fiók létrehozására, a minimalista felület pedig még nem technikai felhasználók számára is gördülékennyé teszi az élményt. A Toron keresztüli hozzáférés további védelmi szintet ad azoknak, akik teljes anonimitást szeretnének fenntartani.

## Az aliastól az emailig
A szolgáltatás használatához olyan aliast kell választani, amely elég hosszú és véletlenszerű ahhoz, hogy más felhasználók ne tudják kitalálni. Ez az alias olyan lesz, mint egy jelszó az email eléréséhez, ezért nem szabad elfelejteni.

Ebből az aliasból származik egy HASH@ghostinbox.it email-cím, ahol a HASH értéke `sha256(alias)`, vagyis az alias SHA-256-tal képzett hashe; a felhasználó ezután ezt az emailt (amely a fogadási sémában látható) használhatja emailek fogadására. A fogadóoldal automatikusan frissül, és megjeleníti a kapott emaileket. A felhasználó létrehozhat email-címet anélkül, hogy belépne a szolgáltatásba, és a webhelyet csak megtekintésre használhatja.

Az emailre kattintva elolvasható annak szövege, és szükség esetén kimásolhatók a megnyitandó linkek; az email formátuma szándékosan csak szöveges, ezért nem jeleníti meg a HTML-alapú emailek grafikus elemeit.

## Kinek van szüksége a Ghostinboxra?
A Ghostinbox többféle privacy- és ideiglenes email-kezelési igényre ad választ:

1. **Spam elleni védelem**: Ideiglenes cím használatával a felhasználók elkerülhetik, hogy valódi email-címüket elárassza a spam vagy a kéretlen newsletterek.
2. **Biztonságos regisztrációk**: Tökéletes online szolgáltatásokra, fórumokra vagy olyan platformokra való regisztrációhoz, amelyek emailes ellenőrzést igényelnek, anélkül hogy a személyes email veszélybe kerülne.
3. **Kézbesíthetőségi tesztek**: Fejlesztők és marketingesek használhatják a Ghostinboxot emailküldés és -fogadás tesztelésére valódi címek bevonása nélkül.
4. **Haladó privacy**: A Tor támogatásának köszönhetően a szolgáltatás ideális azoknak a felhasználóknak, akik anonimak szeretnének maradni webhelyekkel vagy online szolgáltatásokkal való interakció közben.
5. **Ideiglenes használat**: Alkalmas olyan helyzetekre, amikor eldobható email-címre van szükség, például promóciókhoz, ingyenes próbaidőszakokhoz vagy rövid távú kommunikációhoz.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Technikai jellemzők
A Ghostinbox GitHub repositoryja (https://github.com/valerio-vaccaro/ghostinbox.it) egy könnyű implementációt mutat, amely főként Pythonban, a Flask keretrendszerrel készült, az alábbi jellemzőkkel:

- **Serverless megközelítés**: nincs email-szerver; ehelyett egy ingyenes email- és email-továbbítási szolgáltatást használ, így a szolgáltatás architektúrája rendkívül egyszerű és gazdaságos.
- **Architektúra**: A Ghostinbox Flask-alapú kliens-szerver architektúrát használ az ideiglenes email-címek létrehozásának és az üzenetek megjelenítésének kezelésére. A design egyszerűsége nagy kérésmennyiség mellett is magas teljesítményt biztosít.
- **Címgenerálás**: Az ideiglenes email-címek dinamikusan jönnek létre a megadott alias alapján.
- **Tor támogatás**: A szolgáltatás úgy van konfigurálva, hogy onion routingon keresztül is elérhető legyen, biztosítva, hogy a felhasználó IP-címét ne kövessék a webhellyel való interakció során.
- **Üzenetkezelés**: A kapott üzenetek 30 nap után törlődnek.
- **Biztonság**: Személyes adatok vagy üzenetek nem tárolódnak tartósan. A szolgáltatás kialakítása minimalizálja az adatvédelmi incidensek kockázatát, a regisztráció hiánya pedig megszünteti az érzékeny információk megadásának szükségességét.
- **Open-source**: A nyilvános kód lehetővé teszi a fejlesztők számára a rendszer integritásának ellenőrzését, fejlesztések hozzáadását vagy egy testreszabott példány hosztolását.

Technikai erősségek:
- **Abszolút privacy**: Az emailek 30 nap utáni törlése és a Tor támogatása anonim és biztonságos élményt biztosít.
- **Könnyű felépítés**: A Flask implementáció kevés erőforrásra van optimalizálva, így a szolgáltatás skálázható és gyors.
- **Átláthatóság**: Az open-source licenc lehetővé teszi a kódauditot és a testreszabásokat, növelve a felhasználói bizalmat.

## Következtetés
A Ghostinbox elegáns és funkcionális megoldás azoknak, akik gyors, biztonságos és privacy-orientált ideiglenes email-szolgáltatást keresnek. Intuitív felületével, Tor támogatásával és open-source kódjának átláthatóságával egyszerre szól azokhoz a hétköznapi felhasználókhoz, akik meg akarják védeni bejövő fiókjukat a spamtől, és azokhoz a fejlesztőkhöz, akik megbízható rendszert keresnek tesztekhez vagy ideiglenes regisztrációkhoz. A Ghostinbox kipróbálásához látogasd meg a https://ghostinbox.it/ címet. A kód megtekintéséhez vagy a projekthez való hozzájáruláshoz keresd fel a repositoryt itt: https://github.com/valerio-vaccaro/ghostinbox.it.

