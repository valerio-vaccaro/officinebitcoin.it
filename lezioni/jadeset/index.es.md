---
layout: default
title: "Configuración de Jade"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Configuración de Jade

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade llega en un embalaje cuya integridad debe verificarse, comprobando los dos adhesivos holográficos antimanipulación colocados entre la caja (parte inferior) y la tapa (parte superior).

El paquete contiene un pequeño manual de usuario, dos plantillas CompactSeedQR y el hardware wallet.

Jade se enciende manteniendo pulsado el botón inferior y se presenta mostrando los 3 menús:

- Setup Jade
- Scan QR
- Options

En Options se pueden ajustar varios parámetros, según las preferencias personales, pero la inicialización es la primera parte que hay que completar.

Usando el botón de desplazamiento, selecciona el menú __Setup Jade__ y confirma con el botón frontal.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Aparece un aviso para consultar las instrucciones de configuración en el sitio https://blockstream.com/jade/

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

Para una ejecución correcta, se recomienda crear la mnemónica con tiradas de dados y usar esa entropía para crear el wallet. Por tanto, elige __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade advierte que esta configuración tiene algunas funciones técnicas avanzadas. Basta con prestar la máxima atención y pulsar el botón de confirmación.

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

Con el objetivo de introducir la mnemónica generada con entropía de dados, elige __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Ahora debes establecer la longitud de la mnemónica, 12 o 24 palabras. El menú también ofrece la posibilidad de restaurar el wallet escaneando un código QR: se trata del SeedQr, que se tratará en otro lugar.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Por motivos puramente didácticos y de rapidez, este tutorial muestra la configuración con una mnemónica de 12 palabras.

Comienza el procedimiento para introducir la primera palabra y Jade muestra el teclado para escribir las letras correspondientes. Con el botón de desplazamiento, colócate ← → en la posición correcta.

En este ejemplo, la palabra n.º 1 es "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Después de introducir las primeras 3-4 letras, Jade toma palabras del diccionario BIP39 y empieza a ofrecer una serie de sugerencias. Con el botón de desplazamiento, avanza o retrocede hasta encontrar la palabra correcta.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Continúa introduciendo palabras hasta llegar al momento de la última palabra: el checksum.

En este punto, Jade muestra dos posibilidades: introducir una palabra existente u ofrecer la posibilidad de calcular un checksum válido con su propio software.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Nota:

- En el caso de una configuración a partir de una mnemónica de 12 palabras creada con tiradas de dados, se recomienda elegir Existing e introducir las primeras letras de la palabra, eligiéndolas dentro del rango propuesto por la tirada de dados.
- Si la configuración parte, en cambio, de una mnemónica de 24 palabras generada con tiradas de dados, puedes hacer que Jade calcule todos los checksum posibles y luego elegir uno. Es cierto que se pierde algo de entropía, pero solo en la última palabra. Cuando has decidido confiar tus fondos a Jade, es una compensación aceptable.
- En caso de restaurar un wallet existente: introduce el checksum correcto eligiendo Existing.

Continuando con el ejemplo de configuración desde una mnemónica generada con tiradas de dados, elegimos Existing en el menú anterior, con la intención de introducir las letras y encontrar el checksum correspondiente.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

En este punto, Jade propone exportar la frase de recuperación en forma de _CompactSeedQR_.

El _CompactSeedQR_ es una codificación que transforma la frase mnemónica en un código QR que se escanea para restaurar el wallet en Jade.

Si quieres probarlo, consulta la sección al final de este tutorial que explica cómo hacerlo.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Al elegir "No" en el menú anterior, puedes continuar hasta el final de la configuración.

El dispositivo está listo para conectarse a su wallet watch-only.

El siguiente menú muestra las posibilidades de conexión:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Elige USB y confirma con el botón de confirmación.

En este punto, Jade pide conectarse a una companion app.

En el siguiente ejemplo se eligió conectar el dispositivo por USB a Blockstream Green; este wallet, de hecho, permite controlar las actualizaciones de firmware de Jade y, al escuchar el dispositivo por USB, ofrece una configuración guiada.

Abre Green y comprueba los ajustes de red y seguridad.

Si hay una actualización de firmware, Green la señala inmediatamente y se recomienda realizar la actualización.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

Una vez completada la actualización del firmware, Green empieza a interactuar con Jade.

En este punto, el dispositivo de firma pide establecer el duress PIN, que cifrará las claves privadas en Jade, haciéndolas inaccesibles para cualquiera salvo para quien posea el PIN de seis dígitos.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Mientras Green espera con la pantalla mostrada arriba, en Jade aparece la posibilidad de establecer el PIN de 6 dígitos y confirmarlo introduciéndolo de nuevo correctamente.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade crea datos persistentes cifrándolos en el dispositivo.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

Al final de la operación, que puede tardar unos instantes, Green abre el wallet listo para usar.

Al apagar Jade y volver a encenderlo, el dispositivo se presentará como inicializado, con el firmware actualizado y listo para desbloquearse (Unlock Jade) para usarlo con su companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: creación de CompactSeedQR

Al final de la introducción de la mnemónica, omitimos la parte de exportación de claves en formato de código QR para mantener el foco en la fase de configuración. Este tipo de exportación siempre puede hacerse más adelante.

Enciende Jade y desde el menú Options → Temporary Signer → Continue → 12/24 Words vuelves al menú de introducción de la frase de recuperación, al final del cual se propone la pantalla de elección para exportar en formato SeedQR.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Al elegir Yes, se te advierte que debes dibujar el código QR en la plantilla incluida en la caja.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

El procedimiento empieza mostrando una vista general de cómo será el código QR que hay que dibujar (algunas partes están borradas por motivos de privacidad).

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

A continuación, se mostrarán todas las casillas de la cuadrícula, una por una, de A1 a C3 o E5 según la longitud de la frase de recuperación.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

Después de dibujar la última casilla de la cuadrícula, Jade vuelve a mostrar la vista general para una primera verificación. Continúa confirmando Done.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Se habilita la cámara integrada de Jade, con la que debes encuadrar el SeedQR que acabas de dibujar.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Si el dibujo corresponde a lo que Jade propuso en el procedimiento recién completado, se mostrará una señal de confirmación.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

Al pulsar para confirmar Continue, Jade se presenta funcionando desde los menús principales.

El CompactSeedQR es una herramienta para restaurar el wallet en Jade.
