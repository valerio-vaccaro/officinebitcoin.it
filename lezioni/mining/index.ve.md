# Introduzion al Mining
El mining de Bitcoin xe un process fondamental del protocollo che serv a proponer un ordin tra le transazion present nella mempool, scernendone un sotinsem par crear un novo blocco e aggiornar l'stat de la blockchain.

El mining xe progettao par esser decentralizao e casual (tra virgolette, poiché basao su un puzzle crittografich), evitando inscì na gestione centralizaa de le transazion.

## Scopo del Mining
El mining risolve problemi legai a la centralizazion, come:

- Censura: un ent central podarìa blocar quaj transazion, ma con miner decentralizai le transazion ghe pù possibilitaa de esser incluse.
- Doppia spesa: senza un miner corrompibil, xe difficil riscrivere la storia o favorir na transazion a scapit de n'altra.
- Timestamping: forniss un ordin temporal segur e condiviso, minga dipendente da n'autoritaa central, ma dal consenso tra miner e nodi.

# Come Funziona el Mining
El process de mining se pò spiegà passo par passo:

- Scelta de le transazion: el miner scern le transazion dalla mempool, spess privilegiando quelle con fee pù alte, ottimizzando el profit (un problem NP-complet simil al "riempimento del saco").
- Costruzion de la Coinbase: el miner crea na transazion special (coinbase) che assegna a sé stess el premio del blocco (attualmente 3,125 BTC, dimezzao ogni quatro anni) pù le commiss (fee) de le transazion scernide.
- Merkle Root: le transazion scernide vegnarà organizzae in na struttura dati ad albero (Merkle Tree), che genera un Merkle Root, un hash che rappresenta tuti le transazion e el so ordin.
- Header del Blocco: el miner costruiss el prototipo de l'header del blocco, includendo:
1. El timestamp.
2. L'hash del blocco precedente.
3. El Merkle Root.
4. La difficoltaa (target), che dipend dalla rete.
5. Un nonce (numer casual inizializao, par esempi, a zero).
- Puzzle Crittografich: El miner aplica do volte l'algoritmo SHA-256 all'header e verifica se el resultat ghe un numer sufficient de zero inissiali (inferior a la soglia de difficoltaa). Se no lo xe, modifica el nonce o altri campi (es. timestamp o ordin de le transazion) e repeta el calcolo. Quest xe un lavor de forza bruta senza scorciatoie, grazi a le proprietaa de SHA-256.

## Ottimizzazion
Par velocizzar el process, i miner pò calculà el primo SHA-256 sui primi 64 byte de l'header (immutabili) e poeu iterà solo sul resto, cambiando el nonce. La specializazion ga portao a hardware (ASIC) che eseguiss miliardi de tentativi al secondo.

# Process de Validazion
Quand un miner trova na soluzion, trasmet el blocco complet (header + transazion) alla rete. I nodi validaa:
- l'hash de l'header (un solo SHA-256 par confermar).
- la correttezza de le informazion del blocco (timestamp, hash del blocco precedente, Merkle Root e nonce).
- la riproducibilitaa del Merkle Root dopo aver controllao la correttezza de tuti le transazion associade.

Se valido, el blocco ven aggiunto alla blockchain. El premio (coinbase + fee) xe spendibil solo dopo 100 conferme (circa 16 ore), par garantir stabilitaa.

# Costi e Ricompense del Mining
Costi:

- Corrent elettrica: cost variabil principal.
- Hardware: ASIC costosi e a vita breva, rapidamente superai da modeli pù efficienti.
- Infrastrutture: raffreddamento, installazion, manutenzion (es. pannelli solari no xe "gratis").

Ricompense:

- Premio fisso (dimezzao nel 2024 a 3,125 BTC).
- Fee variabili de le transazion.

El miner dev rispettar le regole del consenso: un blocco minga valido ven scartao, sprecando risorse senza ricompensa. Anca un blocco valido pò esser "orfanao" se un altro miner venc la gara, causando perdite.

## Strategia Economica
El mining xe competitivo: i miner cerca de massimizzar el tempo de attività par ammortizzar i costi fissi. Usi spot (es. accender i miner solo con energia in eccesso) xe poco pratici, poiché i costi inissiali richiede continuitaa. El ritorno sull'investimento pò esser longo e incerto.

# Mining in Solo e Pool

- Solo Mining: el miner lavora da solo, costruendo el blocco con un full node o software personalizao. Se trova un blocco, pren tuto el premio, ma la probabilità xe bassissima (poderess voler secoli con un singolo ASIC).
- Pool Mining: protocolli come Stratum permetta ai miner de collaborar:
1. La pool forniss un template (coinbase, Merkle Root, ecc.).
2. I miner invia share (tentativi con un certo numer de zero, inferiori a la difficoltaa del blocco) come prova de lavor.
3. Quand un miner de la pool trova un blocco, el premio ven diviso proporzionalmente a le share inviae.
- Stratum v2: Evoluzion che permetta ai miner de scernir le transazion, riducendo la centralizazion de la pool, anca se richiede controlli par garantir la correttezza (es. fee par la pool).

# Stima de l'Hashrate
L'hashrate (potenza de calcolo) se stima:
- In una Pool: Contando le share ricevue in un'unitaa de tempo, moltiplicade par la difficoltaa de le share. L'è na stima perturbabile dalla fortuna.
- Globale: Usando la difficoltaa de Bitcoin e el tempo medio tra blocchi (circa 10 minuti). Oscillazion xe normali, ma la media xe affidabile.

Hardware come Nerd Miner usa contatori interni par dati precisi, mentre le pool se basa su stime pù variabili, visibili nei grafici oscillanti.

# Programma
Questa lezion xe stada realizzaa par un Satoshi Spritz Connect. 