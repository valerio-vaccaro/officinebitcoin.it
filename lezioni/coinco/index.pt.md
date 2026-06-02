---
layout: default
name: "Compreender o Coin Control manual"
description: "Guia completo para a seleção manual de UTXO. Entenda por que ela é importante e aprenda a fazê-la com várias software wallets (desktop e mobile)"
title: "Compreender o Coin Control manual"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/coinco/cover.webp)

# Compreender o Coin Control manual

## Introdução

A robustez do protocolo Bitcoin é garantida por conceitos básicos simples. Entre eles, a transparência se destaca: todas as transações de Bitcoin são públicas e facilmente verificáveis por qualquer pessoa. Embora esse recurso seja uma pedra fundamental do protocolo, pois evita fraudes e garante a autenticidade dos fundos, ele também pode representar um desafio para a confidencialidade. **Você já se perguntou se tanta transparência pode afetar a sua privacidade?**

Você deveria. Embora acumular satoshis non-KYC seja bastante simples, sua privacidade corre mais risco na fase de gasto.

## O que acontece quando você gasta um UTXO
Gastar Bitcoin não é simplesmente transferir valor para outra pessoa.

Ao consumir um dos seus UTXOs, você precisa satisfazer as condições impostas pela transparência do protocolo, porque precisa provar a propriedade desses fundos. Portanto, você deve:
- expor sua chave pública;
- produzir uma assinatura digital.

O momento do gasto é, portanto, o mais crítico: **gastar bitcoin é um ato que deve ser feito com consciência e com o máximo de controle possível**.

## Coin Control
No protocolo Bitcoin, elementos como "conta" ou "unidade monetária" não existem. O conceito de UTXO não é o foco desta lição, mas convido você a fazer perguntas ao seu Satoshi Spritz de confiança ou a solicitar uma lição aqui na Officine Bitcoin.
O que você precisa saber é que, com Bitcoin, aquilo que você acumula e depois gasta são pequenas ou grandes unidades contábeis medidas em satoshis, representadas por `unspent transaction outputs`, os **UTXOs**, também chamados de `coins`.
Quando você usa UTXOs para criar uma transação, eles são completamente destruídos e novos UTXOs são criados em seu lugar.

As software wallets são desenvolvidas para fazer essa escolha automaticamente, usando coins selecionadas "aleatoriamente" com o único critério de cobrir o valor de gasto necessário.

`Coin Control`, também chamado de `Coin Selection`, é um recurso de algumas software wallets que permite **selecionar manualmente os UTXOs a gastar ao construir sua transação**.

Suponha que você tenha uma wallet com 3 UTXOs, respectivamente de 21,000, 42,000 e 63,000 satoshis.

![img](https://officinebitcoin.it/lezioni/coinco/01.webp)

Se você precisa gastar 24,000 sats e deixa o software selecionar automaticamente, uma boa wallet poderia escolher combinar UTXO1 + UTXO2 para pagar os 24k sats e as taxas de mineração, criando um troco que retorna para um endereço interno da wallet de origem.

![img](https://officinebitcoin.it/lezioni/coinco/02.webp)

Depois da transação, a nova situação na wallet, contando apenas os UTXOs, pode ser resumida da seguinte forma.

![img](https://officinebitcoin.it/lezioni/coinco/03.webp)

Com o software certo e sua própria consciência, porém, você poderia ter feito uma escolha diferente e mais correta. Por exemplo, selecionando apenas UTXO2 (42,000 sats).

![img](https://officinebitcoin.it/lezioni/coinco/04.webp)

Com uma situação final de UTXOs na sua wallet que parece diferente.

![img](https://officinebitcoin.it/lezioni/coinco/05.webp)

## Por que selecionar UTXOs manualmente?
![img](https://officinebitcoin.it/lezioni/coinco/06.webp)

No nosso exemplo, o saldo é na verdade o mesmo: `108,280 sats`. Depois de gastar 24,000 sats, sem coin control teríamos 2 UTXOs na wallet; com coin control manual temos 3 no total.

**Por que fazer tudo isso?**

Há, ou poderia haver, várias razões pelas quais não usamos `UTXO1` **e todas estão na raiz do motivo pelo qual - ao gastar - ativar o coin control manual é uma boa prática a seguir**.

## Privacidade
A principal vantagem, quando falamos de seleção manual de coins, é **maior privacidade para quem gasta**.

Vamos retomar nosso exemplo: gastar 24,000 satoshis _sem coin control_. Como a blockchain do Bitcoin é um registro público, um observador externo pode afirmar, sem dúvida, que os inputs `UTXO1 of 21,000 sats` e `UTXO2 of 42,000 sats`, assim como o troco, `UTXO5 of 38,280 sats`, **pertencem todos ao mesmo usuário**.

Ao selecionar manualmente `UTXO2`, por outro lado, `UTXO1` permanece completamente privado, parado no UTXO set esperando para ser gasto em um momento mais apropriado.

`UTXO1` poderia vir de uma fonte KYC, por exemplo um pagamento recebido por bens e serviços, enquanto os outros UTXOs não.

**Se fosse a sua wallet, você gostaria que um observador externo pudesse rastrear sua identidade com tanta certeza?** Wallets que implementam seleção manual de UTXO permitem, por exemplo, a **segregação de um ou mais UTXOs**, uma função a usar quando essas situações surgem.

Embora eu acredite que fundos KYC devam ser mantidos em uma wallet separada dos bitcoin non-KYC, se esse for o seu caso, segregar alguns dos seus endereços é uma ajuda fundamental, que você pode obter aprendendo a selecionar manualmente seus inputs de gasto.

## Economia de taxas
Selecionar o UTXO correto para um gasto permite otimizar as taxas. Mais uma vez, no nosso exemplo, a software wallet selecionou dois UTXOs para cobrir o gasto. Dois UTXOs significam duas assinaturas a mostrar à rede, portanto um peso de transação maior em termos de vBytes.

Usando coin control manual, você pode selecionar apenas um que seja suficiente para cobrir o valor, economizando taxas porque o "peso" da transação diminui.

Quando as taxas estão altas, mas você é obrigado a gastar bitcoin on-chain (por exemplo, para abrir um canal de Lightning Network), o coin control se torna o incentivo econômico correto para usar.

## Agregação do troco
Ao fazer um pagamento e usar Bitcoin on-chain, a possibilidade de receber troco quase sempre se torna uma certeza. Cada troco é por si só uma pequena perda de privacidade, pois revela à rede um dos seus endereços que pode ser associado ao seu input original.

Considerando que as melhores HD wallets geram endereços especiais para troco, você pode reconhecê-los facilmente e "segregar" todo o troco de várias transações; quando ele atingir uma certa quantia, você pode selecioná-lo e consolidá-lo manualmente, ou trocá-lo na Lightning Network (meu método favorito) para recuperar a privacidade perdida durante o gasto.

## Gastar a partir de uma cold wallet
Uma cold wallet é uma ferramenta com a qual você pode alcançar razoavelmente um bom grau de segurança, para armazenar qualquer quantia de fundos a manter separada por muito tempo. No entanto, imprevistos podem ocorrer, exigindo que você acesse suas economias e cubra despesas inesperadas.

Meu conselho é **nunca gastar diretamente da cold wallet, para evitar receber troco entre os endereços da mesma wallet**. Aprenda a selecionar manualmente os UTXOs necessários para cobrir a despesa, transfira-os para uma hot wallet e prepare sua transação a partir daí. Qualquer troco, então, você pode enviar de volta para um endereço de cold wallet (se o valor for apropriado), ou usá-lo para outros fins.

## Demonstração prática
Depois desta longa introdução, vejamos como colocar coin control em prática com vários softwares desktop e mobile. Usaremos sempre a mesma HD wallet, importada em cada uma das ferramentas escolhidas, para mostrar as pequenas diferenças entre elas.

## Desktop Wallets

## Sparrow
Se você usa Sparrow, abra sua wallet e selecione _UTXOs_ no menu à esquerda. Você verá a lista de todos os UTXOs associados à sua wallet.

Basta clicar em um deles e depois escolher _Send Selected_. Sparrow também mostra o total selecionado para gasto, ao lado do comando.

![img](https://officinebitcoin.it/lezioni/coinco/07.webp)

Você também pode selecionar mais de um. Use a tecla _CTRL_ para selecionar UTXOs não adjacentes na lista.

![img](https://officinebitcoin.it/lezioni/coinco/08.webp)

Depois de selecionar manualmente os UTXOs, Sparrow mostrará claramente, de forma gráfica, como sua transação é construída, para que você possa finalizá-la e concluí-la.

![img](https://officinebitcoin.it/lezioni/coinco/09.webp)

### Segregação de UTXO
Segregar fundos significa "bloqueá-los" dentro da wallet para que não possam ser usados como inputs de transação.

Sparrow permite esse recurso, acessível no menu _UTXOs_. Passe o cursor sobre o UTXO a "bloquear" e clique com o botão direito. Entre as opções, você encontrará _Freeze_. É assim que você pode segregar um UTXO com Sparrow Wallet.

![img](https://officinebitcoin.it/lezioni/coinco/29.webp)

## Electrum
Se sua desktop wallet é Electrum, você pode selecionar manualmente UTXOs tanto nos menus _Addresses_ quanto _Coins_.
Em ambos os menus, a seleção é feita apontando o mouse para o UTXO e escolhendo _Add to coin control_ depois de clicar com o botão direito.

![img](https://officinebitcoin.it/lezioni/coinco/10.webp)

Você também pode selecionar mais de um UTXO, usando a tecla _CTRL_ se eles não forem adjacentes.

![img](https://officinebitcoin.it/lezioni/coinco/11.webp)

Electrum destacará graficamente os UTXOs selecionados em verde e, na parte inferior, uma barra destacada na mesma cor mostra o saldo disponível após o coin control.

![img](https://officinebitcoin.it/lezioni/coinco/12.webp)

Depois que os output(s) forem selecionados, você pode construir sua transação como de costume no menu _Send_.

### Segregação de UTXO
Electrum oferece essa opção no menu _Coins_, selecionando um UTXO específico e depois escolhendo _Freeze_ com o botão direito do mouse. Você também pode "congelar" um endereço sem fundos no menu _Addresses_, ou a "coin", para impedir o gasto.

![img](https://officinebitcoin.it/lezioni/coinco/28.webp)

## Nunchuk
Nunchuk permite selecionar UTXOs no menu principal depois de aberto.
Inicie o Nunchuk e clique em _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/13.webp)

Uma janela se abre com todos os UTXOs da sua wallet, onde você pode selecionar um ou mais marcando a caixa ao lado de cada valor. Depois da seleção, continue com _Create transaction_.

![img](https://officinebitcoin.it/lezioni/coinco/14.webp)

Então você pode inserir o endereço de destino, definir o valor e as taxas.

![img](https://officinebitcoin.it/lezioni/coinco/15.webp)

## Blockstream App
Blockstream App desktop, anteriormente conhecida como Green, permite a seleção de coins depois que você começou a construir a transação. Abra sua wallet e clique em _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/16.webp)

Cole o endereço de destino no campo apropriado e então selecione _Manual coin selection_.
![img](https://officinebitcoin.it/lezioni/coinco/17.webp)
Uma janela se abre onde você pode selecionar um ou mais UTXOs. No exemplo a seguir, selecionamos duas coins. Então confirme a escolha clicando em _Confirm Coin Selection_.

![img](https://officinebitcoin.it/lezioni/coinco/18.webp)

Defina o valor e as taxas, então prossiga como de costume com sua transação.

![img](https://officinebitcoin.it/lezioni/coinco/19.webp)

⚠️ Nota: No menu _Coins_ do Green, existem opções _Lock_/_Unlock_ que sugerem a possibilidade de segregar UTXOs. Isso está disponível apenas nas chamadas contas multisig; o recurso só é ativado para UTXOs muito pequenos, próximos ao limite `Dust`.

## Mobile Wallets

## Blue Wallet
Mesmo no mobile, você pode escolher wallets que permitem seleção manual de UTXO. Vejamos primeiro a Blue Wallet.

Se você usa este software, abra sua wallet e clique para entrar nas telas de comando de uma das suas wallets. Para acessar coin control, você precisa entrar na fase de gasto, então clique em _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/21.webp)

Na tela seguinte, escolha o menu indicado pelos três pontos no canto superior direito. Uma janela suspensa com vários comandos se abre. Escolha o último: _Coin Control_.

![img](https://officinebitcoin.it/lezioni/coinco/22.webp)

Neste ponto, Blue Wallet mostra todos os seus UTXOs. Além dos valores, eles são diferenciados graficamente por cores diferentes.

![img](https://officinebitcoin.it/lezioni/coinco/27.webp)

Selecione o UTXO e então selecione _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/23.webp)

Blue Wallet leva você de volta à janela _Send_ para continuar construindo a transação. Ajuste o valor e as taxas, então escolha _Next_.

![img](https://officinebitcoin.it/lezioni/coinco/24.webp)

Agora você pode concluir a transação como de costume.

### Segregação de UTXO
Blue Wallet também permite segregar UTXOs, tornando-os indisponíveis para gasto, o que é um bom recurso para uma mobile wallet.

Acesse coin control como explicado acima e, depois de selecionar o UTXO, escolha _Freeze_ em vez de _Use Coin_.

![img](https://officinebitcoin.it/lezioni/coinco/26.webp)

## Nunchuk
A versão mobile do Nunchuk também permite que os usuários façam coin control. Se você usa este app no mobile, abra-o e vá ao menu _Wallet_. A partir daí, escolha _View coins_.

![img](https://officinebitcoin.it/lezioni/coinco/30.webp)

Na janela com a lista de UTXOs, clique em _Select_.

![img](https://officinebitcoin.it/lezioni/coinco/38.webp)

Ao lado de cada UTXO, aparece a função de seleção. Como na versão desktop, no Nunchuk mobile, a seleção manual é feita marcando a caixa ao lado do valor. A tela mostra o número de UTXOs selecionados e o valor total disponível. Ao terminar, o símbolo ₿ no canto inferior esquerdo é o comando para começar a construir a transação.

![img](https://officinebitcoin.it/lezioni/coinco/31.webp)

Agora você pode concluir a transação, escolhendo o valor e clicando em _Continue_.

![img](https://officinebitcoin.it/lezioni/coinco/32.webp)

Continue como de costume, colando um endereço de destino, uma descrição e personalizando as configurações de taxa.

## Bitcoin Keeper
Bitcoin Keeper é a última wallet que veremos neste guia. Vejamos seu recurso de coin control com uma wallet single-sig, embora esse uso não seja o objetivo principal deste app específico.

Depois de configurar Keeper no seu telefone, inicie-o e abra uma wallet contendo alguns UTXOs. No centro da tela principal, clique em _View All Coins_.

![img](https://officinebitcoin.it/lezioni/coinco/34.webp)

Keeper mostra uma visão geral dos UTXOs. Para acessar a tela de seleção, clique em _Select To Control_.

![img](https://officinebitcoin.it/lezioni/coinco/35.webp)

Você pode selecionar coins marcando-as, clicando no comando apropriado. Quando terminar, clique em _Send_.

![img](https://officinebitcoin.it/lezioni/coinco/36.webp)

Bitcoin Keeper leva você diretamente ao menu _Send_, onde você pode construir a transação com os UTXOs selecionados.

![img](https://officinebitcoin.it/lezioni/coinco/37.webp)

## Hardware wallet
Cada uma das software wallets vistas neste guia pode ser a interface watch-only da sua hardware wallet. Isso significa que o coin control para um dispositivo de assinatura offline é feito com os passos vistos até aqui.

## Recomendações gerais
Coin control é uma prática muito eficaz para selecionar seus inputs de transação. A seleção manual é ainda mais eficiente se, ao receber seus fundos, você tiver etiquetado bem a origem dos seus satoshis. Se quiser dominar essa técnica, recomendo o tutorial:

https://planb.network/tutorials/privacy/on-chain/utxo-labelling-d997f80f-8a96-45b5-8a4e-a3e1b7788c52
