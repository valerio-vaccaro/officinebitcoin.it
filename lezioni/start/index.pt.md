---
layout: default
name: "Kit inicial de Bitcoin"
description: "Um kit inicial simples e fácil de implementar para usar Bitcoin corretamente. Aprenda a baixar e instalar uma wallet móvel, configurar um POS para pedidos de pagamento e descobrir configurações avançadas da wallet."
title: "Glossário inicial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduções

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](assets/cover.webp)

Esta é uma ótima forma de começar a usar Bitcoin da maneira mais correta possível. O que segue é uma proposta de *starter kit* muito enxuta e fácil de implementar, que você pode configurar de forma independente.

Seja você uma pessoa curiosa, um profissional que quer aceitar Bitcoin como forma de pagamento, ou um usuário experiente procurando soluções para amigos e familiares, este guia permitirá:
- baixar e instalar uma wallet móvel para usar Bitcoin em todos os níveis (onchain para armazenamento de longo prazo; ou Liquid e Lightning para pagamentos instantâneos);
- configurar um POS para gerar pedidos de pagamento a partir do preço dos seus bens/serviços em euros;
- conhecer configurações avançadas da wallet. Deixamos esta parte no fim do guia para simplificar a abordagem inicial, mas olhe sempre esta parte, porque ela é importante.

Vamos primeiro esclarecer o que queremos dizer quando falamos em usar Bitcoin da forma *correta*.

# Glossário inicial
- `Not your keys, not your coins`
  Se você está se aproximando de Bitcoin pela primeira vez, a frase `Not your keys, not your coins` é nova para você e seu significado se reduz à tradução literal. Bitcoin funciona com o princípio da criptografia assimétrica, baseada em pares de chaves públicas e privadas. É com a posse **única** e a gestão individual das chaves privadas que você pode dizer que controla seus Bitcoin.
  
  Portanto, só você deve conhecer as chaves privadas, o segredo que permitirá possuir e eventualmente gastar os bitcoin associados a essas chaves. `Not your keys, not your coins` é praticamente um _mantra_ para bitcoiners no mundo inteiro e também se tornará um para você.

- `Recovery phrase`
  Durante sua breve história, o protocolo Bitcoin evoluiu para tornar mais simples a gestão dos segredos, isto é, das chaves privadas. Hoje elas são representadas como uma sequência de 12 ou 24 palavras em inglês, uma forma mais simples de transcrevê-las e verificá-las. As palavras são o principal segredo a guardar. Devem ser transcritas em papel e mantidas em um lugar muito seguro, como um cofre. Nunca devem ser fotografadas, transferidas para um computador nem, muito menos, compartilhadas com outras pessoas.

- `Wallet`
  A wallet é a ferramenta que permitirá ver seu saldo, aceitar Bitcoin e gastá-los. Durante este tutorial baixaremos uma no seu telefone. A wallet no telefone é chamada `hot wallet`, porque fica em um dispositivo sempre conectado à internet. Para quem está começando, isso é perfeitamente adequado; com estudo, você aprenderá outros métodos para aperfeiçoar o uso da wallet.

- `Non Custodial`
  É fundamental começar a usar Bitcoin com wallets `non-custodial`, isto é, aquelas que **dão a você controle completo sobre as chaves privadas**. Desconfie sempre de quem o empurra para usar ferramentas diferentes, chamadas custodial, para se aproximar de Bitcoin. Wallets custodial são ferramentas cujas chaves você não possui. Não é uma questão de **se**, mas de **quando** elas impedirão permanentemente seu acesso aos fundos.

# Blockstream App (ex Green Wallet)
Para o starter kit, baixaremos Blockstream App, uma wallet `open source` cujo código você pode verificar. A aplicação tem uma longa tradição de desenvolvimento e um bom histórico; a wallet já demonstrou confiabilidade no passado.

---
⚠️ As instruções seguintes são para baixar e instalar o app no Android. Para iOS, você deve usar a loja oficial.

---

## 🌍 Traduções

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

Acesse https://github.com/Blockstream/green_android, o repositório oficial do desenvolvedor no Github.

![img](assets/01.webp)

No meio da página, à direita, selecione `Latest` no espaço dedicado a *Releases* para baixar a versão mais atualizada.

Você chegará a uma página que mostra a última release, 5.1.4 no momento da escrita deste tutorial, em dezembro de 2025. Na mesma página selecione o que pode baixar:

![img](assets/02.webp)

Baixe o arquivo `.apk` sem passar pela Play Store e instale-o no seu telefone Android.

![img](assets/03.webp)

---
⚠️ Seu telefone pode exigir permissões especiais para baixar apps de fontes não certificadas. Conceda essas permissões para continuar.

---
Quando o Android pedir para instalar Blockstream App, clique em `Install`.

![img](assets/04.webp)

Ao final da instalação, escolha `Open`.

![img](assets/05.webp)

Blockstream App abre e, para começar a usar a wallet, escolha `Get Started`.

![img](assets/07.webp)

Blockstream perguntará se você quer participar da coleta de dados para ajudar os desenvolvedores a melhorar o app. Recuse o convite.

![img](assets/08.webp)

# Sua primeira wallet
Você pode começar a criar sua primeira wallet. Clique em `Set Up Mobile Wallet`.

![img](assets/09.webp)

O processo de criação da wallet começa.

![img](assets/10.webp)

Ele termina em poucos segundos. Sua wallet está pronta e, para começar a usá-la, clique em `Continue`.

![img](assets/11.webp)

A wallet abre na tela chamada `Home`. Por enquanto, observe, mas concentre-se imediatamente no menu inferior `Security`.

# Suas chaves, suas moedas

![img](assets/12.webp)

Neste menu será solicitado o backup da sua wallet. Isso nada mais é do que exibir a sequência de 12 palavras que você precisará para restaurá-la no futuro. Essas 12 palavras são sua wallet: **certifique-se de estar em um ambiente seguro, longe de olhares indiscretos, e tenha um caderno ou papel para transcrever as palavras antes de guardá-las em um lugar seguro** (por exemplo, um cofre). Clique em `Back Up Now` e descubra as 12 palavras.

**Anote também a ordem exata das palavras: 1, 2, 3 etc.; escreva as palavras em maiúsculas para melhor leitura futura, mas lembre-se de que, se precisar inseri-las manualmente no futuro, deverá usar minúsculas**.

![img](assets/13.webp)

Depois de transcrever e guardar as palavras em lugar seguro, continue com o starter kit. Todas as configurações adicionais estão no fim do guia.

# Menu TRANSACT
Usar a wallet é extremamente simples:
- vá ao menu `Transact`
- há dois comandos principais: `Send` e `Receive` (**ignore `Buy`**).

![img](assets/17.webp)

Quando você tiver transações, elas aparecerão abaixo dos comandos. Como ainda não há fundos, selecione `Receive` para começar a receber.

Aparece uma série de *Assets*, mas foque apenas em Bitcoin. Você pode escolher entre Bitcoin onchain (ícone laranja) e Liquid (ícone azul), que permitirá pagamentos instantâneos, como com Lightning Network, mas por um mecanismo que veremos depois.

Para começar, escolha Bitcoin Onchain, o ícone laranja.

![img](assets/18.webp)

Aparece um QR code que representa um dos seus endereços Bitcoin, também visível abaixo com `bc1q` seguido de outros caracteres. Você pode mostrar o QR code a uma pessoa que precisa pagar você, para receber seus primeiros fundos, pequenas frações razoáveis de Bitcoin, também chamadas `Satoshi`.

![img](assets/19.webp)

Se voltar e escolher Liquid, o menu sinaliza ⚡️**Lightning Ready**. Saiba que, usando um serviço de `SWAP`, Blockstream App permitirá receber pagamentos quase instantâneos, emitir pedidos de pagamento Lightning Network ou pagar faturas LN, depositando/retirando fundos de uma conta Liquid da mesma wallet.

![img](assets/20.webp)

No menu que se abre depois dessa escolha, selecione como deseja receber fundos, entre Liquid e Lightning. Se escolher Liquid, será mostrado um QR code semelhante ao de Bitcoin Onchain, representando um endereço reconhecível pelo prefixo `lq1q` seguido de outros caracteres.

Se escolher Lightning, será solicitado inserir o valor que deseja receber e confirmar clicando em `Confirm`.

![img](assets/21.webp)

Blockstream App mostra um QR code que representa a fatura LN, pagável com qualquer wallet Lightning Network.

![img](assets/22.webp)

---
⚠️ Na nossa simulação, pedimos para receber 210 sats, mas o QR code resultante avisa que receberemos 160 sats. Swaps têm de fato um custo, cerca de 50 satoshis para cada pagamento recebido. **É importante manter esse aspecto em mente, especialmente ao receber micropagamentos**. Nada muda para quem paga: o pagador verá descontado o valor solicitado na configuração, 210 satoshis.

---

# Você é comerciante? Use o POS
Para tornar este guia um verdadeiro **starter kit**, podemos combinar recebimentos Bitcoin nesta wallet usando um POS externo.

Você pode configurá-lo em poucos passos diretamente em https://btcpos.cash/.

![img](assets/23.webp)

Assim você pode receber pagamentos Lightning diretamente na wallet criada no Blockstream App, compartilhar o link com colaboradores e, para isso, basta seguir os próximos passos e criar um link para manter à mão na tela inicial do telefone. Você precisa copiar o `Descriptor` da wallet e colá-lo no grande espaço central do site.

# 1. Receber os primeiros fundos na rede Liquid
É necessário habilitar a exibição de *Assets* na tela inicial da wallet. Se ela acabou de ser criada, você precisa receber uma fatura LN ou fundos em um endereço Liquid.

Depois de receber fundos, selecione Liquid entre os `Assets` vistos no menu `Home`.

![img](assets/24.webp)

# 2. Acessar os parâmetros necessários
Agora você tem o necessário para acessar os parâmetros que permitirão “transportar” sua wallet para o POS. Tecnicamente, isso se chama *exportação da chave pública* e é um detalhe que você aprenderá estudando. Por enquanto, basta selecionar o menu no canto superior direito:

![img](assets/25.webp)

E escolher `Watch-only` no menu suspenso.
![img](assets/26.webp)

Aparece `Output Descriptors`, exatamente o parâmetro que procuramos. Copie-o com o comando apropriado e volte à página web onde está configurando o POS.

![img](assets/27.webp)

# 3. Configurar o POS
Cole o descriptor no espaço apropriado e clique em `GENERATE POS LINK`. O sistema criará uma URL única, válida apenas para você e sua wallet.

![img](assets/28.webp)

Você também pode definir antes a moeda de referência, escolhendo entre USD, CHF e EUR no menu suspenso onde aparece `Currency`.
![img](assets/29.webp)

# 4. Receber gerando pedidos de pagamento com o POS
Depois de clicar em `GENERATE POS LINK`, a página mostra o resultado: **o link foi criado com sucesso**. Você pode copiá-lo, porque ele permanecerá sempre acessível **somente para sua wallet** na URL gerada.

![img](assets/30.webp)

Você também pode abrir o POS e começar a usá-lo:
![img](assets/31.webp)

Suponha, por exemplo, que você queira gerar uma fatura de 3.351 sats associando uma descrição.

![img](assets/32.webp)

Ao clicar em `CREATE INVOICE`, o POS mostra o QR code ou a fatura textual a apresentar a um possível cliente.

![img](assets/33.webp)

Quando o cliente paga a fatura, na qual lerá corretamente a *description* (Coppa del Nonno neste caso), o POS sinaliza o pagamento recebido.

![img](assets/34.webp)

O que também é lido corretamente na wallet.
![img](assets/35.webp)

Agora basta memorizar e manter o link do POS à mão, para usá-lo quando necessário, inclusive no telefone onde instalou a wallet.

![img](assets/36.webp)

Adicionando-o como link/app na tela inicial

![img](assets/37.webp)

# ⚠️ NOTA IMPORTANTE
Se você reler os passos recém-concluídos sobre o recebimento da fatura neste último exemplo, notará duas coisas importantes:
1. o cliente viu uma fatura de 3.351 sats
2. nossa wallet recebeu 3.293 sats.

Antes de se escandalizar, é necessário voltar à tela inicial do POS, que mostra o texto da imagem abaixo:

![img](assets/38.webp)

A diferença entre 3.351 (fatura enviada ao cliente) e 3.293 (seu recebimento) está exatamente nestes termos:
- 50 sats por cada fatura gerada
- 0,25% como taxa de serviço (8 sats = 0,25% de 3.351)
- Total recebido: 3.293

#### Você está apenas começando e este é um starter kit. Uma pequena taxa é o compromisso para usar Bitcoin em self-custody, sem intermediários, e aproveitar todas as oportunidades, incluindo pequenos pagamentos instantâneos.

#### Com estudo você aprenderá a usar outras ferramentas, que não exigirão outras taxas além das também esperadas para usuários experientes.

---
# Outras configurações

É hora de conhecer bem sua primeira wallet. As configurações são importantes porque ajudarão no uso diário.

## Menu
Os menus do Blockstream App ficam na parte inferior e são:
- Home
- Transact
- Security
- Settings

Continue configurando sua wallet pelo menu `Security`. Além de permitir ver e transcrever as palavras da `Recovery phrase`, este menu oferece outros recursos importantes.

Você pode configurar, por exemplo, login com controle biométrico (se configurado no telefone) ou adicionar um PIN de seis dígitos para acessar a wallet. Essas opções são muito importantes, porque impedem estranhos de acessar e ver sua wallet caso tenham seu telefone em mãos.

![img](assets/14.webp)

Neste menu você também pode decidir o tempo de *Logout*, isto é, quando a wallet se desconecta após alguns minutos de inatividade. Por padrão está em *5 minutes* e você pode variar esse tempo conforme suas necessidades, mais longo ou mais curto.
![img](assets/15.webp)
# Menu SETTINGS
Menu muito importante porque contém todas as configurações da wallet. Clicando nele você pode, por exemplo, renomear a wallet: no nosso exemplo a chamamos *Starter Kit*. Renomear wallets para distingui-las é muito importante quando se usa mais de uma no mesmo dispositivo.

![img](assets/39.webp)

Se você for ao submenu `Denomination`, encontrará configurações muito úteis sobre moeda.
![img](assets/40.webp)

Recomendo usar `satoshi/sats` como unidade para valores em Bitcoin. O Satoshi é a menor unidade de BTC, igual a um centésimo de milionésimo de Bitcoin. Também aparecerá a escolha da exchange de referência para conversão. Use uma que permita visualizar e definir valores em EUR.

![img](assets/41.webp)

Por fim, no menu `Settings` você pode verificar a versão atual do Blockstream App, ver se precisa de atualização e encontrar comandos para solicitar suporte diretamente *in-app*.
![img](assets/42.webp)

# Menu HOME
O `Home` do Blockstream App é o menu onde sua wallet abre a cada novo acesso. Rolando para baixo, você encontrará a opção de comprar Bitcoin por uma exchange integrada. **Não use**.

![img](assets/16.webp)

# Restauração da wallet
Se durante o uso você perceber que precisa trocar de telefone, ou usar a wallet *Starter Kit* em mais de um dispositivo, com Blockstream App você pode fazer isso.

Para prosseguir, basta aprender o procedimento de restauração da wallet, explicado abaixo, incluindo os passos para o caso de perder acesso ao telefone onde começou a usá-la.

Seus fundos, na verdade, não estão “no dispositivo” nem “na wallet”. Os fundos estão na rede Bitcoin, seja Onchain, Lightning ou Liquid. A wallet, mais precisamente as chaves públicas e privadas da sua wallet, é a ferramenta para acessar os endereços usados e o saldo associado.

É para esse procedimento que você transcreveu as 12 palavras e as colocou em lugar seguro... **Você fez isso, certo?** Porque sem essas palavras não terá mais acesso aos fundos.

# a. Nova instalação do Blockstream App
Primeiro, instale Blockstream App novamente com o procedimento mostrado no início. Uma nova release pode ter chegado nesse meio-tempo; use a mais atualizada.

Abra Blockstream App no novo dispositivo e prossiga clicando em `Get Started` e recusando a coleta de dados.

# b. Restaurar a partir de backup
As semelhanças com a primeira instalação param aqui. Quando chegar à tela de criação da wallet, em vez de escolher `Set Up Mobile Wallet` como da primeira vez, escolha `Restore from backup`.

![img](assets/43.webp)

Se estiver usando a rede principal de Bitcoin, isto é, a que usa fundos reais, na próxima tela escolha `Mainnet`.

![img](assets/43.webp)

Aparece a tela com os campos para inserir as palavras da `Recovery phrase`. Reescreva-as em ordem e corretamente, depois selecione `Continue` para recriar a wallet no novo dispositivo.

![img](assets/45.webp)

A fase de restauração da wallet pode levar alguns minutos; espere pacientemente até que termine com sucesso. Ao final, você encontrará sua wallet novamente, com saldo e histórico de transações.

![img](assets/46.webp)

---
⚠️ A wallet recriada no novo dispositivo está 100% ativa. Isso significa que também tem as chaves privadas para gastar. Lembre-se disso caso queira deixá-la com algum colaborador do seu negócio.

**Prefira usar o link do POS para colaboradores, porque ele foi criado apenas com a chave pública (o `descriptor`)**.

---

# Como continuar aprendendo?

![img](assets/47.webp)
![img](assets/48.webp)
