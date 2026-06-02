---
layout: default
name: "Kit inicial de Bitcoin"
description: "Un kit inicial simple y fácil de implementar para usar Bitcoin correctamente. Aprende a descargar e instalar una wallet móvil, configurar un POS para solicitudes de pago y descubrir ajustes avanzados de la wallet."
title: "Glosario inicial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traducciones

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

Esta es una excelente forma de empezar a usar Bitcoin de la manera más correcta posible. Lo que sigue es una propuesta de *starter kit* muy ligero y fácil de implementar, que puedes configurar de forma autónoma.

Tanto si eres una persona curiosa, un profesional que quiere aceptar Bitcoin como método de pago o un usuario experto que busca soluciones para amigos y familiares, esta guía te permitirá:
- descargar e instalar una wallet móvil para usar Bitcoin en todos los niveles (onchain para almacenamiento a largo plazo; o Liquid y Lightning para pagos instantáneos);
- configurar un POS para generar solicitudes de pago a partir del precio de tus bienes/servicios en euros;
- conocer los ajustes avanzados de la wallet. Hemos dejado esta parte al final de la guía para simplificar el primer acercamiento, pero revísala siempre, porque es importante.

Aclaremos primero qué queremos decir al hablar de usar Bitcoin de la forma *correcta*.

# Glosario inicial
- `Not your keys, not your coins`
  Si te estás acercando a Bitcoin por primera vez, la frase `Not your keys, not your coins` te resultará nueva y su sentido se reducirá a la traducción literal. Bitcoin funciona según el principio de la criptografía asimétrica, basada en pares de claves públicas y privadas. Solo con la posesión **única** y la gestión individual de las claves privadas puedes decir que tienes control sobre tus Bitcoin.
  
  Por tanto, debes ser la única persona que conoce las claves privadas, el secreto que te permitirá poseer y eventualmente gastar los bitcoin asociados a esas claves. `Not your keys, not your coins` es prácticamente un _mantra_ para los bitcoiners de todo el mundo y también lo será para ti.

- `Recovery phrase`
  Durante su breve historia, el protocolo Bitcoin ha evolucionado para hacer más sencilla la gestión de los secretos, es decir, de las claves privadas. Hoy se representan como una secuencia de 12 o 24 palabras en inglés, una forma más simple de transcribirlas y verificarlas. Las palabras son el secreto principal que debes conservar. Deben transcribirse en papel y guardarse en un lugar muy seguro, como una caja fuerte. Nunca deben fotografiarse, transferirse a un ordenador ni, mucho menos, compartirse con otras personas.

- `Wallet`
  La wallet es la herramienta que te permitirá ver tu saldo, aceptar Bitcoin y gastarlos. Durante este tutorial descargaremos una en tu teléfono. La wallet del teléfono se llama `hot wallet`, porque está alojada en un dispositivo siempre conectado a internet. Si estás empezando, está perfectamente bien; con el estudio aprenderás otros métodos para perfeccionar el uso de la wallet.

- `Non Custodial`
  Es fundamental empezar a usar Bitcoin mediante wallets `non-custodial`, es decir, aquellas que **te dan control completo sobre las claves privadas**. Desconfía siempre de quien te empuje a usar herramientas distintas, llamadas custodial, para acercarte a Bitcoin. Las wallets custodial son herramientas cuyas claves no posees. No es cuestión de **si**, sino de **cuándo** te impedirán de forma permanente acceder a tus fondos.

# Blockstream App (ex Green Wallet)
Para el starter kit descargaremos Blockstream App, una wallet `open source` cuyo código puedes verificar. La aplicación tiene una larga tradición de desarrollo y una historia sólida; la wallet ha demostrado ser fiable en el pasado.

---
⚠️ Las siguientes instrucciones son para descargar e instalar la app en Android. Para iOS debes usar la tienda oficial.

---

## 🌍 Traducciones

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

Ve al enlace https://github.com/Blockstream/green_android, que es el repositorio oficial de Github del desarrollador.

![img](assets/01.webp)

En el centro de la página, a la derecha, selecciona `Latest` en el espacio dedicado a *Releases* para descargar la versión más actualizada.

Llegarás a una página que te mostrará la última release, 5.1.4 en el momento de escribir este tutorial, en diciembre de 2025. En la misma página selecciona lo que puedes descargar:

![img](assets/02.webp)

Descarga el archivo `.apk` sin pasar por Play Store e instálalo en tu teléfono Android.

![img](assets/03.webp)

---
⚠️ Tu teléfono puede requerir permisos especiales para descargar apps desde fuentes no certificadas. Concede esos permisos para continuar.

---
Cuando Android te pida instalar Blockstream App, pulsa `Install`.

![img](assets/04.webp)

Al final de la instalación, elige `Open`.

![img](assets/05.webp)

Blockstream App se abre y, para empezar a usar la wallet, elige `Get Started`.

![img](assets/07.webp)

Blockstream te preguntará si quieres participar en la recopilación de datos para ayudar a los desarrolladores a mejorar la app. Rechaza la invitación.

![img](assets/08.webp)

# Tu primera wallet
Puedes empezar a crear tu primera wallet. Pulsa `Set Up Mobile Wallet`.

![img](assets/09.webp)

Comienza el proceso de creación de la wallet.

![img](assets/10.webp)

Termina en pocos segundos. Tu wallet está lista y, para empezar a usarla, pulsa `Continue`.

![img](assets/11.webp)

La wallet se abre en la pantalla llamada `Home`. Por ahora obsérvala, pero debes centrarte de inmediato en el menú inferior `Security`.

# Tus claves, tus monedas

![img](assets/12.webp)

En este menú se te pedirá hacer una copia de seguridad de tu wallet. No es otra cosa que mostrar la secuencia de 12 palabras que necesitarás para restaurarla en el futuro. Esas 12 palabras son tu wallet: **asegúrate de estar en un entorno seguro, lejos de miradas indiscretas, y de tener una libreta o papel para transcribirlas antes de guardarlas en un lugar seguro** (por ejemplo, una caja fuerte). Pulsa `Back Up Now` y descubre las 12 palabras.

**Anota también el orden exacto de las palabras: 1, 2, 3, etc.; escribe las palabras en mayúsculas para verlas mejor en el futuro, pero recuerda que si algún día tienes que introducirlas manualmente, deberás usar minúsculas**.

![img](assets/13.webp)

Después de transcribir y guardar las palabras en un lugar seguro, continúa con el starter kit. Todos los ajustes adicionales se encuentran al final de la guía.

# Menú TRANSACT
Usar la wallet es extremadamente simple:
- ve al menú `Transact`
- hay dos comandos principales: `Send` y `Receive` (**ignora `Buy`**).

![img](assets/17.webp)

Cuando tengas transacciones, aparecerán en la parte inferior, debajo de los comandos. Como aún no tienes fondos, para empezar a recibir algunos puedes seleccionar `Receive`.

Aparece una serie de *Assets*, pero céntrate solo en Bitcoin. Puedes elegir entre Bitcoin onchain (icono naranja) y Liquid (icono azul), que te permitirá disfrutar de pagos instantáneos, como con Lightning Network, pero mediante un mecanismo que veremos más adelante.

Para empezar, elige Bitcoin Onchain, el icono naranja.

![img](assets/18.webp)

Lo que aparece es un código QR que representa una de tus direcciones Bitcoin, visible también abajo con la etiqueta `bc1q` seguida de otros caracteres. Puedes mostrar el código QR a una persona que deba pagarte para recibir tus primeros fondos, fracciones razonablemente pequeñas de Bitcoin, también llamadas `Satoshi`.

![img](assets/19.webp)

Si en cambio vuelves atrás y eliges Liquid, el menú señala ⚡️**Lightning Ready**. Debes saber que, usando un servicio de `SWAP`, Blockstream App te permitirá recibir pagos casi instantáneos, emitir solicitudes de pago Lightning Network o pagar facturas LN, depositando/retirando fondos de una cuenta Liquid de tu misma wallet.

![img](assets/20.webp)

En el menú que se abre después de esta elección, selecciona cómo quieres recibir fondos, eligiendo entre Liquid y Lightning. Si eliges Liquid, se mostrará un código QR similar al que aparece al elegir Bitcoin Onchain, que representa una dirección reconocible por el prefijo `lq1q` seguido de otros caracteres.

Si eliges Lightning, se te pedirá introducir el importe que quieres recibir y confirmar pulsando `Confirm`.

![img](assets/21.webp)

Blockstream App te muestra un código QR que representa la factura LN, que puede pagarse con cualquier wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ En nuestra simulación pedimos recibir 210 sats, pero el código QR resultante avisa de que recibiremos 160 sats. Los swaps tienen efectivamente un coste, de unos 50 satoshis por cada pago recibido. **Es importante tener en cuenta este aspecto, sobre todo al recibir micropagos**. Para quien paga no cambia nada: verá descontado el importe solicitado durante la configuración, 210 satoshis.

---

# ¿Eres comerciante? Usa el POS
Para convertir esta guía en un verdadero **starter kit**, podemos combinar los cobros Bitcoin en esta wallet usando un POS externo.

Puedes configurarlo en pocos pasos directamente en https://btcpos.cash/.

![img](assets/23.webp)

Así puedes recibir pagos Lightning directamente en tu wallet creada en Blockstream App, compartir el enlace con colaboradores y, para hacerlo, solo tienes que seguir los siguientes pasos y crear un enlace que mantendrás a mano en la pantalla de inicio del teléfono. Lo que necesitas es copiar el `Descriptor` de tu wallet y pegarlo en el gran espacio central que encuentras en el enlace.

# 1. Recibir los primeros fondos en la red Liquid
Es necesario habilitar la visualización de *Assets* en la pantalla de inicio de tu wallet. Si acaba de crearse, tienes que cobrar una factura LN o recibir fondos en una dirección Liquid.

Después de recibir fondos, puedes seleccionar Liquid entre los `Assets` que ves en el menú `Home`.

![img](assets/24.webp)

# 2. Acceder a los parámetros necesarios
Ahora tienes lo necesario para acceder a los parámetros que permitirán “transportar” tu wallet al POS. Técnicamente se llama *exportación de clave pública* y es un detalle técnico que aprenderás con el estudio. Por ahora, basta con saber que para hacerlo debes seleccionar el menú de la parte superior derecha:

![img](assets/25.webp)

Y elegir `Watch-only` en el menú desplegable que aparece.
![img](assets/26.webp)

Aparece `Output Descriptors`, que es exactamente el parámetro que buscamos. Cópialo con el comando correspondiente y vuelve a la página web donde estás configurando el POS.

![img](assets/27.webp)

# 3. Configurar el POS
Pega el descriptor en el espacio correspondiente y pulsa `GENERATE POS LINK`. El sistema creará una URL única, válida solo para ti y tu wallet.

![img](assets/28.webp)

También puedes configurar primero la moneda de referencia, eligiendo entre USD, CHF y EUR en el menú desplegable donde aparece `Currency`.
![img](assets/29.webp)

# 4. Cobrar generando solicitudes de pago con el POS
Una vez pulsado `GENERATE POS LINK`, la página muestra el resultado: **el enlace se ha creado correctamente**. Puedes copiarlo porque el enlace permanecerá siempre accesible **solo para tu wallet** en la URL generada.

![img](assets/30.webp)

También puedes abrir el POS y empezar a usarlo:
![img](assets/31.webp)

Supón, por ejemplo, que quieres generar una factura de 3.351 sats, asociando una descripción.

![img](assets/32.webp)

Al pulsar `CREATE INVOICE`, el POS muestra el código QR o la factura textual que se presentará a un posible cliente.

![img](assets/33.webp)

Cuando el cliente haya pagado la factura, en la que leerá correctamente la *description* (Coppa del Nonno en este caso), el POS señala el pago recibido.

![img](assets/34.webp)

Y también se lee correctamente en la wallet.
![img](assets/35.webp)

Ahora solo tienes que memorizar y conservar a mano el enlace del POS para usarlo cuando lo necesites, incluso en el teléfono donde has instalado tu wallet.

![img](assets/36.webp)

Añadiéndolo como enlace/app en la pantalla de inicio

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE
Si relees los pasos recién completados sobre el cobro de la factura en este último ejemplo, notarás dos cosas importantes:
1. al cliente se le mostró una factura de 3.351 sats
2. nuestra wallet cobró 3.293 sats.

Antes de escandalizarse, hay que volver a la pantalla inicial del POS, que muestra el texto que ves en la imagen siguiente:

![img](assets/38.webp)

La diferencia entre 3.351 (factura presentada al cliente) y 3.293 (tu cobro) está exactamente en estos términos:
- 50 sats por cada factura generada
- 0,25% como comisión de servicio (8 sats = 0,25% de 3.351)
- Total cobrado: 3.293

#### Estás empezando y esto es un starter kit. Una pequeña comisión es el compromiso para usar Bitcoin en autocustodia, sin intermediarios, y disfrutar de todas las oportunidades, incluidos pequeños pagos instantáneos.

#### Con el estudio aprenderás a usar otras herramientas que no requerirán más comisiones que las previstas también para usuarios expertos.

---
# Otros ajustes

Es hora de conocer bien tu primera wallet. Los ajustes son importantes porque te ayudarán en el uso diario.

## Menú
Los menús de Blockstream App están en la parte inferior y son:
- Home
- Transact
- Security
- Settings

Continúa configurando tu wallet desde el menú `Security`. Además de poder ver y transcribir las palabras de la `Recovery phrase`, este menú pone a tu disposición otras funciones importantes.

Puedes configurar, por ejemplo, el acceso a tu wallet con control biométrico (si está configurado en tu teléfono) o añadir también un PIN de seis dígitos para acceder a la wallet. Estas opciones son muy importantes porque impiden que extraños accedan y vean tu wallet si tienen tu teléfono en la mano.

![img](assets/14.webp)

En este menú también puedes decidir el tiempo de *Logout*, es decir, cuándo la wallet se desconecta después de unos minutos de inactividad. Por defecto está configurado en *5 minutes* y puedes variar ese tiempo según tus necesidades, más largo o más corto, ajustándolo a tu destreza manual.
![img](assets/15.webp)
# Menú SETTINGS
Menú muy importante porque contiene todos los ajustes de la wallet. Al pulsar en este menú puedes, por ejemplo, cambiar el nombre de la wallet: en nuestro ejemplo la llamamos *Starter Kit*. Renombrar wallets para distinguirlas es muy importante cuando usas más de una en el mismo dispositivo y necesitas entender/elegir cuál utilizar.

![img](assets/39.webp)

Si en cambio vas al submenú `Denomination`, encontrarás ajustes muy útiles sobre la moneda.
![img](assets/40.webp)

Recomiendo usar `satoshi/sats` como unidad para los importes en Bitcoin. El Satoshi es la unidad más pequeña de BTC, equivalente a una cienmillonésima parte de Bitcoin. Además aparecerá la elección del mercado de referencia para la conversión. Usa uno que te permita ver y establecer importes en EUR.

![img](assets/41.webp)

Por último, en el menú `Settings` puedes comprobar la versión de Blockstream App actualmente utilizada y verificar si necesita actualizarse, además de encontrar comandos para solicitar soporte directamente *in-app*.
![img](assets/42.webp)

# Menú HOME
El `Home` de Blockstream App es el menú donde se abre tu wallet en cada nuevo acceso. Al desplazarte hacia abajo encontrarás la opción de comprar Bitcoin mediante un exchange integrado. **No la uses**.

![img](assets/16.webp)

# Restauración de la wallet
Si durante el uso te das cuenta de que necesitas cambiar de teléfono, o necesitas usar la wallet *Starter Kit* en más de un dispositivo, con Blockstream App puedes hacerlo.

Para proceder, solo tienes que aprender el procedimiento de restauración de la wallet, explicado a continuación, que incluye los pasos a seguir si pierdes el acceso al teléfono donde empezaste a usar la wallet.

Tus fondos, de hecho, no están “en el dispositivo” ni “en la wallet”. Los fondos están en la red Bitcoin, ya sea Onchain, Lightning o Liquid. La wallet, para ser precisos, las claves públicas y privadas de tu wallet, es la herramienta para acceder a las direcciones usadas y, con ellas, al saldo asociado.

Para este procedimiento transcribiste las 12 palabras y las guardaste en un lugar seguro... **Lo hiciste, ¿verdad?** Porque sin esas palabras ya no tendrás acceso a tus fondos.

# a. Nueva instalación de Blockstream App
Primero instala de nuevo Blockstream App con el procedimiento mostrado al principio. Puede que mientras tanto haya llegado una nueva release; usa la más actualizada.

Inicia Blockstream App en el nuevo dispositivo y continúa pulsando `Get Started` y rechazando la oferta de recopilación de datos.

# b. Restaurar desde copia de seguridad
Las similitudes con la primera instalación terminan aquí. Cuando llegue la pantalla de creación de la wallet, en lugar de elegir `Set Up Mobile Wallet` como hiciste la primera vez, elige `Restore from backup`.

![img](assets/43.webp)

Si estás usando la red principal de Bitcoin, es decir, la que usa fondos reales, en la pantalla siguiente elige `Mainnet`.

![img](assets/43.webp)

Aparece la pantalla con los campos donde introducir las palabras de la `Recovery phrase`. Escríbelas de nuevo en orden y correctamente; después selecciona `Continue` para recrear la wallet en el nuevo dispositivo.

![img](assets/45.webp)

La fase de restauración de la wallet puede tardar unos minutos; espera con paciencia a que termine correctamente. Al final del proceso volverás a encontrar tu wallet, con el saldo y el historial de transacciones.

![img](assets/46.webp)

---
⚠️ La wallet recreada en el nuevo dispositivo está activa al 100%. Esto significa que también tiene las claves privadas para gastar. Recuérdalo si quieres dejarla a algún colaborador para tu negocio.

**Usa más bien el enlace del POS para colaboradores, porque fue creado solo con la clave pública (el `descriptor`)**.

---

# ¿Cómo continuar aprendiendo?

![img](assets/47.webp)
![img](assets/48.webp)
