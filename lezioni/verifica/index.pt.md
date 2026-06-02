---
layout: default
title: "Pré-requisitos para este tutorial"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Lição Bitcoin-only</span> <span>Este projeto é mantido por valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

![cover](https://officinebitcoin.it/lezioni/verifica/1cover.webp)
Verificar assinaturas criptográficas é uma prática de segurança fundamental que **todo usuário de software open-source deveria incluir em sua rotina de bons hábitos**.

O open source é por natureza modificável, o que significa que qualquer pessoa pode, em teoria, introduzir backdoors, ataques ou código malicioso nos aplicativos que você usa para praticar enquanto aprende o protocolo Bitcoin.

Como usuário que está aprofundando seu estudo, você tem a oportunidade de verificar pessoalmente se o software baixado foi adulterado, e deveria fazer isso antes de instalá-lo e usá-lo.

Antes de começarmos, também trazemos um clássico das apresentações para a Officine Bitcoin: o meme. Não será uma apresentação pesada, mas vamos descontrair o ambiente logo de início.

![meme](https://officinebitcoin.it/lezioni/verifica/2meme.webp)

## Como fazer?
Os desenvolvedores sempre lançam novas versões de software acompanhadas por uma assinatura criptográfica.
Isso significa que, além de terem atualizado o software, eles o lançam certificando que o vincularam a uma fingerprint específica. Lembrete: a assinatura digital produzida com a chave privada é única e não modificável.

Tudo de que você precisa é a suíte GPG para prosseguir com a verificação da assinatura.

![img](https://officinebitcoin.it/lezioni/verifica/3.webp)

# Pré-requisitos para este tutorial
- Uma breve revisão de criptografia assimétrica
- Os elementos a verificar:
  - software (binary, apk, etc.)
  - a assinatura digital do desenvolvedor, geralmente um arquivo `.asc`, `.sig` ou um checksum.
- As ferramentas para verificação:
  - suíte GPG
  - um terminal (funciona tanto em Linux quanto em Windows)
# Criptografia assimétrica

![img](https://officinebitcoin.it/lezioni/verifica/4.webp)

Aqui há duas chaves relacionadas entre si: uma chave pública e uma privada. Como os nomes sugerem:
- A chave pública fica livremente disponível e pode ser compartilhada com qualquer pessoa.
- A chave privada é mantida segura por seu proprietário.

Dados criptografados com a chave pública só podem ser descriptografados pela chave privada correspondente. Isso permite que qualquer pessoa envie dados criptografados ao proprietário do par de chaves, sem compartilhamento prévio da parte secreta.

A criptografia de chave pública é mais lenta que a criptografia simétrica e não é adequada para criptografar grandes quantidades de dados. No entanto, ela permite a distribuição segura de chaves de criptografia.
Alguns algoritmos comumente usados para criptografia de chave pública incluem RSA, ECC, ElGamal e DSA.

## Lado do desenvolvedor: nova atualização

O desenvolvedor lança o código open source, que por natureza não é criptografado.
Ele cria um hash criptográfico (que gera o `checksum`) e criptografa o digest com sua chave privada: isso cria a assinatura, aquele arquivo `.sig` ou `.asc` mencionado anteriormente.

Depois desse processo, o desenvolvedor envia ambos os arquivos ao site ou a um repositório GitHub. É aí que começa o seu download.

![img](https://officinebitcoin.it/lezioni/verifica/5.webp)

Em seguida, você precisará da chave pública do desenvolvedor. Às vezes ela está no repositório GitHub, às vezes em servidores públicos (*keyservers*). Mesmo que a busca possa exigir esforço, a chave pública é um elemento essencial para verificar o software, portanto faça o esforço de obtê-la.

Se tiver dificuldades, faça perguntas no grupo Telegram da Officine Bitcoin, onde você encontrará instruções para obter uma chave pública específica.

![img](https://officinebitcoin.it/lezioni/verifica/6.webp)

Para verificar a integridade dos dados, o destinatário descriptografa a assinatura usando a chave pública do remetente, obtendo um resultado:

a. os dados são considerados autênticos e não modificados durante o trânsito.
b. os dados foram potencialmente adulterados.

Ao criptografar o valor do hash com a chave privada, **as assinaturas PGP garantem que o checksum esteja protegido e vinculado à identidade do remetente. Isso impede a falsificação de assinaturas sobre dados alterados**.

Assinaturas podem ser usadas para verificar qualquer coisa: arquivos, emails, documentos e downloads de software. Ao verificar uma assinatura PGP, você prova que os dados realmente vêm de uma fonte confiável e estão intactos.

E é a verificação de um apk móvel que você poderá verificar agora.

Usamos como exemplo o download do Phoenix, um wallet LN non-custodial, para podermos abordá-lo especificamente em uma futura noite da Officine Bitcoin.

# Baixar e verificar Phoenix Wallet (Acinq)
Se você já esteve no site da [Acinq](https://phoenix.acinq.co/), desenvolvedora do Phoenix, já sabe que o download está disponível nas lojas oficiais para Android e iOS.
Talvez você nunca tenha reparado, mas para Android o arquivo apk também está disponível.

![img](https://officinebitcoin.it/lezioni/verifica/8.webp)

[Vamos até lá!](https://github.com/ACINQ/phoenix/releases) para encontrar os arquivos `apk` e `Signature` que você baixará com `wget`.
No caso do Phoenix, o arquivo que contém a assinatura para verificação se chama **`SHA256SUMS.ASC`**.

![img](https://officinebitcoin.it/lezioni/verifica/9.webp)

No mesmo repositório também há instruções para baixar a chave pública correspondente à *signing key E04E48E72C205463* (fingerprint única das chaves de Drouinf).
Copie o link e baixe-o com `wget`, ou siga as instruções sugeridas na seção apropriada do repo.

![img](https://officinebitcoin.it/lezioni/verifica/10.webp)

---
⚠️**A chave pública deve ser importada, não apenas baixada**.
⚠️ Os downloads dos arquivos devem ocorrer no mesmo diretório.

---
# Abra o terminal
Com o terminal, navegue até o diretório onde o apk e o arquivo `SHA256SUMS.ASC` foram baixados e execute os comandos na ordem.

![img](https://officinebitcoin.it/lezioni/verifica/11.webp)

![img](https://officinebitcoin.it/lezioni/verifica/12.webp)

Quando a verificação retorna um resultado positivo, você pode transferir o apk para o seu telefone e instalar o app.

---
# Verificação difícil
Pode haver vários motivos pelos quais a verificação de assinatura não é fácil, e eles quase sempre se devem à desorganização ou à inexperiência:
1. os arquivos apk e/ou .asc foram baixados várias vezes, então no diretório aparecem com, por exemplo, nomes estranhos como **filename-1** ou **filename(1)**
2. apk e .asc não estão no mesmo diretório
3. a chave pública foi baixada, mas não importada para o keyring do gpg.

Outras situações podem ocorrer em que, mesmo operando corretamente, a verificação falha.
É importante verificar o erro que aparece no terminal, copiá-lo e iniciar uma busca na internet pela solução.

# Verificação com Sparrow Wallet
Se você já usa Sparrow Wallet, pode prosseguir para verificar downloads com este software, **cujo download e instalação devem ser precedidos por uma verificação cuidadosa e rigorosa com GPG**.

Inicie o Sparrow wallet e procure no menu `Tools` -> `Verify Downloads`.

![img](https://officinebitcoin.it/lezioni/verifica/13.webp)

Uma interface se abre pedindo que você insira os arquivos recém-baixados. Ao clicar em `Browse`, o gerenciador de arquivos se abre para carregar cada arquivo no campo requerido.

![img](https://officinebitcoin.it/lezioni/verifica/14.webp)

Às vezes o formulário da interface se preenche sozinho. Se isso não acontecer, preencha todos os campos com os arquivos apropriados.

![img](https://officinebitcoin.it/lezioni/verifica/15.webp)

O resultado positivo é mostrado graficamente por marcas verdes e pela confirmação *`Ready to install`* + < filename >.

# Apoio ao estudo
Se você participou da apresentação ao vivo no Telegram, pode considerá-la mais um passo rumo à sua soberania pessoal (não apenas financeira).
Se você perdeu, **não se desespere**: estas notas servem justamente para recuperar o conteúdo e, além disso, saiba que vamos propô-la novamente na Officine.

Para não perder a próxima apresentação, entre no [grupo Telegram](https://t.me/officinebitcoin) para se manter constantemente atualizado.

![img](https://officinebitcoin.it/lezioni/verifica/17.webp)

Você também pode encontrar o [Satoshi Spritz](https://satoshispritz.it/) mais próximo de você. Um Satoshi Spritz é um meetup local onde se fala apenas de Bitcoin, onde você pode levar suas perguntas e obter respostas de outros bitcoiners experientes. No link você encontrará o mapa da península.

![img](https://officinebitcoin.it/lezioni/verifica/16.webp)

Por fim, se você não encontrar um meetup perto de você, pode aproveitar as lives semanais do [SatoshiSpritz Connect](https://t.me/SatoshiSpritzConnect), um meetup virtual criado para quem não pode participar do Satoshi Spritz, ou para ajudar meetups menores a tomar notas e encontrar inspiração para suas próprias apresentações.

![img](https://officinebitcoin.it/lezioni/verifica/18.webp)
