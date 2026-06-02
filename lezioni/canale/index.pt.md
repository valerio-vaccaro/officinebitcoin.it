---
layout: default
title: "Lightning Network non-custodial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/canale/01cover.webp)

# Lightning Network non-custodial
Phoenix da Acinq é um wallet Lightning Network nativo, non-custodial, que oferece um wallet eficiente compatível com o padrão BIP39, bem conectado e que deixa o controle total aos usuários.

Você logo descobrirá que o Phoenix abre um canal LN, por cujo saldo você é 100% responsável.
Para trabalhar bem com o Phoenix, bastam uma atenção mínima e conhecimentos básicos da Lightning Network. Você aprenderá, por exemplo, a manter sob controle a liquidez do seu canal, a mantê-lo equilibrado conforme suas necessidades e a garantir que a Acinq veja você online, para mantê-lo aberto e preservar a infraestrutura LN.

# Operações básicas
Depois de [baixar e verificar o apk do Phoenix](https://officinebitcoin.it/lezioni/verifica/index.html), você pode instalar o app no seu telefone.

O Phoenix abre perguntando se você quer criar um wallet novo ou restaurar um anterior. Se esta é sua primeira experiência com o Phoenix, escolha `Create new wallet`. Em seguida aparecerá uma série de telas de boas-vindas, terminando onde você pressionará `Get started`.

![img](https://officinebitcoin.it/lezioni/canale/03.webp)

## Backup
Quando o Phoenix estiver aberto, **a primeira operação a fazer é, como sempre, o backup do wallet**.

O Phoenix adota o padrão BIP39, caminho de derivação m/84'/0'/0', fornecendo uma sequência de 12 palavras para transcrever em papel e guardar em um local seguro.

![img](https://officinebitcoin.it/lezioni/canale/04.webp)

Entre nos menus e peça ao Phoenix para mostrar a *Recovery phrase*, clicando em `Display seed`.

![img](https://officinebitcoin.it/lezioni/canale/05.webp)

Ao terminar, lembre-se de rolar a tela até o fim para confirmar que você fez o backup e deixar de ver a notificação e o alerta.

![img](https://officinebitcoin.it/lezioni/canale/06.webp)

O Phoenix está essencialmente pronto para uso. Seu novo wallet tem saldo zero e pode ser configurado. No canto inferior esquerdo você encontrará o comando para entrar novamente nas configurações e ajustar opções úteis para o uso diário.

![img](https://officinebitcoin.it/lezioni/canale/07.webp)

## Uso com Tor
Há várias versões do Phoenix, a Acinq desativou o motor Tor integrado. Se você quiser usar o Phoenix com proteção Tor, são necessários dois passos:
- habilitar o Tor nas configurações do Phoenix
- usar um app de terceiros para rotear o tráfego do wallet pela rede onion.

Acesse as configurações e escolha Tor, depois habilite `Enable Tor` e, por fim, roteie o tráfego pelo app que você costuma usar (Orbot, Invizible Pro, etc.). Sem um desses apps de terceiros, mas com o Tor habilitado nas configurações do Phoenix, o wallet não conseguirá se conectar à internet.

![img](https://officinebitcoin.it/lezioni/canale/09.webp)

## Outras configurações
Você pode alterar ou definir várias funções:
- o nome do wallet, clicando na palavra `Wallet` na parte superior;
- a moeda de referência no submenu `Display`.
- definir as taxas em `Channel management`, uma configuração importante porque um valor de taxa baixo demais poderia comprometer a abertura do canal: por padrão está definido em 5,000 sats, aumente para 15,000; de qualquer forma, o Phoenix usará o valor apropriado no momento;
- você deve configurar todas as precauções de segurança que acredita conseguir gerenciar, no submenu `Access control`: PIN para gastar, PIN ou controle biométrico para acesso ao app;
- configurar seu próprio `Electrum server` no menu com esse nome, observando que o Phoenix exige um certificado SSL válido (Let's Encrypt, por exemplo);
- habilitar `Experimental features` para solicitar um endereço LN Bolt12 reutilizável
- gerenciar eventuais fechamentos de canais ou criação/exclusão de múltiplos wallets.

![img](https://officinebitcoin.it/lezioni/canale/08.webp)

# Abertura de canal LN ⚡️

Na tela principal do Phoenix, escolha o comando `Receive`

![img](https://officinebitcoin.it/lezioni/canale/10.webp)

O wallet oferece dois modos de recebimento, ambos com QR code: Lightning e Onchain.

## Pagar uma invoice Lightning

![img](https://officinebitcoin.it/lezioni/canale/11.webp)

Uma forma rápida de abrir seu canal LN é criar uma invoice com o Phoenix e pagá-la com outro wallet LN.

O primeiro pagamento recebido determina a abertura de um canal, cuja liquidez é definida pelo valor da invoice que você acabou de criar (excluindo as taxas da transação onchain de abertura do canal).

Os fundos podem ficar imediatamente disponíveis, apesar de ser exibido um aviso temporário de espera por confirmações onchain. Ou talvez você precise esperar para usá-los.

## Transação onchain
Abrir um canal LN é sempre uma transação onchain, multisig 2-de-2: você e a contraparte (Acinq) estão estabelecendo as condições, com seus fundos.

Se você não tem a opção de pagar ou receber uma invoice Lightning, mas tem fundos onchain, pode usar o endereço onchain que o Phoenix mostra para você.

Depois da transação, o Phoenix fica assim:

![img](https://officinebitcoin.it/lezioni/canale/12.webp)

O app avisa que você precisa esperar 3 confirmações da blockchain antes de poder usar os fundos.

# Gerenciar a liquidez do canal
Assim que você receber as 3 confirmações, seu wallet LN estará pronto para uso.

Inicialmente ele tem toda a liquidez de saída e você só pode gastar; você pode ver isso em `Settings -> Advanced -> Payment Channels`

![img](https://officinebitcoin.it/lezioni/canale/13.webp)

Você pode criar liquidez de entrada pagando uma ou mais invoices Lightning Network.

# Usar o wallet

Usar o Phoenix wallet é uma experiência agradável e muito simples.

As únicas coisas a ter em mente são:
1. o canal que você acabou de criar é um smart contract entre você e a Acinq, financiado com seus fundos;
2. o trabalho pesado de fazer backup dos estados do canal e manter sua infraestrutura é feito pela Acinq, que cobrará alguns sat extras em taxas pelas operações de pagamento que você realizar;
3. acesse seu wallet regularmente, abrindo-o e fazendo operações de tempos em tempos porque, se a contraparte notar sua ausência e considerar você um "zombie", ela pode decidir fechar o canal. A Acinq fecha canais para evitar gastar recursos e tempo mantendo backups e canais inativos;
4. você também pode decidir fechar este canal, caso não precise mais usá-lo.
5. em caso de fechamento do canal, o procedimento de `cooperative closure` é o melhor, porque evita muitos problemas.

## Splicing
Uma menção especial vai para a técnica de `Splicing`, implementada pela Acinq e que permite aumentar ou reduzir a capacidade total do canal.

Splicing é interessante: se você tem um canal com capacidade `tot`, pode expandi-lo ou reduzi-lo. Pode parecer que essas operações dependem das necessidades de cada pessoa, **mas não é tão simples**.

Você deve sempre lembrar que **Phoenix é um wallet Lightning Network** e, embora tenha suporte ao Layer1 do Bitcoin, deve ser usado para pequenos pagamentos no Layer2.

**Toda operação onchain, de fato, será interpretada pela Acinq como um motivo para modificar a capacidade do canal**:
- receber um valor de `xsats` no Phoenix vindo de um wallet onchain: a Acinq expande o canal, levando a capacidade de `tot` para `tot + xsats`
- pagar um valor de `ysats` do Phoenix para um endereço onchain: a Acinq reduz o canal, levando a capacidade de `tot` para `tot - ysats`.

`Splicing` é uma transação onchain (multisig 2-de-2) que incorre em taxas. Embora menores do que as de abertura/fechamento de canal, fazer essas operações sem cuidado ou no momento errado pode resultar em custos desnecessariamente altos.

Para mover de LN para Onchain e vice-versa, tente usar ferramentas de `swap` apropriadas e não use o Phoenix Wallet para isso.

# Recuperar fundos
Por último, mas o mais importante de tudo, é aqui que entra em jogo a importância de ter ferramentas **non-custodial**.

Se e quando o canal for fechado, você pode recuperar seus fundos onchain **importando as 12 palavras de backup em um wallet que suporte o padrão BIP39**.

O Electrum wallet, entre outros, é uma opção que torna essa operação simples e intuitiva.

Se o wallet for, em vez disso, *custodial* e você não possuir as chaves, poderá encontrar problemas, desde dificuldades para interagir com um *atendimento ao cliente impessoal*, passando por se submeter a um `kyc` pesado para recuperá-las, **até a impossibilidade de recuperar seus fundos (qualquer que seja o valor total)**.

Vale a pena?

# Apoio ao estudo
Se você participou da apresentação ao vivo no Telegram, pode considerá-la mais um passo rumo à sua soberania pessoal (não apenas financeira).
Se você perdeu, **não se desespere**: estas notas servem justamente para recuperar o conteúdo e, além disso, saiba que vamos propô-la novamente na Officine.

Para não perder a próxima apresentação, entre no [grupo Telegram](https://t.me/officinebitcoin) para se manter constantemente atualizado.

![img](https://officinebitcoin.it/lezioni/canale/14.webp)

Você também pode encontrar o [Satoshi Spritz](https://satoshispritz.it/) mais próximo de você. Um Satoshi Spritz é um meetup local onde se discute apenas Bitcoin, onde você pode levar suas perguntas e obter respostas de outros bitcoiners experientes. No link você encontrará o mapa da península.

![img](https://officinebitcoin.it/lezioni/canale/15.webp)

Por fim, se você não encontrar um meetup perto de você, pode aproveitar as transmissões ao vivo semanais do [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), um meetup virtual criado para quem não pode participar do Satoshi Spritz, ou para ajudar meetups menores a tomar notas e encontrar inspiração para suas próprias apresentações.

![img](https://officinebitcoin.it/lezioni/canale/16.webp)
