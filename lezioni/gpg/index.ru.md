---
layout: default
title: "Учебные пособия GPG и YubiKey"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only урок</span> <span>Этот проект поддерживается valerio-vaccaro</span></p>

## 🌍 Переводы

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Учебники GPG и YubiKey

В этом уроке вы познакомитесь с использованием Gnu Privacy Guard (GPG):
- для создания новой пары ключей, 
- добавить субключи для подписи и шифрования, 
- сделать резервную копию всех ключей, 
- перенести субключи в YubiKey и 
- зашифровать/подписать файл с помощью YubiKey.

Он предназначен для Linux для команд, протестированных в GPG 2.2.40/Debian 12. Те же команды могут работать аналогичным образом в других версиях Linux, а также в macOS и Windows (за исключением зашифрованных файловых систем).

Этот процесс соответствует лучшим практикам безопасности, таким как автономная генерация ключей и безопасное резервное копирование.

## Установка
Установите gpg и необходимые утилиты.

```bash
sudo apt update
sudo apt install gnupg scdaemon pcscd yubikey-manager
```

Убедитесь, что установлена версия 2.1.17 или новее (рекомендуется 2.4.5).

```bash
gpg --version
```

Проверьте работу YubiKey

```bash
ykman info
```

Убедитесь, что апплет OpenPGP включен и режим CCID активен.

Используйте машину с воздушным зазором (без Интернета) для генерации ключей и предотвращения утечек.

Помните, что PIN-коды YubiKey по умолчанию не являются безопасными и являются:
- PIN-код пользователя по умолчанию: 123456.
- PIN-код администратора по умолчанию: 12345678.
Замените их перед использованием (см. шаг 4).

## Шаг 1
Сгенерируйте пару первичных ключей GPG (публичный и приватный) исключительно для сертификации (C), из них будут происходить все остальные ключи, которые мы собираемся строить.

Запустите генерацию ключей, используя --expert, чтобы получить доступ к дополнительным параметрам.

```bash
gpg --expert --full-gen-key
```


Выберите тип ключа:

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

Выберите (8) RSA (установите свои возможности), чтобы иметь возможность настроить поведение клавиши.

Затем установите функции:

```
Possible actions for a RSA key: Sign Certify Encrypt Authenticate 
Current allowed actions: Sign Certify Encrypt 

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection? S
```

Выключите подпись и шифрование (нажмите S, E).

Сохраните сертификацию (по завершении нажмите Q).

В результате среди разрешенных на данный момент действий остается только Certify.

Установите размер ключа:

```
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 4096
```

Введите 4096 (максимум, поддерживаемый YubiKey 4/5).

Установите крайний срок:

```
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 
```

Введите 3 года (3 года) или по вашему желанию. Подтвердите дату.

Введите свой идентификатор пользователя:

```
GnuPG needs to construct a user ID to identify your key.

Real name: Satoshi Spritz
Email address: info@satoshispritz.it
Comment: 
You selected this USER-ID:
    "Satoshi Spritz <info@satoshispritz.it>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
```

Укажите свое имя и адрес электронной почты. Оставьте комментарий пустым. Подтвердите О.

Введите надежную парольную фразу (смесь букв, цифр и символов; избегайте общих слов).

Пример: Tr0ub4dor&3xplor3r!2025

Парольная фраза помогает защитить ваш закрытый ключ.

Генерируйте энтропию, перемещая мышь, вводя случайный текст или используя rng-tools (Linux, и только если вы понимаете, как это работает):

```bash
sudo apt install rng-tools
sudo rngd -r /dev/urandom
```

Дождитесь завершения генерации ключа. Обратите внимание на идентификатор ключа (например, C2033656849FC82BA3C365E33C9BF8B9CB86875D) из вывода:

```
gpublic and secret key created and signed.

pub   rsa2048 2025-07-20 [C]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid                      Satoshi Spritz <info@satoshispritz.it>

```

Создайте сертификат для отзыва ключа в случае компрометации (даже если ваш клиент уже создал его):

```bash
gpg --output revoke_master_satoshispritz.asc --gen-revoke C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Выберите причину (например, 1 = взломанный ключ) и сохраните.

## Шаг 2
Создайте субключи для подписи и шифрования, затем добавите два субключа для подписи (S) и шифрования (E). 

Первичный ключ остается только для сертификации.

Давайте изменим ключ:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Введите парольную фразу, если потребуется.

Добавьте субключ для подписи:

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

Выберите (4) RSA (только подпись).

Размер набора: 4096.

Срок действия набора: 2 года (2 года, субключи можно менять чаще).

Подтвердите и введите парольную фразу.

Добавьте субключ для шифрования:

```
gpg> addkey
```

Выберите (6) RSA (только шифрование).

Размер набора: 4096.

Срок действия набора: 2 года.

Подтвердите и введите парольную фразу.

Сохранить изменения:

```
gpg> save
```

Проверьте субключи:

```bash
gpg --list-keys --with-subkey-fingerprints C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Пример вывода:

```
pub   rsa4096 2025-07-20 [C] [expires: 2028-07-20]
      C2033656849FC82BA3C365E33C9BF8B9CB86875D
uid           [ultimate] Satoshi Spritz <info@satoshispritz.it>
sub   rsa4096 2025-07-20 [S] [expires: 2027-07-20]
      1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3
sub   rsa4096 2025-07-20 [E] [expires: 2027-07-20]
      94C11C615BE049B97899FA3C8DC3736F499D6C3E

```

Обратите внимание на отпечатки ключей подписи (S) и шифрования (E).

## Шаг 3
Резервное копирование всех ключей. В целях безопасности создайте резервную копию основного ключа, дополнительных ключей и открытого ключа на двух зашифрованных USB-накопителях.

Подготовьте USB-накопители: вставьте два USB-накопителя (например, /dev/sdb и /dev/sdc).

Создайте зашифрованные разделы (например, с помощью LUKS):

```bash
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup luksOpen /dev/sdb1 backup1
sudo mkfs.ext4 /dev/mapper/backup1
sudo mount /dev/mapper/backup1 /mnt/backup1
```

Повторите то же самое для /dev/sdc1 (например, смонтируйте в /mnt/backup2).

Экспортировать закрытые ключи. Экспортируйте первичный ключ и субключи:

```bash
gpg --armor --export-secret-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/secret_master_satoshispritz.asc
gpg --armor --export-secret-keys 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/secret_sign_satoshispritz.asc
gpg --armor --export-secret-keys 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/secret_encrypt_satoshispritz.asc
```

Экспортировать открытые ключи:

```bash
gpg --armor --export C2033656849FC82BA3C365E33C9BF8B9CB86875D! > /mnt/backup1/public_master_satoshispritz.asc
gpg --armor --export 1E3C548D2CA2927D205C1A85426E4AB8E6D72AC3! > /mnt/backup2/public_sign_satoshispritz.asc
gpg --armor --export 94C11C615BE049B97899FA3C8DC3736F499D6C3E! > /mnt/backup2/public_encrypt_satoshispritz.asc
```

Экспортируйте сертификат отзыва:

```bash
cp revoke_master_satoshispritz.asc /mnt/backup1/revoke_master_satoshispritz.asc
cp revoke_master_satoshispritz.asc /mnt/backup2/revoke_master_satoshispritz.asc
```

Разбирайте безопасно:

```bash
sudo umount /mnt/backup1
sudo cryptsetup luksClose backup1
```

Повторите для резервного копирования2. Храните USB-накопители в отдельных безопасных местах (например, в сейфе).

Удалить локальные ключи (необязательно). Если вы используете компьютер с воздушным зазором, удалите каталог GPG:

```bash
rm -rf ~/.gnupg
```

Ключи будут импортированы в автомобиль, в котором вы собираетесь их использовать.

Если нет воздушного зазора, удерживайте клавиши до момента передачи на YubiKey.

## Шаг 4
Перенесите дополнительные ключи подписи и шифрования в YubiKey, оставив первичный ключ в автономном режиме.

Введите YubiKey и проверьте:

```bash
gpg --card-status
```

В выводе должен отображаться апплет OpenPGP (например, версия: 2.0).

Измените PIN-коды по умолчанию:

```bash
gpg --change-pin
```

PIN-код пользователя: установите новый PIN-код из 6–8 цифр (например, 654321).
PIN-код администратора: установите новый 8-значный PIN-код (например, 87654321).

Измените ключ передачи:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Выберите и передайте субключ подписи: перечислите ключи для определения индексов субключей:

```
gpg> list
```

Пример:

```
sec  rsa4096/3C9BF8B9CB86875D
     created: 2025-07-20  expires: 2028-07-20  usage: C   
     trust: ultimate      validity: ultimate
ssb  rsa4096/426E4AB8E6D72AC3
     created: 2025-07-20  expires: 2027-07-20  usage: S   
ssb  rsa4096/8DC3736F499D6C3E
     created: 2025-07-20  expires: 2027-07-20  usage: E
```

Выберите субключ подписи:

```
gpg> key 1
```

Подключ подписи будет отмечен звездочкой (*).

Перенос в YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection?
```

Введите PIN-код администратора (например, 87654321). Закрытый субключ подписи переносится в YubiKey и заменяется заглушкой в ​​связке ключей.

Выберите и передайте субключ шифрования. Отмените выбор субключа подписи:

```
gpg> key 1
```

Выберите субключ шифрования:

```
gpg> key 2
```

Перенос в YubiKey:

```
gpg> keytocard
Please select where to store the key:
   (2) Encryption key
Your selection? 2
```

Введите PIN-код администратора еще раз.

Сохранить изменения:

```
gpg> save
```

Частные субключи теперь находятся на YubiKey с локальными заглушками.

Проверьте YubiKey:

```bash
gpg --card-status
```

Убедитесь, что в слотах ключа подписи и ключа шифрования указаны отпечатки субключей.

Экспортировать частные субключи (для проверки резервной копии):

```bash
gpg --armor --export-secret-subkeys C2033656849FC82BA3C365E33C9BF8B9CB86875D > secret-subkeys-satoshispritz.asc
```

Удалите локальный каталог GPG:

```bash
rm -rf ~/.gnupg
```

Повторно импортируйте открытый ключ и заглушки:

```bash
gpg --import public.asc
gpg --import secret-subkeys-satoshispritz.asc
```

Закрытого первичного ключа больше нет на компьютере.

## Шаг 5
Используйте YubiKey, чтобы зашифровать и подписать файл для получателя.

Подготовьте тестовый файл:

```bash
echo "Questo è un messaggio segreto." > test.txt
```

Получите открытый ключ получателя (например, bob@example.com):

```bash
gpg --keyserver hkps://keys.openpgp.org --search-keys bob@example.com
```

Или импортируйте из файла:

```bash
gpg --import bob_public.asc
```

Зашифровать и подписать: зашифровать для bob@example.com и подписать с помощью YubiKey:

```bash
gpg --encrypt --sign --recipient bob@example.com test.txt
```

При появлении запроса введите свой PIN-код пользователя (например, 654321). 

Если YubiKey требует сенсорного подтверждения (необязательно, устанавливается с помощью сенсорных клавиш ykman openpgp), коснитесь YubiKey.

Сгенерированный результат будет test.txt.gpg.

Расшифруйте файл (требуется YubiKey):

```bash
gpg --decrypt test.txt.gpg > test_decrypted.txt
```

Введите свой PIN-код пользователя и при необходимости нажмите YubiKey. 

Убедитесь, что файл test_decrypted.txt соответствует файлу test.txt.

Боб может расшифровать с помощью своего закрытого ключа и проверить вашу подпись:

```bash
gpg --decrypt test.txt.gpg
```

Если вы просто хотите подписать файл, вы можете использовать следующие команды.

```bash
gpg --detach-sign test.txt
```

Будет создан выходной файл с именем test.txt.sig.

Чтобы проверить это:

```bash
gpg --verify test.txt.sig test.txt
```

## Техника безопасности
- Всегда создавайте ключи на автономном компьютере, чтобы избежать раскрытия.
- Храните USB-накопители с закрытыми ключами в отдельных безопасных местах (например, в сейфе или банке).
- Используйте надежные и уникальные PIN-коды. Если количество попыток ввода PIN-кода превышено (3 для пользователя, 3 для администратора), YubiKey блокируется и требует сброса, при этом все ключи теряются.
- Держите revoke.asc доступным, но безопасным, чтобы отозвать ключ в случае взлома.
- Создавайте новые субключи до истечения срока действия (например, каждый год) следующим образом:

```bash
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
gpg> addkey
```

Перенесите новые субключи в YubiKey и обновите открытый ключ на серверах:

```bash
gpg --keyserver hkps://keys.openpgp.org --send-keys C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Используйте второй YubiKey для резервирования:

```bash
gpg --import secret.asc
gpg --expert --edit-key C2033656849FC82BA3C365E33C9BF8B9CB86875D
```

Повторите действия с ключ-картой для второго YubiKey.

Если необходимо сбросить YubiKey:

```bash
ykman openpgp reset
```

Чтобы восстановить субключи из резервной копии:

```bash
gpg --import secret.asc
```

«Неиспользуемый открытый ключ»: убедитесь, что открытый ключ получателя импортирован и заслуживает доверия:

```bash
gpg --edit-key bob@example.com
gpg> trust
```
Установите значение 5 = Максимальная уверенность.

