![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
La verifica de le firme crittografiche xe na pratica de sicuresa fondamental che **ogni utente de software open-source el dovaria inserir ne le routine de le bone abitudini**.

Open source xe par la so natura modificabile e questo vol dir che chiunque el pode, a livel teorego, introdur backdoor, atachi o codice malevolo ne le aplicassion che te dopre par esercitarte, intanto che te impari el protocollo Bitcoin.

Come utente che xe in del approfondir el studio, te ghe la possibilità de verificar personalmente se el software scaricà xe stà manomesso, e te el dovaria far prima de installarlo e doprarlo.

Prima de scominsiar, portemo anca in Officine Bitcoin un classico de le presentassion: el meme. No sarà na presentassion pesada, ma decomprimemo l'atmosfera già de subito.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Come far?
I svilupatori rilassa le novi version de software acompanandole sempre co na firma crittografica.
Questo vol dir che - oltre ad aver agiornà el software - i rilassa certificando de averlo vinciolà co na specifica impronta digital. Reminder: la firma digital prodota co la ciave privada, xe unica e no modificabile.

Tuto quel che te ghe bisogno xe la suite GPG par proceder a la verifica de la firma.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Pre requisiti par sta esercitassion
- Un breve ripasso su la crittografia asimetrica
- I elementi da verificar:
  - software (binario, apk ecc)
  - la firma digital de lo svilupador, normalmente un file `.asc`, `.sig` o un checksum.
- I strumenti par far la verifica:
  - GPG suite
  - un terminal (el val sia par Linux sia par Win)
# Crittografia asimetrica

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Qua ghe xe do ciave correlate tra lore: na ciave publica e na privada. Come sugera i nomi:
- La ciave publica xe disponibile liberamente e la pode esser condividesta co chiunque.
- La ciave privada xe tenesta al sicuro dal so proprietario.

I dati cifrai co la ciave publica i pode esser decifrai solo da la ciave privada corrispondente. Questo permete a chiunque de mandar dati crittografai al proprietario de la coppia de ciave, sensa previa condividission de la parte segreta.

La crittografia a ciave publica xe pi lenta de la crittografia simetrica e no xe adata a cifrar dati de grandi dimension. Tutiàvia, la permete la distribussion sicura de le ciave de crittografia.
Alcuni algoritmi doprai comunemente par la crittografia a ciave publica include RSA, ECC, ElGamal e DSA.

## Parte svilupador: novo agiornamento

Lo svilupador rilassa el codice open source, par la so natura no cifrà.
El ne fa un hash crittografego (e questo genera el `checksum`) e el cifra el digest co la so ciave privada: questo crea la firma, quel file `.sig` o `.asc` anticipà prima.

Dopo quel processo, lo svilupador el carica sul sito o su un repository Github tuti e do i file. Xe là che scominsia el to download.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Poi te servirà la ciave publica de lo svilupador. A volte la se trova nel repository Github, a volte su server publici (*keyserver*). Anca se la ricerca pode richieder sforzo, la ciave publica xe un elemento indispensabile par verificar el software, quindi impegnite par ottegnerla.

In caso de dificoltà, fa domande sul grupo Telegram de Officine Bitcoin, dove te trovarè le indicassion par ottegner na specifica ciave publica.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Par verificar l'integrità de i dati, el destinatario el decifra la firma doprando la ciave publica del mittente, ottegendo un risultà:

a. i dati i xe considerai autentici e no modificai durante el transito.
b. i dati i xe stai potenzialmente manomessi.

Crittografando el valor hash co la ciave privada, **le firme PGP garantisce che el checksum stesso sia proteto e colegà a l'identità del mittente. Questo impedise la falsificassion de le firme su dati alterai**.

Le firme le pode esser doprae par verificar qualcossa: file, e-mail, documenti e download de software. Quando se controla na firma PGP, se dimostra che i dati i vien de fato da na fonte affidabile e i xe integri.

E xe la verifica de un apk par celular che te poderè verificar adesso.

Dopremo come esempi el download de Phoenix, wallet LN non-custodial, par trattarlo in del specific in na prossima serada de Officine Bitcoin.

# Download e verifica Phoenix Wallet (Acinq)
Se te xe già stà sul sito de [Acinq](https://phoenix.acinq.co/), lo svilupador de Phoenix, te sai già che el download xe disponibile su i store ufficiali par Android e iOS.
Magari no te ghe mai fato caso, ma par Android xe disponibile anca el file apk.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Andemo là!](https://github.com/ACINQ/phoenix/releases) par trovar i file `apk` e `Signature` che te scaricarè co `wget`.
Nel caso de Phoenix el file che contien la firma par la verifica xe nominà **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

Nel stesso repository ghe xe anca le indicassion par scaricar la ciave publica corrispondente a la *signing key E04E48E72C205463* (impronta digital unica de le ciave de Drouinf).
Copia el link e scaricala co `wget`, oppur segui le istrucion sugeride ne la sezion apposita del repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**La ciave publica la deve esser importada, oltre che scaricada**.
⚠️ El download de i file el deve suceder ne la stessa directory.

---
# Vèrt el terminal
Co el terminal, posissionite ne la directory dove xe stai scaricai l'apk e el file `SHA256SUMS.ASC` ed eseguì i comandi ne l'ordine.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Quando la verifica ga restituì esito positivo, te poderè trasferir l'apk sul celular e installar l'app.

---
# Verifica dificoltosa
Ghe pode esser diverse rason par cui la verifica de le firme no xe agevole, e le xe quasi sempre da imputar al disordine o a l'esperienza:
1. i file apk e/o .asc i xe stai scaricai pi volte, quindi ne la directory i resulta - par esempi nomi strani tipo **nomefile-1** o **nomefile(1)**
2. apk e .asc no stà ne la stessa directory
3. la ciave publica xe stada scaricada ma no importada nel keyring gpg.

Pode invece capitar altre situassion, par le quali - anca operando coretamente - la verifica no riese.
Xe importante verificar l'eror che compare a terminal, copiarlo e scominsiar na ricerca su internet par la solusion.

# Verifica co Sparrow Wallet
Se invece te dopre già Sparrow Wallet, te pode proceder a verificar i download co sto software, **el cui download e installassion i deve esser precedui da un'attenta e rigorosa verifica co GPG**.

Lancia Sparrow wallet e cerca nel menu `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Se vèrt n'interfacia che la domanda de inserir i file appena scaricai. Clicando su `Browse` se vèrt el file manager, par caricar ogni file nel campo richiesto.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

A volte el form de l'interfacia el se completa da solo. Se no el fa, riempi tuti i campi co i file apropriai.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

L'esito, positivo, xe mostrà graficamente de le spunte verdi e de la conferma *`Ready to install`* + < nome file >.

# Suporto al studio
Se te xe partisipà a la presentassion in direta Telegram, te pode considerarla un ulterior passo verso la toa personal sovranità (no solo finanziaria).
Se te te la xe persa **no desperar**: sti apunti i serve appunto par recuperar e, in oltre, te devi saver che la riproporemo ancora su Officine.

Par no perder la prossima presentassion, unissite al [grupo Telegram](https://t.me/officinebitcoin), par restar in agiornamento costante.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Te pode anca cercar el [Satoshi Spritz](https://satoshispritz.it/) pi vesin a ti. Un Satoshi Spritz xe un meetup locale dove se parla solo de Bitcoin, dove te pode portar le to domande e far te risponder da altri bitcoiner esperti. Al link te trovarè la mapa de la penisola.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

In fin, se no te trovi el meetup vesin a ti, te pode aprofitar de le direte settimanai de [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), un meetup virtual creà par chi che no pode partisipar ai Satoshi Spritz, o par ajudar i meetup pi picini a prender apunti e trovar ispirassion par le so presentassion.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
