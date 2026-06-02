---
layout: default
title: "Tutorial de GPG e YubiKey"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Tutorial de GPG e YubiKey

Esta aula orienta você no uso do Gnu Privacy Guard (GPG):
- para criar um novo par de chaves,
- adicionar subchaves para assinatura e criptografia,
- fazer backup de todas as chaves,
- transferir subchaves para uma YubiKey, e
- criptografar/assinar um arquivo usando Yubikey.

Ela foi pensada para Linux, com comandos testados em GPG 2.2.40/Debian 12. Os mesmos comandos podem funcionar de modo semelhante em outras versões de Linux e também em MacOSX e Windows (exceto para sistemas de arquivos criptografados).

O processo segue boas práticas de segurança, como geração de chaves offline e backups seguros.

## Instalação
Instale gpg e os utilitários necessários

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Certifique-se de que a versão seja 2.1.17 ou posterior (2.4.5 recomendada).

```bash
gpg --version
```

Verifique o funcionamento da YubiKey

```bash
ykman info
```

Garanta que o applet OpenPGP esteja habilitado e que o modo CCID esteja ativo.

Use uma máquina isolada da rede (sem internet) para gerar as chaves e evitar vazamentos.

Lembre-se de que os PINs padrão da YubiKey não são seguros e são:
- Default User PIN: 123456
- Default Admin PIN: 12345678
Altere-os antes de usar (veja o Passo 4).

## Passo 1
Gere um par de chaves GPG primário (pública e privada) apenas para certificação (C); todas as outras chaves derivarão dele.

Inicie a geração de chaves usando --expert para opções avançadas.

```bash
gpg --expert --full-gen-key
```

Selecione o tipo de chave:

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

Escolha (8) RSA (set your own capabilities) para personalizar o comportamento da chave.

Configure as capacidades:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Desative Sign e Encrypt (pressione S, E).

Mantenha Certify (pressione Q quando terminar).

Como resultado, apenas Certify permanece entre as ações permitidas.

Configure o tamanho da chave:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Digite 4096 (máximo suportado pela YubiKey 4/5).

Configure a expiração:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Digite 3y (3 anos) ou sua preferência. Confirme a data.

Digite o User ID:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Informe nome e e-mail. Deixe o comentário em branco. Confirme com O.

Digite uma passphrase forte (misture letras, números e símbolos; evite palavras comuns).

Exemplo: Tr0ub4dor&3xplor3r!2025

A passphrase protege sua chave privada.

Gere entropia movendo o mouse, digitando aleatoriamente ou usando rng-tools (Linux e somente se você entender bem):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Aguarde a conclusão da geração da chave. Anote o key ID (por exemplo, C2033656849FC82BA3C365E33C9BF8B9CB86875D) na saída:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Crie um certificado de revogação caso a chave seja comprometida (seu cliente pode já tê-lo criado):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Escolha o motivo (por exemplo, 1 = chave comprometida) e salve.

## Passo 2
Crie subchaves de assinatura e criptografia. Duas subchaves serão adicionadas para assinatura (S) e criptografia (E).

A chave primária permanece apenas para certificação.

Edite a chave:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Digite a passphrase se solicitado.

Adicione a subchave de assinatura:

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

Escolha (4) RSA (sign only).

Configure o tamanho: 4096.

Configure a expiração: 2y (2 anos, subchaves podem ser rotacionadas com mais frequência).

Confirme e digite a passphrase.

Adicione a subchave de criptografia:

```
gpg> addkey
```

Escolha (6) RSA (encrypt only).

Configure o tamanho: 4096.

Configure a expiração: 2y.

Confirme e digite a passphrase.

Salve as alterações:

```
gpg> save
```

Verifique as subchaves:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Saída de exemplo:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Anote as fingerprints das subchaves de assinatura (S) e criptografia (E).

## Passo 3
Backup de todas as chaves. Faça backup da chave primária, das subchaves e da chave pública em duas unidades USB criptografadas por segurança.

Prepare as unidades USB: insira duas unidades USB (por exemplo, /dev/sdb e /dev/sdc).

Crie partições criptografadas (por exemplo, com LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Repita para /dev/sdc1 (por exemplo, montada em /mnt/backup2).

Exporte as chaves privadas: exporte a chave primária e as subchaves:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Exporte as chaves públicas:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Exporte o certificado de revogação:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Desmonte com segurança:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Repita para backup2. Guarde as unidades USB em locais separados e seguros (por exemplo, cofre).

Exclua as chaves locais (opcional): se estiver usando uma máquina isolada da rede, exclua o diretório GPG:

```bash
rm -rf ~/.gnupg
```

Depois disso, as chaves precisarão ser importadas na máquina em que serão usadas.

Se a máquina não estiver isolada da rede, mantenha as chaves até transferi-las para a YubiKey.

## Passo 4
Transfira as subchaves de assinatura e criptografia para a YubiKey, mantendo a chave primária offline.

Insira a Yubikey e verifique:

```bash
gpg --card-status
```

A saída deve mostrar o applet OpenPGP (por exemplo, Version: 2.0).

Altere os PINs padrão:

```bash
gpg --change-pin
```

User PIN: defina um novo PIN de 6-8 dígitos (por exemplo, 654321).
Admin PIN: defina um novo PIN de 8 dígitos (por exemplo, 87654321).

Edite a chave para transferência:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Selecione e transfira a subchave de assinatura: liste as chaves para identificar os índices das subchaves:

```
gpg> list
```

Exemplo:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Selecione a subchave de assinatura:

```
gpg> key 1
```

A subchave de assinatura terá um asterisco (*).

Transfira para a YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Digite o Admin PIN (por exemplo, 87654321). A subchave privada de assinatura é transferida para a YubiKey e substituída por um stub no keyring.

Selecione e transfira a subchave de criptografia: desselecione a subchave de assinatura:

```
gpg> key 1
```

Selecione a subchave de criptografia:

```
gpg> key 2
```

Transfira para a YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Digite o Admin PIN novamente.

Salve as alterações:

```
gpg> save
```

As subchaves privadas agora estão na YubiKey, com stubs locais.

Verifique a YubiKey:

```bash
gpg --card-status
```

Verifique se os slots Signature key e Encryption key mostram as fingerprints das subchaves.

Exporte as subchaves privadas (para verificar o backup):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Exclua o diretório GPG local:

```bash
rm -rf ~/.gnupg
```

Reimporte a chave pública e os stubs:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

A chave privada primária não está mais no computador.

## Passo 5
Use a YubiKey para criptografar e assinar um arquivo para um destinatário.

Prepare um arquivo de teste:

```bash
echo "This is a secret message." > test.txt
```

Obtenha a chave pública do destinatário (por exemplo, bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Ou importe de um arquivo:

```bash
gpg --import bob_public.asc
```

Criptografe e assine: criptografe para bob@example.com e assine com Yubikey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

Digite o User PIN (por exemplo, 654321) quando solicitado.

Se a YubiKey exigir confirmação por toque (opcional, configurada via ykman openpgp keys set-touch), toque na YubiKey.

A saída será test.txt.gpg

Descriptografe o arquivo (requer YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Digite o User PIN e toque na Yubikey se necessário.

Verifique se test_decrypted.txt corresponde a test.txt.

Bob pode descriptografar com sua chave privada e verificar sua assinatura:

```bash
gpg --decrypt test.txt.gpg
```

Se você quiser apenas assinar o arquivo, pode usar os seguintes comandos.

```bash
gpg --detach-sign test.txt
```

Isso gerará um arquivo de saída chamado test.txt.sig

Para verificá-lo:

```bash
gpg --verify test.txt.sig test.txt
```

## Práticas de segurança
- Gere sempre as chaves em uma máquina offline para evitar exposição.
- Armazene unidades USB com chaves privadas em locais separados e seguros (por exemplo, cofre ou banco).
- Use PINs fortes e únicos. Se as tentativas de PIN forem excedidas (3 para User, 3 para Admin), a Yubikey bloqueia e exige reset, perdendo todas as chaves.
- Mantenha revoke.asc acessível, mas seguro, para revogar a chave se ela for comprometida.
- Crie novas subchaves antes da expiração (por exemplo, todos os anos) da seguinte forma:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Transfira novas subchaves para a YubiKey e atualize a chave pública nos servidores:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Use uma segunda YubiKey para redundância:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Repita os passos de keytocard para a segunda YubiKey.

Se precisar resetar a Yubikey:

```bash
ykman openpgp reset
```

Para restaurar subchaves a partir do backup:

```bash
gpg --import secret.asc
```

“Public Key Not Usable”: certifique-se de que a chave pública do destinatário foi importada e é confiável:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Defina como 5 = Ultimate trust.
