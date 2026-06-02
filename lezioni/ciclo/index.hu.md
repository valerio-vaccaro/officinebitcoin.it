---
layout: default
title: "A Bitcoin-tranzakció életciklusa"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# A Bitcoin-tranzakció életciklusa

## Mi az a Bitcoin-tranzakció
A Bitcoin-tranzakció a blockchainen rögzített művelet, amely értéket továbbít egy vagy több bemenetből (korábban kapott pénzekből, úgynevezett UTXOs - Unspent Transaction Outputs) egy vagy több kimenetbe (új címzettekhez).
A bemenetek korábbi tranzakciók még el nem költött kimenetei, míg a kimenetek satoshikat rendelnek meghatározott címekhez. Kivétel a "coinbase" tranzakció, minden blokk első tranzakciója, amely bemenetek nélkül hoz létre új bitcoinokat (bányászati jutalmat és díjakat). Ha egy bemenetből nem költik el az összes pénzt, a különbözet (change) egy további kimeneten keresztül visszatér a küldőhöz, vagy ha nincs kezelve, örökre elveszik.

## Az életciklus fázisai
Ez a tranzakció életciklusa:

- Létrehozás: A wallet felépíti a tranzakciót úgy, hogy kiválasztja, mely UTXO-kat költse el a küldendő összeg és a díjak minimalizálását célzó stratégia alapján. Ha a bemenet meghaladja a kimenetet, létrejön egy "change" kimenet, amely visszakerül a küldőhöz, de ez növeli a tranzakció méretét és költségét. Egyes walletek próbálják ezt elkerülni.
- Aláírás: A tranzakciót bemenetenként egy vagy több digitális aláírással írják alá, ezzel hitelesítve azt. Ez a lépés alapvető az érvényességhez, és multisig tranzakciók esetén több felet is érinthet.
- Közzététel: Az aláírt tranzakciót továbbítják a hálózatnak ("broadcast"), és bekerül a helyi node mempooljába. A mempool konszenzusszabályok (például érvényes aláírások, rendelkezésre álló pénzek) és helyi szabályok (például 400 KB maximális méret a spam megelőzésére) szerint validálja a tranzakciót. Ezután a node továbbterjeszti a peereknek, amelyek validálják és beteszik a saját mempooljaikba, így lépcsőzetes broadcast jön létre. A mempoolok node-onként eltérhetnek a különböző beállítások vagy kapcsolatok miatt.
- Megerősítés: Egy bányász blokkba foglalja a tranzakciót, ezzel megerősítve azt a blockchainen. Amíg azonban nincs több megerősítése (rá következő blokkok), továbbra is sebezhető cserékkel vagy forkokkal szemben. Egy alacsony díjú tranzakció sokáig a mempoolban maradhat vagy eldobódhat, de akár hónapok után is kibányászható, ha a bemenetek továbbra is elköltetlenek.

## Problémakezelés
- A tranzakció eltűnt a mempoolból: Ha egy alacsony díjú tranzakciót eltávolítanak (például forgalmi csúcsok miatt), kézzel újra lehet továbbítani (rebroadcast) a TXID használatával, akár scripts vagy explorerek segítségével is. Valaki ezt harmadik felek nevében is megteheti.
- Replace-by-Fee (RBF): Ha a díj nem elegendő, a tranzakció lecserélhető egy többet fizető tranzakcióra, feltéve hogy RBF flaggel van megjelölve. Egy javaslat szerint minden tranzakciónak implicit módon cserélhetőnek kellene lennie, mivel a bányászok amúgy is a magasabb díjakat részesítik előnyben.
- Child Pays for Parent (CPFP): Ha az RBF nem használható (például nem a saját tranzakciódról van szó, vagy elfogytak a pénzek), az elakadt tranzakció egyik kimenetét egy új, magas díjat fizető tranzakcióval költik el, így mindkettő vonzóvá válik a bányászok számára. A díjak összegének mindkettőt fedeznie kell. Gond akkor keletkezik, ha a node-ok eldobják az első tranzakciót, megszakítva a láncot; egy fejlesztés alatt álló protokoll tranzakciócsomagok továbbításával igyekszik ezt elkerülni.

## Végső megerősítés
Egy tranzakció csak több megerősítéssel (felette lévő blokkokkal) tekinthető véglegesnek. Egyetlen megerősítés nem elég, mert forkok vagy dupla költés érvényteleníthetnék. A White Paper 6 megerősítést javasol (körülbelül 60 percet, átlagosan 10 percenkénti blokkokkal), de a szám az összeg és a kockázat alapján változik. A blokkidők szórása nagy, de az átlagot a bányászati nehézség tartja fenn.

## Következtetés
A ciklus azzal zárul, hogy a tranzakció "bevésődik" a blockchainbe, véglegesen rögzítve az értékátvitelt.

## Program
Ez a lecke egy Satoshi Spritz Connect alkalomra készült.
