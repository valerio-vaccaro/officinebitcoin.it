# Introduzione al Mining
Il mining di Bitcoin è un processo fondamentale del protocollo che serve a proporre un ordine tra le transazioni presenti nella mempool, selezionandone un sottoinsieme per creare un nuovo blocco e aggiornare lo stato della blockchain.

Il mining è progettato per essere decentralizzato e casuale (tra virgolette, poiché basato su un puzzle crittografico), evitando così una gestione centralizzata delle transazioni.

##Scopo del Mining
Il mining risolve problemi legati alla centralizzazione, come:

- Censura: un ente centrale potrebbe bloccare alcune transazioni, ma con miner decentralizzati le transazioni hanno più possibilità di essere incluse.
- Doppia spesa: senza un miner corrompibile, è difficile riscrivere la storia o favorire una transazione a scapito di un’altra.
- Timestamping: fornisce un ordine temporale sicuro e condiviso, non dipendente da un’autorità centrale, ma dal consenso tra miner e nodi.

# Come Funziona il Mining
Il processo di mining può essere spiegato passo per passo:

- Scelata delle transazioni: il miner sceglie le transazioni dalla mempool, spesso privilegiando quelle con fee più alte, ottimizzando il profitto (un problema NP-completo simile al “riempimento dello zaino”).
- Costruzione della Coinbase: il miner crea una transazione speciale (coinbase) che assegna a sé stesso il premio del blocco (attualmente 3,125 BTC, dimezzato ogni quattro anni) più le commissioni (fee) delle transazioni selezionate.
- Merkle Root: le transazioni scelte vengono organizzate in una struttura dati ad albero (Merkle Tree), che genera un Merkle Root, un hash che rappresenta tutte le transazioni e il loro ordine.
- Header del Blocco: il miner costruisce il prototipo dell’header del blocco, includendo:
1. Il timestamp.
2. L’hash del blocco precedente.
3. Il Merkle Root.
4. La difficoltà (target), che dipende dalla rete.
5. Un nonce (numero casuale inizializzato, ad esempio, a zero).
- Puzzle Crittografico: Il miner applica due volte l’algoritmo SHA-256 all’header e verifica se il risultato ha un numero sufficiente di zeri iniziali (inferiore alla soglia di difficoltà). Se non lo è, modifica il nonce o altri campi (es. timestamp o ordine delle transazioni) e ripete il calcolo. Questo è un lavoro di forza bruta senza scorciatoie, grazie alle proprietà di SHA-256.

## Ottimizzazioni
Per velocizzare il processo, i miner possono calcolare il primo SHA-256 sui primi 64 byte dell’header (immutabili) e poi iterare solo sul resto, cambiando il nonce. La specializzazione ha portato a hardware (ASIC) che eseguono miliardi di tentativi al secondo.

# Processo di Validazione
Quando un miner trova una soluzione, trasmette il blocco completo (header + transazioni) alla rete. I nodi validano:
- l’hash dell’header (un solo SHA-256 per confermare).
- la correttezza delle informazioni del blocco (timestamp, hash del blocco precedente, Merkle Root e nonce).
- la riproducibilità del Merkle Root dopo aver controllato la correttezza di tutte le transazioni associate.

Se valido, il blocco viene aggiunto alla blockchain. Il premio (coinbase + fee) è spendibile solo dopo 100 conferme (circa 16 ore), per garantire stabilità.

# Costi e Ricompense del Mining
Costi:

- Corrente elettrica: costo variabile principale.
- Hardware: ASIC costosi e a vita breve, rapidamente superati da modelli più efficienti.
- Infrastrutture: raffreddamento, installazione, manutenzione (es. pannelli solari non sono “gratis”).

Ricompense:

- Premio fisso (dimezzato nel 2024 a 3,125 BTC).
- Fee variabili delle transazioni.

Il miner deve rispettare le regole del consenso: un blocco non valido viene scartato, sprecando risorse senza ricompensa. Anche un blocco valido può essere “orfanato” se un altro miner vince la gara, causando perdite.

## Strategia Economica
Il mining è competitivo: i miner cercano di massimizzare il tempo di attività per ammortizzare i costi fissi. Usi spot (es. accendere i miner solo con energia in eccesso) sono poco pratici, poiché i costi iniziali richiedono continuità. Il ritorno sull’investimento può essere lungo e incerto.

# Mining in Solo e Pool

- Solo Mining: il miner lavora da solo, costruendo il blocco con un full node o software personalizzato. Se trova un blocco, prende tutto il premio, ma la probabilità è bassissima (potrebbero volerci secoli con un singolo ASIC).
- Pool Mining: protocolli come Stratum permettono ai miner di collaborare:
1. La pool fornisce un template (coinbase, Merkle Root, ecc.).
2. I miner inviano share (tentativi con un certo numero di zeri, inferiori alla difficoltà del blocco) come prova di lavoro.
3. Quando un miner della pool trova un blocco, il premio viene diviso proporzionalmente alle share inviate.
- Stratum v2: Evoluzione che consente ai miner di scegliere le transazioni, riducendo la centralizzazione della pool, anche se richiede controlli per garantire la correttezza (es. fee per la pool).

# Stima dell’Hashrate
L’hashrate (potenza di calcolo) si stima:
- In una Pool: Contando le share ricevute in un’unità di tempo, moltiplicate per la difficoltà delle share. È una stima perturbabile dalla fortuna.
- Globale: Usando la difficoltà di Bitcoin e il tempo medio tra blocchi (circa 10 minuti). Oscillazioni sono normali, ma la media è affidabile.

Hardware come Nerd Miner usa contatori interni per dati precisi, mentre le pool si basano su stime più variabili, visibili nei grafici oscillanti.

#Programma
Questa lezione è stata realizzata per un Satoshi Spritz Connect.
