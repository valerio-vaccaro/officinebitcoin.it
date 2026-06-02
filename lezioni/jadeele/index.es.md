---
layout: default
title: "Jade con Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traducciones

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade con Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Después de inicializar Jade, es posible empezar a usarlo y, para hacerlo, hay que elegir un wallet de visualización.

Jade es un dispositivo que puede usarse con distintos wallets, o companion apps como las define Blockstream en su sitio web.

En este tutorial se verán las fases de uso, vía USB, con Electrum Wallet.

Toma el Jade inicializado. Al encenderlo, aparece así:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Al seleccionar Unlock Jade, aparece el menú en el que se debe elegir cómo conectar el dispositivo a la companion app.

Con Electrum es posible conectar Jade solo vía USB, por lo que se debe elegir esa opción.

Inicia Electrum, que se abrirá proponiendo como opción predeterminada la apertura del último wallet utilizado.

Si es la primera vez que conectas Jade a Electrum, selecciona Create New Wallet y luego Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Da un nombre al wallet, por ejemplo Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Selecciona Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

Al elegir el keystore, es fundamental seleccionar Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum inicia el escaneo en busca del dispositivo hardware

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

Al conectar el USB al PC (ya conectado por el lado USB C a Jade), el hardware wallet muestra la pantalla de bloqueo. Jade se desbloquea introduciendo el PIN de seis dígitos configurado durante el setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Una vez desbloqueado el dispositivo hardware, Electrum detecta Jade. Continúa haciendo clic en Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

En este punto Electrum pide configurar la script policy; elige Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Comienza la fase de transferencia de la clave pública desde el wallet en Jade a Electrum de visualización.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

Al finalizar la exportación de la clave pública, el procedimiento ha terminado.

El wallet watch-only está listo y Electrum avisa de la finalización con la pantalla siguiente.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

El wallet se ha creado realmente y es posible empezar a explorarlo: se ven las addresses, la wallet information y, sobre todo, se puede notar abajo a la derecha la indicación de que se trata de un wallet creado desde Blockstream Jade. El punto verde junto al logo de Blockstream indica que el dispositivo está encendido y conectado correctamente.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Transacciones de recepción y de gasto

Desde el menú Receive de Electrum, genera un scriptPubKey (dirección) para recibir fondos. Empieza siempre con un importe pequeño y haz una prueba de recepción+gasto.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Una vez recibidos los sats, se puede comprobar su llegada en el menú History.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Una vez confirmada la transacción, se puede gastar este UTXO y terminar la prueba.

El gasto requerirá el uso de Jade para firmar.

Ve al menú Send de Electrum, pega un scriptPubKey y compruébalo bien.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Cuando hayas terminado, pulsa Pay.

Se abre la ventana de transacción, en la que es importante establecer las fees de transacción correctas. Terminados todos los ajustes, haz clic en Preview abajo a la derecha.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

La ventana de transacción muestra algunos detalles importantes, ante todo el status: Unsigned.

En esta fase también es posible ver el comando Sign, precisamente para aplicar la firma con Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum avisa de que hay que seguir las instrucciones en el dispositivo hardware, que está listo para firmar.

Antes, sin embargo, es mejor verificar qué se está firmando: todos los parámetros de la transacción recién configurada también aparecen en Jade y es posible verificarlos todos.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Para continuar, asegúrate de colocar siempre el cursor en la flecha → que lleva a las fases siguientes, y nunca en la "X" que cancela la operación.

La visualización de las verificaciones termina cuando Jade muestra las fees. En este punto, confirmar equivale a poner la firma.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Durante un breve instante Jade procesa la firma.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Mientras tanto, en Electrum se puede comprobar el status de la transacción, que ha cambiado de Unsigned a Signed, y ahora es posible propagar la transacción haciendo clic en Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

El wallet, probado de esta manera, puede utilizarse para recibir UTXO destinados a conservarse de forma segura.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
