#Descriptor
I descriptor sono un concetto relativamente nuovo e non ancora molto diffuso, ma utile per descrivere la struttura dei wallet Bitcoin. I descriptor sono stringhe di caratteri leggibili (alfanumerici, esadecimali e alcuni simboli come parentesi), progettate per rappresentare in modo chiaro e standardizzato un wallet, ovvero l’insieme di chiavi pubbliche e private necessarie per calcolare saldi, ricevere e spendere Bitcoin.

## Evoluzione della gestione dei wallet
Per contestualizzare i descriptor, il relatore ripercorre l’evoluzione dei wallet:

- Primi wallet (pre-BIP-32): nei primi tempi, con Bitcoin Core, i wallet erano file contenenti chiavi generate casualmente. Ogni volta che si esaurivano gli indirizzi, ne venivano aggiunti di nuovi, rendendo necessario un backup frequente per non perdere fondi. Questo sistema era inefficiente.
- BIP-32 (HD Wallet): con l’introduzione della generazione gerarchica deterministica, un seed (seme) generava una chiave master, da cui derivavano tutti gli indirizzi. Bastava fare il backup del seed, ma non era ancora una soluzione completa.
- Mnemoniche (BIP-39): successivamente, il seed è stato derivato da una sequenza di 12 o 24 parole (mnemonica), più facile da salvare. Tuttavia, per ricostruire un wallet, servivano anche informazioni sui percorsi di derivazione (es. Legacy, SegWit), altrimenti i fondi potevano risultare irreperibili.

La sola mnemonica non basta, soprattutto per wallet complessi come i multisig (che richiedono più firme) o quelli con script avanzati (es. timelock o condizioni di eredità). Alcuni wallet tentano tutte le derivazioni possibili per trovare i fondi, mentre altri (es. Electrum) richiedono di specificare il tipo di wallet. Nei multisig, inoltre, servono le chiavi pubbliche degli altri partecipanti, complicando ulteriormente il backup.

## Cosa sono i Descriptor e perché servono
I descriptor nascono per superare questi limiti, offrendo una descrizione completa e flessibile della struttura di un wallet. Non sostituiscono la mnemonica, ma la integrano, includendo:

- Chiavi pubbliche estese (xpub, ypub, ecc.).
- Percorsi di derivazione (es. m/44'/0'/0' per Legacy).
- Eventuali script o condizioni di spesa (es. multisig, timelock).

##Esempi pratici
- Single-sig Legacy: Un descriptor semplice potrebbe essere `pk([fingerprint/derivation]xpub...)`, dove:
1. pk indica una chiave pubblica.
2. [fingerprint/derivation] specifica la chiave master e il percorso.
3. xpub genera gli indirizzi (es. 0/* per ricevere, 1/* per il change).
- Multisig: Un esempio è `sortedmulti(2, xpub1, xpub2, xpub3)`, che descrive un wallet 2-di-3, ordinando le chiavi per consistenza.
- Script complessi: Con script come p2sh (pay to script hash) o p2wsh (pay to witness script hash), si possono includere condizioni avanzate, come timelock o combinazioni logiche (and, or).

## Descriptor e Taproot
Un caso interessante è il descriptor per Taproot (tr), che supporta due modalità di spesa:

- Firma diretta con una chiave specifica.
- Un albero di condizioni (es. eredità o timelock), mantenendo la complessità nascosta sulla blockchain fino alla spesa.

## Vantaggi dei Descriptor
- Backup completo: racchiudono tutte le informazioni necessarie per ricostruire un wallet senza tentativi.
- Compatibilità: ideali per wallet watch-only, dove si monitorano i fondi senza chiavi private.
- Flessibilità: supportano single-sig, multisig e script complessi.
- Privacy: non rivelano segreti e possono essere condivisi come una xpub.

## Limiti e compatibilità
Non tutti i wallet supportano i descriptor pienamente. Ad esempio, Bitcoin Core ne implementa solo un sottoinsieme e richiede due descriptor separati per indirizzi e change. Software come Sparrow o Specter offrono un supporto migliore, permettendo di importare/esportare descriptor e visualizzarne la struttura.

Esperimenti possono essere fatti con:
- Sparrow: supporta i descriptor, con un’interfaccia grafica per crearli o analizzarli.
- BDK: libreria con interfaccia a riga di comando per gestire descriptor complessi.
- Testnet/Signet: ambienti sicuri per testare senza rischiare fondi reali.

#Riferimenti
- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

#Programma
Questa lezione è stata realizzata per un Satoshi Spritz Connect.