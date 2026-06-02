---
layout: default
title: "Le cycle de vie d'une transaction Bitcoin"
---

<p class="site-kicker"><strong>Officine Bitcoin</strong> <span>Leçon Bitcoin-only</span> <span>Ce projet est maintenu par valerio-vaccaro</span></p>

## 🌍 Traduzioni

[🇨🇳 中文](./index.zh.html) [🇬🇧 English](./index.en.html) [🇪🇸 Español](./index.es.html) [🇵🇹 Português](./index.pt.html) [🇷🇺 Русский](./index.ru.html) [🇫🇷 Français](./index.fr.html) [🇩🇪 Deutsch](./index.de.html) [🇮🇹 Italiano](./index.html) [🇭🇺 Magyar](./index.hu.html) [🏳️ Milanés](./index.mi.html) [🏳️ Veneto](./index.ve.html)

# Le cycle de vie d'une transaction Bitcoin

## Qu'est-ce qu'une transaction Bitcoin
Une transaction Bitcoin est une action enregistrée sur la blockchain qui transfère de la valeur depuis une ou plusieurs entrées (des fonds reçus auparavant, appelés UTXOs - Unspent Transaction Outputs) vers une ou plusieurs sorties (de nouveaux destinataires).
Les entrées sont des sorties de transactions passées qui n'ont pas encore été dépensées, tandis que les sorties attribuent des satoshis à des adresses précises. La transaction "coinbase" fait exception: première transaction de chaque bloc, elle crée de nouveaux bitcoins (récompense de minage et frais) sans entrées. Si tous les fonds d'une entrée ne sont pas dépensés, la différence (change) revient à l'expéditeur par une sortie supplémentaire ou, si elle n'est pas gérée, elle est perdue pour toujours.

## Phases du cycle de vie
Voici le cycle de vie de la transaction:

- Création: Le wallet construit la transaction en choisissant quels UTXOs dépenser selon le montant à envoyer et la stratégie de minimisation des frais. Si l'entrée dépasse la sortie, une sortie de "change" est générée et renvoyée à l'expéditeur, mais cela augmente la taille et le coût de la transaction. Certains wallets essaient de l'éviter.
- Signature: La transaction est signée avec une ou plusieurs signatures numériques pour chaque entrée, ce qui l'authentifie. Cette étape est essentielle à sa validité et peut impliquer plusieurs parties dans le cas de transactions multisig.
- Diffusion: La transaction signée est transmise au réseau ("broadcast") et insérée dans le mempool du noeud local. Le mempool valide la transaction selon les règles de consensus (par exemple signatures valides, fonds disponibles) et les règles locales (par exemple taille maximale de 400 KB pour éviter le spam). Ensuite, le noeud la propage à ses pairs, qui la valident et l'insèrent dans leurs mempools, créant une diffusion en cascade. Les mempools varient d'un noeud à l'autre à cause de configurations ou de connexions différentes.
- Confirmation: Un mineur inclut la transaction dans un bloc, ce qui la confirme sur la blockchain. Cependant, tant qu'elle n'a pas davantage de confirmations (blocs suivants), elle reste vulnérable aux remplacements ou aux forks. Une transaction avec des frais faibles peut rester longtemps dans le mempool ou être rejetée, mais elle pourrait être minée même après des mois si les entrées restent non dépensées.

## Gestion des problèmes
- Transaction disparue du mempool: Si une transaction avec des frais faibles est supprimée (par exemple en raison de pics de trafic), elle peut être retransmise manuellement (rebroadcast) avec le TXID, même au moyen de scripts ou d'explorateurs. Quelqu'un peut le faire pour le compte de tiers.
- Replace-by-Fee (RBF): Si les frais sont insuffisants, la transaction peut être remplacée par une autre qui paie davantage, à condition qu'elle soit marquée avec le flag RBF. Une proposition suggère que toutes les transactions devraient être implicitement remplaçables, puisque les mineurs préfèrent de toute façon des frais plus élevés.
- Child Pays for Parent (CPFP): Si RBF ne peut pas être utilisé (par exemple parce qu'il ne s'agit pas de votre propre transaction ou parce que les fonds sont épuisés), une sortie de la transaction bloquée est dépensée avec une nouvelle transaction qui paie des frais élevés, rendant les deux attractives pour les mineurs. La somme des frais doit couvrir les deux. Des problèmes apparaissent si les noeuds abandonnent la première transaction, ce qui brise la chaîne; un protocole en développement vise à transmettre des paquets de transactions pour éviter cela.

## Confirmation finale
Une transaction n'est considérée comme finale qu'avec plusieurs confirmations (des blocs au-dessus d'elle). Une seule confirmation ne suffit pas, car des forks ou une double dépense pourraient l'invalider. Le White Paper suggère 6 confirmations (environ 60 minutes, avec des blocs toutes les 10 minutes en moyenne), mais ce nombre varie selon le montant et le risque. La variance des temps de bloc est élevée, mais la moyenne est maintenue grâce à la difficulté de minage.

## Conclusion
Le cycle se termine avec la transaction "gravée" dans la blockchain, enregistrant définitivement le transfert de valeur.

## Programme
Cette leçon a été créée pour un Satoshi Spritz Connect.
