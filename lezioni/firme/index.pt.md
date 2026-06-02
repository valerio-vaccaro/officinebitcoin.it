---
layout: default
title: "Assinaturas digitais"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Assinaturas digitais
O tema desta aula será assinaturas digitais e como elas se aplicam ao Bitcoin.

## O que é uma assinatura?
Precisamos entender o que queremos dizer com assinatura digital. Quando pensamos em uma assinatura normal, geralmente pensamos em outra coisa: como estamos falando de documentos digitais, a assinatura digital liga tanto a identidade do autor quanto o estado do documento assinado; portanto, essencialmente, a assinatura também depende do documento que vamos assinar.

Essa é uma diferença muito grande em relação ao mundo físico, onde colocamos a assinatura praticamente sem nos preocuparmos com o suporte no qual a fazemos. É claro que talvez não assinemos cheques ou outros documentos sem nos preocupar com isso, mas, essencialmente, a assinatura que vamos apor não varia.

Assinaturas digitais são algo um pouco diferente; normalmente elas se baseiam em algoritmos de chave pública e chave privada. Isso significa que, em algum lugar do mundo, nosso wallet possui um par de chaves, pública e privada, e nossa (pseudo-)identidade está ligada à chave pública que todos conhecem ou que tornaremos conhecida por todos.

Usaremos nossa chave privada, que é um número, e com certa mágica matemática produziremos uma assinatura que é outro número diferente e que prova que um certo estado de um certo documento pertence a, ou é conhecido por, uma certa identidade conectada a uma chave pública. O que vou assinar é a impressão digital (ou HASH) de um determinado documento (ou PAYLOAD).

Também preciso de algum gerador de números aleatórios; jogo todos esses dados em uma "caixa preta" que produz uma assinatura para mim. Assim, a assinatura é algo que prova posse porque estou assinando com meu segredo, mas também prova que aquilo que estou assinando não foi modificado.

Se eu modificar o PAYLOAD, modifico o HASH e obviamente isso invalida a assinatura.

Então, essencialmente, por que essa assinatura mais complexa foi introduzida no mundo digital? Bem, porque no mundo digital, ao contrário do físico (e talvez quem faltou à escola se lembre), copiar uma assinatura é muito mais simples.

A assinatura digital, por outro lado, contém informações sobre o documento e por isso muda para cada documento; ela não pode ser colada e reutilizada em um documento diferente.

A assinatura digital, portanto, serve para:
- provar que criei uma determinada mensagem, estou solicitando uma determinada ação ou estou declarando um determinado estado de um sistema, e
- provar que aquela mensagem, aquele documento ou aquela cadeia de dados não foi manipulada, isto é, que ela é de fato aquilo que eu queria assinar.
- tornar uma determinada ação não repudiável; se eu produzi uma assinatura, fui realmente eu que fiz isso para aquele documento específico.

## Assinaturas no Bitcoin
Essa tecnologia é usada no Bitcoin sob a sigla ECDSA (Elliptic Curve Digital Signature Algorithm), que é um algoritmo para produzir assinaturas digitais em curvas elípticas; por enquanto não trataremos de outros esquemas de assinatura.

Lembre-se de que no Bitcoin é possível produzir assinaturas para:
- texto arbitrário, pouco importante e pouco usado
- novas transações, com o objetivo de autorizar o gasto de um determinado UTXO

Mas como essas assinaturas se vinculam à transação? Cada endereço tem um mecanismo de gasto, scripts que devem ser executados para saber se um gasto pode ser autorizado. Dentro desses scripts há comandos (ou OPCODES) destinados à verificação de assinaturas digitais, como OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Lembre-se de que uma transação Bitcoin é composta por:
- Inputs, isto é, os fundos que vou gastar e para os quais devo produzir um script de gasto
- Outputs, isto é, os novos endereços para onde os fundos irão (e para cada endereço está conectado um modo de gasto bem definido.

Essencialmente, na maioria dos casos terei de produzir PARA CADA INPUT a(s) assinatura(s) necessária(s) para completar o script de gasto.

Lembre-se de que essa ação nos permite provar que aquele input é nosso e que queremos gastá-lo (queremos transferir a propriedade integralmente, dividi-la ou juntá-la com outros inputs).

Obviamente, a transação é válida se todos os inputs estiverem corretamente assinados; se até mesmo um dos inputs não estiver assinado, aquela transação não pode ser considerada válida.

A assinatura é verificável por todos e é não repudiável, mas, por flexibilidade, Satoshi introduziu de forma muito inteligente vários modos de assinatura: a assinatura é sempre a mesma, mas o PAYLOAD muda, isto é, a porção da transação que é objeto da assinatura. Isso permite, por exemplo, a geração de esquemas e protocolos complexos nos quais pedaços de transações podem ser combinados entre si; Satoshi chamou esses modos (verdadeiras flags na linguagem de scripting) de SIGHASH.

## SIGHASH
O SIGHASH mais simples é SIGHASH_ALL, que significa gerar uma assinatura com TODOS OS INPUTS e TODOS OS OUTPUTS; esse é o modo mais simples e mais usado para fazer uma assinatura.

Uma primeira diferença pode ocorrer com SIGHASH_NONE, que assina TODOS OS INPUTS, mas NENHUM dos OUTPUTS, permitindo que outputs sejam adicionados ou que fees sejam modificadas depois. ATENÇÃO: com esse esquema, se não estiver protegido por multisig ou por outros recursos, um miner ou qualquer pessoa que veja uma transação com esse esquema de assinatura pode substituir os outputs redirecionando os fundos para seu próprio endereço.

Uma flag mais interessante é SIGHASH_SINGLE, na qual um par de input e output é assinado desde que estejam inseridos em uma transação no mesmo nível (por exemplo, quinto input e quinto output); isso permitiria compor transações maiores com base nesses pares, mas não dá a possibilidade de introduzir troco, isto é, exige o gasto total do input.

Em paralelo, todos esses SIGHASH podem ser combinados com a flag ANYONECANPAY, que limita a assinatura apenas ao input para o qual a assinatura está sendo produzida, dando assim a qualquer pessoa a possibilidade de adicionar inputs à transação.

Todas essas assinaturas são assinaturas válidas independentemente do tipo de endereço e dos scripts, deixando a máxima flexibilidade de expressão ao wallet, que normalmente usará SIGHASH_ALL, mas também poderia seguir protocolos mais complexos que exigem esquemas de assinatura diferentes. No caso de multisig, então, não há necessidade de usar o mesmo tipo de assinatura; um wallet 2-of-2 poderia assinar alguns de seus UTXO com SIGHASH_NONE e ANYONECANPAY para dar controle total ao segundo assinante, que poderia, por exemplo, reunir todos esses inputs em uma transação a ser assinada com SIGHASH_ALL.

## Assinaturas em texto arbitrário
Para completar, as mesmas assinaturas usadas para inputs de transações também podem ser usadas para assinar texto arbitrário.

O Bitcoin propõe um esquema em que texto é acrescentado para impedir que essa funcionalidade seja usada para assinar partes de transações; portanto, se você tem Bitcoin Core ou até alguns wallets, pode procurar uma funcionalidade de assinatura de mensagens de texto baseada em um determinado endereço seu.

O wallet usará a chave privada associada à chave pública que gerou aquele endereço para fazer assinaturas de mensagens de texto.

No momento da verificação, obtém-se a chave pública, que pode então ser usada para regenerar o endereço; assim, se eu tenho o texto e a assinatura, extraio a chave pública que o assinou e, a partir da chave pública, posso recalcular o endereço e verificá-lo, por exemplo, com o endereço fornecido.

## Programa
A aula sobre assinaturas pode ser repetida; aqui está uma lista das que já foram realizadas:

| Data        | Notas                                          |
|-------------|------------------------------------------------|
|||
