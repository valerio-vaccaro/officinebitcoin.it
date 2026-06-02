---
layout: default
name: "Comprender el Coin Control manual"
description: "Guía completa para la selección manual de UTXO. Entiende por qué es importante y aprende a hacerlo con varias software wallets (de escritorio y móviles)"
title: "Comprender el Coin Control manual"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Comprender el Coin Control manual

## Introducción

La solidez del protocolo Bitcoin está garantizada por conceptos básicos sencillos. Entre ellos destaca la transparencia: todas las transacciones de Bitcoin son públicas y cualquiera puede verificarlas fácilmente. Aunque esta característica es una piedra angular del protocolo, porque evita el fraude y garantiza la autenticidad de los fondos, también puede suponer un reto para la confidencialidad. **¿Te has preguntado alguna vez si tanta transparencia puede afectar a tu privacidad?**

Deberías hacerlo. Aunque acumular satoshis non-KYC es bastante sencillo, tu privacidad corre más riesgo durante la fase de gasto.

## Qué ocurre cuando gastas un UTXO
Gastar Bitcoin no es simplemente transferir valor a otra persona.

Al consumir uno de tus UTXOs, debes satisfacer las condiciones impuestas por la transparencia del protocolo, porque tienes que demostrar la propiedad de esos fondos. Por tanto, debes:
- exponer tu clave pública;
- producir una firma digital.

El momento del gasto es, por tanto, el más crítico: **gastar bitcoin es un acto que debe hacerse con conciencia y con el mayor control posible**.

## Coin Control
En el protocolo Bitcoin no existen elementos como "cuenta" o "unidad monetaria". El concepto de UTXO no es el foco de esta lección, pero te invito a hacer preguntas a tu Satoshi Spritz de confianza o a solicitar una lección aquí en Officine Bitcoin.
Lo que necesitas saber es que, con Bitcoin, lo que acumulas y luego gastas son unidades contables pequeñas o grandes medidas en satoshis, representadas por `unspent transaction outputs`, los **UTXOs**, también llamados `coins`.
Cuando usas UTXOs para crear una transacción, estos se destruyen por completo y se crean nuevos UTXOs en su lugar.

Las software wallets están desarrolladas para tomar esta decisión automáticamente, usando coins seleccionadas "al azar" con el único criterio de cubrir el importe de gasto requerido.

`Coin Control`, también llamado `Coin Selection`, es una función de algunas software wallets que te permite **seleccionar manualmente los UTXOs que gastar al construir tu transacción**.

Supongamos que tienes una wallet con 3 UTXOs, respectivamente de 21,000, 42,000 y 63,000 satoshis.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Si necesitas gastar 24,000 sats y dejas que el software seleccione automáticamente, una buena wallet podría elegir combinar UTXO1 + UTXO2 para pagar los 24k sats y las comisiones de minería, creando un cambio que vuelve a una dirección interna de la wallet de origen.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Después de la transacción, la nueva situación en la wallet, contando solo los UTXOs, puede resumirse así.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Con el software adecuado y tu propia conciencia, sin embargo, podrías haber tomado una decisión distinta y más correcta. Por ejemplo, seleccionando solo UTXO2 (42,000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Con una situación final de UTXOs en tu wallet que se ve diferente.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## ¿Por qué seleccionar manualmente los UTXOs?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

En nuestro ejemplo, el saldo es en realidad el mismo: `108,280 sats`. Después de gastar 24,000 sats, sin coin control tendríamos 2 UTXOs en la wallet; con coin control manual tenemos 3 en total.

**¿Por qué hacer todo esto?**

Hay, o podría haber, varias razones por las que no usamos `UTXO1` **y todas están en la raíz de por qué - al gastar - activar el coin control manual es una buena práctica a seguir**.

## Privacidad
La ventaja principal, cuando hablamos de selección manual de coins, es **una mayor privacidad para quien gasta**.

Volvamos a nuestro ejemplo: gastar 24,000 satoshis _sin coin control_. Como la blockchain de Bitcoin es un registro público, un observador externo puede afirmar, sin duda, que los inputs `UTXO1 of 21,000 sats` y `UTXO2 of 42,000 sats`, así como el cambio, `UTXO5 of 38,280 sats`, **pertenecen todos al mismo usuario**.

Al seleccionar manualmente `UTXO2`, en cambio, `UTXO1` permanece completamente privado, dentro del UTXO set a la espera de ser gastado en un momento más apropiado.

`UTXO1` podría venir de una fuente KYC, por ejemplo un pago recibido por bienes y servicios, mientras que los otros UTXOs no.

**Si fuera tu wallet, ¿querrías que un observador externo pudiera rastrear tu identidad con tanta certeza?** Las wallets que implementan selección manual de UTXO permiten, por ejemplo, la **segregación de uno o más UTXOs**, una función que conviene usar cuando se presentan estas situaciones.

Aunque creo que los fondos KYC deberían mantenerse en una wallet separada de los bitcoin non-KYC, si este es tu caso, segregar algunas de tus direcciones es una ayuda fundamental, que puedes obtener aprendiendo a seleccionar manualmente tus inputs de gasto.

## Ahorro en comisiones
Seleccionar el UTXO correcto para un gasto te permite optimizar las comisiones. De nuevo, en nuestro ejemplo, la software wallet seleccionó dos UTXOs para cubrir el gasto. Dos UTXOs significan dos firmas que mostrar a la red, así que un mayor peso de transacción en términos de vBytes.

Usando coin control manual, puedes seleccionar solo uno que sea suficiente para cubrir el importe, ahorrando comisiones porque el "peso" de la transacción disminuye.

Cuando las comisiones son altas, pero te ves obligado a gastar bitcoin on-chain (por ejemplo, para abrir un canal de Lightning Network), el coin control se convierte en el incentivo económico correcto para usarlo.

## Agregación del cambio
Al hacer un pago y usar Bitcoin on-chain, la posibilidad de recibir cambio casi siempre se convierte en una certeza. Cada cambio es en sí mismo una pequeña pérdida de privacidad, ya que revela a la red una de tus direcciones que puede asociarse con tu input original.

Teniendo en cuenta que las mejores HD wallets generan direcciones especiales para el cambio, puedes reconocerlas fácilmente y "segregar" todo el cambio de varias transacciones; cuando alcance una cierta cantidad, puedes seleccionarlo y consolidarlo manualmente, o intercambiarlo en Lightning Network (mi método favorito) para recuperar la privacidad perdida durante el gasto.

## Gastar desde una cold wallet
Una cold wallet es una herramienta con la que puedes alcanzar razonablemente un buen grado de seguridad, para almacenar cualquier cantidad de fondos que quieras apartar durante mucho tiempo. Sin embargo, pueden surgir imprevistos que te obliguen a acceder a tus ahorros y cubrir gastos inesperados.

Mi consejo es **no gastar nunca directamente desde la cold wallet, para evitar recibir cambio entre las direcciones de esa misma wallet**. Aprende a seleccionar manualmente los UTXOs necesarios para cubrir el gasto, transfiérelos a una hot wallet y prepara tu transacción desde ahí. Cualquier cambio, después, puedes enviarlo de vuelta a una dirección de cold wallet (si el importe es adecuado), o usarlo para otros fines.

## Demostración práctica
Después de esta larga introducción, veamos cómo poner en práctica coin control con distintos software de escritorio y móviles. Usaremos siempre la misma HD wallet, importada en cada una de las herramientas elegidas, para mostrarte las pequeñas diferencias entre ellas.

## Desktop Wallets

## Sparrow
Si usas Sparrow, abre tu wallet y selecciona _UTXOs_ en el menú de la izquierda. Verás la lista de todos los UTXOs asociados a tu wallet.

Simplemente haz clic en uno y luego elige _Send Selected_. Sparrow también te muestra el total seleccionado para gastar, junto al comando.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

También puedes seleccionar más de uno. Usa la tecla _CTRL_ para seleccionar UTXOs no adyacentes en la lista.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Después de seleccionar manualmente los UTXOs, Sparrow te mostrará claramente, de forma gráfica, cómo se construye tu transacción, que luego puedes finalizar y completar.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Segregación de UTXO
Segregar fondos significa "bloquearlos" dentro de la wallet para que no puedan usarse como inputs de transacción.

Sparrow permite esta función, accesible desde el menú _UTXOs_. Pasa el cursor sobre el UTXO que quieres "bloquear" y haz clic derecho. Entre las opciones encontrarás _Freeze_. Así puedes segregar un UTXO con Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Si tu desktop wallet es Electrum, puedes seleccionar manualmente UTXOs tanto desde los menús _Addresses_ como _Coins_.
En ambos menús, la selección se realiza colocando el ratón sobre el UTXO y eligiendo _Add to coin control_ después de hacer clic derecho.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

También puedes seleccionar más de un UTXO, usando la tecla _CTRL_ si no son adyacentes.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum resaltará gráficamente en verde los UTXOs seleccionados y, en la parte inferior, una barra resaltada con el mismo color muestra el saldo disponible después del coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Una vez seleccionados los output(s), puedes construir tu transacción como siempre desde el menú _Send_.

### Segregación de UTXO
Electrum ofrece esta opción en el menú _Coins_ seleccionando un UTXO específico y luego eligiendo _Freeze_ con el botón derecho del ratón. También puedes "congelar" una dirección sin fondos desde el menú _Addresses_, o la "coin" para impedir el gasto.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk te permite seleccionar UTXOs desde el menú principal una vez abierto.
Inicia Nunchuk y haz clic en _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Se abre una ventana con todos los UTXOs de tu wallet, donde puedes seleccionar uno o más marcando la casilla junto a cada importe. Después de la selección, continúa con _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Luego puedes introducir la dirección de destino, definir el importe y las comisiones.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, antes conocida como Green, permite la selección de coins una vez que has empezado a construir la transacción. Abre tu wallet y haz clic en _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Pega la dirección de destino en el campo correspondiente y luego selecciona _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Se abre una ventana donde puedes seleccionar uno o más UTXOs. En el ejemplo siguiente, seleccionamos dos coins. Luego confirma la elección haciendo clic en _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Define el importe y las comisiones, luego procede como siempre con tu transacción.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Nota: En el menú _Coins_ de Green hay opciones _Lock_/_Unlock_ que sugieren la posibilidad de segregar UTXOs. Esto solo está disponible en las llamadas cuentas multisig; la función solo se activa para UTXOs muy pequeños, cerca del umbral `Dust`.

## Mobile Wallets

## Blue Wallet
Incluso en móvil, puedes elegir wallets que permitan la selección manual de UTXO. Veamos primero Blue Wallet.

Si usas este software, abre tu wallet y haz clic para entrar en las pantallas de comando de una de tus wallets. Para acceder a coin control, debes entrar en la fase de gasto, así que haz clic en _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

En la pantalla siguiente, elige el menú indicado por los tres puntos en la parte superior derecha. Se abre una ventana desplegable con varios comandos. Elige el último: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

En este punto, Blue Wallet muestra todos tus UTXOs. Además de los importes, se diferencian gráficamente por colores distintos.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Selecciona el UTXO y luego selecciona _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet te devuelve a la ventana _Send_ para continuar construyendo la transacción. Ajusta el importe y las comisiones, luego elige _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Ahora puedes completar la transacción como siempre.

### Segregación de UTXO
Blue Wallet también te permite segregar UTXOs, dejándolos no disponibles para gastar, una función interesante para una mobile wallet.

Accede a coin control como se explicó arriba y, después de seleccionar el UTXO, elige _Freeze_ en lugar de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
La versión móvil de Nunchuk también permite a los usuarios realizar coin control. Si usas esta app en móvil, ábrela y ve al menú _Wallet_. Desde ahí, elige _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

En la ventana con la lista de UTXOs, haz clic en _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Junto a cada UTXO aparece la función de selección. Como en la versión de escritorio, en Nunchuk mobile la selección manual se realiza marcando la casilla junto al importe. La pantalla muestra el número de UTXOs seleccionados y el importe total disponible. Una vez terminado, el símbolo ₿ en la parte inferior izquierda es el comando para empezar a construir la transacción.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Ahora puedes completar la transacción, eligiendo el importe y haciendo clic en _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continúa como siempre, pegando una dirección de destino, una descripción y personalizando la configuración de comisiones.

## Bitcoin Keeper
Bitcoin Keeper es la última wallet que veremos en esta guía. Veamos su función de coin control con una wallet single-sig, aunque ese uso no sea el propósito principal de esta app en particular.

Después de configurar Keeper en tu teléfono, lánzala y abre una wallet que contenga algunos UTXOs. En el centro de la pantalla principal, haz clic en _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper muestra una vista general de los UTXOs. Para acceder a la pantalla de selección, haz clic en _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Puedes seleccionar coins marcándolas, haciendo clic en el comando correspondiente. Cuando termines, haz clic en _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper te lleva directamente al menú _Send_, donde puedes construir la transacción con los UTXOs seleccionados.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Cada una de las software wallets vistas en esta guía puede ser la interfaz watch-only de tu hardware wallet. Esto significa que el coin control para un dispositivo de firma offline se realiza con los pasos vistos hasta ahora.

## Recomendaciones generales
Coin control es una práctica muy eficaz para seleccionar tus inputs de transacción. La selección manual es aún más eficiente si, al recibir tus fondos, has etiquetado bien el origen de tus satoshis. Si quieres dominar esta técnica, recomiendo el tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
