# Mnemonics & Dice: learn to create your mnemonic

## Introduction
Creating the mnemonic using your own entropy source reduces the attack surface of a Bitcoin wallet; however, some factors must be taken into account:

- the process must be as simple and fast as possible without frills or unnecessary repetitions,
- entropy should not be copied to unnecessary devices and the need to perform calculations or processing should be kept to a minimum,
- the use of software/scripts/programs must be avoided unless you have performed an accurate code review and all dependencies,
- different setups may require slightly different processes.

## Word creation
The first step is calculating the 12 or 24 words of the mnemonic; 12 words are normally more than sufficient for the security of a Bitcoin wallet.

For word generation, you can use the method described in [TRGM](https://github.com/valerio-vaccaro/TRMG) using 3 dice of which 1 has 8 faces and 2 have 16 faces. EACH dice roll corresponds to ONE AND ONLY ONE word; to find it, simply scroll through the site's table looking for the correspondence of the dice with the roll performed (the first die is ALWAYS the one with 8 faces). The word column contains the word you're looking for.

The recommendation is to generate all 12 or 24 words and possibly correct the last one or anyway use the dice to generate the entropy relative to the last word.

## Checksum calculation
The last word is not completely decided by us but contains a control part, i.e., we cannot fully choose all 11 bits of entropy that compose it; we can instead choose the first 7 in the case of a 12-word mnemonic or the first 3 in the case of a 24-word mnemonic.

Let's say our last word is BACON corresponding to rolls 1, 9, and 11 (remember that the first die is ALWAYS the one with 8 faces), the table also reports Group 12 and Group 24 which allow us to group words considering only the entropy of the first two rolls (group 12) or only the first roll (group 24).

Let's assume we want to build a 12-word mnemonic, which means the checksum will be a word among the 16 possible ones having the same group 12 as bacon, i.e., 0001000; the possible words are:

|First|Second|Third|Index|Word	|Index in binary|Group 12	|Group 24|
|---|---|---|-------|-----------|---------------|-----------|---|
|1  |9	|1	|128	|avoid	    |00010000000	|0001000	|000|
|1  |9	|2	|129	|awake	    |00010000001	|0001000	|000|
|1  |9	|3	|130	|aware	    |00010000010	|0001000	|000|
|1  |9	|4	|131	|away	    |00010000011	|0001000	|000|
|1  |9	|5	|132	|awesome	|00010000100	|0001000	|000|
|1  |9	|6	|133	|awful	    |00010000101	|0001000	|000|
|1  |9	|7	|134	|awkward	|00010000110	|0001000	|000|
|1  |9	|8	|135	|axis	    |00010000111	|0001000	|000|
|1  |9	|9	|136	|baby	    |00010001000	|0001000	|000|
|1  |9	|10	|137	|bachelor	|00010001001	|0001000	|000|
|1  |9	|11	|138	|bacon	    |00010001010	|0001000	|000|
|1  |9	|12	|139	|badge	    |00010001011	|0001000	|000|
|1  |9	|13	|140	|bag    	|00010001100	|0001000	|000|
|1  |9	|14	|141	|balance	|00010001101	|0001000	|000|
|1  |9	|15	|142	|balcony	|00010001110	|0001000	|000|
|1  |9	|16	|143	|ball   	|00010001111	|0001000	|000|

How to find the only correct word among the various ones? It depends on your setup, let's see some examples:

- bruteforce, i.e., try all of them in sequence until you find the correct one (very arduous with 24-word mnemonics), this is the method to use with Ledger or with Electrum (making sure to select the BIP39 flag),
- calculate all possible words with the first 11 or 23 words and search for the only one that falls in this set, this method is usable with Jade and with other hardware wallets capable of calculating all possible final words of a mnemonic,
- enter the complete mnemonic and let the hardware wallet fix it for us, as Specter-DIY does very elegantly, for example.

## Backup (topic of another lesson)
It's fundamental to have a good backup policy, therefore:
- multiple backups,
- on multiple media and
- possibly encrypted or split (but you need to know how to do it well).

## Bibliography

- [TRMG](https://github.com/valerio-vaccaro/TRMG)

## Repetitions
This lesson is repetitive and will be repeated every month. Below is a list of repetitions already held.

| Date        | Notes                                          |
|-------------|------------------------------------------------|
| 240102-2100 | First lesson                                   | 