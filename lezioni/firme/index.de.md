---
layout: default
title: "Digitale Signaturen"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Bitcoin-only-Lektion</span> <span>Dieses Projekt wird von valerio-vaccaro gepflegt</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Digitale Signaturen
Das Thema dieser Lektion sind digitale Signaturen und ihre Anwendung auf Bitcoin.

## Was ist eine Signatur?
Wir müssen verstehen, was wir mit digitaler Signatur meinen. Wenn wir an eine normale Signatur denken, denken wir gewöhnlich an etwas anderes: Da es hier um digitale Dokumente geht, verknüpft die digitale Signatur sowohl die Identität des Autors als auch den Zustand des signierten Dokuments. Im Wesentlichen hängt die Signatur also auch von dem Dokument ab, das wir signieren wollen.

Das ist ein sehr großer Unterschied zur physischen Welt, in der wir die Unterschrift praktisch ohne Rücksicht auf den Träger leisten, auf dem wir unterschreiben. Natürlich würden wir Schecks oder andere Dokumente vielleicht nicht ohne jede Aufmerksamkeit unterschreiben, aber im Kern ändert sich die Unterschrift, die wir anbringen, nicht.

Digitale Signaturen sind etwas anderes; normalerweise beruhen sie auf Algorithmen mit öffentlichem und privatem Schlüssel. Das bedeutet, dass unser wallet irgendwo auf der Welt ein Schlüsselpaar besitzt, öffentlich und privat, und dass unsere (Pseudo-)Identität mit dem öffentlichen Schlüssel verbunden ist, den alle kennen oder den wir allen bekannt machen.

Wir verwenden unseren privaten Schlüssel, der eine Zahl ist, und erzeugen mit etwas mathematischer Magie eine Signatur, die eine andere Zahl ist und beweist, dass ein bestimmter Zustand eines bestimmten Dokuments zu einer bestimmten, mit einem öffentlichen Schlüssel verbundenen Identität gehört oder ihr bekannt ist. Was ich signiere, ist der Fingerabdruck (oder HASH) eines bestimmten Dokuments (oder PAYLOAD).

Außerdem brauche ich einen Zufallszahlengenerator; ich werfe all diese Daten in eine "Black Box", die für mich eine Signatur erzeugt. Die Signatur beweist also Besitz, weil ich mit meinem Geheimnis signiere, beweist aber auch, dass das, was ich signiere, nicht verändert wurde.

Wenn ich den PAYLOAD ändere, ändere ich den HASH, und das macht die Signatur natürlich ungültig.

Warum wurde diese komplexere Signatur also in der digitalen Welt eingeführt? Weil es in der digitalen Welt, anders als in der physischen (und vielleicht erinnern sich diejenigen daran, die in der Schule nicht aufgepasst haben), viel einfacher ist, eine Signatur zu kopieren.

Die digitale Signatur enthält dagegen Informationen über das Dokument und ändert sich daher für jedes Dokument; sie kann nicht auf ein anderes Dokument kopiert und dort wiederverwendet werden.

Die digitale Signatur dient daher dazu:
- zu beweisen, dass ich eine bestimmte Nachricht erstellt habe, eine bestimmte Aktion anfordere oder einen bestimmten Zustand eines Systems erkläre, und
- zu beweisen, dass diese Nachricht, dieses Dokument oder diese Datenkette nicht manipuliert wurde, also tatsächlich das ist, was ich signieren wollte.
- eine bestimmte Aktion nicht abstreitbar zu machen; wenn ich eine Signatur erzeugt habe, war ich es wirklich, der dies für genau dieses Dokument getan hat.

## Signaturen in Bitcoin
Diese Technologie wird in Bitcoin unter dem Akronym ECDSA (Elliptic Curve Digital Signature Algorithm) verwendet, einem Algorithmus zur Erzeugung digitaler Signaturen auf elliptischen Kurven; andere Signaturschemata behandeln wir vorerst nicht.

Denke daran, dass man in Bitcoin Signaturen erzeugen kann für:
- beliebigen Text, wenig wichtig und wenig verwendet
- neue Transaktionen, mit dem Zweck, das Ausgeben eines bestimmten UTXO zu autorisieren

Aber wie sind diese Signaturen mit der Transaktion verbunden? Jede Adresse hat einen Ausgabemechanismus, also scripts, die ausgeführt werden müssen, um zu wissen, ob eine Ausgabe autorisiert werden kann. Innerhalb dieser scripts gibt es Befehle (oder OPCODES) zur Prüfung digitaler Signaturen, wie OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Denke daran, dass eine Bitcoin-Transaktion besteht aus:
- Inputs, also den Mitteln, die ich ausgeben werde und für die ich ein Ausgabescript erzeugen muss
- Outputs, also den neuen Adressen, an die die Mittel gehen werden (und mit jeder Adresse ist ein genau definierter Ausgabemodus verbunden.

Im Wesentlichen muss ich daher in den meisten Fällen FÜR JEDEN INPUT die Signatur(en) erzeugen, die notwendig sind, um das Ausgabescript zu vervollständigen.

Denke daran, dass diese Aktion uns erlaubt zu beweisen, dass dieser input uns gehört und dass wir ihn ausgeben wollen (wir wollen das Eigentum vollständig übertragen, es aufteilen oder mit anderen inputs zusammenführen).

Offensichtlich ist die Transaktion gültig, wenn alle inputs korrekt signiert sind; wenn auch nur einer der inputs nicht signiert ist, kann diese Transaktion nicht als gültig betrachtet werden.

Die Signatur ist von allen überprüfbar und nicht abstreitbar, aber aus Flexibilitätsgründen hat Satoshi sehr geschickt verschiedene Signaturmodi eingeführt: Die Signatur ist immer gleich, aber der PAYLOAD ändert sich, also der Teil der Transaktion, der Gegenstand der Signatur ist. Dadurch können zum Beispiel komplexe Schemata und Protokolle erzeugt werden, in denen Teile von Transaktionen miteinander kombiniert werden können; Satoshi nannte diese Modi (echte flags in der Scriptsprache) SIGHASH.

## SIGHASH
Der einfachste SIGHASH ist SIGHASH_ALL, was bedeutet, eine Signatur mit ALLEN INPUTS und ALLEN OUTPUTS zu erzeugen; dies ist der einfachste und meistverwendete Modus zum Erstellen einer Signatur.

Ein erster Unterschied ergibt sich mit SIGHASH_NONE, das ALLE INPUTS signiert, aber KEINEN der OUTPUTS, wodurch später outputs hinzugefügt oder fees geändert werden können. ACHTUNG: Wenn dieses Schema nicht durch multisig oder andere Funktionen geschützt ist, kann ein miner oder jeder, der eine Transaktion mit diesem Signaturschema sieht, die outputs ersetzen und die Mittel auf seine eigene Adresse umleiten.

Ein interessanteres flag ist SIGHASH_SINGLE, bei dem ein Paar aus input und output signiert wird, sofern beide auf derselben Ebene in eine Transaktion eingefügt sind (zum Beispiel fünfter input und fünfter output); dies würde erlauben, größere Transaktionen aus solchen Paaren zusammenzusetzen, bietet aber keine Möglichkeit, Wechselgeld einzuführen, erfordert also die vollständige Ausgabe des inputs.

Parallel dazu können alle diese SIGHASH mit dem flag ANYONECANPAY kombiniert werden, das die Signatur nur auf den input beschränkt, für den die Signatur erzeugt wird, und damit jedem die Möglichkeit gibt, inputs zur Transaktion hinzuzufügen.

Alle diese Signaturen sind gültige Signaturen, unabhängig von Adresstyp und scripts, und lassen dem wallet maximale Ausdrucksflexibilität. Normalerweise wird es SIGHASH_ALL verwenden, könnte aber auch komplexeren Protokollen folgen, die andere Signaturschemata erfordern. Bei multisig ist es dann nicht nötig, denselben Signaturtyp zu verwenden; ein 2-of-2-wallet könnte einige seiner UTXO mit SIGHASH_NONE und ANYONECANPAY signieren, um dem zweiten Signierer die volle Kontrolle zu geben, der zum Beispiel all diese inputs in einer Transaktion sammeln könnte, die mit SIGHASH_ALL zu signieren ist.

## Signaturen auf beliebigem Text
Der Vollständigkeit halber können dieselben Signaturen, die für Transaktions-inputs verwendet werden, auch zum Signieren beliebigen Textes genutzt werden.

Bitcoin schlägt ein Schema vor, bei dem Text hinzugefügt wird, um zu verhindern, dass diese Funktion zum Signieren von Transaktionsteilen verwendet wird. Wenn du also Bitcoin Core oder auch einige wallets hast, kannst du nach einer Funktion zum Signieren von Textnachrichten suchen, die auf einer bestimmten deiner Adressen basiert.

Das wallet verwendet den privaten Schlüssel, der mit dem öffentlichen Schlüssel verknüpft ist, aus dem diese Adresse erzeugt wurde, um Textnachrichtensignaturen zu erstellen.

Bei der Verifikation wird der öffentliche Schlüssel erhalten, der dann zur erneuten Erzeugung der Adresse verwendet werden kann. Wenn ich also den Text und die Signatur habe, extrahiere ich den öffentlichen Schlüssel, der ihn signiert hat, und aus dem öffentlichen Schlüssel kann ich die Adresse neu berechnen und sie zum Beispiel mit der bereitgestellten vergleichen.

## Programm
Die Lektion über Signaturen kann wiederholt werden; hier ist eine Liste der bereits gehaltenen:

| Datum       | Notizen                                        |
|-------------|------------------------------------------------|
|||
