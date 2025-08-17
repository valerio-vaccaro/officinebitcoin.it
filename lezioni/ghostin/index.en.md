# Ghostinbox.it: Use email without having an email 
Ghostinbox is a web platform that allows users to create temporary email addresses to receive messages without revealing their real email address. The service is ideal for quick registrations, account verifications, email deliverability testing, or any situation where you want to avoid spam or protect your identity.

Unlike traditional email services, Ghostinbox doesn't require registration or store personal data, making it an excellent choice for those who prioritize privacy. Additionally, Tor network support allows anonymous access to the service, hiding the user's IP address. The open-source nature of the project ensures transparency and allows developers to examine the code for potential vulnerabilities or customizations.

## How does Ghostinbox work?
![alt text](https://officinebitcoin.it/lezioni/ghostin/front.png)

Using Ghostinbox is extremely intuitive and doesn't require technical skills:

1. **Access the site**: Visit https://ghostinbox.it/ (or via Tor for greater anonymity).
2. **Generate a temporary email address**: Click the button to create a new temporary email address (e.g., random@ghostinbox.it). The address is immediately active and ready to use.
3. **Receive messages**: Use the generated address to receive emails, for example for online service registrations, account verifications, or testing. Messages appear in real-time in the inbox on the site.
4. **Monitor messages**: Access the temporary inbox directly on Ghostinbox to view received messages. No external email client is required.

![alt text](https://officinebitcoin.it/lezioni/ghostin/email.png)

The service is designed to be fast and friction-free: no account creation is needed, and the minimalist interface makes the experience smooth even for non-technical users. The ability to access via Tor adds an additional level of protection for those who want to maintain complete anonymity.

## From alias to email
To use the service, you need to choose an alias that should be long enough and random enough so that it cannot be guessed by other users. This alias will be like a password to access the email and therefore should not be forgotten.

From this alias, an email address HASH@ghostinbox.it is derived where HASH equals `sha256(alias)`, i.e., the hash of the alias using SHA-256; a user can then use this email (shown in the receiving scheme) to receive emails. The receiving page updates automatically showing received emails. A user can create an email address without accessing the service and use the website only for consultation.

By clicking on the email, you can read its text and possibly copy links to click; the email format is deliberately text-only and therefore won't show any of the graphic features of HTML-based emails.

## Who needs Ghostinbox?
Ghostinbox addresses various needs related to privacy and temporary email management:

1. **Spam protection**: Using a temporary address, users can avoid their real email address being flooded with spam or unwanted newsletters.
2. **Secure registrations**: Perfect for signing up to online services, forums, or platforms that require email verification without compromising personal email.
3. **Deliverability testing**: Developers and marketers can use Ghostinbox to test email sending and receiving without involving real addresses.
4. **Advanced privacy**: Thanks to Tor support, the service is ideal for users who want to maintain anonymity during interaction with websites or online services.
5. **Temporary use**: Suitable for situations where a disposable email address is needed, such as for promotions, free trials, or short-term communications.

![alt text](https://officinebitcoin.it/lezioni/ghostin/stats.png)

## Technical features
The GitHub repository of Ghostinbox (https://github.com/valerio-vaccaro/ghostinbox.it) reveals a lightweight implementation, written mainly in Python with the Flask framework, with the following characteristics:

- **Serverless approach**: there is no email server but a free email and email forwarding service is exploited, making the service architecture extremely simple and economical.
- **Architecture**: Ghostinbox uses a client-server architecture based on Flask to manage the generation of temporary email addresses and message display. The simplicity of the design ensures high performance even with high request volumes.
- **Address generation**: Temporary email addresses are generated dynamically based on the entered alias.
- **Tor support**: The service is configured to be accessible via onion routing, ensuring that the user's IP address is not tracked during interaction with the site.
- **Message management**: Received messages are deleted after 30 days.
- **Security**: No personal data or messages are permanently stored. The service design minimizes breach risks, and the absence of registration eliminates the need to provide sensitive information.
- **Open-source**: The public code allows developers to verify system integrity, contribute improvements, or host a customized instance.

Technical strengths:
- **Absolute privacy**: Email deletion after 30 days and Tor support ensure an anonymous and secure experience.
- **Lightweight**: The Flask implementation is optimized for low resources, making the service scalable and fast.
- **Transparency**: The open-source license allows code auditing and customizations, increasing user trust.

## Conclusion
Ghostinbox is an elegant and functional solution for those seeking a fast, secure, and privacy-oriented temporary email service. With its intuitive interface, Tor support, and open-source code transparency, it appeals both to common users who want to protect their inbox from spam and to developers who need a reliable system for testing or temporary registrations. To try Ghostinbox, visit https://ghostinbox.it/. To explore the code or contribute to the project, consult the repository at https://github.com/valerio-vaccaro/ghostinbox.it.

