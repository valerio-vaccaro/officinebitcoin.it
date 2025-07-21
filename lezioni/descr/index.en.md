# Descriptors
Descriptors are a relatively new concept and not yet very widespread, but useful for describing Bitcoin wallet structure. Descriptors are readable character strings (alphanumeric, hexadecimal, and some symbols like parentheses), designed to represent clearly and in a standardized way a wallet, i.e., the set of public and private keys necessary to calculate balances, receive and spend Bitcoin.

## Evolution of wallet management
To contextualize descriptors, the speaker traces the evolution of wallets:

- Early wallets (pre-BIP-32): in the early days, with Bitcoin Core, wallets were files containing randomly generated keys. Every time addresses ran out, new ones were added, making frequent backup necessary to avoid losing funds. This system was inefficient.
- BIP-32 (HD Wallet): with the introduction of hierarchical deterministic generation, a seed generated a master key, from which all addresses derived. Just backing up the seed was enough, but it wasn't yet a complete solution.
- Mnemonics (BIP-39): subsequently, the seed was derived from a sequence of 12 or 24 words (mnemonic), easier to save. However, to reconstruct a wallet, information on derivation paths (e.g., Legacy, SegWit) was also needed, otherwise funds could be unrecoverable.

The mnemonic alone is not enough, especially for complex wallets like multisig (which require multiple signatures) or those with advanced scripts (e.g., timelock or inheritance conditions). Some wallets try all possible derivations to find funds, while others (e.g., Electrum) require specifying the wallet type. In multisig, moreover, the public keys of other participants are needed, further complicating backup.

## What are Descriptors and why they are needed
Descriptors were born to overcome these limitations, offering a complete and flexible description of wallet structure. They don't replace the mnemonic, but integrate it, including:

- Extended public keys (xpub, ypub, etc.).
- Derivation paths (e.g., m/44'/0'/0' for Legacy).
- Any spending scripts or conditions (e.g., multisig, timelock).

## Practical examples
- Single-sig Legacy: A simple descriptor might be `pk([fingerprint/derivation]xpub...)`, where:
1. pk indicates a public key.
2. [fingerprint/derivation] specifies the master key and path.
3. xpub generates addresses (e.g., 0/* for receiving, 1/* for change).
- Multisig: An example is `sortedmulti(2, xpub1, xpub2, xpub3)`, which describes a 2-of-3 wallet, ordering keys for consistency.
- Complex scripts: With scripts like p2sh (pay to script hash) or p2wsh (pay to witness script hash), advanced conditions can be included, such as timelock or logical combinations (and, or).

## Descriptors and Taproot
An interesting case is the descriptor for Taproot (tr), which supports two spending modes:

- Direct signature with a specific key.
- A tree of conditions (e.g., inheritance or timelock), keeping complexity hidden on the blockchain until spending.

## Advantages of Descriptors
- Complete backup: they contain all information needed to reconstruct a wallet without attempts.
- Compatibility: ideal for watch-only wallets, where funds are monitored without private keys.
- Flexibility: support single-sig, multisig, and complex scripts.
- Privacy: don't reveal secrets and can be shared like an xpub.

## Limitations and compatibility
Not all wallets fully support descriptors. For example, Bitcoin Core only implements a subset and requires two separate descriptors for addresses and change. Software like Sparrow or Specter offer better support, allowing import/export of descriptors and visualization of their structure.

Experiments can be done with:
- Sparrow: supports descriptors, with a graphical interface to create or analyze them.
- BDK: library with command-line interface to manage complex descriptors.
- Testnet/Signet: safe environments to test without risking real funds.

## References

- [BIP-380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)
- [Bitcoin Improvement Proposal 380](https://github.com/bitcoin/bips/blob/master/bip-0380.mediawiki)

# Program
This lesson was created for a Satoshi Spritz Connect. 