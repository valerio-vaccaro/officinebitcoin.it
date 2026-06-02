---
layout: default
title: "Descritores de Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Descritores de Bitcoin

## Introdução

## Descritores
Os descritores são um conceito relativamente novo e ainda pouco difundido, mas úteis para descrever a estrutura de uma wallet Bitcoin. Os descritores são cadeias de caracteres legíveis (alfanuméricas, hexadecimais e alguns símbolos como parênteses), criadas para representar de forma clara e padronizada uma wallet, ou seja, o conjunto de chaves públicas e privadas necessário para calcular saldos, receber e gastar Bitcoin.

## Evolução da gestão de wallets
Para contextualizar os descritores, o palestrante percorre a evolução das wallets:

- Wallets iniciais (pre-BIP-32): nos primeiros tempos, com Bitcoin Core, as wallets eram arquivos que continham chaves geradas aleatoriamente. Sempre que os endereços acabavam, novos eram adicionados, tornando necessárias cópias de segurança frequentes para evitar a perda de fundos. Esse sistema era ineficiente.
- BIP-32 (HD Wallet): com a introdução da geração determinística hierárquica, um seed gerava uma chave mestra, da qual todos os endereços derivavam. Bastava fazer backup do seed, mas isso ainda não era uma solução completa.
- Mnemônicos (BIP-39): depois, o seed passou a ser derivado de uma sequência de 12 ou 24 palavras (mnemonic), mais fácil de guardar. Porém, para reconstruir uma wallet, também eram necessárias informações sobre os caminhos de derivação (por exemplo, Legacy, SegWit); caso contrário, os fundos poderiam ficar irrecuperáveis.

O mnemonic sozinho não é suficiente, especialmente para wallets complexas como multisig (que exigem várias assinaturas) ou aquelas com scripts avançados (por exemplo, timelock ou condições de herança). Algumas wallets tentam todas as derivações possíveis para encontrar fundos, enquanto outras (por exemplo, Electrum) exigem a especificação do tipo de wallet. Em multisig, além disso, são necessárias as chaves públicas dos outros participantes, o que complica ainda mais o backup.

## O que são descritores e por que são necessários
Os descritores surgiram para superar essas limitações, oferecendo uma descrição completa e flexível da estrutura da wallet. Eles não substituem o mnemonic, mas o complementam, incluindo:

- Chaves públicas estendidas (xpub, ypub, etc.).
- Caminhos de derivação (por exemplo, m/44'/0'/0' para Legacy).
- Quaisquer scripts ou condições de gasto (por exemplo, multisig, timelock).

## Exemplos práticos
- Legacy single-sig: um descritor simples poderia ser `pk([fingerprint/derivation]xpub...)`, em que:
1. pk indica uma chave pública.
2. [fingerprint/derivation] especifica a chave mestra e o caminho.
3. xpub gera endereços (por exemplo, 0/* para recebimento, 1/* para change).
- Multisig: um exemplo é `sortedmulti(2, xpub1, xpub2, xpub3)`, que descreve uma wallet 2-of-3, ordenando as chaves por consistência.
- Scripts complexos: com scripts como p2sh (pay to script hash) ou p2wsh (pay to witness script hash), é possível incluir condições avançadas, como timelock ou combinações lógicas (and, or).

## Descritores e Taproot
Um caso interessante é o descritor para Taproot (tr), que aceita dois modos de gasto:

- Assinatura direta com uma chave específica.
- Uma árvore de condições (por exemplo, herança ou timelock), mantendo a complexidade oculta na blockchain até o momento do gasto.

## Vantagens dos descritores
- Backup completo: contêm todas as informações necessárias para reconstruir uma wallet sem tentativas às cegas.
- Compatibilidade: ideais para watch-only wallets, nas quais os fundos são monitorados sem chaves privadas.
- Flexibilidade: aceitam single-sig, multisig e scripts complexos.
- Privacidade: não revelam segredos e podem ser compartilhados como um xpub.

## Limitações e compatibilidade
Nem todas as wallets têm suporte completo a descritores. Por exemplo, Bitcoin Core implementa apenas um subconjunto e exige dois descritores separados para endereços e change. Softwares como Sparrow ou Specter oferecem suporte melhor, permitindo importar/exportar descritores e visualizar sua estrutura.

Experimentos podem ser feitos com:
- Sparrow: suporta descritores, com uma interface gráfica para criá-los ou analisá-los.
- BDK: biblioteca com interface de linha de comando para gerenciar descritores complexos.
- Testnet/Signet: ambientes seguros para testar sem arriscar fundos reais.

## Referências

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

## Programa
Esta aula foi criada para um Satoshi Spritz Connect.
