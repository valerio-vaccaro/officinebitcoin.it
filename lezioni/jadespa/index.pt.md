---
layout: default
title: "Jade airgapped com Sparrow Wallet"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Jade airgapped com Sparrow Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/0.jpg)

Usar o Jade para comunicações completamente airgapped é possível graças às características do seu firmware e hardware.

A câmera integrada e a tela, de fato, cumprem exatamente a função de adquirir e enviar mensagens de e para o wallet watch-only.

Este tutorial mostra como usar o Jade airgapped com Sparrow Wallet.

O procedimento envolve primeiro a configuração, depois a exportação da chave pública estendida do Jade para o Sparrow-watch-only e, por fim, uma transação de gasto.

Por escolha didática, decidiu-se começar mostrando a sequência de operações a partir do Jade.

## Configuração avançada

A escolha de usar o dispositivo airgapped envolve uma configuração real, ou seja, deve ser feita no momento da inicialização do Jade (1), que portanto deve se apresentar como não inicializado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/1.jpg)

Aparece um aviso para verificar as instruções de configuração no site https://blockstream.com/jade/.

![alt text](https://officinebitcoin.it/lezioni/jadespa/2.jpg)

A configuração do Jade para uso airgapped só pode ser feita escolhendo Advanced Setup.

![alt text](https://officinebitcoin.it/lezioni/jadespa/3.jpg)

O Jade avisa que essa configuração tem alguns recursos técnicos avançados. Basta prestar a máxima atenção e clicar no botão de confirmação.

![alt text](https://officinebitcoin.it/lezioni/jadespa/4.jpg)

Com o objetivo de inserir a mnemônica gerada com entropia de dados, escolha Restore Wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/5.jpg)

Agora você deve definir o comprimento da mnemônica, 12 ou 24 palavras. O menu também oferece a possibilidade de restaurar o wallet escaneando um código QR: este é o SeedQr, que foi tratado no tutorial dedicado à configuração.

![alt text](https://officinebitcoin.it/lezioni/jadespa/6.jpg)

Por motivos puramente didáticos e de rapidez, este tutorial mostra a configuração com uma mnemônica de 12 palavras.

O próximo passo deve ser seguido conforme descrito, para poder acessar a funcionalidade airgapped. Você deve, de fato, escolher exportar a frase de recuperação em formato CompactSeedQR, selecionando Yes.

![alt text](https://officinebitcoin.it/lezioni/jadespa/7.jpg)

Depois da escolha, você é avisado de que deve desenhar o código QR no modelo fornecido na caixa, como mostrado na seção "Extra" da aula dedicada à configuração.

![alt text](https://officinebitcoin.it/lezioni/jadespa/8.jpg)

Ao fim do procedimento, é necessário verificar a correspondência entre o que foi desenhado e o CompactSeedQR mostrado pelo dispositivo. De fato, a câmera integrada do Jade é habilitada, com a qual você deve enquadrar o SeedQR recém-desenhado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/9.jpg)

Se o desenho corresponder ao que o dispositivo propôs no procedimento recém-concluído, será exibido um sinal de confirmação.

![alt text](https://officinebitcoin.it/lezioni/jadespa/10.jpg)

Agora o Jade mostra as opções para conectar o dispositivo a uma companion app: escolha QR.

![alt text](https://officinebitcoin.it/lezioni/jadespa/11.jpg)

O próximo passo também exige uma escolha do usuário: salvar as chaves criptografadas no dispositivo ou carregá-las a cada sessão, escaneando o SeedQR recém-desenhado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/12.jpg)

Nota:

É útil entender estas duas opções de acesso:

- QR PIN Unlock: Durante a inicialização, o Jade salvará os dados do wallet criptografando-os no dispositivo; eles estarão sempre acessíveis desbloqueando o Jade com o procedimento QR PIN.
- SeedQR: o SeedQR deve ser escaneado pelo Jade toda vez que você quiser carregar as chaves no dispositivo.

Por escolha didática, na opção anterior foi escolhido SeedQR, portanto o dispositivo será usado stateless: o Jade avisa que a sessão é temporária e que as chaves serão "esquecidas" pelo dispositivo quando ele for desligado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/13.jpg)

Exportação da chave pública

Agora que o Jade está configurado especificamente para funcionar totalmente airgapped, passamos à fase delicada de exportar a chave pública.
 
Partindo sempre do Jade, que voltou aos menus iniciais, escolha Options.

![alt text](https://officinebitcoin.it/lezioni/jadespa/14.jpg)

Nota: o fato de o Jade estar no modo Temporary Signer é visível pelo ícone que representa um relógio ao lado da indicação Active.

Em Options, escolha Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/15.jpg)

Depois selecione Export Xpub

![alt text](https://officinebitcoin.it/lezioni/jadespa/16.jpg)

Neste ponto, a tela do Jade mostra um código QR dinâmico que representa a chave pública estendida. Em Options deste submenu, você pode escolher a exportação de multisig/singlesig e o caminho de derivação.

Para este tutorial, foi escolhida a exportação de um singlesig full segwit.

![alt text](https://officinebitcoin.it/lezioni/jadespa/17.jpg)

É nesta fase que o Sparrow entra em cena. Inicie o programa e crie um novo wallet escolhendo New Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/18.jpg)

Dê um nome ao wallet e clique em Create Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/19.jpg)

Na próxima tela de configurações, clique em Airgapped Hardware Wallet

![alt text](https://officinebitcoin.it/lezioni/jadespa/20.jpg)

Abre-se uma janela do Sparrow mostrando os hardware wallets implementados. Escolha Jade

![alt text](https://officinebitcoin.it/lezioni/jadespa/21.jpg)

Neste ponto, a câmera do PC com o qual você está operando é ativada.

![alt text](https://officinebitcoin.it/lezioni/jadespa/22.jpg)

Se você tiver mais de uma webcam disponível, selecione a melhor no menu suspenso onde aparece Default Camera.

Agora pegue o Jade (que enquanto isso continua mostrando o código QR dinâmico que representa o Xpub) e coloque a tela diante da câmera do PC, mantendo o código QR dentro do espaço tracejado.

![alt text](https://officinebitcoin.it/lezioni/jadespa/23.jpg)

Abaixo da imagem da câmera há uma barra de progresso que fica azul.

O avanço da aquisição do Xpub no Sparrow é indicado dessa forma: de 0 a 100%.

Nesta fase, alguns ajustes podem ser necessários: aumentar/diminuir o brilho da tela do Jade, bem como sua iluminação frontal, ou escolher no menu suspenso do Sparrow Use HD Capture ou uma redução de resolução.

Não se assuste com esses detalhes; depois de configurar seu ambiente pessoal de trabalho, essas fases ocorrerão com total conforto e facilidade. (2)

De fato, a exportação ocorreu quando a janela da câmera se fecha e, ao retornar às Settings do Sparrow, aparecem todos os dados do wallet watch-only.

![alt text](https://officinebitcoin.it/lezioni/jadespa/24.jpg)

Pela estrutura do Sparrow, agora é necessário aplicar a script policy clicando em Apply.

A criação do wallet prossegue com a inserção e confirmação de uma senha para criptografar o arquivo do wallet.

![alt text](https://officinebitcoin.it/lezioni/jadespa/25.jpg)

E se conclui quando a barra de progresso no canto inferior direito preencheu o campo até 100%.

![alt text](https://officinebitcoin.it/lezioni/jadespa/26.jpg)

## Transação de gasto

Se, hipoteticamente, o Jade exerce o papel de hardware wallet pessoal, deve-se assumir que ele possui fundos e que estes deverão ser gastos no futuro.

Depois de escolher o Sparrow como wallet watch-only e o Jade como dispositivo de assinatura, vejamos como construir, assinar e propagar uma transação com essas duas ferramentas.

![alt text](https://officinebitcoin.it/lezioni/jadespa/27.jpg)

No exemplo, há um saldo total disponível de 56,598 sats.

No menu esquerdo do Sparrow, selecione Send e comece a construir a transação de gasto. Depois de configurar tudo, clique em Create transaction no canto inferior direito.

![alt text](https://officinebitcoin.it/lezioni/jadespa/28.jpg)

Aparece uma janela avançada de transação, onde é visível que o Sparrow reconhece o Jade como dispositivo de assinatura (Signing Wallet).

Se as configurações forem satisfatórias, clique em Finalize Transaction.

![alt text](https://officinebitcoin.it/lezioni/jadespa/29.jpg)

Aparece a tela de assinaturas. Em um sistema airgapped, a exportação do .psbt acontece por código QR, então no Sparrow clique em Show QR no canto inferior esquerdo.

![alt text](https://officinebitcoin.it/lezioni/jadespa/30.jpg)

Aparece uma janela mostrando um código QR dinâmico, que representa a psbt, que então precisará ser escaneada com a câmera do Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/31.jpg)

Pegue o Jade e, nos menus principais, selecione Scan QR

![alt text](https://officinebitcoin.it/lezioni/jadespa/32.jpg)

Enquadre com a câmera do Jade, agora ativada, o código QR dinâmico que o Sparrow está gerando. Uma barra azul na tela do hardware wallet indica a porcentagem de conclusão da leitura.

Quando a importação da psbt termina, o Jade mostra os detalhes da transação para verificação: endereço de destino e valor em uma primeira tela

![alt text](https://officinebitcoin.it/lezioni/jadespa/33.jpg)

e as taxas em uma segunda tela. Ao confirmar nesta última, a assinatura é aplicada pelo Jade.

![alt text](https://officinebitcoin.it/lezioni/jadespa/34.jpg)

Automaticamente, a tela do Jade mostra outro código QR dinâmico: é a transação assinada.

Entre as opções desta tela, você pode aumentar/diminuir a densidade para melhorar a comunicação com a wallet app.

![alt text](https://officinebitcoin.it/lezioni/jadespa/35.jpg)

Enquanto isso, o Sparrow, que deixamos exibindo um código QR dinâmico, deve ser configurado para receber a transação assinada e propagá-la.

Você deve então clicar em Scan QR para reativar a webcam do PC.

![alt text](https://officinebitcoin.it/lezioni/jadespa/36.jpg)

Posicione a tela do Jade diante da webcam e deixe o Sparrow importar a transação assinada.

![alt text](https://officinebitcoin.it/lezioni/jadespa/37.jpg)

A barra de progresso abaixo da imagem deve chegar a 100% até que a importação ocorra, o que o Sparrow mostra da seguinte forma.

![alt text](https://officinebitcoin.it/lezioni/jadespa/38.jpg)

Agora toda a transação é verificada novamente e, se estiver correta, você pode propagá-la clicando em Broadcast Transaction.

No menu Transactions, aparece a transação de saída.

![alt text](https://officinebitcoin.it/lezioni/jadespa/39.png)

Notas

- (1) – Se o Jade já estiver inicializado, basta ir ao menu Options → Settings → Factory reset
- (2) – O Jade Original tem uma tela muito pequena e, para enquadrar o código QR dinâmico no espaço tracejado que o Sparrow mostra, é necessário aproximar a tela a poucos centímetros. Portanto, pode ser necessário usar uma webcam de altíssima resolução com distância focal adequada, ou recorrer a apps como Iriun para "transformar" um telefone na câmera do PC. Os telefones, de fato, têm capacidade superior de foco a curta distância.
