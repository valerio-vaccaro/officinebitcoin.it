---
layout: default
title: "Jade airgapped con Sparrow Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade airgapped con Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Usar Jade para comunicaciones completamente airgapped es posible gracias a las características de su firmware y hardware.

La cámara integrada y la pantalla, de hecho, cumplen exactamente la función de adquirir y enviar mensajes hacia y desde el wallet watch-only.

Este tutorial muestra cómo usar Jade airgapped con Sparrow Wallet.

El procedimiento incluye primero la configuración, luego la exportación de la clave pública extendida desde Jade a Sparrow-watch-only y, finalmente, una transacción de gasto.

Por elección didáctica, se decidió empezar mostrando la secuencia de operaciones desde Jade.

## Configuración avanzada

La elección de usar el dispositivo airgapped implica una configuración real, es decir, debe hacerse en el momento de la inicialización de Jade (1), por lo que debe presentarse como no inicializado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Aparece un aviso para consultar las instrucciones de configuración en el sitio https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

La configuración de Jade para uso airgapped solo puede realizarse eligiendo Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

Jade advierte que esta configuración tiene algunas funciones técnicas avanzadas. Basta con prestar la máxima atención y pulsar el botón de confirmación.

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Con el objetivo de introducir la mnemónica generada con entropía de dados, elige Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Ahora debes establecer la longitud de la mnemónica, 12 o 24 palabras. El menú también ofrece la posibilidad de restaurar el wallet escaneando un código QR: se trata del SeedQr, que se explicó en el tutorial dedicado a la configuración.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Por motivos puramente didácticos y de rapidez, este tutorial muestra la configuración con una mnemónica de 12 palabras.

El siguiente paso debe seguirse como se describe para poder acceder a la funcionalidad airgapped. De hecho, debes elegir exportar la frase de recuperación en formato CompactSeedQR, seleccionando Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Después de elegir, se te advierte que debes dibujar el código QR en la plantilla incluida en la caja, como se muestra en la sección "Extra" de la lección dedicada a la configuración.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Al final del procedimiento, debes verificar la correspondencia entre lo dibujado y el CompactSeedQR mostrado por el dispositivo. De hecho, se habilita la cámara integrada de Jade, con la que debes encuadrar el SeedQR que acabas de dibujar.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Si el dibujo corresponde a lo que el dispositivo propuso en el procedimiento recién completado, se muestra una señal de confirmación.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Ahora Jade muestra las opciones para conectar el dispositivo a una companion app: elige QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

El siguiente paso también requiere una elección del usuario: guardar las claves cifradas en el dispositivo o cargarlas en cada sesión escaneando el SeedQR recién dibujado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

Nota:

Es útil entender estas dos opciones de acceso:

- QR PIN Unlock: Durante la inicialización, Jade guardará los datos del wallet cifrándolos en el dispositivo; siempre serán accesibles desbloqueando Jade con el procedimiento QR PIN.
- SeedQR: Jade debe escanear el SeedQR cada vez que se quieran cargar las claves en el dispositivo.

Por elección didáctica, en la opción anterior se eligió SeedQR, por lo que el dispositivo se usará stateless: Jade advierte que la sesión es temporal y que las claves serán "olvidadas" por el dispositivo cuando se apague.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Exportación de clave pública

Ahora que Jade está configurado específicamente para funcionar completamente airgapped, pasamos a la fase delicada de exportar la clave pública.
 
Partiendo siempre de Jade, que ha vuelto a los menús iniciales, elige Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

Nota: que Jade esté en modo Temporary Signer es visible por el icono que representa un reloj junto a la indicación Active.

En Options, elige Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Luego selecciona Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

En este punto, la pantalla de Jade muestra un código QR dinámico que representa la clave pública extendida. En Options de este submenú, puedes elegir la exportación de multisig/singlesig y la ruta de derivación.

Para este tutorial, se eligió exportar un singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

Es en esta fase cuando entra en juego Sparrow. Inicia el programa y crea un nuevo wallet eligiendo New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Da un nombre al wallet y luego haz clic en Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

En la siguiente pantalla de ajustes, haz clic en Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Se abre una ventana de Sparrow que muestra los hardware wallets implementados. Elige Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

En este punto, se activa la cámara del PC con el que estás trabajando.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Si tienes más de una webcam disponible, selecciona la mejor en el menú desplegable donde aparece Default Camera.

Ahora toma Jade (que mientras tanto sigue mostrando el código QR dinámico que representa el Xpub) y coloca la pantalla frente a la cámara del PC, manteniendo el código QR dentro del espacio delimitado por líneas discontinuas.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Debajo de la imagen de la cámara hay una barra de desplazamiento que se vuelve azul.

El avance de la adquisición del Xpub en Sparrow se indica de ese modo: de 0 a 100%.

En esta fase pueden ser necesarios algunos ajustes: aumentar/disminuir el brillo de la pantalla de Jade, así como la iluminación frontal, o elegir en el menú desplegable de Sparrow Use HD Capture o una reducción de resolución.

No te asustes por estos detalles: una vez configurado tu entorno personal de trabajo, estas fases procederán con completa comodidad y facilidad. (2)

De hecho, la exportación se ha producido cuando se cierra la ventana de la cámara y, al volver a Settings de Sparrow, aparecen todos los datos del wallet watch-only.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Por la estructura de Sparrow, ahora es necesario aplicar la script policy haciendo clic en Apply.

La creación del wallet continúa introduciendo y confirmando una contraseña para cifrar el archivo del wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

Y concluye cuando la barra de desplazamiento situada abajo a la derecha ha llenado el campo hasta el 100%.

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transacción de gasto

Si, hipotéticamente, Jade cumple el papel de hardware wallet personal, hay que asumir que tiene fondos y que estos deberán gastarse en el futuro.

Después de elegir Sparrow como wallet watch-only y Jade como dispositivo de firma, veamos cómo construir, firmar y propagar una transacción con estas dos herramientas.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

En el ejemplo, hay disponible un saldo total de 56,598 sats.

En el menú izquierdo de Sparrow, selecciona Send y empieza a construir la transacción de gasto. Después de configurar todo, haz clic en Create transaction abajo a la derecha.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Aparece una ventana avanzada de transacción, donde se ve que Sparrow reconoce a Jade como dispositivo de firma (Signing Wallet).

Si los ajustes son satisfactorios, haz clic en Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Aparece la pantalla de firmas. En un sistema airgapped, la exportación del .psbt se realiza mediante código QR, así que en Sparrow haz clic en Show QR abajo a la izquierda.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Aparece una ventana con un código QR dinámico, que representa la psbt y que luego deberá escanearse con la cámara de Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Toma Jade y desde los menús principales selecciona Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Encuadra con la cámara de Jade, ya activada, el código QR dinámico que Sparrow está generando. Una barra azul en la pantalla del hardware wallet indica el porcentaje de lectura completado.

Cuando termina la importación de la psbt, Jade muestra los detalles de la transacción para su verificación: dirección de destino e importe en una primera pantalla

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

y las comisiones en una segunda pantalla. Al confirmar en esta última, Jade aplica la firma.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automáticamente, la pantalla de Jade muestra otro código QR dinámico: es la transacción firmada.

Entre las opciones de esta pantalla, puedes aumentar/disminuir la densidad para mejorar la comunicación con la wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Mientras tanto, Sparrow, que dejamos mostrando un código QR dinámico, debe configurarse para recibir la transacción firmada y propagarla.

Por tanto, debes hacer clic en Scan QR para reactivar la webcam del PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Coloca la pantalla de Jade frente a la webcam y deja que Sparrow importe la transacción firmada.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

La barra de desplazamiento bajo la imagen debe completarse al 100% hasta que se produzca la importación, que Sparrow muestra de la siguiente manera.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Ahora toda la transacción se verifica de nuevo y, si está correcta, se puede propagar haciendo clic en Broadcast Transaction.

En el menú Transactions aparece la transacción saliente.

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Notas

- (1) – Si Jade ya está inicializado, basta con ir al menú Options → Settings → Factory reset
- (2) – Jade Original tiene una pantalla muy pequeña y, para encuadrar el código QR dinámico en el espacio discontinuo que muestra Sparrow, es necesario acercar la pantalla a unos pocos centímetros. Por tanto, podría ser necesario equiparse con una webcam de muy alta resolución con una distancia focal adecuada, o recurrir a apps como Iriun para "transformar" un teléfono en la cámara del PC. Los teléfonos, de hecho, tienen una capacidad de enfoque superior a corta distancia.
