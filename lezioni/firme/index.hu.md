---
layout: default
title: "Digitális aláírások"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Digitális aláírások
Ennek a leckének a témája a digitális aláírás és annak alkalmazása a Bitcoinban.

## Mi az aláírás?
Meg kell értenünk, mit értünk digitális aláírás alatt. Amikor egy hagyományos aláírásra gondolunk, általában valami más jut eszünkbe: mivel digitális dokumentumokról beszélünk, a digitális aláírás összekapcsolja a szerző személyazonosságát és az aláírt dokumentum állapotát is, tehát lényegében az aláírás attól a dokumentumtól is függ, amelyet alá akarunk írni.

Ez nagyon nagy különbség a fizikai világhoz képest, ahol az aláírást gyakorlatilag anélkül helyezzük el, hogy törődnénk azzal a hordozóval, amelyen megtesszük. Természetesen csekkeket vagy más dokumentumokat talán nem írnánk alá figyelmetlenül, de lényegében az általunk elhelyezett aláírás nem változik.

A digitális aláírások kissé mások; általában nyilvános és privát kulcsos algoritmusokra támaszkodnak. Ez azt jelenti, hogy valahol a világban a walletünk rendelkezik egy nyilvános és egy privát kulcsból álló kulcspárral, és a (pszeudo-)azonosságunk ahhoz a nyilvános kulcshoz kapcsolódik, amelyet mindenki ismer, vagy amelyet mindenki számára ismertté teszünk.

A privát kulcsunkat fogjuk használni, amely egy szám, és némi matematikai varázslattal létrehozunk egy aláírást, amely egy másik szám, és bizonyítja, hogy egy adott dokumentum adott állapota egy nyilvános kulcshoz kapcsolt bizonyos identitáshoz tartozik, vagy az számára ismert. Amit aláírok, az egy adott dokumentum (vagy PAYLOAD) ujjlenyomata (vagy HASH).

Szükségem van továbbá valamilyen véletlenszám-generátorra; ezeket az adatokat bedobom egy "fekete dobozba", amely elkészíti számomra az aláírást. Az aláírás tehát egyrészt birtoklást bizonyít, mert a titkommal írok alá, másrészt azt is bizonyítja, hogy amit aláírok, azt nem módosították.

Ha módosítom a PAYLOAD értékét, módosítom a HASH értékét is, és ez nyilvánvalóan érvényteleníti az aláírást.

Miért vezették be tehát ezt a bonyolultabb aláírást a digitális világban? Azért, mert a digitális világban, a fizikai világtól eltérően (és erre talán azok is emlékeznek, akik ellógták az iskolát), egy aláírás lemásolása sokkal egyszerűbb.

A digitális aláírás viszont információt tartalmaz a dokumentumról, ezért minden dokumentumnál megváltozik, és nem lehet beilleszteni, majd újra felhasználni egy másik dokumentumon.

A digitális aláírás tehát arra szolgál, hogy:
- bizonyítsa, hogy létrehoztam egy adott üzenetet, egy adott műveletet kérek, vagy egy rendszer adott állapotát jelentem ki, és
- bizonyítsa, hogy az az üzenet, dokumentum vagy adatkarakterlánc nem lett manipulálva, vagyis valóban az, amit alá akartam írni.
- egy adott műveletet letagadhatatlanná tegyen; ha én hoztam létre az aláírást, akkor valóban én tettem ezt az adott dokumentumra.

## Aláírások a Bitcoinban
Ezt a technológiát a Bitcoinban ECDSA (Elliptic Curve Digital Signature Algorithm) néven használják; ez egy elliptikus görbéken digitális aláírásokat létrehozó algoritmus. Egyelőre más aláírási sémákkal nem foglalkozunk.

Ne feledd, hogy Bitcoinban aláírásokat lehet létrehozni:
- tetszőleges szöveghez, ami nem túl fontos és nem túl gyakran használt
- új tranzakciókhoz, egy adott UTXO elköltésének engedélyezése céljából

De hogyan kapcsolódnak ezek az aláírások a tranzakcióhoz? Minden címnek van egy költési mechanizmusa, vagyis olyan scripts, amelyeket végre kell hajtani annak eldöntéséhez, hogy egy költés engedélyezhető-e. Ezekben a scripts elemekben vannak digitális aláírások ellenőrzésére szolgáló parancsok (vagy OPCODES), például OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Ne feledd, hogy egy Bitcoin-tranzakció a következőkből áll:
- Inputs, vagyis azok az összegek, amelyeket el fogok költeni, és amelyekhez költési scriptet kell létrehoznom
- Outputs, vagyis az új címek, ahová az összegek kerülnek (és minden címhez egy jól meghatározott költési mód kapcsolódik.

Lényegében tehát a legtöbb esetben MINDEN INPUT ESETÉBEN létre kell hoznom a költési script befejezéséhez szükséges aláírás(oka)t.

Ne feledd, hogy ez a művelet lehetővé teszi annak bizonyítását, hogy az adott input a miénk, és el akarjuk költeni (teljes egészében át akarjuk adni a tulajdont, fel akarjuk osztani, vagy más inputokkal akarjuk egyesíteni).

Nyilvánvaló, hogy a tranzakció akkor érvényes, ha minden input helyesen alá van írva; ha akár egyetlen input nincs aláírva, az a tranzakció nem tekinthető érvényesnek.

Az aláírás mindenki által ellenőrizhető és letagadhatatlan, de a rugalmasság érdekében Satoshi nagyon okosan különféle aláírási módokat vezetett be: maga az aláírás mindig ugyanaz, de a PAYLOAD változik, vagyis a tranzakciónak az a része, amely az aláírás tárgya. Ez lehetővé teszi például összetett sémák és protokollok létrehozását, amelyekben tranzakciódarabok kombinálhatók egymással; Satoshi ezeket a módokat (a scripting nyelv valódi flagjeit) SIGHASH néven nevezte el.

## SIGHASH
A legegyszerűbb SIGHASH a SIGHASH_ALL, ami azt jelenti, hogy az aláírás az ÖSSZES INPUT és az ÖSSZES OUTPUT alapján készül; ez az aláírás készítésének legegyszerűbb és leggyakrabban használt módja.

Az első eltérés a SIGHASH_NONE esetében jelenik meg, amely az ÖSSZES INPUTOT aláírja, de az OUTPUTOK KÖZÜL EGYET SEM, így később outputok adhatók hozzá vagy fees módosíthatók. FIGYELEM: ezzel a sémával, ha nem védi multisig vagy más funkció, egy miner vagy bárki, aki lát egy ilyen aláírási sémájú tranzakciót, lecserélheti az outputokat, és az összegeket a saját címére irányíthatja.

Érdekesebb flag a SIGHASH_SINGLE, amelyben egy input-output pár kerül aláírásra, feltéve, hogy ugyanazon a szinten szerepelnek egy tranzakcióban (például ötödik input és ötödik output); ez lehetővé tenné nagyobb tranzakciók összeállítását ezekből a párokból, de nem ad lehetőséget váltó bevezetésére, vagyis az input teljes elköltését követeli meg.

Ezekkel párhuzamosan minden SIGHASH kombinálható az ANYONECANPAY flaggel, amely az aláírást csak arra az inputra korlátozza, amelyhez az aláírás készül, így bárkinek lehetőséget ad arra, hogy inputokat adjon a tranzakcióhoz.

Ezek az aláírások mind érvényes aláírások a cím és a scripts típusától függetlenül, maximális kifejezési rugalmasságot hagyva a wallet számára, amely normál esetben SIGHASH_ALL-t használ, de követhet bonyolultabb protokollokat is, amelyek eltérő aláírási sémákat igényelnek. Multisig esetén nincs szükség ugyanazon aláírástípus használatára; egy 2-of-2 wallet például aláírhatja néhány UTXO-ját SIGHASH_NONE és ANYONECANPAY használatával, hogy teljes kontrollt adjon a második aláírónak, aki például ezeket az inputokat egy SIGHASH_ALL-lal aláírandó tranzakcióban gyűjtheti össze.

## Aláírások tetszőleges szövegen
A teljesség kedvéért: ugyanazok az aláírások, amelyeket tranzakciós inputokhoz használunk, tetszőleges szöveg aláírására is használhatók.

A Bitcoin olyan sémát javasol, amelyben szöveg kerül hozzáadásra annak megakadályozására, hogy ezt a funkciót tranzakciórészek aláírására használják; ezért ha Bitcoin Core-od vagy akár bizonyos walletjeid vannak, kereshetsz egy adott címedhez kapcsolódó szöveges üzenet-aláírási funkciót.

A wallet az adott címet létrehozó nyilvános kulcshoz tartozó privát kulcsot fogja használni a szöveges üzenetek aláírásához.

Ellenőrzéskor megkapjuk a nyilvános kulcsot, amely aztán felhasználható a cím újbóli előállítására; ha tehát megvan a szöveg és az aláírás, kinyerem az azt aláíró nyilvános kulcsot, és a nyilvános kulcsból újraszámolhatom a címet, majd összevethetem például a megadott címmel.

## Program
Az aláírásokról szóló lecke megismételhető; itt van a már megtartott alkalmak listája:

| Dátum       | Megjegyzések                                   |
|-------------|------------------------------------------------|
|||
