# Digital Signatures
The topic of this lesson will be digital signatures and how they apply to Bitcoin.

## What is a signature?
We need to understand what we mean by digital signature. When we think of a normal signature, we normally think of something else, since we're talking about digital documents, the digital signature links both the author's identity and the state of the signed document, so essentially the signature also depends on the document we're going to sign.

This is a very big difference from the physical world, where instead we place the signature practically without caring about the support on which we do it. Of course, we might not go and sign checks or other documents without worrying about it, but essentially the signature we're going to affix doesn't vary.

Digital signatures are something a bit different; digital signatures normally rely on public and private key algorithms. This means that somewhere in the world, our wallet has a pair of keys, public and private, and our (pseudo-)identity is linked to the public key that everyone knows or that we will make known to everyone.

We will use our private key, which is a number, and with some mathematical magic we will produce a signature that is a different number and that proves that a certain state of a certain document belongs to or is known by a certain identity connected to a public key. What I'm going to sign is the fingerprint (or HASH) of a certain document (or PAYLOAD).

I also need some random number generator, I throw all this data into a "black box" that produces a signature for me, so the signature is something that proves possession because I'm signing with my secret but also proves that what I'm signing hasn't been modified.

If I modify the PAYLOAD, I modify the HASH and obviously this invalidates the signature.

So essentially why was this more complex signature introduced in the digital world? Well, because in the digital world, unlike the physical one (and maybe those who skipped school remember), copying a signature is much simpler.

The digital signature instead has information about the document and therefore changes for each document and cannot be pasted and reused on a different document.

The digital signature therefore serves to:
- prove that I created a certain message or am requesting a certain action or am declaring a certain state of a system and
- prove that that message or that document or that string of data has not been manipulated, i.e., that it is actually the one I wanted to sign.
- make a certain action non-repudiable; if I produced a signature, it was really me who did it for that specific document.

## Signatures in Bitcoin
This technology is used in Bitcoin under the acronym ECDSA (Elliptic Curve Digital Signature Algorithm), which is an algorithm for producing digital signatures on elliptic curves; for now we won't cover other signature schemes.

Remember that in Bitcoin you can produce signatures for:
- arbitrary text, not very important and used
- new transactions, with the purpose of authorizing the spending of a certain UTXO

But how do these signatures link to the transaction? Each address has a spending mechanism, scripts that must be executed to know if a spend can be authorized. Within these scripts there are commands (or OPCODES) intended for checking digital signatures such as OP_CHECKSIG, OP_CHECKSIGVERIFY, OP_CHECKMULTISIG, OP_CHECKMULTISIGVERIFY

Remember that a Bitcoin transaction consists of:
- Inputs, i.e., the funds I'm going to spend and for which I must produce a spending script
- Outputs, i.e., the new addresses where the funds will go (and for each address a well-defined spending mode is connected.

Essentially, in most cases I will therefore have to produce FOR EACH INPUT the signature(s) necessary to complete the spending script.

Remember that this action allows us to prove that that input is ours and that we want to spend it (we want to pass ownership in full or we want to divide it or we want to join it with other inputs).

Obviously the transaction is valid if all inputs are correctly signed, while if even one of the inputs is not signed, that transaction cannot be considered valid.

The signature is verifiable by everyone and is non-repudiable, but for flexibility Satoshi very cleverly introduced various signature modes, i.e., the signature is always the same but the PAYLOAD changes, i.e., the portion of transaction that is the subject of the signature; this allows, for example, the generation of complex schemes and protocols in which pieces of transactions can be combined with each other; Satoshi called these modes (real flags in the scripting language) SIGHASH.

## SIGHASH
The simplest SIGHASH is SIGHASH_ALL which means generating a signature with ALL INPUTS and ALL OUTPUTS; this is the simplest and most used mode for making a signature.

A first difference can be had with SIGHASH_NONE which signs ALL INPUTS, but NONE of the OUTPUTS, allowing output to be added or fees modified afterwards. WARNING that with this scheme, if not protected by multisig or other features, a miner or anyone who sees a transaction with this signature scheme can replace the outputs redirecting the funds to their own address.

A more interesting flag is SIGHASH_SINGLE in which a pair of input and output is signed provided they are inserted in a transaction at the same level (e.g., fifth input and fifth output); this would allow composing larger transactions based on these pairs but doesn't give the possibility of introducing change, i.e., it requires the total spending of the input.

Parallel to all these SIGHASH can be combined with the ANYONECANPAY flag which limits the signature only to the input for which the signature is being produced, thus giving anyone the possibility to add inputs to the transaction.

These signatures are all valid signatures regardless of the type of address and scripts, leaving maximum flexibility of expression to the wallet, which will normally use SIGHASH_ALL but could also follow more complex protocols that require different signature schemes. In case of multisig, then there's no need to use the same type of signature; a 2-of-2 wallet could sign some of its UTXOs with SIGHASH_NONE and ANYONECANPAY in order to give full control to the second signer who could, for example, collect all these inputs in a transaction to be signed with SIGHASH_ALL.

## Signatures on arbitrary text
For completeness, the same signatures used for transaction inputs can also be used to sign arbitrary text.

Bitcoin proposes a scheme in which text is added to prevent this functionality from being used to sign parts of transactions, so if you have Bitcoin Core or even some wallets, you can look for a text message signing functionality based on a certain address of yours.

The wallet will use the private key associated with the public key that generated that address to make text message signatures.

At verification time, the public key is obtained which can then be used to regenerate the address, so if I have the text and the signature, I extract the public key that signed it, and from the public key I can recalculate the address and check it, for example, with the one provided.

## Program
The lesson on signatures can be repeated; here's a list of those already held:

| Date        | Notes                                          |
|-------------|------------------------------------------------|
||| 