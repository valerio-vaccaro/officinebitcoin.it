---
layout: default
title: "Előfeltételek ehhez az útmutatóhoz"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
A kriptográfiai aláírások ellenőrzése alapvető biztonsági gyakorlat, amelyet **minden open-source szoftverfelhasználónak be kellene építenie a jó szokásai közé**.

Az open source természeténél fogva módosítható, ami azt jelenti, hogy elméletileg bárki beépíthet backdoors-t, támadásokat vagy rosszindulatú kódot azokba az alkalmazásokba, amelyeket gyakorlásra használsz, miközben a Bitcoin protokollt tanulod.

Felhasználóként, aki elmélyíti a tanulmányait, lehetőséged van személyesen ellenőrizni, hogy a letöltött szoftvert manipulálták-e, és ezt meg is kellene tenned, mielőtt telepíted és használod.

Mielőtt elkezdenénk, egy klasszikust is hozunk az Officine Bitcoin előadásaiból: a meme-et. Nem lesz nehéz előadás, de oldjuk a hangulatot már az elején.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Hogyan kell csinálni?
A fejlesztők mindig kriptográfiai aláírással együtt adnak ki új szoftververziókat.
Ez azt jelenti, hogy a szoftver frissítése mellett úgy adják ki, hogy tanúsítják: egy meghatározott fingerprinthez kötötték. Emlékeztető: a privát kulccsal létrehozott digitális aláírás egyedi és módosíthatatlan.

Mindössze a GPG suite-re van szükséged az aláírás ellenőrzéséhez.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Előfeltételek ehhez az útmutatóhoz
- Az aszimmetrikus kriptográfia rövid áttekintése
- Az ellenőrizendő elemek:
  - software (binary, apk, etc.)
  - a fejlesztő digitális aláírása, általában egy `.asc`, `.sig` fájl vagy egy checksum.
- Az ellenőrzéshez szükséges eszközök:
  - GPG suite
  - terminál (Linuxon és Windowson is működik)
# Aszimmetrikus kriptográfia

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Itt két, egymással összefüggő kulcs van: egy nyilvános kulcs és egy privát kulcs. Ahogy a nevük is sugallja:
- A nyilvános kulcs szabadon elérhető, és bárkivel megosztható.
- A privát kulcsot a tulajdonosa biztonságban tartja.

A nyilvános kulccsal titkosított adatok csak a hozzá tartozó privát kulccsal fejthetők vissza. Ez lehetővé teszi, hogy bárki titkosított adatokat küldjön a kulcspár tulajdonosának anélkül, hogy előzetesen megosztaná a titkos részt.

A nyilvános kulcsú kriptográfia lassabb, mint a szimmetrikus kriptográfia, és nem alkalmas nagy mennyiségű adat titkosítására. Ugyanakkor lehetővé teszi a titkosítási kulcsok biztonságos elosztását.
A nyilvános kulcsú kriptográfiában gyakran használt algoritmusok közé tartozik az RSA, az ECC, az ElGamal és a DSA.

## Fejlesztői oldal: új frissítés

A fejlesztő kiadja az open source kódot, amely természeténél fogva nincs titkosítva.
Létrehoz egy kriptográfiai hash-t (amely előállítja a `checksum`-ot), majd a digestet a privát kulcsával titkosítja: így jön létre az aláírás, az a korábban említett `.sig` vagy `.asc` fájl.

E folyamat után a fejlesztő mindkét fájlt feltölti a webhelyre vagy egy GitHub repositoryba. Innen indul a te letöltésed.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Ezután szükséged lesz a fejlesztő nyilvános kulcsára. Néha a GitHub repositoryban található, néha nyilvános szervereken (*keyservers*). Még ha a keresés erőfeszítést is igényelhet, a nyilvános kulcs elengedhetetlen elem a szoftver ellenőrzéséhez, ezért tegyél erőfeszítést a megszerzésére.

Ha nehézségeid vannak, kérdezz az Officine Bitcoin Telegram csoportjában, ahol útmutatást találsz egy adott nyilvános kulcs megszerzéséhez.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Az adatintegritás ellenőrzéséhez a címzett a küldő nyilvános kulcsával visszafejti az aláírást, és eredményt kap:

a. az adatok hitelesnek és az átvitel során módosítatlannak tekinthetők.
b. az adatokat potenciálisan manipulálták.

A hash érték privát kulccsal történő titkosításával **a PGP aláírások garantálják, hogy maga a checksum védett, és kapcsolódik a küldő személyazonosságához. Ez megakadályozza az aláírás hamisítását módosított adatokon**.

Az aláírások bárminek az ellenőrzésére használhatók: fájlok, emails, dokumentumok és szoftverletöltések esetén. Amikor PGP aláírást ellenőrzöl, bizonyítod, hogy az adatok valóban megbízható forrásból származnak és sértetlenek.

Most pedig egy mobil apk ellenőrzését fogod tudni elvégezni.

Példaként a Phoenix letöltését használjuk, amely egy non-custodial LN wallet, hogy egy későbbi Officine Bitcoin estén külön is foglalkozhassunk vele.

# Phoenix Wallet (Acinq) letöltése és ellenőrzése
Ha már jártál [Acinq](https://phoenix.acinq.co/) oldalán, a Phoenix fejlesztőjénél, akkor már tudod, hogy a letöltés elérhető az Android és iOS hivatalos store-jaiban.
Talán nem vetted észre, de Androidhoz az apk fájl is elérhető.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Menjünk oda!](https://github.com/ACINQ/phoenix/releases), hogy megtaláljuk az `apk` és `Signature` fájlokat, amelyeket `wget`-tel fogsz letölteni.
A Phoenix esetében az ellenőrzéshez szükséges aláírást tartalmazó fájl neve **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

Ugyanebben a repositoryban útmutató is található a *signing key E04E48E72C205463* kulcshoz tartozó nyilvános kulcs letöltéséhez (Drouinf kulcsainak egyedi fingerprintje).
Másold ki a linket és töltsd le `wget`-tel, vagy kövesd a repo megfelelő szakaszában javasolt utasításokat.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**A nyilvános kulcsot importálni kell, nem elég csak letölteni**.
⚠️ A fájlok letöltésének ugyanabba a könyvtárba kell történnie.

---
# Nyisd meg a terminált
A terminállal navigálj abba a könyvtárba, ahová az apk és a `SHA256SUMS.ASC` fájl letöltődött, majd sorrendben futtasd a parancsokat.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Amikor az ellenőrzés pozitív eredményt ad, átmásolhatod az apk-t a telefonodra, és telepítheted az appot.

---
# Nehéz ellenőrzés
Több oka is lehet annak, hogy az aláírás ellenőrzése nem könnyű, és ezek szinte mindig rendetlenségből vagy tapasztalatlanságból erednek:
1. az apk és/vagy .asc fájlokat többször töltötték le, ezért a könyvtárban például furcsa nevekkel jelennek meg, mint **filename-1** vagy **filename(1)**
2. az apk és a .asc nincs ugyanabban a könyvtárban
3. a nyilvános kulcsot letöltötték, de nem importálták a gpg keyringbe.

Előfordulhatnak más helyzetek is, amikor még helyes eljárás mellett is sikertelen az ellenőrzés.
Fontos megnézni a terminálban megjelenő hibát, kimásolni, és keresést indítani az interneten a megoldásra.

# Ellenőrzés Sparrow Wallet segítségével
Ha már használod a Sparrow Walletet, ezzel a szoftverrel is ellenőrizheted a letöltéseket, **amelynek letöltését és telepítését gondos és szigorú GPG-ellenőrzésnek kell megelőznie**.

Indítsd el a Sparrow walletet, és keresd meg a `Tools` menüben a `Verify Downloads` pontot.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Megnyílik egy felület, amely arra kér, hogy illeszd be a frissen letöltött fájlokat. A `Browse` gombra kattintva megnyílik a fájlkezelő, hogy minden fájlt betölts a megfelelő mezőbe.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

Néha a felület űrlapja magától kitöltődik. Ha nem, tölts ki minden mezőt a megfelelő fájlokkal.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

A pozitív eredmény grafikusan, zöld pipákkal és a *`Ready to install`* + < filename > megerősítéssel jelenik meg.

# Tanulási támogatás
Ha részt vettél a Telegramon tartott élő bemutatón, tekintheted ezt egy további lépésnek a személyes szuverenitásod felé (nem csak pénzügyi értelemben).
Ha lemaradtál róla, **ne ess kétségbe**: ezek a jegyzetek pontosan a pótlást szolgálják, és ráadásul tudd, hogy az Officine keretében újra javasolni fogjuk.

Hogy ne maradj le a következő bemutatóról, csatlakozz a [Telegram csoporthoz](https://t.me/officinebitcoin), hogy folyamatosan naprakész maradj.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Megtalálhatod a hozzád legközelebbi [Satoshi Spritz](https://satoshispritz.it/) eseményt is. A Satoshi Spritz egy helyi meetup, ahol kizárólag Bitcoinról beszélnek, ahová elviheted a kérdéseidet, és válaszokat kaphatsz más tapasztalt bitcoinerektől. A linken megtalálod a félsziget térképét.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

Végül, ha nem találsz meetupot a közeledben, kihasználhatod a [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect) heti élő streamjeit, egy virtuális meetupot, amelyet azoknak hoztak létre, akik nem tudnak részt venni a Satoshi Spritz eseményeken, illetve hogy segítsen a kisebb meetupoknak jegyzetelni és inspirációt találni saját előadásaikhoz.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
