# Jade Setup

![alt text](https://officinebitcoin.it/lezioni/jadeset/0_Cover.jpg)

Jade arrives in packaging that must be verified to be intact, checking the two anti-tamper holographic stickers placed between the box (lower) and the lid (upper).

The package contains a small user manual, two CompactSeedQR templates, as well as the hardware wallet.

Jade turns on by holding down the lower button and presents itself showing the 3 menus:

- Setup Jade
- Scan QR
- Options

You can set various parameters in Options, depending on personal preferences, but initialization is the first part to complete.

By acting with the scroll button, you then select the __Setup Jade__ menu and confirm with the front button.

![alt text](https://officinebitcoin.it/lezioni/jadeset/1.jpg)

A notice appears to check the setup instructions from the website https://blockstream.com/jade/

![alt text](https://officinebitcoin.it/lezioni/jadeset/2.jpg)

For proper execution, it's recommended to create the mnemonic with dice rolls and use this entropy to create the wallet. Therefore, choose __Advanced Setup__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/3.jpg)

Jade warns that this setup has some advanced technical features. It's sufficient to pay maximum attention and click the confirmation button

![alt text](https://officinebitcoin.it/lezioni/jadeset/4.jpg)

With the aim of entering the mnemonic generated with dice entropy, choose __Restore Wallet__.

![alt text](https://officinebitcoin.it/lezioni/jadeset/5.jpg)

You must now set the length of the mnemonic, 12 or 24 words. The menu also offers the possibility to restore the wallet by scanning a QR code: this is the SeedQr which will be covered elsewhere.

![alt text](https://officinebitcoin.it/lezioni/jadeset/6.jpg)

For purely educational and speed reasons, this tutorial shows setup with a 12-word mnemonic.

The procedure for entering the first word begins and Jade shows the keyboard to enter the respective letters. With the scroll button, position yourself ← → in the correct position.

In this example, word #1 is "below".

![alt text](https://officinebitcoin.it/lezioni/jadeset/7.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/8.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/9.jpg)

After entering the first 3-4 letters, Jade picks words from the BIP39 dictionary and starts providing a series of suggestions. With the scroll button, go forward or backward until you find the correct word.

![alt text](https://officinebitcoin.it/lezioni/jadeset/10.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/11.jpg)

Continue with word entry until you reach the moment of the last word: the checksum.

At this point, Jade shows two possibilities: enter an existing word or offers the possibility to calculate a valid checksum with its own software.

![alt text](https://officinebitcoin.it/lezioni/jadeset/12.jpg)

Note:

- In the case of setup from a 12-word mnemonic created with dice rolls, it's recommended to choose Existing and enter the first letters of the word, choosing them from the range proposed by the dice roll.
- If the setup starts, instead, from a 24-word mnemonic generated with dice rolls, you can have Jade calculate all possible checksums and then choose one. It's true that you lose some entropy, but only in the last word. When you've decided to entrust your funds to Jade, it's an acceptable trade-off.
- In case of restoring an existing wallet: enter the correct checksum by choosing Existing.

Continuing with the example of setup from a mnemonic generated with dice rolls, we choose Existing in the previous menu, with the intent of entering the letters and finding the corresponding checksum.

![alt text](https://officinebitcoin.it/lezioni/jadeset/13.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/14.jpg)

At this point, Jade proposes exporting the recovery phrase in the form of _CompactSeedQR_.

The _CompactSeedQR_ is an encoding that transforms the mnemonic phrase into a QR code to be scanned for wallet restoration on Jade.

If you want to try doing this, see the section at the bottom of this tutorial that explains how to do it.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

By choosing "No" in the previous menu, you can proceed to the end of setup.

The device is ready to be connected to its watch-only wallet.

The next menu shows the connection possibilities:

- USB
- QR code
- Bluetooth

![alt text](https://officinebitcoin.it/lezioni/jadeset/16.jpg)

Choose USB and confirm with the confirm button

At this point, Jade asks to be connected to a companion app.

In the following example, it was chosen to connect the device via USB to Blockstream Green; this wallet, in fact, allows you to control firmware updates for Jade and, by listening to the device via USB, offers guided setup.

Open Green and check the network and security settings.

If there's a firmware update, Green signals it immediately and it's recommended to perform the upgrade.

![alt text](https://officinebitcoin.it/lezioni/jadeset/17.jpg)

After the firmware update is complete, Green starts interacting with Jade.

The signing device, at this point, asks to set the duress PIN, which will encrypt the private keys on Jade, making them inaccessible to anyone, except for those who possess the six-digit PIN.

![alt text](https://officinebitcoin.it/lezioni/jadeset/18.jpg)

While Green waits with the screen shown above, on Jade appears the possibility to set the 6-digit PIN and confirm it by re-entering it correctly.

![alt text](https://officinebitcoin.it/lezioni/jadeset/19.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/20.jpg)

Jade creates persistent data by encrypting it on the device.

![alt text](https://officinebitcoin.it/lezioni/jadeset/21.jpg)

At the end of the operation, which may take a few moments, Green opens the wallet ready for use.

By turning off Jade and turning it back on, the device will present itself as initialized, with updated firmware and ready to be unlocked (Unlock Jade) for use with its companion app.

![alt text](https://officinebitcoin.it/lezioni/jadeset/22.jpg)

## Extra: CompactSeedQR creation

At the end of entering the mnemonic, we bypassed the part of exporting keys in QR code format, to stay focused on the setup phase. This type of export can always be done later.

Turn on Jade and from the Options menu → Temporary Signer → Continue → 12/24 Words you return to the recovery phrase entry menu, at the end of which the choice screen for export in SeedQR format is proposed.

![alt text](https://officinebitcoin.it/lezioni/jadeset/15.jpg)

By choosing Yes, you're warned that you must draw the QR code on the template provided in the box.

![alt text](https://officinebitcoin.it/lezioni/jadeset/24.jpg)

The procedure begins by showing an overview of how the QR code to be drawn will be (some parts are erased for privacy reasons)

![alt text](https://officinebitcoin.it/lezioni/jadeset/25.jpg)

Subsequently, all the grid boxes will be shown, one by one, from A1 to C3 or E5 depending on the length of the recovery phrase.

![alt text](https://officinebitcoin.it/lezioni/jadeset/26.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/27.jpg)

![alt text](https://officinebitcoin.it/lezioni/jadeset/28.jpg)

After drawing the last box of the grid, Jade shows the overview again for a first verification. Continue by confirming Done.

![alt text](https://officinebitcoin.it/lezioni/jadeset/29.jpg)

Jade's built-in camera is enabled, with which you must frame the SeedQR just drawn.

![alt text](https://officinebitcoin.it/lezioni/jadeset/30.jpg)

If the drawing corresponds to what Jade proposed in the procedure just completed, a confirmation signal will be displayed.

![alt text](https://officinebitcoin.it/lezioni/jadeset/31.jpg)

By clicking to confirm Continue, Jade presents itself working from the main menus.

The CompactSeedQR is a tool to restore the wallet on Jade. 