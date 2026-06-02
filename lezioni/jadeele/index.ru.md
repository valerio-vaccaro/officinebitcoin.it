---
layout: default
title: "Jade с Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Урок Bitcoin-only</span> <span>Этот проект поддерживает valerio-vaccaro</span></p>

## 🌍 Переводы

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade с Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

После инициализации Jade можно начать им пользоваться, а для этого нужно выбрать wallet для просмотра.

Jade - это устройство, которое можно использовать с разными wallets, или companion apps, как Blockstream называет их на своем сайте.

В этом руководстве показаны этапы использования через USB с Electrum Wallet.

Возьмите инициализированный Jade. Сразу после включения он выглядит так:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

При выборе Unlock Jade появляется меню, в котором нужно выбрать способ подключения устройства к companion app.

С Electrum подключить Jade можно только через USB, поэтому следует выбрать этот вариант.

Запустите Electrum. Он откроется с вариантом по умолчанию: открыть последний использованный wallet.

Если Jade подключается к Electrum впервые, выберите Create New Wallet, а затем Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Дайте wallet имя, например Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Выберите Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

При выборе keystore принципиально важно выбрать Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum начинает сканирование в поисках hardware-устройства

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

При подключении USB к ПК (со стороны USB C он уже подключен к Jade) hardware wallet показывает экран блокировки. Jade разблокируется вводом шестизначного PIN, заданного во время setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

После разблокировки hardware-устройства Electrum обнаруживает Jade. Продолжайте, нажав Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

На этом этапе Electrum просит настроить script policy; выберите Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Начинается этап передачи публичного ключа из wallet на Jade в wallet просмотра Electrum.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

После завершения экспорта публичного ключа процедура окончена.

Watch-only wallet готов, и Electrum сообщает о завершении следующим экраном.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

Wallet действительно создан, и его можно начать изучать: видны addresses, wallet information и, что особенно важно, внизу справа можно заметить указание, что это wallet, созданный из Blockstream Jade. Зеленая точка рядом с логотипом Blockstream означает, что устройство включено и подключено правильно.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Транзакции получения и траты

В меню Receive Electrum сгенерируйте scriptPubKey (адрес) для получения средств. Всегда начинайте с небольшой суммы и выполняйте тест получение+трата.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

После получения sats их поступление можно проверить в меню History.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

После подтверждения транзакции можно потратить этот UTXO и завершить тест.

Для траты потребуется использовать Jade для подписи.

Перейдите в меню Send Electrum, вставьте scriptPubKey и внимательно проверьте его.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Когда закончите, нажмите Pay.

Откроется окно транзакции, в котором важно установить правильные transaction fees. После завершения всех настроек нажмите Preview внизу справа.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

Окно транзакции показывает несколько важных деталей, прежде всего status: Unsigned.

На этом этапе также можно увидеть команду Sign, предназначенную для добавления подписи с помощью Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum предупреждает, что нужно следовать инструкциям на hardware-устройстве, которое готово к подписи.

Однако перед этим лучше проверить, что именно подписывается: все параметры только что настроенной транзакции также появляются на Jade, и их все можно проверить.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Чтобы продолжить, убедитесь, что курсор всегда находится на стрелке →, ведущей к следующим этапам, и никогда на "X", который отменяет операцию.

Отображение проверок заканчивается, когда Jade показывает fees. В этот момент подтверждение равнозначно добавлению подписи.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Короткое мгновение Jade обрабатывает подпись.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Тем временем в Electrum можно проверить status транзакции: он изменился с Unsigned на Signed, и теперь транзакцию можно распространить, нажав Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

Wallet, протестированный таким образом, можно использовать для получения UTXO, предназначенных для безопасного хранения.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
