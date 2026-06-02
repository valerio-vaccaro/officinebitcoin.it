---
layout: default
title: "GPG- und YubiKey-Tutorial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# GPG- und YubiKey-Tutorial

Diese Lektion führt dich durch die Verwendung von Gnu Privacy Guard (GPG):
- zum Erstellen eines neuen Schlüsselpaars,
- zum Hinzufügen von Unterschlüsseln für Signatur und Verschlüsselung,
- zum Sichern aller Schlüssel,
- zum Übertragen von Unterschlüsseln auf eine YubiKey, und
- zum Verschlüsseln/Signieren einer Datei mit Yubikey.

Sie ist für Linux gedacht, mit Befehlen, die unter GPG 2.2.40/Debian 12 getestet wurden. Dieselben Befehle können ähnlich auch auf anderen Linux-Versionen sowie auf MacOSX und Windows funktionieren (mit Ausnahme verschlüsselter Dateisysteme).

Der Ablauf folgt bewährten Sicherheitspraktiken wie Offline-Schlüsselerzeugung und sicheren Backups.

## Installation
Installiere gpg und die notwendigen Hilfsprogramme

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Stelle sicher, dass die Version 2.1.17 oder neuer ist (2.4.5 empfohlen).

```bash
gpg --version
```

Prüfe die YubiKey-Funktion

```bash
ykman info
```

Stelle sicher, dass das OpenPGP-Applet aktiviert ist und der CCID-Modus aktiv ist.

Verwende eine vom Netz getrennte Maschine (kein Internet), um Schlüssel zu erzeugen und Lecks zu vermeiden.

Beachte, dass die Standard-PINs der YubiKey nicht sicher sind und lauten:
- Default User PIN: 123456
- Default Admin PIN: 12345678
Ändere sie vor der Verwendung (siehe Schritt 4).

## Schritt 1
Erzeuge ein primäres GPG-Schlüsselpaar (öffentlich und privat) nur für Zertifizierung (C); alle anderen Schlüssel werden davon abgeleitet.

Starte die Schlüsselerzeugung mit --expert für erweiterte Optionen.

```bash
gpg --expert --full-gen-key
```

Wähle den Schlüsseltyp:

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

Wähle (8) RSA (set your own capabilities), um das Schlüsselverhalten anzupassen.

Lege die Fähigkeiten fest:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Deaktiviere Sign und Encrypt (S, E drücken).

Behalte Certify bei (Q drücken, wenn fertig).

Damit bleibt nur Certify unter den erlaubten Aktionen.

Lege die Schlüsselgröße fest:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Gib 4096 ein (Maximum, das von YubiKey 4/5 unterstützt wird).

Lege den Ablaufzeitpunkt fest:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Gib 3y (3 Jahre) oder deine bevorzugte Dauer ein. Bestätige das Datum.

Gib die User ID ein:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Gib Namen und E-Mail-Adresse an. Lasse den Kommentar leer. Bestätige mit O.

Gib eine starke passphrase ein (Buchstaben, Zahlen und Symbole mischen; gängige Wörter vermeiden).

Beispiel: Tr0ub4dor&3xplor3r!2025

Die passphrase schützt deinen privaten Schlüssel.

Erzeuge Entropie, indem du die Maus bewegst, zufällig tippst oder rng-tools verwendest (Linux und nur, wenn du es gut verstehst):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Warte, bis die Schlüsselerzeugung abgeschlossen ist. Notiere die key ID (z. B. C2033656849FC82BA3C365E33C9BF8B9CB86875D) aus der Ausgabe:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Erstelle ein Widerrufszertifikat für den Fall, dass der Schlüssel kompromittiert wird (dein Client hat es möglicherweise bereits erstellt):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Wähle den Grund (z. B. 1 = Schlüssel kompromittiert) und speichere.

## Schritt 2
Erstelle Signatur- und Verschlüsselungs-Unterschlüssel. Zwei Unterschlüssel werden für Signatur (S) und Verschlüsselung (E) hinzugefügt.

Der primäre Schlüssel bleibt nur für Zertifizierung.

Bearbeite den Schlüssel:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Gib die passphrase ein, falls danach gefragt wird.

Füge den Signatur-Unterschlüssel hinzu:

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

Wähle (4) RSA (sign only).

Lege die Größe fest: 4096.

Lege den Ablauf fest: 2y (2 Jahre, Unterschlüssel können häufiger rotiert werden).

Bestätige und gib die passphrase ein.

Füge den Verschlüsselungs-Unterschlüssel hinzu:

```
gpg> addkey
```

Wähle (6) RSA (encrypt only).

Lege die Größe fest: 4096.

Lege den Ablauf fest: 2y.

Bestätige und gib die passphrase ein.

Speichere die Änderungen:

```
gpg> save
```

Prüfe die Unterschlüssel:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Beispielausgabe:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Notiere die Fingerprints der Signatur- (S) und Verschlüsselungs-Unterschlüssel (E).

## Schritt 3
Backup aller Schlüssel. Sichere den primären Schlüssel, die Unterschlüssel und den öffentlichen Schlüssel aus Sicherheitsgründen auf zwei verschlüsselten USB-Laufwerken.

Bereite die USB-Laufwerke vor: Stecke zwei USB-Laufwerke ein (z. B. /dev/sdb und /dev/sdc).

Erstelle verschlüsselte Partitionen (z. B. mit LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Wiederhole dies für /dev/sdc1 (z. B. unter /mnt/backup2 eingehängt).

Exportiere private Schlüssel: Exportiere den primären Schlüssel und die Unterschlüssel:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Exportiere öffentliche Schlüssel:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Exportiere das Widerrufszertifikat:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Sicher aushängen:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Wiederhole dies für backup2. Bewahre die USB-Laufwerke an getrennten, sicheren Orten auf (z. B. Safe).

Lokale Schlüssel löschen (optional): Wenn du eine vom Netz getrennte Maschine verwendest, lösche das GPG-Verzeichnis:

```bash
rm -rf ~/.gnupg
```

Die Schlüssel müssen danach auf der Maschine importiert werden, auf der du sie verwenden wirst.

Wenn die Maschine nicht vom Netz getrennt ist, behalte die Schlüssel bis zur Übertragung auf die YubiKey.

## Schritt 4
Übertrage die Signatur- und Verschlüsselungs-Unterschlüssel auf die YubiKey und halte den primären Schlüssel offline.

Stecke die Yubikey ein und prüfe:

```bash
gpg --card-status
```

Die Ausgabe sollte das OpenPGP-Applet anzeigen (z. B. Version: 2.0).

Ändere die Standard-PINs:

```bash
gpg --change-pin
```

User PIN: Setze eine neue 6- bis 8-stellige PIN (z. B. 654321).
Admin PIN: Setze eine neue 8-stellige PIN (z. B. 87654321).

Bearbeite den Schlüssel für die Übertragung:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Signatur-Unterschlüssel auswählen und übertragen: Liste die Schlüssel auf, um die Indizes der Unterschlüssel zu identifizieren:

```
gpg> list
```

Beispiel:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Wähle den Signatur-Unterschlüssel:

```
gpg> key 1
```

Der Signatur-Unterschlüssel hat dann ein Sternchen (*).

Auf die YubiKey übertragen:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Gib die Admin PIN ein (z. B. 87654321). Der private Signatur-Unterschlüssel wird auf die YubiKey übertragen und im keyring durch einen Stub ersetzt.

Verschlüsselungs-Unterschlüssel auswählen und übertragen: Wähle den Signatur-Unterschlüssel ab:

```
gpg> key 1
```

Wähle den Verschlüsselungs-Unterschlüssel:

```
gpg> key 2
```

Auf die YubiKey übertragen:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Gib die Admin PIN erneut ein.

Speichere die Änderungen:

```
gpg> save
```

Die privaten Unterschlüssel befinden sich nun auf der YubiKey, mit lokalen Stubs.

Prüfe die YubiKey:

```bash
gpg --card-status
```

Prüfe, dass die Slots Signature key und Encryption key die Fingerprints der Unterschlüssel anzeigen.

Private Unterschlüssel exportieren (zur Überprüfung des Backups):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Lösche das lokale GPG-Verzeichnis:

```bash
rm -rf ~/.gnupg
```

Importiere den öffentlichen Schlüssel und die Stubs erneut:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

Der primäre private Schlüssel befindet sich nicht mehr auf dem Computer.

## Schritt 5
Verwende die YubiKey, um eine Datei für einen Empfänger zu verschlüsseln und zu signieren.

Bereite eine Testdatei vor:

```bash
echo "This is a secret message." > test.txt
```

Hole den öffentlichen Schlüssel des Empfängers (z. B. bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Oder importiere ihn aus einer Datei:

```bash
gpg --import bob_public.asc
```

Verschlüsseln und signieren: Für bob@example.com verschlüsseln und mit Yubikey signieren:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Gib die User PIN ein (z. B. 654321), wenn du dazu aufgefordert wirst.

Wenn YubiKey eine Berührungsbestätigung verlangt (optional, über ykman openpgp keys set-touch gesetzt), berühre die YubiKey.

Die Ausgabe ist test.txt.gpg

Entschlüssele die Datei (erfordert YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Gib die User PIN ein und berühre die Yubikey, falls nötig.

Prüfe, dass test_decrypted.txt mit test.txt übereinstimmt.

Bob kann mit seinem privaten Schlüssel entschlüsseln und deine Signatur prüfen:

```bash
gpg --decrypt test.txt.gpg
```

Wenn du die Datei nur signieren möchtest, kannst du die folgenden Befehle verwenden.

```bash
gpg --detach-sign test.txt
```

Dies erzeugt eine Ausgabedatei namens test.txt.sig

Zum Prüfen:

```bash
gpg --verify test.txt.sig test.txt
```

## Sicherheitspraktiken
- Erzeuge Schlüssel immer auf einer Offline-Maschine, um Offenlegung zu vermeiden.
- Bewahre USB-Laufwerke mit privaten Schlüsseln an getrennten, sicheren Orten auf (z. B. Safe oder Bank).
- Verwende starke, eindeutige PINs. Wenn die PIN-Versuche überschritten werden (3 für User, 3 für Admin), sperrt sich die Yubikey und erfordert ein Zurücksetzen, wobei alle Schlüssel verloren gehen.
- Halte revoke.asc zugänglich, aber sicher, um den Schlüssel bei Kompromittierung zu widerrufen.
- Erstelle neue Unterschlüssel vor Ablauf (z. B. jährlich) wie folgt:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Übertrage neue Unterschlüssel auf die YubiKey und aktualisiere den öffentlichen Schlüssel auf Servern:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Verwende eine zweite YubiKey für Redundanz:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Wiederhole die keytocard-Schritte für die zweite YubiKey.

Wenn du die Yubikey zurücksetzen musst:

```bash
ykman openpgp reset
```

Zum Wiederherstellen von Unterschlüsseln aus dem Backup:

```bash
gpg --import secret.asc
```

“Public Key Not Usable”: Stelle sicher, dass der öffentliche Schlüssel des Empfängers importiert und vertrauenswürdig ist:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Auf 5 = Ultimate trust setzen.
