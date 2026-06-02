---
layout: default
title: "Tutorial de GPG y YubiKey"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Tutorial de GPG y YubiKey

Esta lección te guía en el uso de Gnu Privacy Guard (GPG):
- para crear un nuevo par de claves,
- añadir subclaves para firma y cifrado,
- hacer una copia de seguridad de todas las claves,
- transferir subclaves a una YubiKey, y
- cifrar/firmar un archivo usando Yubikey.

Está diseñada para Linux, con comandos probados en GPG 2.2.40/Debian 12. Los mismos comandos pueden funcionar de forma similar en otras versiones de Linux y también en MacOSX y Windows (excepto en lo relativo a sistemas de archivos cifrados).

El proceso sigue buenas prácticas de seguridad, como la generación de claves sin conexión y copias de seguridad seguras.

## Instalación
Instala gpg y las utilidades necesarias

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Asegúrate de que la versión sea 2.1.17 o posterior (se recomienda 2.4.5).

```bash
gpg --version
```

Comprueba el funcionamiento de la YubiKey

```bash
ykman info
```

Asegúrate de que el applet OpenPGP esté habilitado y que el modo CCID esté activo.

Usa una máquina aislada de la red (sin internet) para generar las claves y evitar filtraciones.

Recuerda que los PIN predeterminados de YubiKey no son seguros y son:
- Default User PIN: 123456
- Default Admin PIN: 12345678
Cámbialos antes de usarla (consulta el Paso 4).

## Paso 1
Genera un par de claves GPG primario (pública y privada) solo para certificación (C); todas las demás claves derivarán de esta.

Inicia la generación de claves usando --expert para opciones avanzadas.

```bash
gpg --expert --full-gen-key
```

Selecciona el tipo de clave:

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

Elige (8) RSA (set your own capabilities) para personalizar el comportamiento de la clave.

Configura las capacidades:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Deshabilita Sign y Encrypt (pulsa S, E).

Mantén Certify (pulsa Q cuando termines).

Como resultado, solo Certify permanecerá entre las acciones permitidas.

Configura el tamaño de la clave:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Introduce 4096 (máximo admitido por YubiKey 4/5).

Configura la caducidad:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Introduce 3y (3 años) o tu preferencia. Confirma la fecha.

Introduce el User ID:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Proporciona nombre y correo electrónico. Deja el comentario en blanco. Confirma con O.

Introduce una passphrase fuerte (mezcla letras, números y símbolos; evita palabras comunes).

Ejemplo: Tr0ub4dor&3xplor3r!2025

La passphrase protege tu clave privada.

Genera entropía moviendo el ratón, escribiendo al azar o usando rng-tools (Linux y solo si lo entiendes bien):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Espera a que termine la generación de la clave. Anota el key ID (por ejemplo, C2033656849FC82BA3C365E33C9BF8B9CB86875D) de la salida:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Crea un certificado de revocación por si la clave se ve comprometida (tu cliente puede haberlo creado ya):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Elige el motivo (por ejemplo, 1 = clave comprometida) y guarda.

## Paso 2
Crea subclaves de firma y cifrado. Se añadirán dos subclaves para firma (S) y cifrado (E).

La clave primaria queda solo para certificación.

Edita la clave:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Introduce la passphrase si se solicita.

Añade la subclave de firma:

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

Elige (4) RSA (sign only).

Configura el tamaño: 4096.

Configura la caducidad: 2y (2 años; las subclaves pueden rotarse con más frecuencia).

Confirma e introduce la passphrase.

Añade la subclave de cifrado:

```
gpg> addkey
```

Elige (6) RSA (encrypt only).

Configura el tamaño: 4096.

Configura la caducidad: 2y.

Confirma e introduce la passphrase.

Guarda los cambios:

```
gpg> save
```

Comprueba las subclaves:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Salida de ejemplo:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Anota las huellas digitales de las subclaves de firma (S) y cifrado (E).

## Paso 3
Copia de seguridad de todas las claves. Haz una copia de seguridad de la clave primaria, las subclaves y la clave pública en dos unidades USB cifradas por seguridad.

Prepara las unidades USB: inserta dos unidades USB (por ejemplo, /dev/sdb y /dev/sdc).

Crea particiones cifradas (por ejemplo, con LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Repite para /dev/sdc1 (por ejemplo, montada en /mnt/backup2).

Exporta las claves privadas: exporta la clave primaria y las subclaves:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Exporta las claves públicas:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Exporta el certificado de revocación:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Desmonta de forma segura:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Repite para backup2. Guarda las unidades USB en ubicaciones separadas y seguras (por ejemplo, una caja fuerte).

Elimina las claves locales (opcional): si usas una máquina aislada de la red, elimina el directorio GPG:

```bash
rm -rf ~/.gnupg
```

Luego las claves deberán importarse en la máquina donde vayas a usarlas.

Si la máquina no está aislada de la red, conserva las claves hasta transferirlas a la YubiKey.

## Paso 4
Transfiere las subclaves de firma y cifrado a la YubiKey, manteniendo la clave primaria sin conexión.

Inserta la Yubikey y comprueba:

```bash
gpg --card-status
```

La salida debería mostrar el applet OpenPGP (por ejemplo, Version: 2.0).

Cambia los PIN predeterminados:

```bash
gpg --change-pin
```

User PIN: establece un nuevo PIN de 6-8 dígitos (por ejemplo, 654321).
Admin PIN: establece un nuevo PIN de 8 dígitos (por ejemplo, 87654321).

Edita la clave para la transferencia:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Selecciona y transfiere la subclave de firma: lista las claves para identificar los índices de las subclaves:

```
gpg> list
```

Ejemplo:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Selecciona la subclave de firma:

```
gpg> key 1
```

La subclave de firma tendrá un asterisco (*).

Transfiérela a la YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Introduce el Admin PIN (por ejemplo, 87654321). La subclave privada de firma se transfiere a la YubiKey y se sustituye por un stub en el keyring.

Selecciona y transfiere la subclave de cifrado: deselecciona la subclave de firma:

```
gpg> key 1
```

Selecciona la subclave de cifrado:

```
gpg> key 2
```

Transfiérela a la YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Introduce de nuevo el Admin PIN.

Guarda los cambios:

```
gpg> save
```

Las subclaves privadas están ahora en la YubiKey, con stubs locales.

Comprueba la YubiKey:

```bash
gpg --card-status
```

Comprueba que las ranuras Signature key y Encryption key muestren las huellas digitales de las subclaves.

Exporta las subclaves privadas (para verificar la copia de seguridad):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Elimina el directorio GPG local:

```bash
rm -rf ~/.gnupg
```

Vuelve a importar la clave pública y los stubs:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

La clave privada primaria ya no está en el ordenador.

## Paso 5
Usa la YubiKey para cifrar y firmar un archivo para un destinatario.

Prepara un archivo de prueba:

```bash
echo "This is a secret message." > test.txt
```

Obtén la clave pública del destinatario (por ejemplo, bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

O impórtala desde un archivo:

```bash
gpg --import bob_public.asc
```

Cifra y firma: cifra para bob@example.com y firma con Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Introduce el User PIN (por ejemplo, 654321) cuando se solicite.

Si YubiKey requiere confirmación táctil (opcional, configurada mediante ykman openpgp keys set-touch), toca la YubiKey.

La salida será test.txt.gpg

Descifra el archivo (requiere YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Introduce el User PIN y toca la Yubikey si es necesario.

Comprueba que test_decrypted.txt coincida con test.txt.

Bob puede descifrarlo con su clave privada y verificar tu firma:

```bash
gpg --decrypt test.txt.gpg
```

Si solo quieres firmar el archivo, puedes usar los siguientes comandos.

```bash
gpg --detach-sign test.txt
```

Esto generará un archivo de salida llamado test.txt.sig

Para verificarlo:

```bash
gpg --verify test.txt.sig test.txt
```

## Prácticas de seguridad
- Genera siempre las claves en una máquina sin conexión para evitar exposición.
- Guarda las unidades USB con claves privadas en ubicaciones separadas y seguras (por ejemplo, caja fuerte o banco).
- Usa PIN fuertes y únicos. Si se superan los intentos de PIN (3 para User, 3 para Admin), la Yubikey se bloquea y requiere un restablecimiento, lo que elimina todas las claves.
- Mantén revoke.asc accesible pero seguro para revocar la clave si se ve comprometida.
- Crea nuevas subclaves antes de la caducidad (por ejemplo, cada año) como se indica:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Transfiere las nuevas subclaves a la YubiKey y actualiza la clave pública en los servidores:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Usa una segunda YubiKey para redundancia:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Repite los pasos de keytocard para la segunda YubiKey.

Si necesitas restablecer la Yubikey:

```bash
ykman openpgp reset
```

Para restaurar subclaves desde la copia de seguridad:

```bash
gpg --import secret.asc
```

“Public Key Not Usable”: asegúrate de que la clave pública del destinatario esté importada y sea de confianza:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Configura en 5 = Ultimate trust.
