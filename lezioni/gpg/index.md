# Tutorial GPG:

Questa lezione ti guida attraverso l'uso di Gnu Privacy Guard (GPG):
- per creare una nuova coppia di chiavi, 
- aggiungere sottochiavi per firma e crittografia, 
- fare il backup di tutte le chiavi, 
- trasferire le sottochiavi su un YubiKey e 
- crittografare/firmare un file usando Yubikey.

È progettato per Linux on comandi testati su GPG 2.2.40/Debian 12. Gli stessi comandi possono funzionare similmente su altre versioni di Linux e anche su MacOsX e Windows (ad eccezione dei filesystem crittografati).

Il processo segue le migliori pratiche di sicurezza, come la generazione delle chiavi offline e backup sicuri.

## Installazione
Installa gpg e le utilities necessarie

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Assicurati che la versione sia 2.1.17 o successiva (2.4.5 consigliata).

```bash
gpg --version
```

Verifica il funzionamento della YubiKey

```bash
ykman info
```

Assicurati che l'applet OpenPGP sia abilitata e la modalità CCID attiva.

Usa una macchina air-gapped (senza internet) per generare le chiavi e prevenire perdite.

Ricorda che i PIN YubiKey di default non sono sicuri e sono:
- PIN Utente predefinito: 123456
- PIN Admin predefinito: 12345678
Cambiali prima dell'uso (vedi Passo 4).

## Passo 1
Genera una coppia di chiavi GPG primaria (pubblica e privata) per esclusivamente per certificazione (C), da queste discenderanno tutte le altre chiavi che andremo a costruire.

Avvia la Generazione della chiave usando --expert per accedere alle opzioni avanzate.

```bash
gpg --expert --full-gen-key
```


Seleziona il Tipo di Chiave:

```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card
Your selection? 8
```

Scegli (8) RSA (set your own capabilities) per poter customizzare il comportamento della chiave.

Imposta quindi le funzionalità:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Disattiva Sign e Encrypt (premi S, E).

Mantieni Certify (premi Q quando finito).

Come risultato tra le azioni attualmente consentite rimane solo Certify

Imposta la Dimensione della Chiave:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Inserisci 4096 (massimo supportato da YubiKey 4/5).

Imposta la Scadenza:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Inserisci 3y (3 anni) o la tua preferenza. Conferma la data.

Inserisci l'ID Utente:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Fornisci nome ed email. Lascia il commento vuoto. Conferma con O.

Inserisci una passphrase forte (mescola lettere, numeri, simboli; evita parole comuni).

Esempio: Tr0ub4dor&3xplor3r!2025

La passphrase consente di protegge la tua chiave privata.

Genera entropia muovendo il mouse, digita casualmente o usa rng-tools (Linux e solo se ne comprendi bene il funzionamento):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Attendi il completamento della generazione della chiave. Annota l'ID della chiave (es. C2033656849FC82BA3C365E33C9BF8B9CB86875D) dall'output:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Crea un certificato per revocare la chiave se compromessa (anche se il tuo client potrebbe già averla creata):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Scegli il motivo (es. 1 = chiave compromessa) e salva.

## Passo 2
Creare Sottochiavi per Firma e Crittografia, verrano quindi aggiunte due sottochiavi per firma (S) e crittografia (E). 

La chiave primaria resta solo per certificazione.

Modifichiamo la chiave:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Inserisci la passphrase se richiesto.

Aggiungi sottochiave per Firma:

```
gpg> addkey
Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (12) ECC (encrypt only)
  (13) Existing key
  (14) Existing key from card
Your selection? 4
```

Scegli (4) RSA (solo firma).

Imposta dimensione: 4096.

Imposta scadenza: 2y (2 anni, le sottochiavi possono essere ruotate più frequentemente).

Conferma e inserisci la passphrase.

Aggiungi sottochiave per Crittografia:

```
gpg> addkey
```

Scegli (6) RSA (solo crittografia).

Imposta dimensione: 4096.

Imposta scadenza: 2y.

Conferma e inserisci la passphrase.

Salva le Modifiche:

```
gpg> save
```

Verifica le sottochiavi:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Esempio di output:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Annota le impronte delle sottochiavi per firma (S) e crittografia (E).

## Passo 3
Backup di Tutte le ChiaviEsegui il backup della chiave primaria, delle sottochiavi e della chiave pubblica su due unità USB crittografate per sicurezza.

Prepara le Unità USB:Inserisci due unità USB (es. /dev/sdb e /dev/sdc).

Crea partizioni crittografate (es. con LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Ripeti per /dev/sdc1 (es. monta su /mnt/backup2).

Esporta le Chiavi Private:Esporta la chiave primaria e le sottochiavi:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Esporta le chiave pubbliche:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Esporta il Certificato di Revoca:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Smonta in Modo Sicuro:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Ripeti per backup2. Conserva le unità USB in luoghi separati e sicuri (es. cassaforte).

Elimina le Chiavi Locali (Facoltativo):Se usi una macchina air-gapped, elimina la directory GPG:

```bash
rm -rf ~/.gnupg
```

Le chiavi andranno poi importare sulla macchina in cui andrai a usarle.

Se non air-gapped, mantieni le chiavi fino al trasferimento su YubiKey.

## Passo 4
Trasferisci le sottochiavi di firma e crittografia sul YubiKey, mantenendo la chiave primaria offline.

Inserisci Yubikey e verifica:

```bash
gpg --card-status
```

L'output dovrebbe mostrare l'applet OpenPGP (es. Version: 2.0).

Cambia i PIN predefiniti:

```bash
gpg --change-pin
```

PIN Utente: Imposta un nuovo PIN di 6-8 cifre (es. 654321).
PIN Admin: Imposta un nuovo PIN di 8 cifre (es. 87654321).

Modifica la Chiave per il Trasferimento:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Seleziona e Trasferisci la Sottochiave di Firma:Elenca le chiavi per identificare gli indici delle sottochiavi:

```
gpg> list
```

Esempio:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Seleziona la sottochiave di firma:

```
gpg> key 1
```

La sottochiave di firma avrà un asterisco (*).

Trasferisci su YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Inserisci il PIN Admin (es. 87654321). La sottochiave privata di firma viene trasferita sul YubiKey e sostituita da uno stub nel portachiavi.

Seleziona e Trasferisci la Sottochiave di Crittografia:Deseleziona la sottochiave di firma:

```
gpg> key 1
```

Seleziona la sottochiave di crittografia:

```
gpg> key 2
```

Trasferisci su YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Inserisci di nuovo il PIN Admin.

Salva le Modifiche:

```
gpg> save
```

Le sottochiavi private sono ora sul YubiKey, con stub locali.

Verifica YubiKey:

```bash
gpg --card-status
```

Controlla che gli slot Signature key e Encryption key mostrino le impronte digitali delle sottochiavi.

Esporta le sottochiavi private (per verifica del backup):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Elimina la directory GPG locale:

```bash
rm -rf ~/.gnupg
```

Reimporta la chiave pubblica e gli stub:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

La chiave primaria privata non è più sul computer.

## Passo 5
Usa YubiKey per crittografare e firmare un file per un destinatario.

Prepara un File di Prova:

```bash
echo "Questo è un messaggio segreto." > test.txt
```

Ottieni la chiave pubblica del destinatario (es. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Oppure importa da un file:

```bash
gpg --import bob_public.asc
```

Crittografa e Firma:Crittografa per bob@example.com e firma con Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Inserisci il PIN Utente (es. 654321) quando richiesto. 

Se YubiKey richiede la conferma tattile (opzionale, impostata tramite ykman openpgp keys set-touch), tocca YubiKey.

L'output generato sarà test.txt.gpg

Decrittografa il file (richiede YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Inserisci il PIN Utente e tocca Yubikey se necessario. 

Verifica che test_decrypted.txt corrisponda a test.txt.

Bob può decriptare con la sua chiave privata e verificare la tua firma:

```bash
gpg --decrypt test.txt.gpg
```

Se invece vuoi solo firmare il file puoi usare i seguenti comandi.

```bash
gpg --detach-sign test.txt
```

Verrà generato un file di output chiamato test.txt.sig

Per verificarlo:

```bash
gpg --verify test.txt.sig test.txt
```

## Pratiche di sicurezza
- Genera sempre le chiavi su una macchina offline per evitare esposizioni.
- Conserva le unità USB con le chiavi private in luoghi separati e sicuri (es. cassaforte o banca).
- Usa PIN forti e unici. Se i tentativi di PIN sono superati (3 per Utente, 3 per Admin), Yubikey si blocca e richiede un reset, perdendo tutte le chiavi.
- Mantieni revoke.asc accessibile ma sicuro per revocare la chiave se compromessa.
- Crea nuove sottochiavi prima della scadenza (es. ogni anno) in queta maniera:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Trasferisci le nuove sottochiavi sul YubiKey e aggiorna la chiave pubblica sui server:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Usa un secondo YubiKey per ridondanza:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Ripeti i passaggi keytocard per il secondo YubiKey.

Se fosse necessario resettare Yubikey:

```bash
ykman openpgp reset
```

Mentre per ripristina le sottochiavi dal backup:

```bash
gpg --import secret.asc
```

“Chiave Pubblica Non Utilizzabile”:Assicurati che la chiave pubblica del destinatario sia importata e fidata:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Imposta a 5 = Fiducia massima.

