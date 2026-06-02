---
layout: default
title: "Descriptor Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Descriptor Bitcoin

## Introduzion

I descriptor hinn on concetto relativamente nuovo e minga ancora assai diffuso, ma utile per descrivere la struttura di wallet Bitcoin. I descriptor hinn stringhe de caratteri leggibili (alfanumerici, esadecimali e alcuni simboli come parentesi), progettate per rappresentare in modo chiaro e standardizzato on wallet, ovver l’insieme de ciav pubbliche e private necessarie per calcolare saldi, ricevere e spend Bitcoin.

## Evoluzion de la gestion di wallet
Per contestualizzare i descriptor, el relatore ripercorre l’evoluzion di wallet:

- Primi wallet (pre-BIP-32): nei primi tempi, con Bitcoin Core, i wallet erano file contenenti ciav generate casualmente. Ogni volta che si esaurivano i indirizzi, ne venivano aggiunti de nuovi, rendendo necessario on backup frequente per minga perdere fond. Quest sistema era inefficiente.
- BIP-32 (HD Wallet): con l’introduzion de la generazion gerarchica deterministica, on seed (seme) generava ona chiave master, da cui derivavano tutti i indirizzi. Bastava fare el backup del seed, ma minga era ancora ona soluzion completa.
- Mnemoniche (BIP-39): successivamente, el seed l'è stato derivato da ona sequenza de 12 o 24 paroll (mnemonica), più facil da salvare. Tuttavia, per ricostruire on wallet, servivano anca informazion sui percorsi de derivazion (es. Legacy, SegWit), altrimenti i fond potevano risultare irreperibili.

La sola mnemonica minga basta, soprattutto per wallet complessi come i multisig (che richiedono più firme) o quelli con script avanzati (es. timelock o condizion de eredità). Alcuni wallet tentano tutte i derivazion possibili per trovare i fond, mentre altri (es. Electrum) richiedono de specificare el tipo de wallet. Nei multisig, inoltre, servono i ciav pubbliche di altri partecipanti, complicando ulteriormente el backup.

## Cosa hinn i Descriptor e perché servono
I descriptor nascono per superare questi limiti, offrendo ona descrizion completa e flessibile de la struttura de on wallet. Minga sostituiscono la mnemonica, ma la integrano, includendo:

- Chiavi pubbliche estese (xpub, ypub, ecc.).
- Percorsi de derivazion (es. m/44'/0'/0' per Legacy).
- Eventuali script o condizion de spesa (es. multisig, timelock).

##Esempi pratici
- Single-sig Legacy: On descriptor sempliz potrebbe essere `pk([fingerprint/derivation]xpub...)`, indoe:
1. pk indica ona chiave pubblica.
2. [fingerprint/derivation] specifica la chiave master e el percorso.
3. xpub genera i indirizzi (es. 0/* per ricevere, 1/* per el change).
- Multisig: On esempio l'è `sortedmulti(2, xpub1, xpub2, xpub3)`, che descrive on wallet 2-de-3, ordinando i ciav per consistenza.
- Script complessi: Con script come p2sh (pay to script hash) o p2wsh (pay to witness script hash), si possono includere condizion avanzate, come timelock o combinazion logiche (and, or).

## Descriptor e Taproot
On caso interessante l'è el descriptor per Taproot (tr), che supporta due modalità de spesa:

- Firma diretta con ona chiave specifica.
- On albero de condizion (es. eredità o timelock), mantenendo la complessità nascosta sulla blockchain fino a la spesa.

## Vantaggi di Descriptor
- Backup completo: racchiudono tutte i informazion necessarie per ricostruire on wallet senza tentativi.
- Compatibilità: ideali per wallet watch-only, indoe si monitorano i fond senza ciav private.
- Flessibilità: supportano single-sig, multisig e script complessi.
- Privacy: minga rivelano segreti e possono essere condivisi come ona xpub.

## Limiti e compatibilità
Minga tutti i wallet supportano i descriptor pienamente. Ad esempio, Bitcoin Core ne implementa domà on sottoinsieme e richiede due descriptor separati per indirizzi e change. Software come Sparrow o Specter offrono on supporto migliore, permettendo de importare/esportare descriptor e visualizzarne la struttura.

Esperimenti possono essere fatti con:
- Sparrow: supporta i descriptor, con on’interfaccia grafica per crearli o analizzarli.
- BDK: libreria con interfaccia a riga de comando per gestire descriptor complessi.
- Testnet/Signet: ambienti sicuri per testare senza rischiare fond reali.

## Riferimenti

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programma
Questa lezion l'è stata realizzata per on Satoshi Spritz Connect.
