# Firma digitale in Bitcoin (ECDSA)

## Introduzion
Le firme digitali xe na componente fondamentale de Bitcoin che permet de provar l'autenticità de le transazioni e l'identità del mittente. In questa lezion esploreremo come funziona ECDSA (Elliptic Curve Digital Signature Algorithm) in Bitcoin.

## Concetto de firma digitale

### Differenza da le firme fisiche
- **Firma fisica**: Sempre uguale, indipendente dal contenuto
- **Firma digitale**: Unica par ogni messagio, dipendente dal contenuto

### Proprietà
- **Autenticazion**: Prova l'identità del firmatario
- **Integrità**: Garantisce che il messagio non sia stato modificato
- **Non ripudio**: Impedisce al firmatario di negar la firma

## Criptografia a chiave pubblica

### Chiave privata
- Segreta, conosciuta solo dal proprietario
- Usata par firmar
- Mai condivisa

### Chiave pubblica
- Pubblica, condivisa con tutti
- Usata par verificare le firme
- Derivata dalla chiave privata

### Funzionamento
```
Messagio + Chiave Privata → Firma
Messagio + Firma + Chiave Pubblica → Verifica
```

## ECDSA in Bitcoin

### Curva ellittica
- Bitcoin usa la curva secp256k1
- Equazion: y² = x³ + 7
- Ordine: ~2²⁵⁶

### Generazion de le chiavi
```python
import hashlib
import secrets

# Genera chiave privata casuale
private_key = secrets.randbelow(2**256)

# Calcola chiave pubblica
# (semplificato - in realtà usa moltiplicazion de punto)
public_key = private_key * G  # G xe il punto generatore
```

### Firma
```python
def sign_message(message, private_key):
    # Hash del messagio
    message_hash = hashlib.sha256(message.encode()).digest()
    
    # Genera k casuale
    k = secrets.randbelow(2**256)
    
    # Calcola R = k * G
    R = k * G
    
    # Calcola S = k⁻¹ * (hash + private_key * R_x) mod n
    S = (pow(k, -1, n) * (int.from_bytes(message_hash, 'big') + private_key * R[0])) % n
    
    return (R[0], S)
```

### Verifica
```python
def verify_signature(message, signature, public_key):
    R, S = signature
    message_hash = hashlib.sha256(message.encode()).digest()
    
    # Calcola w = S⁻¹ mod n
    w = pow(S, -1, n)
    
    # Calcola u1 = hash * w mod n
    u1 = (int.from_bytes(message_hash, 'big') * w) % n
    
    # Calcola u2 = R * w mod n
    u2 = (R * w) % n
    
    # Calcola P = u1 * G + u2 * public_key
    P = u1 * G + u2 * public_key
    
    # Verifica che P_x = R
    return P[0] == R
```

## SIGHASH flags

### SIGHASH_ALL (default)
- Firma tutti gli input e output
- Più sicuro, meno flessibile

### SIGHASH_NONE
- Firma solo gli input
- Output possono esser modificati
- Pericoloso

### SIGHASH_SINGLE
- Firma input e output corrispondente
- Altri output possono esser modificati

### ANYONECANPAY
- Combinabile con altri flag
- Permette di aggiunger input
- Usato par CoinJoin

## Firma de messagi arbitrari

### Bitcoin Message Signing
```python
def sign_bitcoin_message(message, private_key):
    # Formato Bitcoin
    bitcoin_message = f"\x18Bitcoin Signed Message:\n{len(message)}"
    bitcoin_message += message
    
    # Hash doppio
    hash1 = hashlib.sha256(bitcoin_message.encode()).digest()
    hash2 = hashlib.sha256(hash1).digest()
    
    # Firma
    return sign_message(hash2, private_key)
```

### Verifica
```python
def verify_bitcoin_message(message, signature, public_key):
    # Stesso processo de firma
    bitcoin_message = f"\x18Bitcoin Signed Message:\n{len(message)}"
    bitcoin_message += message
    
    hash1 = hashlib.sha256(bitcoin_message.encode()).digest()
    hash2 = hashlib.sha256(hash1).digest()
    
    return verify_signature(hash2, signature, public_key)
```

## Sicurezza

### Attacchi comuni
- **Replay attack**: Riutilizzo de firme
- **Malleability**: Modifica de firme valide
- **Nonce reuse**: Riutilizzo del valore k

### Best practices
- Usa sempre k casuale
- Verifica le firme
- Non riutilizzare chiavi
- Mantien le chiavi private sicure

## Applicazioni in Bitcoin

### Transazioni
- Firma de input
- Autorizazion de spesa
- Verifica de proprietà

### Messagi
- Prova de proprietà de indirisi
- Autenticazion
- Comunicazion sicura

### Smart contracts
- Multi-sig
- Time-locks
- Condizioni complesse

## Conclusione
Le firme digitali ECDSA xe na componente critica de Bitcoin che garantisce sicurezza e autenticità. La comprension de come funzionano xe essenziale par sviluppatori e utenti avanzati. 