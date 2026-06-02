---
layout: default
title: "Установите Debian"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only урок</span> <span>Этот проект поддерживается valerio-vaccaro</span></p>

## 🌍 Переводы

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Установите Debian
Подготовим флешку с образом Debian, скачанным с официального сайта.

Подключаем все кабели (дисплей, клавиатуру, мышь и Ethernet).

![alt text](https://officinebitcoin.it/lezioni/debian/1.jpg)

Подключаем установочную флешку.

![alt text](https://officinebitcoin.it/lezioni/debian/2.jpg)

Включим компьютер и убедимся, что наша флешка с Debian на борту работает.

![alt text](https://officinebitcoin.it/lezioni/debian/3.jpg)

## Установка
Если все работает правильно, должен запуститься установщик Debian, и в итоге мы окажемся на следующем экране.

![alt text](https://officinebitcoin.it/lezioni/debian/4.jpg)

Выбираем первую строку и запускаем графическую установку.

Первое, что нас спросят, это язык, для этой установки я выберу «Английский», который на мой взгляд более понятен, чем любой другой перевод.

![alt text](https://officinebitcoin.it/lezioni/debian/5.jpg)

На этом этапе нас спросят о нашем географическом положении. Чтобы найти Италию, мы должны выбрать ДРУГАЯ->ЕВРОПА->ИТАЛИЯ.

![alt text](https://officinebitcoin.it/lezioni/debian/6.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/8.jpg)

Здесь я тоже выбираю английскую локализацию.

![alt text](https://officinebitcoin.it/lezioni/debian/9.jpg)

И я настраиваю итальянскую клавиатуру, так как она у меня есть.

![alt text](https://officinebitcoin.it/lezioni/debian/10.jpg)

Затем мы выбираем имя пользователя и оставляем домен пустым.

![alt text](https://officinebitcoin.it/lezioni/debian/11.jpg)

На этом этапе Debian попросит выбрать пароль для пользователя root...

![alt text](https://officinebitcoin.it/lezioni/debian/12.jpg)

и создайте пользователя с соответствующим паролем.

![alt text](https://officinebitcoin.it/lezioni/debian/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/15.jpg)

Теперь нам нужно выбрать установочный диск, мы будем использовать весь диск и нам нужно выбрать диск, на который будет производиться установка.

![alt text](https://officinebitcoin.it/lezioni/debian/16.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/17.jpg)

Затем нам нужно выбрать структуру разделов, а пока мы оставим все в одном разделе.

![alt text](https://officinebitcoin.it/lezioni/debian/18.jpg)

Debian предлагает нам таблицу разделов, но... она добавила ненужный нам раздел подкачки, поэтому давайте выберем его и удалим из списка.

![alt text](https://officinebitcoin.it/lezioni/debian/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/20.jpg)

Теперь, когда мы удалили его, мы можем, наконец, написать нашу таблицу.

![alt text](https://officinebitcoin.it/lezioni/debian/21.jpg)

Debian хотел бы вернуться к настройке таблицы разделов, но мы отклоняем приглашение.

![alt text](https://officinebitcoin.it/lezioni/debian/22.jpg)

И мы подтверждаем наше желание написать обновленную таблицу.

![alt text](https://officinebitcoin.it/lezioni/debian/23.jpg)

Теперь нас спрашивают, хотим ли мы использовать зеркало Debian, и мы выбираем его.

![alt text](https://officinebitcoin.it/lezioni/debian/24.jpg)

Мы выбираем свою страну.

![alt text](https://officinebitcoin.it/lezioni/debian/25.jpg)

Обычно зеркало Гарра быстрое и надежное, мы пользуемся им.

![alt text](https://officinebitcoin.it/lezioni/debian/26.jpg)

У меня нет прокси, поэтому я оставляю поле пустым.

![alt text](https://officinebitcoin.it/lezioni/debian/27.jpg)

Но какие программы устанавливать? Так как мы создаем сервер, то отключаем графическое окружение (снимая первые две галочки) и выбираем SSH, к которому нам нужно будет получить удаленный доступ.

![alt text](https://officinebitcoin.it/lezioni/debian/28.jpg)

Установка начнется.

В конце нас спрашивают, хотим ли мы установить grub который позволит нам запустить Linux, отвечаем утвердительно и выбираем тот же диск, на который мы установили операционную систему.

![alt text](https://officinebitcoin.it/lezioni/debian/29.jpg)

![alt text](https://officinebitcoin.it/lezioni/debian/30.jpg)

Урааа, мы закончили, пришло время вынуть USB-накопитель и приступить к перезагрузке компьютера.

![alt text](https://officinebitcoin.it/lezioni/debian/31.jpg)

Если все работает правильно, мы должны увидеть терминал, предлагающий нам войти в систему с одним из профилей, созданных во время установки.

## Конфигурация

### Давайте соединимся
Давайте подключимся к нашему серверу с помощью `ssh username@ip`, где имя пользователя будет именем, выбранным при установке, а IP-адресом компьютера, на котором мы установили. 

Очевидно, что этот шаг можно пропустить, если вы устанавливаете систему с помощью монитора и клавиатуры вместо подключения по сети.

Обратите внимание, что Debian ЗАПРЕЩАЕТ вам подключаться через ssh с использованием учетных данных суперпользователя (т. е. root).

### Репозитории
Давайте обновим репозитории сейчас.

Становимся суперпользователем командой `su` и набираем пароль root.

Редактируем файл репозитория командой `nano /etc/apt/sources.list` и удаляем все присутствующие строки.

Добавим следующие строки.

```                                                                    
deb http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-proposed-updates contrib main non-free non-free-firmware

deb http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian/ bookworm-backports contrib main non-free non-free-firmware

deb http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware
# deb-src http://deb.debian.org/debian-security/ bookworm-security contrib main non-free non-free-firmware

```

Затем мы можем сохранить файл, нажав клавиши `CTRL+x`, а затем `y`.

Команда `apt udate` позволяет нам проверить, что все прошло гладко, и обновить список пакетов.

### Давайте обновим систему
Чтобы обновить систему, просто выполните следующие команды:

- `apt update` для обновления списка пакетов,
- `apt upgrade` для обновления установленных пакетов, для которых существует новая версия.

### Давайте установим Tor и будем использовать его по ssh
Чтобы установить Tor, просто используйте простую команду `apt install tor`.

После установки мы можем настроить его с помощью следующей команды `nano /etc/tor/torrc`.

Внизу файла добавляем следующие строки.

```
HiddenServiceDir /var/lib/tor/hidden_service/
HiddenServicePort 22 127.0.0.1:22
```

И мы перезапускаем tor с помощью `systemctl restart tor`, теперь мы можем найти наш луковый адрес с помощью `cat /var/lib/tor/hidden_service/hostname`.

Используя Tor, мы теперь можем подключиться к нашей машине из любой точки мира с помощью `torify ssh username@indirizzoonion.onion`.

## Программа
Установка Debian - это повторяющееся занятие, вот список уже проведенных:

| Дата | Заметки |
|------------------------|------------------------------------------------|
| 240415-2200 | Первый урок |
