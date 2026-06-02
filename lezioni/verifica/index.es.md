---
layout: default
title: "Requisitos previos para este tutorial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lección Bitcoin-only</span> <span>Este proyecto es mantenido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
Verificar firmas criptográficas es una práctica de seguridad fundamental que **todo usuario de software open-source debería incluir en su rutina de buenos hábitos**.

El open source es por naturaleza modificable, lo que significa que cualquiera puede, en teoría, introducir backdoors, ataques o código malicioso en las aplicaciones que usas para practicar mientras aprendes el protocolo Bitcoin.

Como usuario que está profundizando en su estudio, tienes la oportunidad de verificar personalmente si el software descargado ha sido manipulado, y deberías hacerlo antes de instalarlo y utilizarlo.

Antes de empezar, también traemos un clásico de las presentaciones a Officine Bitcoin: el meme. No será una presentación pesada, pero despejemos el ambiente desde el principio.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## ¿Cómo se hace?
Los desarrolladores siempre publican nuevas versiones de software acompañadas por una firma criptográfica.
Esto significa que, además de haber actualizado el software, lo publican certificando que lo han vinculado a una fingerprint específica. Recordatorio: la firma digital producida con la clave privada es única e inmodificable.

Todo lo que necesitas es la suite GPG para proceder con la verificación de la firma.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Requisitos previos para este tutorial
- Un breve repaso de criptografía asimétrica
- Los elementos que hay que verificar:
  - software (binary, apk, etc.)
  - la firma digital del desarrollador, normalmente un archivo `.asc`, `.sig` o un checksum.
- Las herramientas para la verificación:
  - suite GPG
  - un terminal (funciona tanto en Linux como en Windows)
# Criptografía asimétrica

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Aquí hay dos claves relacionadas entre sí: una clave pública y una privada. Como sugieren sus nombres:
- La clave pública está libremente disponible y puede compartirse con cualquiera.
- La clave privada se mantiene segura por su propietario.

Los datos cifrados con la clave pública solo pueden descifrarse con la clave privada correspondiente. Esto permite que cualquiera envíe datos cifrados al propietario del par de claves, sin compartir previamente la parte secreta.

La criptografía de clave pública es más lenta que la criptografía simétrica y no es adecuada para cifrar grandes cantidades de datos. Sin embargo, permite distribuir de forma segura las claves de cifrado.
Algunos algoritmos usados habitualmente para criptografía de clave pública incluyen RSA, ECC, ElGamal y DSA.

## Lado del desarrollador: nueva actualización

El desarrollador publica el código open source, que por naturaleza no está cifrado.
Crea un hash criptográfico (que genera el `checksum`) y cifra el digest con su clave privada: esto crea la firma, ese archivo `.sig` o `.asc` mencionado antes.

Después de este proceso, el desarrollador sube ambos archivos al sitio o a un repositorio GitHub. Ahí es donde empieza tu descarga.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Después necesitarás la clave pública del desarrollador. A veces está en el repositorio GitHub, a veces en servidores públicos (*keyservers*). Aunque la búsqueda pueda requerir esfuerzo, la clave pública es un elemento esencial para verificar el software, así que haz el esfuerzo de obtenerla.

Si tienes dificultades, haz preguntas en el grupo Telegram de Officine Bitcoin, donde encontrarás instrucciones para obtener una clave pública específica.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Para verificar la integridad de los datos, el destinatario descifra la firma usando la clave pública del remitente y obtiene un resultado:

a. los datos se consideran auténticos y no modificados durante el tránsito.
b. los datos han sido potencialmente manipulados.

Al cifrar el valor hash con la clave privada, **las firmas PGP garantizan que el checksum esté protegido y vinculado a la identidad del remitente. Esto impide falsificar firmas sobre datos alterados**.

Las firmas pueden usarse para verificar cualquier cosa: archivos, emails, documentos y descargas de software. Al comprobar una firma PGP, demuestras que los datos realmente provienen de una fuente confiable y están intactos.

Y es la verificación de un apk móvil lo que podrás verificar ahora.

Usamos como ejemplo la descarga de Phoenix, un wallet LN non-custodial, para poder tratarlo específicamente en una futura velada de Officine Bitcoin.

# Descargar y verificar Phoenix Wallet (Acinq)
Si ya has estado en el sitio de [Acinq](https://phoenix.acinq.co/), desarrollador de Phoenix, ya sabes que la descarga está disponible en las tiendas oficiales para Android e iOS.
Quizá nunca lo notaste, pero para Android también está disponible el archivo apk.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[¡Vamos allí!](https://github.com/ACINQ/phoenix/releases) para encontrar los archivos `apk` y `Signature` que descargarás con `wget`.
En el caso de Phoenix, el archivo que contiene la firma para la verificación se llama **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

En el mismo repositorio también hay instrucciones para descargar la clave pública correspondiente a la *signing key E04E48E72C205463* (fingerprint única de las claves de Drouinf).
Copia el enlace y descárgalo con `wget`, o sigue las instrucciones sugeridas en la sección correspondiente del repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**La clave pública debe importarse, no solo descargarse**.
⚠️ Las descargas de los archivos deben realizarse en el mismo directorio.

---
# Abre el terminal
Con el terminal, navega hasta el directorio donde se descargaron el apk y el archivo `SHA256SUMS.ASC`, y ejecuta los comandos en orden.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Cuando la verificación devuelve un resultado positivo, puedes transferir el apk a tu teléfono e instalar la app.

---
# Verificación difícil
Puede haber varias razones por las que la verificación de la firma no sea fácil, y casi siempre se deben al desorden o a la inexperiencia:
1. los archivos apk y/o .asc se descargaron varias veces, por lo que en el directorio aparecen con, por ejemplo, nombres extraños como **filename-1** o **filename(1)**
2. apk y .asc no están en el mismo directorio
3. la clave pública se descargó, pero no se importó al keyring de gpg.

También pueden darse otras situaciones en las que, incluso operando correctamente, la verificación falle.
Es importante comprobar el error que aparece en el terminal, copiarlo e iniciar una búsqueda en internet para encontrar la solución.

# Verificación con Sparrow Wallet
Si ya usas Sparrow Wallet, puedes proceder a verificar descargas con este software, **cuya descarga e instalación deben estar precedidas por una verificación cuidadosa y rigurosa con GPG**.

Inicia Sparrow wallet y busca en el menú `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Se abre una interfaz que te pide insertar los archivos recién descargados. Al hacer clic en `Browse`, se abre el gestor de archivos para cargar cada archivo en el campo requerido.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

A veces el formulario de la interfaz se rellena por sí solo. Si no lo hace, completa todos los campos con los archivos adecuados.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

El resultado positivo se muestra gráficamente mediante marcas verdes y la confirmación *`Ready to install`* + < filename >.

# Apoyo para el estudio
Si asististe a la presentación en directo por Telegram, puedes considerarla un paso más hacia tu soberanía personal (no solo financiera).
Si te la perdiste, **no desesperes**: estas notas sirven precisamente para ponerte al día y, además, debes saber que la propondremos de nuevo en Officine.

Para no perderte la próxima presentación, únete al [grupo Telegram](https://t.me/officinebitcoin) y mantente constantemente actualizado.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

También puedes encontrar el [Satoshi Spritz](https://satoshispritz.it/) más cercano a ti. Un Satoshi Spritz es un meetup local donde solo se habla de Bitcoin, donde puedes llevar tus preguntas y obtener respuestas de otros bitcoiners expertos. En el enlace encontrarás el mapa de la península.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

Por último, si no encuentras un meetup cerca de ti, puedes aprovechar las transmisiones en directo semanales de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creado para quienes no pueden asistir a Satoshi Spritz, o para ayudar a los meetups más pequeños a tomar notas y encontrar inspiración para sus propias presentaciones.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
