---
layout: default
title: "Bitcoin-Deskriptoren"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Bitcoin-Deskriptoren

## Einführung

## Deskriptoren
Deskriptoren sind ein relativ neues und noch nicht sehr weit verbreitetes Konzept, aber sie sind nützlich, um die Struktur einer Bitcoin wallet zu beschreiben. Deskriptoren sind lesbare Zeichenketten (alphanumerisch, hexadezimal und mit einigen Symbolen wie Klammern), die eine wallet klar und standardisiert darstellen sollen, also die Menge der öffentlichen und privaten Schlüssel, die nötig ist, um Salden zu berechnen, Bitcoin zu empfangen und auszugeben.

## Entwicklung der Wallet-Verwaltung
Um Deskriptoren einzuordnen, zeichnet der Sprecher die Entwicklung von wallets nach:

- Frühe wallets (pre-BIP-32): In den Anfangstagen waren wallets bei Bitcoin Core Dateien, die zufällig erzeugte Schlüssel enthielten. Jedes Mal, wenn die Adressen aufgebraucht waren, wurden neue hinzugefügt. Dadurch waren häufige Backups nötig, um den Verlust von Geldern zu vermeiden. Dieses System war ineffizient.
- BIP-32 (HD Wallet): Mit der Einführung der hierarchisch-deterministischen Erzeugung generierte ein seed einen Hauptschlüssel, von dem alle Adressen abgeleitet wurden. Ein Backup des seed reichte aus, aber es war noch keine vollständige Lösung.
- Mnemonics (BIP-39): Später wurde der seed aus einer Folge von 12 oder 24 Wörtern (mnemonic) abgeleitet, die leichter aufzubewahren ist. Um eine wallet wiederherzustellen, waren jedoch auch Informationen über Ableitungspfade (z. B. Legacy, SegWit) nötig, sonst konnten die Gelder unwiederbringlich sein.

Das mnemonic allein reicht nicht aus, insbesondere bei komplexen wallets wie multisig (die mehrere Signaturen erfordern) oder solchen mit erweiterten scripts (z. B. timelock oder Vererbungsbedingungen). Einige wallets probieren alle möglichen Ableitungen aus, um Gelder zu finden, während andere (z. B. Electrum) verlangen, dass der wallet-Typ angegeben wird. Bei multisig werden außerdem die öffentlichen Schlüssel der anderen Teilnehmer benötigt, was das Backup weiter erschwert.

## Was Deskriptoren sind und warum sie gebraucht werden
Deskriptoren wurden geschaffen, um diese Einschränkungen zu überwinden. Sie bieten eine vollständige und flexible Beschreibung der wallet-Struktur. Sie ersetzen das mnemonic nicht, sondern ergänzen es, unter anderem mit:

- Erweiterten öffentlichen Schlüsseln (xpub, ypub usw.).
- Ableitungspfaden (z. B. m/44'/0'/0' für Legacy).
- Beliebigen Ausgabescripts oder Bedingungen (z. B. multisig, timelock).

## Praktische Beispiele
- Legacy single-sig: Ein einfacher Deskriptor könnte `pk([fingerprint/derivation]xpub...)` sein, wobei:
1. pk einen öffentlichen Schlüssel angibt.
2. [fingerprint/derivation] den Hauptschlüssel und den Pfad angibt.
3. xpub Adressen erzeugt (z. B. 0/* für Empfang, 1/* für change).
- Multisig: Ein Beispiel ist `sortedmulti(2, xpub1, xpub2, xpub3)`, das eine 2-of-3-wallet beschreibt und die Schlüssel zur Konsistenz sortiert.
- Komplexe scripts: Mit scripts wie p2sh (pay to script hash) oder p2wsh (pay to witness script hash) können erweiterte Bedingungen eingebunden werden, etwa timelock oder logische Kombinationen (and, or).

## Deskriptoren und Taproot
Ein interessanter Fall ist der Deskriptor für Taproot (tr), der zwei Ausgabemodi unterstützt:

- Direkte Signatur mit einem bestimmten Schlüssel.
- Ein Baum von Bedingungen (z. B. Vererbung oder timelock), der die Komplexität bis zur Ausgabe auf der blockchain verborgen hält.

## Vorteile von Deskriptoren
- Vollständiges Backup: Sie enthalten alle Informationen, die nötig sind, um eine wallet ohne Suchläufe wiederherzustellen.
- Kompatibilität: ideal für watch-only wallets, bei denen Gelder ohne private Schlüssel überwacht werden.
- Flexibilität: Sie unterstützen single-sig, multisig und komplexe scripts.
- Datenschutz: Sie verraten keine Geheimnisse und können wie ein xpub geteilt werden.

## Einschränkungen und Kompatibilität
Nicht alle wallets unterstützen Deskriptoren vollständig. Bitcoin Core implementiert zum Beispiel nur eine Teilmenge und benötigt zwei getrennte Deskriptoren für Adressen und change. Software wie Sparrow oder Specter bietet bessere Unterstützung und ermöglicht den Import/Export von Deskriptoren sowie die Visualisierung ihrer Struktur.

Experimente lassen sich durchführen mit:
- Sparrow: unterstützt Deskriptoren und bietet eine grafische Oberfläche, um sie zu erstellen oder zu analysieren.
- BDK: Bibliothek mit Befehlszeilenschnittstelle zur Verwaltung komplexer Deskriptoren.
- Testnet/Signet: sichere Umgebungen zum Testen, ohne echte Gelder zu riskieren.

## Referenzen

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programm
Diese Lektion wurde für einen Satoshi Spritz Connect erstellt.
