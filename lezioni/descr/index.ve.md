---
layout: default
title: "Descriptor Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Sto progetto xe mantegnuo da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Descriptor Bitcoin

## Introduzione

I descriptor xe un concetto relativamente nuovo e no ancora tanto diffuso, ma utile par descrivere la struttura dei wallet Bitcoin. I descriptor xe stringhe de caratteri leggibili (alfanumerici, esadecimali e alcuni simboli come parentesi), progettate par rappresentare in modo chiaro e standardizzato un wallet, ovvero l’insieme de ciavi publiche e private necessarie par calcolare saldi, ricevere e spender Bitcoin.

## Evoluzione de la gestion dei wallet
Par contestualizzare i descriptor, el relatore ripercorre l’evoluzione dei wallet:

- Primi wallet (pre-BIP-32): nei primi tempi, co Bitcoin Core, i wallet erano file contenenti ciavi generate casualmente. Ogni volta che si esaurivano i indirizzi, ne venivano aggiunti de nuovi, rendendo necessario un backup frequente par no perdere fondi. Sto sistema era inefficiente.
- BIP-32 (HD Wallet): co l’introduzione de la generazione gerarchica deterministica, un seed (seme) generava na chiave master, da cui derivavano tutti i indirizzi. Bastava fare el backup del seed, ma no era ancora na soluzione completa.
- Mnemoniche (BIP-39): successivamente, el seed xe stato derivato da na sequenza de 12 o 24 parole (mnemonica), più facile da salvare. Tuttavia, par ricostruire un wallet, servivano anca informazioni sui percorsi de derivazione (es. Legacy, SegWit), altrimenti i fondi potevano risultare irreperibili.

La sola mnemonica no basta, soprattutto par wallet complessi come i multisig (che richiedono più firme) o quelli co script avanzati (es. timelock o condizioni de eredità). Alcuni wallet tentano tutte le derivazioni possibili par trovare i fondi, mentre altri (es. Electrum) richiedono de specificare el tipo de wallet. Nei multisig, inoltre, servono le ciavi publiche dei altri partecipanti, complicando ulteriormente el backup.

## Cosa xe i Descriptor e perché servono
I descriptor nascono par superare sti limiti, offrendo na descrizione completa e flessibile de la struttura de un wallet. No sostituiscono la mnemonica, ma la integrano, includendo:

- Chiavi pubbliche estese (xpub, ypub, ecc.).
- Percorsi de derivazione (es. m/44'/0'/0' par Legacy).
- Eventuali script o condizioni de spesa (es. multisig, timelock).

##Esempi pratici
- Single-sig Legacy: Un descriptor semplice potrebbe essere `pk([fingerprint/derivation]xpub...)`, dove:
1. pk indica na chiave pubblica.
2. [fingerprint/derivation] specifica la chiave master e el percorso.
3. xpub genera i indirizzi (es. 0/* par ricevere, 1/* par el change).
- Multisig: Un esempio xe `sortedmulti(2, xpub1, xpub2, xpub3)`, che descrive un wallet 2-de-3, ordinando le ciavi par consistenza.
- Script complessi: Co script come p2sh (pay to script hash) o p2wsh (pay to witness script hash), si possono includere condizioni avanzate, come timelock o combinazioni logiche (and, or).

## Descriptor e Taproot
Un caso interessante xe el descriptor par Taproot (tr), che supporta due modalità de spesa:

- Firma diretta co na chiave specifica.
- Un albero de condizioni (es. eredità o timelock), mantenendo la complessità nascosta sulla blockchain fino a la spesa.

## Vantaggi dei Descriptor
- Backup completo: racchiudono tutte le informazioni necessarie par ricostruire un wallet senza tentativi.
- Compatibilità: ideali par wallet watch-only, dove si monitorano i fondi senza ciavi private.
- Flessibilità: supportano single-sig, multisig e script complessi.
- Privacy: no rivelano segreti e possono essere condivisi come na xpub.

## Limiti e compatibilità
No tutti i wallet supportano i descriptor pienamente. Ad esempio, Bitcoin Core ne implementa solo un sottoinsieme e richiede due descriptor separati par indirizzi e change. Software come Sparrow o Specter offrono un supporto migliore, permettendo de importare/esportare descriptor e visualizzarne la struttura.

Esperimenti possono essere fatti co:
- Sparrow: supporta i descriptor, co un’interfaccia grafica par crearli o analizzarli.
- BDK: libreria co interfaccia a riga de comando par gestire descriptor complessi.
- Testnet/Signet: ambienti sicuri par testare senza rischiare fondi reali.

## Riferimenti

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programma
Sta lezione xe stata realizzata par un Satoshi Spritz Connect.
