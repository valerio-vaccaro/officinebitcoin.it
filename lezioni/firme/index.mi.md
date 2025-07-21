# Firme Digitali in Bitcoin (ECDSA)

## Introduzion
Le firme digitali hann un rol fondamental nel protocoll Bitcoin, permettend di autenticà transazion e assicurà che solt i proprietari de le claav privad possen spend i fond associad. In questa lezion, esplorerem i concett fondamental de le firme digitali, con particolare attenzion a l'algoritmo ECDSA (Elliptic Curve Digital Signature Algorithm) doprad da Bitcoin.

## Cossa hinn le Firme Digitali?

Una **firma digital** l'è un meccanism matematic che permet de:
1. **Verificà l'autenticità** de un messagg o documento
2. **Assicurà l'integrità** de i dat (che minga sien staa alterad)
3. **Garantì la non-repudiazione** (l'autor minga pö negà de aver firmà)

### Differenz con le firme tradizional

| Aspett | Firma tradizional | Firma digital |
|--------|-------------------|---------------|
| **Supporto fisic** | Carta, penna | Dat digital |
| **Copiabilità** | Difficil da copià | Facil da copià |
| **Verifica** | Confronto visivo | Algoritmo matematic |
| **Sicurezza** | Basad su caratteristiche fisiche | Basad su crittografia |
| **Scalabilità** | Limitada | Alta |

## Criptografia a Claav Pubblica/Privada

Le firme digitali hann basad su la **criptografia asimmetrica**, che dopra do claav matematicament correlad:

### Claav Privada
- **Segreta**: Domà el proprietari la conoss
- **Firma**: Usada per firmà messagg
- **Sicurezza**: Deve vess protetta a ogni cost

### Claav Pubblica
- **Pubblica**: Chiunque la pö conoss
- **Verifica**: Usada per verificà le firme
- **Distribuzion**: Pö vess condivisa liberament

### Funzionament

```
Messaggio + Claav Privada → Firma Digital
Messaggio + Firma + Claav Pubblica → Verifica (Vera/Falsa)
```

## ECDSA in Bitcoin

Bitcoin dopra **ECDSA** (Elliptic Curve Digital Signature Algorithm) con la curva **secp256k1** per generà e verificà le firme.

### Vantagg de ECDSA

1. **Efficienza**: Le claav ECDSA hann pù cort de quelle RSA per la stess sicurezza
2. **Velocità**: Le operazion de firm e verifica hann pù veloci
3. **Sicurezza**: La sicurezza l'è basad su la difficoltà del problema del logaritmo discreto su curve ellittiche

### Process de Firm

1. **Hash del messaggio**: El messaggio vegn convertì in un hash (SHA-256)
2. **Generazion di parametri**: Se generen parametri casual per la firma
3. **Calcolo della firma**: Se calcola la firma doprand la claav privada
4. **Output**: La firma consist in do numer (r, s)

### Process de Verifica

1. **Hash del messaggio**: Se calcola l'hash del messaggio original
2. **Calcolo di parametri**: Se calcolen parametri derivad dalla firma
3. **Verifica**: Se verifica se la firma l'è valida doprand la claav pubblica
4. **Risultat**: Vera o Falsa

## Applicazion in Bitcoin

### Autenticazion de Transazion

In Bitcoin, le firme digitali hann doprad per autenticà le transazion:

```
Transazione + Claav Privada → Firma Digital
Transazione + Firma + Claav Pubblica → Verifica
```

### UTXO e Firme

Ogni UTXO (Unspent Transaction Output) l'è associà a una claav pubblica. Per spend un UTXO, te devi:

1. **Creà una transazion** che referenzia l'UTXO
2. **Firmà la transazion** con la claav privada corrispondent
3. **Includ la firma** nella transazion
4. **Includ la claav pubblica** per permet la verifica

### Esempi pratici

#### Transazion P2PKH (Pay to Public Key Hash)

```
Input:
  - UTXO: 0.1 BTC
  - ScriptSig: <Firma> <Claav Pubblica>

Output:
  - ScriptPubKey: OP_DUP OP_HASH160 <Hash Claav Pubblica> OP_EQUALVERIFY OP_CHECKSIG
```

#### Process de Verifica

1. Se estrae la claav pubblica dal ScriptSig
2. Se calcola l'hash de la claav pubblica
3. Se confronta con l'hash nel ScriptPubKey
4. Se verifica la firma doprand la claav pubblica

## SIGHASH Flags

Bitcoin supporta divers tip de firme attraverso i **SIGHASH flags**, che determinan quell part de la transazion vegn firmada:

### SIGHASH_ALL (Default)
- **Cosa se firma**: Tutti i input e output
- **Flessibilità**: Bass
- **Sicurezza**: Alt
- **Uso**: Transazion standard

### SIGHASH_NONE
- **Cosa se firma**: Tutti i input, nissun output
- **Flessibilità**: Alt
- **Sicurezza**: Bass
- **Uso**: Transazion malleabil

### SIGHASH_SINGLE
- **Cosa se firma**: Tutti i input, un output specific
- **Flessibilità**: Media
- **Sicurezza**: Media
- **Uso**: Transazion con output multipl

### SIGHASH_ANYONECANPAY
- **Cosa se firma**: Domà l'input specific
- **Flessibilità**: Molt alt
- **Sicurezza**: Bass
- **Uso**: CoinJoin, transazion collaborativ

### Combinazion

I flag poden vess combinad:
- `SIGHASH_ALL | SIGHASH_ANYONECANPAY`: Firma domà l'input specific
- `SIGHASH_NONE | SIGHASH_ANYONECANPAY`: Firma domà l'input, permet modifiche a output

## Firmà Messagg Arbitrari

Oltra a firmà transazion, te pödet anca firmà messagg arbitrari con le tue claav Bitcoin:

### Format de Messagg

Bitcoin usa un format standard per i messagg da firmà:

```
Bitcoin Signed Message:
<Messaggio>
```

### Esempi de Codice

#### Firmà un Messaggio (Python)

```python
import hashlib
from bitcoin import *

# Messaggio da firmare
message = "Hello, Bitcoin!"

# Claav privada (in formato WIF)
private_key = "5KJvsngHeMpm884wtkJNzQGaCErckhHJBGFsvd3VyK5qMZXj3hS"

# Formatta il messaggio
formatted_message = f"Bitcoin Signed Message:\n{message}"
message_hash = hashlib.sha256(formatted_message.encode()).digest()

# Firma il messaggio
signature = ecdsa_raw_sign(message_hash, private_key)

print(f"Firma: {signature}")
```

#### Verificà una Firma (Python)

```python
import hashlib
from bitcoin import *

# Messaggio originale
message = "Hello, Bitcoin!"

# Claav pubblica
public_key = "04a1b2c3d4e5f6..."

# Firma
signature = "3045022100..."

# Formatta il messaggio
formatted_message = f"Bitcoin Signed Message:\n{message}"
message_hash = hashlib.sha256(formatted_message.encode()).digest()

# Verifica la firma
is_valid = ecdsa_raw_verify(message_hash, signature, public_key)

print(f"Firma valida: {is_valid}")
```

## Sicurezza e Best Practices

### Minacce Comuni

1. **Replay Attack**: Reinvio de transazion firmad
2. **Malleability**: Modifiche non autorizzad a transazion
3. **Key Reuse**: Doprà la stess claav per pù transazion
4. **Side-channel Attack**: Attacc basad su caratteristiche fisiche

### Misure de Sicurezza

1. **Claav Uniche**: Usa claav divers per ogni transazion
2. **Hardware Wallet**: Conserva claav privad su dispositiv sicur
3. **Backup Sicur**: Fà backup de claav in locazion sicur
4. **Verifica**: Semper verifica le transazion prima de firmàle

### Validazion de Firma

Prima de accettà una transazion, Bitcoin Core verifica:

1. **Formato**: La firma l'è nel format corrett
2. **Curva**: La firma l'è generata con secp256k1
3. **Verifica**: La firma l'è matematicament valida
4. **Autorizzazion**: La claav pubblica autorizza la spesa

## Limitazion e Considerazion

### Limitazion de ECDSA

1. **Malleability**: Le firme ECDSA poden vess malleabil
2. **Quantum Resistance**: ECDSA minga l'è resistent a computer quantistic
3. **Determinismo**: Le firme ECDSA hann non-deterministiche

### Alternative

1. **Schnorr Signatures**: Firma pù efficient e sicur
2. **Taproot**: Implementazion de Schnorr in Bitcoin
3. **Multi-signature**: Firma con pù claav

## Implementazion Pratica

### Firmà Transazion con Bitcoin Core

```bash
# Crea una transazione raw
bitcoin-cli createrawtransaction '[{"txid":"...","vout":0}]' '{"address":0.1}'

# Firma la transazione
bitcoin-cli signrawtransactionwithwallet "raw_transaction_hex"

# Invia la transazione
bitcoin-cli sendrawtransaction "signed_transaction_hex"
```

### Verificà Firma con Bitcoin Core

```bash
# Verifica una transazione
bitcoin-cli getrawtransaction "txid" true

# Verifica un messaggio firmato
bitcoin-cli verifymessage "address" "signature" "message"
```

## Conclusión

Le firme digitali ECDSA hann un component fondamental del protocoll Bitcoin, permettend di autenticà transazion e assicurà la sicurezza de la rete. La comprension de come funzionen l'è essenzial per sviluppator e utent che vören interagì con Bitcoin a livell avanzà.

Con l'evoluzion de Bitcoin e l'introduzion de tecnologie come Schnorr signatures e Taproot, le capacità de firm digital continuen a migliorà, offrend maggior sicurezza, efficienza e flessibilità.

Per approfondì l'argoment, raccomandi de:
1. Studiar la matematica de le curve ellittiche
2. Sperimentar con librerie crittografiche
3. Implementar sistemi de firm personalizzad
4. Seguì gli sviluppi de Bitcoin Core 