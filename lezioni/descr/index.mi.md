# Bitcoin Descriptors

## Introduzion
I Bitcoin Descriptors hinn un standard per descriv completament la struttura de un wallet Bitcoin. Hinn staa introdott per risolv i limitazion de i wallet tradizional e fornì una rappresentazion pù flessibil e potenta de le claav e indirizz Bitcoin.

## Evoluzion de la gestión de wallet

### Prima de BIP-32
Inizialment, i wallet Bitcoin dopraven un approcci sempliz: ogni indirizz aveva la so claav privada indipendenta. Quest creava problem significativ:
- **Backup compless**: Ogni claav doveva vess salvada individualment
- **Gestión difficil**: Aggiung noeuv indirizz richiedeva backup manual
- **Risch de perdita**: Se una claav se perdeva, i fond associad erann persi per semper

### BIP-32 - HD Wallets
BIP-32 ha introdott i **Hierarchical Deterministic (HD) Wallets**, che permetten de derivà un numero infinit de claav da una singola "claav master":
- **Backup sempliz**: Domà la claav master deve vess salvada
- **Gerarchia**: Le claav vegnen organizzad in una struttura ad alber
- **Determinismo**: Le stess claav vegnen sempre generad da la stess seed

### BIP-39 - Mnemonic phrases
BIP-39 ha aggiunt le **mnemonic phrases** (12 o 24 parol) per rendà el backup pù user-friendly:
- **Memorizzazion**: Le parol poden vess ricordad pù facilment
- **Cross-platform**: Le stess parol funzionen su divers wallet
- **Recupero**: El wallet pö vess restaurà da le parol

## Perchè i Descriptors?

Mentre BIP-32 e BIP-39 hann migliorà significativamente la gestión de wallet, anca questi approcci hann limitazion:

### Problem con i wallet tradizional
1. **Descrizion incompleta**: I wallet tradizional minga descrivon completament la struttura
2. **Incompatibilità**: Divers wallet implementen BIP-32 in mod divers
3. **Flessibilità limitada**: Difficil da supportà script compless
4. **Watch-only incomplet**: I wallet watch-only minga poden sempre ricostruì la struttura completa

### Soluzion: i Descriptors
I descriptors risolven questi problem fornend una **descrizion completa e standardizzata** de la struttura del wallet.

## Cossa hinn i Descriptors?

Un descriptor l'è una **stringa testual** che descriv completament come derivà le claav e indirizz de un wallet. La stringa contien tutt le informazion necessari per ricostruì la struttura del wallet.

### Component de base
Un descriptor tipic contien:
- **Tip de script**: P2PKH, P2SH, P2WPKH, P2WSH, P2TR, etc.
- **Extended Public Key (xpub)**: La claav pubblica master
- **Derivation path**: El cammin per derivà le claav specific
- **Range**: L'intervall de indirizz da generà

## Esempi pratici

### Single-sig wallet
```
wpkh([fingerprint/derivation]xpub.../0/*)
```

**Esempi concret**:
```
wpkh([a4b4/84h/0h/0h]xpub6C.../0/*)
```

Quest descriptor descriv:
- `wpkh`: Witness Public Key Hash (Native SegWit)
- `[a4b4/84h/0h/0h]`: Fingerprint e derivation path
- `xpub6C...`: Extended public key
- `/0/*`: Indirizz de riceviment (0) con range infinit (*)

### Multi-sig wallet
```
wsh(multi(2,[fingerprint/derivation]xpub1...,[fingerprint/derivation]xpub2...))
```

**Esempi concret**:
```
wsh(multi(2,[a4b4/84h/0h/0h]xpub6C...,[b5c5/84h/0h/0h]xpub6D...))
```

Quest descriptor descriv:
- `wsh`: Witness Script Hash
- `multi(2,...)`: Multi-signature con 2 de 2 firm
- Do extended public key per i do partecipant

### Script compless
```
wsh(and_v(v:pk([fingerprint/derivation]xpub.../0/*),older(52560)))
```

Quest descriptor implementa un **timelock**: la transazion pö vess spess domà dopo 52560 blocch (circa un agn).

## Vantagg de i Descriptors

### 1. Backup completo
Un descriptor contien tutt le informazion necessari per ricostruì el wallet:
- Struttura de le claav
- Tip de script
- Derivation path
- Configurazion de multi-sig

### 2. Compatibilità
I descriptors hinn uno standard, quindi funzionen su divers wallet:
- Bitcoin Core
- Sparrow
- Specter
- BDK (Bitcoin Development Kit)

### 3. Flessibilità
I descriptors permetten script molt compless:
- Multi-signature
- Timelock
- Escrow
- Covenants (quand disponibil)

### 4. Privacy
I descriptors permetten wallet watch-only complet:
- Tutti i indirizz poden vess generad
- Le transazion poden vess monitorad
- La struttura completa l'è visibil

## Limitazion e compatibilità

### Wallet che supporten descriptors
- **Bitcoin Core**: Support complet
- **Sparrow**: Support complet
- **Specter**: Support complet
- **BDK**: Support complet

### Wallet con support limità
- **Electrum**: Support parzial
- **Blue Wallet**: Support limità
- **Mobile wallet**: Generalment minga support

### Wallet minga compatibil
- **Hardware wallet**: Generalment minga support direct
- **Exchange wallet**: Minga support
- **Custodial wallet**: Minga applicabil

## Implementazion pratica

### Bitcoin Core
```bash
# Importa un descriptor
bitcoin-cli importdescriptors '[{"desc":"wpkh([a4b4/84h/0h/0h]xpub6C.../0/*)","timestamp":"now"}]'

# Lista i descriptors importad
bitcoin-cli listdescriptors
```

### Sparrow
1. Vèrt Sparrow
2. Crea un noeuv wallet
3. Scegli "Import Descriptor"
4. Incolla el descriptor
5. Configura el wallet

### Specter
1. Vèrt Specter
2. Crea un noeuv wallet
3. Scegli "Import from descriptor"
4. Inseriss el descriptor
5. Configura i partecipant (per multi-sig)

## Cas d'us avanzad

### Multi-sig con hardware wallet
```
wsh(multi(2,[fingerprint/derivation]xpub1...,[fingerprint/derivation]xpub2...))
```

Quest permet de combinà:
- Una claav su hardware wallet
- Una claav su software wallet
- Maggior sicurezza

### Timelock per eredità
```
wsh(and_v(v:pk([fingerprint/derivation]xpub.../0/*),older(52560)))
```

Quest permet de creà fond che poden vess spess domà dopo un cert temp.

### Escrow con multi-sig
```
wsh(multi(2,[fingerprint/derivation]xpub1...,[fingerprint/derivation]xpub2...,[fingerprint/derivation]xpub3...))
```

Quest permet de creà un escrow con un terz arbitro.

## Best practices

### 1. Backup sicur
- Salva i descriptors in locazion sicur
- Usa backup multipl
- Testa el backup regolarment

### 2. Documentazion
- Documenta la struttura del wallet
- Spiega el significat de ogni component
- Mantegn aggiornad la documentazion

### 3. Test
- Testa i descriptors su testnet
- Verifica la compatibilità
- Controlla le funzionalità

### 4. Sicurezza
- Usa hardware wallet quand possibil
- Implementa multi-sig per fond important
- Considera timelock per fond long-term

## Conclusión

I Bitcoin Descriptors rappresenten un evoluzion significativa nella gestión de wallet Bitcoin. Fornissen:

- **Flessibilità**: Support per script compless
- **Compatibilità**: Standard cross-platform
- **Sicurezza**: Backup complet e sicur
- **Privacy**: Wallet watch-only complet

Mentre minga tutt i wallet supporten ancora descriptors, l'adopzion l'è in cresciuta e rappresenta el futur de la gestión de wallet Bitcoin.

Per inizià con descriptors, raccomandi de:
1. Studiar la documentazion ufficial
2. Sperimentar su testnet
3. Usar wallet che supporten descriptors
4. Implementar gradualment in wallet esistent

I descriptors hinn uno strument potente che permet de sfruttà tutt le capacità del protocoll Bitcoin, dalla sempliz single-sig ai script pù compless e avanzad. 