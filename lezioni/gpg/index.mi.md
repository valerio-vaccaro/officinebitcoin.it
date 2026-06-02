---
layout: default
title: "Tutorial GPG e YubiKey"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lezion Bitcoin-only</span> <span>Quest progett l'e mantegnuu da valerio-vaccaro</span></p>

## 🌍 Traduzion

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Tutorial GPG e YubiKey

Questa lezion te guida attraverso l'uso de Gnu Privacy Guard (GPG):
- per creare ona nuova coppia de ciav, 
- aggiungere sottociav per firma e crittografia, 
- fare el backup de tutte i ciav, 
- trasferire i sottociav su on YubiKey e 
- crittografare/firmare on file usando Yubikey.

L'è progettato per Linux on comandi testati su GPG 2.2.40/Debian 12. I stessi comandi possono funzionare similmente su altre versioni de Linux e anca su MacOsX e Windows (ad eccezion di filesystem crittografati).

El processo segue i migliori pratiche de sicurezza, come la generazion di ciav offline e backup sicuri.

## Installazion
Installa gpg e i utilities necessarie

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Assegurati che la version sia 2.1.17 o successiva (2.4.5 consigliata).

```bash
gpg --version
```

Verifica el funzionamento de la YubiKey

```bash
ykman info
```

Assegurati che l'applet OpenPGP sia abilitata e la modalità CCID attiva.

Usa ona macchina air-gapped (senza internet) per generà i ciav e prevenire perdite.

Ricorda che i PIN YubiKey de default minga hinn sicuri e hinn:
- PIN Utente predefinito: 123456
- PIN Admin predefinito: 12345678
Cambiali prima dell'uso (vedi Passo 4).

## Passo 1
Genera ona coppia de ciav GPG primaria (pubblica e privata) per esclusivamente per certificazion (C), da queste discenderanno tutte i altre ciav che andremo a costruire.

Avvia la Generazion de la chiave usando --expert per accedere a le opzion avanzate.

```bash
gpg --expert --full-gen-key
```


Seleziona el Tipo de Chiave:

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

Scegli (8) RSA (set your own capabilities) per poter customizzare el comportamento de la chiave.

Imposta donca i funzionalità:

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

Mantieni Certify (premi Q quand finito).

Come risultato tra i azion attualmente consentite rimane domà Certify

Imposta la Dimensione de la Chiave:

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

Fornisci nome ed email. Lascia el commento vuoto. Conferma con O.

Inserisci ona passphrase forte (mescola lettere, numeri, simboli; evita paroll comuni).

Esempio: Tr0ub4dor&3xplor3r!2025

La passphrase consente de protegge la tua chiave privata.

Genera entropia muovendo el mouse, digita casualmente o usa rng-tools (Linux e domà se ne comprendi ben el funzionamento):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Attendi el completamento de la generazion de la chiave. Annota l'ID de la chiave (es. C2033656849FC82BA3C365E33C9BF8B9CB86875D) dall'output:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Crea on certificato per revocare la chiave se compromessa (anca se el tuo client potrebbe già averla creata):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Scegli el motivo (es. 1 = chiave compromessa) e salva.

## Passo 2
Creare Sottociav per Firma e Crittografia, verrano donca aggiunte due sottociav per firma (S) e crittografia (E). 

La chiave primaria resta domà per certificazion.

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

Scegli (4) RSA (domà firma).

Imposta dimensione: 4096.

Imposta scadenza: 2y (2 anni, i sottociav possono essere ruotate più frequentemente).

Conferma e inserisci la passphrase.

Aggiungi sottochiave per Crittografia:

```
gpg> addkey
```

Scegli (6) RSA (domà crittografia).

Imposta dimensione: 4096.

Imposta scadenza: 2y.

Conferma e inserisci la passphrase.

Salva i Modifiche:

```
gpg> save
```

Verifica i sottociav:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Esempio de output:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Annota i impronte di sottociav per firma (S) e crittografia (E).

## Passo 3
Backup de Tutte i ChiaviEsegui el backup de la chiave primaria, di sottociav e de la chiave pubblica su due unità USB crittografate per sicurezza.

Prepara i Unità USB:Inserisci due unità USB (es. /dev/sdb e /dev/sdc).

Crea partizion crittografate (es. con LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Ripeti per /dev/sdc1 (es. monta su /mnt/backup2).

Esporta i Chiavi Private:Esporta la chiave primaria e i sottociav:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Esporta i chiave pubbliche:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Esporta el Certificato de Revoca:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Smonta in Modo Sicuro:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Ripeti per backup2. Conserva i unità USB in luoghi separati e sicuri (es. cassaforte).

Elimina i Chiavi Locali (Facoltativo):Se usi ona macchina air-gapped, elimina la directory GPG:

```bash
rm -rf ~/.gnupg
```

I ciav andranno poi importare sulla macchina in cui andrai a usarle.

Se minga air-gapped, mantieni i ciav fino al trasferimento su YubiKey.

## Passo 4
Trasferisci i sottociav de firma e crittografia sul YubiKey, mantenendo la chiave primaria offline.

Inserisci Yubikey e verifica:

```bash
gpg --card-status
```

L'output dovrebbe mostrare l'applet OpenPGP (es. Version: 2.0).

Cambia i PIN predefiniti:

```bash
gpg --change-pin
```

PIN Utente: Imposta on nuovo PIN de 6-8 cifre (es. 654321).
PIN Admin: Imposta on nuovo PIN de 8 cifre (es. 87654321).

Modifica la Chiave per el Trasferimento:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Seleziona e Trasferisci la Sottochiave de Firma:Elenca i ciav per identificare i indici di sottociav:

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

Seleziona la sottochiave de firma:

```
gpg> key 1
```

La sottochiave de firma avrà on asterisco (*).

Trasferisci su YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Inserisci el PIN Admin (es. 87654321). La sottochiave privata de firma viene trasferita sul YubiKey e sostituita da uno stub nel portaciav.

Seleziona e Trasferisci la Sottochiave de Crittografia:Deseleziona la sottochiave de firma:

```
gpg> key 1
```

Seleziona la sottochiave de crittografia:

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

Inserisci de nuovo el PIN Admin.

Salva i Modifiche:

```
gpg> save
```

I sottociav private hinn ora sul YubiKey, con stub locali.

Verifica YubiKey:

```bash
gpg --card-status
```

Controlla che i slot Signature key e Encryption key mostrino i impronte digitali di sottociav.

Esporta i sottociav private (per verifica del backup):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Elimina la directory GPG locale:

```bash
rm -rf ~/.gnupg
```

Reimporta la chiave pubblica e i stub:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

La chiave primaria privata minga l'è più sul computer.

## Passo 5
Usa YubiKey per crittografare e firmare on file per on destinatario.

Prepara on File de Prova:

```bash
echo "Questo è un messaggio segreto." > test.txt
```

Ottieni la chiave pubblica del destinatario (es. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Oppur importa da on file:

```bash
gpg --import bob_public.asc
```

Crittografa e Firma:Crittografa per bob@example.com e firma con Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Inserisci el PIN Utente (es. 654321) quand richiesto. 

Se YubiKey richiede la conferma tattile (opzionale, impostata tramite ykman openpgp keys set-touch), tocca YubiKey.

L'output generato sarà test.txt.gpg

Decrittografa el file (richiede YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Inserisci el PIN Utente e tocca Yubikey se necessario. 

Verifica che test_decrypted.txt corrisponda a test.txt.

Bob può decriptare con la sua chiave privata e verificà la tua firma:

```bash
gpg --decrypt test.txt.gpg
```

Se invece vuoi domà firmare el file te pödet doprà i seguenti comandi.

```bash
gpg --detach-sign test.txt
```

Verrà generato on file de output chiamato test.txt.sig

Per verificarlo:

```bash
gpg --verify test.txt.sig test.txt
```

## Pratiche de sicurezza
- Genera semper i ciav su ona macchina offline per evitare esposizion.
- Conserva i unità USB con i ciav private in luoghi separati e sicuri (es. cassaforte o banca).
- Usa PIN forti e unici. Se i tentativi de PIN hinn superati (3 per Utente, 3 per Admin), Yubikey si blocca e richiede on reset, perdendo tutte i ciav.
- Mantieni revoke.asc accessibile ma segur per revocare la chiave se compromessa.
- Crea nuove sottociav prima de la scadenza (es. ogni anno) in queta maniera:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Trasferisci i nuove sottociav sul YubiKey e aggiorna la chiave pubblica sui server:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Usa on secondo YubiKey per ridondanza:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Ripeti i passaggi keytocard per el secondo YubiKey.

Se fosse necessario resettare Yubikey:

```bash
ykman openpgp reset
```

Mentre per ripristina i sottociav dal backup:

```bash
gpg --import secret.asc
```

“Chiave Pubblica Minga Utilizzabile”:Assegurati che la chiave pubblica del destinatario sia importata e fidata:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Imposta a 5 = Fiducia massima.

