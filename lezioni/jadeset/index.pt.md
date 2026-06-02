---
layout: default
title: "Configuração do Jade"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Configuração do Jade

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

O Jade chega em uma embalagem cuja integridade deve ser verificada, conferindo os dois adesivos holográficos antiviolação colocados entre a caixa (parte inferior) e a tampa (parte superior).

A embalagem contém um pequeno manual do usuário, dois modelos CompactSeedQR e o hardware wallet.

O Jade liga mantendo pressionado o botão inferior e se apresenta mostrando os 3 menus:

- Setup Jade
- Scan QR
- Options

Em Options é possível definir vários parâmetros, de acordo com as preferências pessoais, mas a inicialização é a primeira parte a ser concluída.

Usando o botão de rolagem, selecione então o menu __Setup Jade__ e confirme com o botão frontal.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

Aparece um aviso para verificar as instruções de configuração no site https://blockstream.com/jade/

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

Para uma execução correta, recomenda-se criar a mnemônica com lançamentos de dados e usar essa entropia para criar o wallet. Portanto, escolha __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

O Jade avisa que essa configuração tem alguns recursos técnicos avançados. Basta prestar a máxima atenção e clicar no botão de confirmação.

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

Com o objetivo de inserir a mnemônica gerada com entropia de dados, escolha __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

Agora você deve definir o comprimento da mnemônica, 12 ou 24 palavras. O menu também oferece a possibilidade de restaurar o wallet escaneando um código QR: este é o SeedQr, que será tratado em outro lugar.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

Por motivos puramente didáticos e de rapidez, este tutorial mostra a configuração com uma mnemônica de 12 palavras.

Começa o procedimento para inserir a primeira palavra e o Jade mostra o teclado para digitar as respectivas letras. Com o botão de rolagem, posicione-se ← → na posição correta.

Neste exemplo, a palavra n.º 1 é "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

Depois de inserir as primeiras 3-4 letras, o Jade seleciona palavras do dicionário BIP39 e começa a fornecer uma série de sugestões. Com o botão de rolagem, avance ou volte até encontrar a palavra correta.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Continue inserindo as palavras até chegar ao momento da última palavra: o checksum.

Neste ponto, o Jade mostra duas possibilidades: inserir uma palavra existente ou oferecer a possibilidade de calcular um checksum válido com seu próprio software.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Nota:

- No caso de configuração a partir de uma mnemônica de 12 palavras criada com lançamentos de dados, recomenda-se escolher Existing e inserir as primeiras letras da palavra, escolhendo-as dentro do intervalo proposto pelo lançamento de dados.
- Se a configuração começar, em vez disso, a partir de uma mnemônica de 24 palavras gerada com lançamentos de dados, você pode fazer o Jade calcular todos os checksums possíveis e depois escolher um. É verdade que se perde um pouco de entropia, mas apenas na última palavra. Quando você decide confiar seus fundos ao Jade, é uma compensação aceitável.
- Em caso de restauração de um wallet existente: insira o checksum correto escolhendo Existing.

Continuando com o exemplo de configuração a partir de uma mnemônica gerada com lançamentos de dados, escolhemos Existing no menu anterior, com a intenção de inserir as letras e encontrar o checksum correspondente.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

Neste ponto, o Jade propõe exportar a frase de recuperação na forma de _CompactSeedQR_.

O _CompactSeedQR_ é uma codificação que transforma a frase mnemônica em um código QR a ser escaneado para restauração do wallet no Jade.

Se quiser tentar fazer isso, veja a seção no fim deste tutorial que explica como proceder.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Ao escolher "No" no menu anterior, você pode prosseguir até o fim da configuração.

O dispositivo está pronto para ser conectado ao seu wallet watch-only.

O menu seguinte mostra as possibilidades de conexão:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Escolha USB e confirme com o botão de confirmação.

Neste ponto, o Jade pede para ser conectado a uma companion app.

No exemplo a seguir, foi escolhida a conexão do dispositivo via USB ao Blockstream Green; esse wallet, de fato, permite controlar atualizações de firmware do Jade e, ao escutar o dispositivo via USB, oferece uma configuração guiada.

Abra o Green e verifique as configurações de rede e segurança.

Se houver uma atualização de firmware, o Green sinaliza imediatamente e recomenda-se realizar o upgrade.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

Depois que a atualização do firmware é concluída, o Green começa a interagir com o Jade.

O dispositivo de assinatura, neste ponto, pede para definir o duress PIN, que irá criptografar as chaves privadas no Jade, tornando-as inacessíveis a qualquer pessoa, exceto a quem possuir o PIN de seis dígitos.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

Enquanto o Green aguarda com a tela mostrada acima, no Jade aparece a possibilidade de definir o PIN de 6 dígitos e confirmá-lo inserindo-o novamente corretamente.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

O Jade cria dados persistentes criptografando-os no dispositivo.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

Ao fim da operação, que pode levar alguns instantes, o Green abre o wallet pronto para uso.

Ao desligar o Jade e ligá-lo novamente, o dispositivo se apresentará como inicializado, com firmware atualizado e pronto para ser desbloqueado (Unlock Jade) para uso com sua companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: criação do CompactSeedQR

Ao fim da inserção da mnemônica, pulamos a parte de exportação das chaves em formato de código QR para manter o foco na fase de configuração. Esse tipo de exportação sempre pode ser feito depois.

Ligue o Jade e, no menu Options → Temporary Signer → Continue → 12/24 Words, você retorna ao menu de inserção da frase de recuperação, ao fim do qual é proposta a tela de escolha para exportação em formato SeedQR.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

Ao escolher Yes, você é avisado de que deve desenhar o código QR no modelo fornecido na caixa.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

O procedimento começa mostrando uma visão geral de como será o código QR a ser desenhado (algumas partes foram apagadas por motivos de privacidade).

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

Em seguida, todas as casas da grade serão mostradas, uma por uma, de A1 a C3 ou E5, dependendo do comprimento da frase de recuperação.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

Depois de desenhar a última casa da grade, o Jade mostra novamente a visão geral para uma primeira verificação. Continue confirmando Done.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

A câmera integrada do Jade é habilitada, com a qual você deve enquadrar o SeedQR recém-desenhado.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

Se o desenho corresponder ao que o Jade propôs no procedimento recém-concluído, será exibido um sinal de confirmação.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

Ao clicar para confirmar Continue, o Jade se apresenta funcionando a partir dos menus principais.

O CompactSeedQR é uma ferramenta para restaurar o wallet no Jade.
