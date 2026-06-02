---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix de Acinq es un wallet Lightning Network nativo, non-custodial, que ofrece un wallet eficiente conforme al estándar BIP39, bien conectado y que deja a los usuarios el control completo.

Pronto descubrirás que Phoenix abre un canal LN, de cuyo saldo eres responsable al 100%.
Para trabajar bien con Phoenix solo hacen falta una atención mínima y conocimientos básicos de Lightning Network. Aprenderás, por ejemplo, a mantener bajo control la liquidez de tu canal, a equilibrarlo según tus necesidades y a asegurarte de que Acinq te vea en línea para mantenerlo abierto y sostener la infraestructura LN.

# Operaciones básicas
Después de [descargar y verificar el apk de Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), puedes instalar la app en tu teléfono.

Phoenix se abre preguntándote si quieres crear un wallet nuevo o restaurar uno anterior. Si esta es tu primera experiencia con Phoenix, elige `Create new wallet`. Seguirá una serie de pantallas de bienvenida, que terminará donde pulsarás `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Una vez abierto Phoenix, **la primera operación que debes hacer es, como siempre, hacer el backup del wallet**.

Phoenix adopta el estándar BIP39, con ruta de derivación m/84'/0'/0', proporcionando una secuencia de 12 palabras para transcribir en papel y guardar en un lugar seguro.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entra en los menús y pide a Phoenix que te muestre la *Recovery phrase*, haciendo clic en `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Cuando termines, recuerda desplazarte hasta el final de la pantalla para confirmar que has realizado el backup y dejar de ver la notificación y la alerta.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

Phoenix está esencialmente listo para usarse. Tu nuevo wallet tiene saldo cero y se puede configurar. En la parte inferior izquierda encontrarás el comando para volver a entrar en los ajustes y configurar opciones útiles para el uso diario.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Uso con Tor
Desde hace varias versiones de Phoenix, Acinq ha desactivado el motor Tor integrado. Si quieres usar Phoenix con la protección de Tor, se requieren dos pasos:
- habilitar Tor en los ajustes de Phoenix
- usar una app de terceros para enrutar el tráfico del wallet por la red onion.

Accede a los ajustes y elige Tor, luego habilita `Enable Tor` y, por último, enruta el tráfico mediante la app que uses habitualmente (Orbot, Invizible Pro, etc.). Sin una de estas apps de terceros, pero con Tor habilitado en los ajustes de Phoenix, el wallet no podrá conectarse a internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Otros ajustes
Puedes cambiar o establecer varias funciones:
- el nombre del wallet, haciendo clic en la palabra `Wallet` en la parte superior;
- la moneda de referencia desde el submenú `Display`.
- establecer las comisiones en `Channel management`, un ajuste importante porque un valor de comisión demasiado bajo podría comprometer la apertura del canal: por defecto está fijado en 5,000 sats, súbelo a 15,000; Phoenix usará igualmente el valor adecuado en ese momento;
- deberías configurar todas las precauciones de seguridad que sientas que puedes gestionar, en el submenú `Access control`: PIN para gastar, PIN o control biométrico para acceder a la app;
- configurar tu propio `Electrum server` en el menú con ese nombre, teniendo en cuenta que Phoenix requiere un certificado SSL válido (Let's Encrypt, por ejemplo);
- habilitar `Experimental features` para solicitar una dirección LN Bolt12 reutilizable
- gestionar posibles cierres de canales o la creación/eliminación de varios wallets.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Apertura de un canal LN ⚡️

Desde la pantalla principal de Phoenix, elige el comando `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

El wallet te ofrece dos modos de recepción, ambos con código QR: Lightning y Onchain.

## Pagar una factura Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Una forma rápida de abrir tu canal LN es crear una factura con Phoenix y pagarla con otro wallet LN.

El primer pago entrante determina la apertura de un canal, cuya liquidez queda definida por el importe de la factura que acabas de crear (excluidas las comisiones de la transacción onchain de apertura del canal).

Los fondos podrían estar disponibles de inmediato, aunque se muestre un aviso temporal de espera de confirmaciones onchain. O quizá tengas que esperar para usarlos.

## Transacción onchain
Abrir un canal LN siempre es una transacción onchain, multisig 2-de-2: tú y la contraparte (Acinq) establecéis las condiciones, con tus fondos.

Si no tienes la posibilidad de pagar o recibir una factura Lightning, pero tienes fondos onchain, puedes usar la dirección onchain que Phoenix muestra para ti.

Después de la transacción, Phoenix se ve así:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

La app te advierte de que debes esperar 3 confirmaciones de blockchain antes de poder usar los fondos.

# Gestionar la liquidez del canal
En cuanto recibes las 3 confirmaciones, tu wallet LN está listo para usarse.

Al principio tiene toda la liquidez saliente y solo puedes gastar; puedes verlo en `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Puedes crear liquidez entrante pagando una o más facturas Lightning Network.

# Usar el wallet

Usar Phoenix wallet es una experiencia agradable y muy sencilla.

Lo único que debes tener presente es:
1. el canal que acabas de crear es un smart contract entre tú y Acinq, financiado con tus fondos;
2. el trabajo pesado de respaldar los estados del canal y mantener su infraestructura lo gestiona Acinq, que te cobrará algunos sat extra en comisiones por las operaciones de pago que realices;
3. accede a tu wallet con regularidad, abriéndolo y haciendo operaciones de vez en cuando porque, si la contraparte nota tu ausencia y te considera un "zombie", podría decidir cerrar el canal. Acinq cierra canales para evitar gastar recursos y tiempo manteniendo backups y canales inactivos;
4. también puedes decidir cerrar este canal si ya no necesitas usarlo.
5. en caso de cierre del canal, el procedimiento de `cooperative closure` es el mejor, porque evita muchos problemas.

## Splicing
Una mención especial merece la técnica `Splicing`, implementada por Acinq y que permite aumentar o reducir la capacidad total del canal.

Splicing es interesante: si tienes un canal con capacidad `tot`, puedes ampliarlo o reducirlo. Podría parecer que estas operaciones dependen de las necesidades de cada persona, **pero no es tan simple**.

Siempre debes tener presente que **Phoenix es un wallet Lightning Network** y, aunque tenga soporte para el Layer1 de Bitcoin, debería usarse para pagos pequeños en Layer2.

**Toda operación onchain, de hecho, será interpretada por Acinq como una razón para modificar la capacidad del canal**:
- recibir un importe de `xsats` en Phoenix desde un wallet onchain: Acinq amplía el canal, llevando la capacidad de `tot` a `tot + xsats`
- pagar un importe de `ysats` desde Phoenix a una dirección onchain: Acinq reduce el canal, llevando la capacidad de `tot` a `tot - ysats`.

`Splicing` es una transacción onchain (multisig 2-de-2) que implica comisiones. Aunque sean menores que las de apertura/cierre de canal, hacer estas operaciones sin cuidado o en el momento equivocado podría generar costes innecesariamente altos.

Para pasar de LN a Onchain y viceversa, intenta usar herramientas de `swap` adecuadas y no uses Phoenix Wallet para esto.

# Recuperar fondos
Por último, pero lo más importante de todo, aquí entra en juego la importancia de tener herramientas **non-custodial**.

Si y cuando el canal se cierre, puedes recuperar tus fondos onchain **importando las 12 palabras de backup en un wallet que soporte el estándar BIP39**.

Electrum wallet, entre otros, es una opción que hace que esta operación sea simple e intuitiva.

Si el wallet es, en cambio, *custodial* y no posees las claves, podrías encontrarte con problemas que van desde dificultades para interactuar con un *servicio de atención al cliente impersonal*, pasando por someterte a un pesado `kyc` para recuperarlas, **hasta la imposibilidad de recuperar tus fondos (sea cual sea el importe total)**.

¿Merece la pena?

# Apoyo al estudio
Si asististe a la presentación en directo en Telegram, puedes considerarla un paso más hacia tu soberanía personal (no solo financiera).
Si te la perdiste, **no desesperes**: estas notas sirven precisamente para ponerte al día y, además, debes saber que volveremos a proponerla en Officine.

Para no perderte la próxima presentación, únete al [grupo de Telegram](https://t.me/officinebitcoin) para mantenerte constantemente actualizado.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

También puedes encontrar el [Satoshi Spritz](https://satoshispritz.it/) más cercano. Un Satoshi Spritz es un meetup local donde se habla solo de Bitcoin, al que puedes llevar tus preguntas y recibir respuestas de otros bitcoiners expertos. En el enlace encontrarás el mapa de la península.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Por último, si no encuentras un meetup cerca de ti, puedes aprovechar las transmisiones en directo semanales de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creado para quienes no pueden asistir a Satoshi Spritz, o para ayudar a meetups más pequeños a tomar notas y encontrar inspiración para sus propias presentaciones.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
