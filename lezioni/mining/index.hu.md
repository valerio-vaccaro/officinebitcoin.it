---
layout: default
title: "Bevezetés a bányászatba"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bevezetés a bányászatba
A Bitcoin-bányászat a protokoll alapvető folyamata, amely arra szolgál, hogy sorrendet javasoljon a mempoolban lévő tranzakciók között, kiválasszon egy részhalmazt egy új blokk létrehozásához, és frissítse a blockchain állapotát.

A bányászatot decentralizáltnak és véletlenszerűnek tervezték (idézőjelben, mivel kriptográfiai feladványon alapul), így elkerülhető a tranzakciók központosított kezelése.

## A bányászat célja
A bányászat a központosítással kapcsolatos problémákat oldja meg, például:

- Cenzúra: egy központi szereplő blokkolhatna bizonyos tranzakciókat, de decentralizált bányászok mellett a tranzakcióknak nagyobb esélyük van bekerülni.
- Kétszeres költés: korruptálható bányász nélkül nehéz átírni a történelmet, vagy egy tranzakciót egy másik rovására előnyben részesíteni.
- Timestamping: biztonságos és közös időbeli sorrendet biztosít, amely nem központi hatóságtól, hanem a bányászok és node-ok közötti konszenzustól függ.

# Hogyan működik a bányászat
A bányászati folyamat lépésről lépésre így magyarázható:

- Tranzakciók kiválasztása: a bányász tranzakciókat választ a mempoolból, gyakran a magasabb díjakat fizetőket részesítve előnyben, a profit optimalizálása érdekében (egy NP-complete probléma, hasonló a "knapsack problem"-hez).
- Coinbase létrehozása: a bányász létrehoz egy speciális tranzakciót (coinbase), amely saját magának rendeli a blokk jutalmát (jelenleg 3.125 BTC, négyévente felezve), valamint a kiválasztott tranzakciók díjait.
- Merkle Root: a kiválasztott tranzakciókat fa adatszerkezetbe rendezik (Merkle Tree), amely létrehoz egy Merkle Root értéket, egy hasht, amely az összes tranzakciót és azok sorrendjét reprezentálja.
- Block Header: a bányász elkészíti a blokkfejléc prototípusát, amely tartalmazza:
1. A timestampet.
2. Az előző blokk hashét.
3. A Merkle Root értéket.
4. A nehézséget (target), amely a hálózattól függ.
5. Egy nonce értéket (véletlen szám, például nullára inicializálva).
- Kriptográfiai feladvány: a bányász kétszer alkalmazza az SHA-256 algoritmust a fejlécre, és ellenőrzi, hogy az eredmény elegendő számú vezető nullát tartalmaz-e (a nehézségi küszöb alatt van-e). Ha nem, módosítja a nonce értéket vagy más mezőket (pl. timestamp vagy tranzakciós sorrend), és megismétli a számítást. Ez rövidítések nélküli brute force munka, az SHA-256 tulajdonságainak köszönhetően.

## Optimalizálások
A folyamat gyorsítása érdekében a bányászok kiszámíthatják az első SHA-256-ot a fejléc első 64 bájtján (változtathatatlan rész), majd csak a maradékon iterálnak, a nonce módosításával. A specializáció olyan hardware-hez (ASIC) vezetett, amely másodpercenként milliárdnyi próbálkozást végez.

# Validálási folyamat
Amikor egy bányász megoldást talál, továbbítja a teljes blokkot (fejléc + tranzakciók) a hálózatnak. A node-ok ellenőrzik:
- a fejléc hashét (egy egyszeri SHA-256 a megerősítéshez).
- a blokkinformációk helyességét (timestamp, előző blokk hashe, Merkle Root és nonce).
- a Merkle Root reprodukálhatóságát az összes kapcsolódó tranzakció helyességének ellenőrzése után.

Ha érvényes, a blokk hozzáadódik a blockchainhez. A jutalom (coinbase + díjak) csak 100 megerősítés után költhető el (körülbelül 16 óra), a stabilitás biztosítása érdekében.

# Bányászati költségek és jutalmak
Költségek:

- Villamos energia: fő változó költség.
- Hardware: drága és rövid élettartamú ASIC-ek, amelyeket gyorsan felülmúlnak a hatékonyabb modellek.
- Infrastruktúra: hűtés, telepítés, karbantartás (például a napelemek nem "ingyenesek").

Jutalmak:

- Fix jutalom (2024-ben 3.125 BTC-re feleződött).
- Változó tranzakciós díjak.

A bányásznak tiszteletben kell tartania a konszenzusszabályokat: az érvénytelen blokkot eldobják, ami jutalom nélküli erőforrás-pazarlást jelent. Még egy érvényes blokk is "árvává" válhat, ha egy másik bányász nyeri a versenyt, veszteségeket okozva.

## Gazdasági stratégia
A bányászat versengő tevékenység: a bányászok igyekeznek maximalizálni az üzemidőt a fix költségek amortizálása érdekében. Az alkalmi használat (például a bányászok bekapcsolása csak többletenergia esetén) nem praktikus, mivel a kezdeti költségek folyamatosságot igényelnek. A befektetés megtérülése hosszú és bizonytalan lehet.

# Solo és pool bányászat

- Solo Mining: a bányász egyedül dolgozik, a blokkot teljes node-dal vagy egyedi szoftverrel építi. Ha talál egy blokkot, az egész jutalmat megkapja, de ennek valószínűsége rendkívül alacsony (egyetlen ASIC-kel évszázadokig is eltarthat).
- Pool Mining: az olyan protokollok, mint a Stratum, lehetővé teszik a bányászok együttműködését:
1. A pool sablont ad (coinbase, Merkle Root stb.).
2. A bányászok shares értékeket küldenek (bizonyos számú nullával rendelkező próbálkozásokat, a blokk nehézsége alatt) a munka bizonyítékaként.
3. Amikor egy poolbányász blokkot talál, a jutalmat a beküldött shares arányában osztják fel.
- Stratum v2: olyan fejlődési lépés, amely lehetővé teszi a bányászok számára a tranzakciók kiválasztását, csökkentve a pool központosítását, bár ellenőrzéseket igényel a helyesség biztosításához (pl. a poolnak járó díjak).

# Hashrate becslése
A hashrate (számítási teljesítmény) becslése:
- Poolban: az időegység alatt kapott shares megszámlálásával, megszorozva a share nehézségével. Ez olyan becslés, amelyet a szerencse befolyásolhat.
- Globálisan: a Bitcoin nehézségét és a blokkok közötti átlagos időt (körülbelül 10 perc) használva. Az ingadozások normálisak, de az átlag megbízható.

Az olyan hardware, mint a Nerd Miner, belső számlálókat használ a pontos adatokhoz, míg a poolok változékonyabb becslésekre támaszkodnak, amelyek ingadozó grafikonokon láthatók.

# Program
Ez a lecke egy Satoshi Spritz Connect számára készült.
