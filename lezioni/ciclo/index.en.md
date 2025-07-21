# The Bitcoin Transaction Lifecycle

## What is a Bitcoin Transaction
A Bitcoin transaction is an action recorded on the blockchain that transfers value from one or more inputs (previously received funds, called UTXOs - Unspent Transaction Outputs) to one or more outputs (new recipients). 
Inputs are outputs from past transactions that have not yet been spent, while outputs assign satoshis to specific addresses. An exception is the "coinbase" transaction, the first of each block, which generates new bitcoins (mining reward and fees) without inputs. If not all funds from an input are spent, the difference (change) returns to the sender through an additional output or, if not managed, is lost forever.

## Lifecycle Phases
This is the transaction lifecycle:

- Creation: The wallet builds the transaction by choosing which UTXOs to spend based on the amount to send and the strategy to minimize fees. If the input exceeds the output, a "change" output is generated that returns to the sender, but this increases the transaction size and costs. Some wallets try to avoid this.
- Signing: The transaction is signed with one or more digital signatures for each input, authenticating it. This step is crucial for validity and may involve multiple parties in case of multisig transactions.
- Broadcasting: The signed transaction is transmitted to the network ("broadcast") and inserted into the local node's mempool. The mempool validates the transaction according to consensus rules (e.g., valid signatures, available funds) and local rules (e.g., maximum size of 400 KB to prevent spam). Then, the node propagates it to peers, who validate it and insert it into their mempools, creating a cascading broadcast. Mempools vary between nodes due to different configurations or connections.
- Confirmation: A miner includes the transaction in a block, confirming it on the blockchain. However, until it has more confirmations (subsequent blocks), it remains vulnerable to replacements or forks. A transaction with low fees may remain in the mempool for a long time or be discarded, but could be mined even after months if the inputs remain unspent.

## Problem Management
- Transaction disappeared from mempool: If a transaction with low fees is removed (e.g., due to traffic spikes), it can be manually retransmitted (rebroadcast) using the TXID, even with scripts or explorers. Someone might do this on behalf of third parties.
- Replace-by-Fee (RBF): If the fee is insufficient, the transaction can be replaced with one that pays more, provided it's marked with the RBF flag. A proposal suggests that all transactions should be implicitly replaceable, since miners prefer higher fees anyway.
- Child Pays for Parent (CPFP): If RBF cannot be used (e.g., not your own transaction or exhausted funds), an output from the stuck transaction is spent with a new transaction that pays high fees, making both attractive to miners. The sum of fees must cover both. Problems arise if nodes discard the first transaction, breaking the chain; a protocol in development aims to transmit transaction packages to avoid this.

## Final Confirmation
A transaction is considered final only with multiple confirmations (blocks above it). A single confirmation is not enough, as forks or double-spending could invalidate it. The White Paper suggests 6 confirmations (about 60 minutes, with blocks every 10 minutes on average), but the number varies based on amount and risk. Variance in block times is high, but the average is maintained thanks to mining difficulty.

## Conclusion
The cycle closes with the transaction "carved" into the blockchain, permanently recording the value transfer.

## Program
This lesson was created for a Satoshi Spritz Connect. 