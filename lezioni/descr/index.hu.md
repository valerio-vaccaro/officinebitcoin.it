---
layout: default
title: "Bitcoin descriptorok"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only lecke</span> <span>Ezt a projektet valerio-vaccaro tartja karban</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bitcoin descriptorok

## Bevezetés

## Descriptorok
A descriptorok viszonylag új, és még nem túl elterjedt fogalmak, de hasznosak a Bitcoin wallet szerkezetének leírására. A descriptorok olvasható karakterláncok (alfanumerikus és hexadecimális karakterek, valamint néhány jel, például zárójelek), amelyek arra szolgálnak, hogy világosan és szabványosított módon ábrázoljanak egy walletet, vagyis a nyilvános és privát kulcsok azon készletét, amely az egyenlegek kiszámításához, valamint Bitcoin fogadásához és elköltéséhez szükséges.

## A wallet-kezelés fejlődése
A descriptorok kontextusba helyezéséhez az előadó áttekinti a walletek fejlődését:

- Korai walletek (pre-BIP-32): a kezdeti időkben, Bitcoin Core használatakor, a walletek véletlenszerűen generált kulcsokat tartalmazó fájlok voltak. Amikor elfogytak a címek, újakat adtak hozzá, ezért gyakori biztonsági mentésre volt szükség a pénzeszközök elvesztésének elkerüléséhez. Ez a rendszer nem volt hatékony.
- BIP-32 (HD Wallet): a hierarchikus determinisztikus generálás bevezetésével egy seed létrehozott egy mesterkulcsot, amelyből az összes cím származott. Elég volt a seedről biztonsági mentést készíteni, de ez még nem jelentett teljes megoldást.
- Mnemonicok (BIP-39): később a seed egy 12 vagy 24 szóból álló sorozatból (mnemonic) származott, amelyet könnyebb volt megőrizni. Egy wallet helyreállításához azonban a derivációs útvonalakról (például Legacy, SegWit) is szükség volt információra, különben a pénzeszközök visszaállíthatatlanná válhattak.

A mnemonic önmagában nem elég, különösen az olyan összetett walleteknél, mint a multisig (amely több aláírást igényel), vagy azoknál, amelyek fejlett scripteket használnak (például timelock vagy öröklési feltételek). Egyes walletek minden lehetséges derivációt kipróbálnak a pénzeszközök megtalálásához, míg mások (például az Electrum) megkövetelik a wallet típusának megadását. Multisig esetén ráadásul a többi résztvevő nyilvános kulcsaira is szükség van, ami tovább bonyolítja a biztonsági mentést.

## Mik azok a descriptorok, és miért van rájuk szükség
A descriptorok azért jöttek létre, hogy feloldják ezeket a korlátokat, és teljes, rugalmas leírást adjanak a wallet szerkezetéről. Nem helyettesítik a mnemonicot, hanem kiegészítik azt, többek között ezekkel:

- Kiterjesztett nyilvános kulcsok (xpub, ypub, stb.).
- Derivációs útvonalak (például m/44'/0'/0' Legacy esetén).
- Bármilyen költési script vagy feltétel (például multisig, timelock).

## Gyakorlati példák
- Legacy single-sig: egy egyszerű descriptor lehet például `pk([fingerprint/derivation]xpub...)`, ahol:
1. pk egy nyilvános kulcsot jelöl.
2. [fingerprint/derivation] megadja a mesterkulcsot és az útvonalat.
3. xpub címeket generál (például 0/* fogadáshoz, 1/* change-hez).
- Multisig: példa erre a `sortedmulti(2, xpub1, xpub2, xpub3)`, amely egy 2-of-3 walletet ír le, és a következetesség érdekében rendezi a kulcsokat.
- Összetett scriptek: olyan scriptek esetén, mint a p2sh (pay to script hash) vagy a p2wsh (pay to witness script hash), fejlett feltételek is beilleszthetők, például timelock vagy logikai kombinációk (and, or).

## Descriptorok és Taproot
Érdekes eset a Taproot (tr) descriptora, amely két költési módot támogat:

- Közvetlen aláírás egy adott kulccsal.
- Feltételekből álló fa (például öröklés vagy timelock), amely a komplexitást a költésig rejtve tartja a blockchainen.

## A descriptorok előnyei
- Teljes biztonsági mentés: minden olyan információt tartalmaznak, amely egy wallet próbálgatás nélküli helyreállításához szükséges.
- Kompatibilitás: ideálisak watch-only wallets esetén, ahol a pénzeszközöket privát kulcsok nélkül figyelik.
- Rugalmasság: támogatják a single-sig, multisig és összetett scripteket.
- Adatvédelem: nem fednek fel titkokat, és megoszthatók úgy, mint egy xpub.

## Korlátok és kompatibilitás
Nem minden wallet támogatja teljes mértékben a descriptorokat. A Bitcoin Core például csak egy részhalmazt valósít meg, és két külön descriptort igényel a címekhez és a change-hez. Az olyan szoftverek, mint a Sparrow vagy a Specter, jobb támogatást kínálnak, lehetővé téve a descriptorok importálását/exportálását és szerkezetük megjelenítését.

Kísérletezni ezekkel lehet:
- Sparrow: támogatja a descriptorokat, grafikus felülettel azok létrehozásához vagy elemzéséhez.
- BDK: parancssori felülettel rendelkező könyvtár összetett descriptorok kezeléséhez.
- Testnet/Signet: biztonságos környezetek teszteléshez, valódi pénzeszközök kockáztatása nélkül.

## Hivatkozások

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Program
Ez a lecke egy Satoshi Spritz Connect alkalomra készült.
