# El ciclo de vita de na transazion Bitcoin

## Introduzion
Na transazion Bitcoin xe na struttura de dati che descrive el trasferimento de valore da un o più indirisi (input) a un o più indirisi (output). El ciclo de vita de na transazion Bitcoin xe composto da diverse fasi che vanno da la creazion a la conferma definitiva.

## Fasi del ciclo de vita

### 1. Creazion
La prima fase xe la creazion de la transazion. L'utente, tramite un wallet, crea na transazion specificando:
- I input (UTXO da spender)
- I output (indirisi de destinazion e quantità)
- Le fee de transazion

### 2. Firma
Prima de esser inviada, la transazion deve esser firmada con le chiavi private corrispondenti ai input. La firma prova che l'utente xe el proprietario legitimo dei fondi.

### 3. Broadcast
Una volta firmada, la transazion xe inviada (broadcast) a la rete Bitcoin. El wallet la invia a uno o più nodi, che la propagano ulteriormente.

### 4. Validazion
I nodi de la rete validano la transazion verificando:
- La correttezza de le firme
- La disponibilità dei fondi
- La conformità a le regole del protocollo
- Le dimensioni e le fee

### 5. Mempool
Se valida, la transazion xe inserida nel mempool (memory pool) de i nodi. El mempool xe na coda temporanea de transazioni in attesa de esser incluse in un blocco.

### 6. Mining
I miner selezionano transazioni dal mempool par includerle in un blocco. Le transazioni con fee più alte hanno priorità maggiore.

### 7. Conferma
Quando un miner trova na soluzion valida, el blocco xe propagato a la rete. La transazion riceve la prima conferma.

### 8. Conferme multiple
Ogni blocco successivo che xe minato sopra el blocco che contien la transazion aggiunge na conferma. Più conferme = maggiore sicurezza.

## Problemi e soluzioni

### Transazioni non confermate
Se na transazion rimane nel mempool par troppo tempo, può esser rimossa. Soluzioni:
- **RBF (Replace By Fee)**: Crear na nova transazion con fee più alte
- **CPFP (Child Pays For Parent)**: Crear na transazion figlia che paga fee più alte

### Doppia spesa
Teoricamente possibile ma praticamente impossibile con conferme sufficienti.

## Tempi tipici
- **Broadcast**: Secondi
- **Prima conferma**: ~10 minuti (media)
- **6 conferme**: ~1 ora (considerada sicura)
- **Conferme definitive**: 100+ conferme

## Monitoraggio
I utenti possono monitorar le transazioni tramite:
- Explorer de blocco
- Wallet
- API de nodi
- Servizi online

## Conclusione
El ciclo de vita de na transazion Bitcoin xe na combinazion de crittografia, economia e consenso distribuito che garantisce la sicurezza e l'immutabilità del sistema. 