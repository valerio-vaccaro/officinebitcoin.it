---
layout: default
title: "Jade com Electrum Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduções

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade com Electrum Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/0_cover.jpg)

Depois de inicializar o Jade, é possível começar a usá-lo e, para isso, é preciso escolher um wallet de visualização.

Jade é um dispositivo que pode ser usado com vários wallets, ou companion apps como a Blockstream as define no seu site.

Neste tutorial serão vistas as etapas de utilização, via USB, com Electrum Wallet.

Pegue o Jade inicializado. Assim que é ligado, ele aparece desta forma:


![alt text](https://officinebitcoin.it/lezioni/jadeele/001.jpg)

Ao selecionar Unlock Jade, aparece o menu no qual se deve escolher como conectar o dispositivo à companion app.

Com Electrum é possível conectar Jade somente via USB, portanto essa opção deve ser escolhida.

Inicie Electrum, que abrirá propondo como opção padrão a abertura do último wallet utilizado.

Se esta for a primeira vez que Jade é conectado ao Electrum, selecione Create New Wallet e depois Finish.

![alt text](https://officinebitcoin.it/lezioni/jadeele/1.jpg)

Dê um nome ao wallet, por exemplo Jade_Officine.

![alt text](https://officinebitcoin.it/lezioni/jadeele/3.jpg)

Selecione Standard Wallet

![alt text](https://officinebitcoin.it/lezioni/jadeele/4.jpg)

Na escolha do keystore, é fundamental selecionar Use a hardware device.

![alt text](https://officinebitcoin.it/lezioni/jadeele/5.jpg)

Electrum inicia a varredura em busca do dispositivo hardware

![alt text](https://officinebitcoin.it/lezioni/jadeele/6.jpg)

Ao conectar o USB ao PC (já conectado pelo lado USB C ao Jade), o hardware wallet mostra a tela de bloqueio. Jade é desbloqueado inserindo o PIN de seis dígitos definido durante o setup


![alt text](https://officinebitcoin.it/lezioni/jadeele/7.jpg)

Com o dispositivo hardware desbloqueado, Electrum detecta Jade. Continue clicando em Next.

![alt text](https://officinebitcoin.it/lezioni/jadeele/8.jpg)

Neste ponto Electrum pede para definir a script policy; escolha Native Segwit.

![alt text](https://officinebitcoin.it/lezioni/jadeele/9.jpg)

Começa a fase de transferência da chave pública do wallet no Jade para o Electrum de visualização.

![alt text](https://officinebitcoin.it/lezioni/jadeele/10.jpg)

Ao final da exportação da chave pública, o procedimento está concluído.

O wallet watch-only está pronto e Electrum avisa sobre a conclusão com a tela a seguir.

![alt text](https://officinebitcoin.it/lezioni/jadeele/11.jpg)

O wallet foi efetivamente criado e é possível começar a explorá-lo: veem-se os addresses, as wallet information e, sobretudo, é possível notar no canto inferior direito a indicação de que se trata de um wallet criado a partir de Blockstream Jade. O ponto verde ao lado do logo Blockstream indica que o dispositivo está ligado e conectado corretamente.

![alt text](https://officinebitcoin.it/lezioni/jadeele/12.jpg)

Transações de recebimento e de gasto

No menu Receive de Electrum, gere um scriptPubKey (endereço) para receber fundos. Comece sempre com um valor pequeno e faça um teste de recebimento+gasto.

![alt text](https://officinebitcoin.it/lezioni/jadeele/13.jpg)

Depois de recebidos os sats, é possível verificar a chegada deles no menu History.

![alt text](https://officinebitcoin.it/lezioni/jadeele/14.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeele/15.jpg)

Uma vez confirmada a transação, é possível gastar este UTXO e terminar o teste.

O gasto exigirá o uso de Jade para assinar.

Vá ao menu Send de Electrum, cole um scriptPubKey e confira-o bem.

![alt text](https://officinebitcoin.it/lezioni/jadeele/16.jpg)

Quando terminar, pressione Pay.

Abre-se a janela de transação, na qual é importante definir as fees de transação corretas. Concluídas todas as configurações, clique em Preview no canto inferior direito.

![alt text](https://officinebitcoin.it/lezioni/jadeele/17.jpg)

A janela de transação mostra alguns detalhes importantes, antes de tudo o status: Unsigned.

Nesta fase também é possível ver o comando Sign, justamente para aplicar a assinatura com Jade.

![alt text](https://officinebitcoin.it/lezioni/jadeele/18.jpg)

Electrum avisa para seguir as instruções no dispositivo hardware, que está pronto para assinar.

Antes, porém, é melhor verificar o que está sendo assinado: todos os parâmetros da transação recém-configurada também aparecem em Jade e é possível verificá-los todos.

![alt text](https://officinebitcoin.it/lezioni/jadeele/19.jpg)

Para continuar, certifique-se de posicionar o cursor sempre na seta → que leva às fases seguintes, e nunca no "X" que cancela a operação.

A visualização das verificações termina quando Jade mostra as fees. Neste ponto, confirmar equivale a colocar a assinatura.

![alt text](https://officinebitcoin.it/lezioni/jadeele/20.jpg)

Por um breve instante Jade processa a assinatura.

![alt text](https://officinebitcoin.it/lezioni/jadeele/21.jpg)

Enquanto isso, em Electrum é possível verificar o status da transação, que mudou de Unsigned para Signed, e agora é possível propagar a transação clicando em Broadcast.

![alt text](https://officinebitcoin.it/lezioni/jadeele/22.jpg)

O wallet, testado dessa forma, pode ser usado para receber UTXO destinados a serem guardados com segurança.

![alt text](https://officinebitcoin.it/lezioni/jadeele/23.jpg)
