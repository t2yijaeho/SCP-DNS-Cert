# Launch Certbot on Ubuntu

To launch Certbot on Ubuntu, follow the step-by-step instructions below

## ***Step 1. Run the CLI Command*** 

A wildcard certificate is a type of SSL/TLS certificate that is used to secure a domain and all its subdomains. It allows you to secure multiple subdomains under a single certificate, simplifying the certificate management process

In the provided command, you can obtain a wildcard certificate. The asterisk (*) symbol before the dot (.) represents the wildcard character, indicating that the certificate will cover all subdomains of the specified domain.

Execute the following command in the terminal:

***Replace `<Your Domain Name>` with the actual domain name you intend to secure with the certificate***

```Bash
sudo certbot certonly \
    --manual \
    -d *.<Your Domain Name> \
    --key-type rsa \
    --preferred-challenges dns
```

This command initiates Certbot in ***`certonly`*** mode, specifically designed for certificate generation. The ***`--manual`*** option indicates that you will manually perform the necessary DNS validation steps

***`-d *.<Your Domain Name>`*** defines the domain name and wildcard notation to obtain a certificate that covers the specified domain and all its subdomains

By specifying the ***`--key-type rsa`*** option, you ensure that the RSA key type is used for generating the certificate. RSA is a widely-used asymmetric encryption algorithm for secure communication.

***Please note that the Samsung Cloud Platform currently only supports RSA type certificates. Therefore, it is essential to use the RSA key type when generating the certificate to ensure compatibility with the platform***

The ***`--preferred-challenges dns`*** option indicates that the preferred challenge method for validating domain ownership is DNS-based. This means you will be required to create a DNS TXT record with a specific value as part of the validation process.

Example output:

```Bash
ubuntu@T3SCP:~$ sudo certbot certonly --manual -d *.xxxxx.com --preferred-challenges dns
Saving debug log to /var/log/letsencrypt/letsencrypt.log
```

## ***Step 2. Enter Your Email Address*** 

When prompted, enter your email address. This email address will be used for urgent renewal and security notices

Example:

***Enter `<Your EMail Address>` with your email address***

```Bash
Enter email address (used for urgent renewal and security notices)
 (Enter 'c' to cancel): <Your EMail Address>
```

## ***Step 3. Consent to the Terms of Service*** 

You will be presented with the Let's Encrypt Terms of Service. Read the terms and indicate your agreement to proceed.

Example:

```Bash
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.3-September-21-2022.pdf. You must
agree in order to register with the ACME server. Do you agree?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: Y
```

## ***Step 4. Select Email Notice Preference*** 

You will be asked whether you are willing to share your email address with the Electronic Frontier Foundation (EFF), the non-profit organization that develops Certbot and supports digital freedom initiatives.

Upon confirming your willingness to share your email address, the account will be registered, and the certificate issuance process will proceed

Example:

```Bash
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: Y
Account registered.
```

## ***Step 5. Obtain the TXT Record Value*** 

You will receive instructions to deploy a DNS TXT record for your domain. The TXT record serves as proof of ownership during the certification process

Example:

```Bash
Requesting a certificate for *.xxxxx.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:

_acme-challenge.xxxxx.com.

with the following value:

imN0tSaying1mLazyBut1mEfficientAtD0ingN0thing

Before continuing, verify the TXT record has been deployed. Depending on the DNS
provider, this may take some time, from a few seconds to multiple minutes. You can
check if it has finished deploying with aid of online tools, such as the Google
Admin Toolbox: https://toolbox.googleapps.com/apps/dig/#TXT/_acme-challenge.xxxxx.com.
Look for one or more bolded line(s) below the line ';ANSWER'. It should show the
value(s) you've just added.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue
```

Follow the instructions to add the TXT record to your DNS configuration. Make sure the record is correctly deployed before proceeding

## ***Step 6. Receiving the Certificate and Key*** 

Once the certificate issuance process is completed, you will receive the certificate and its corresponding key. The following information will be displayed:

```Bash
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/xxxxx.com/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/xxxxx.com/privkey.pem
This certificate expires on 2023-08-19.
These files will be updated when the certificate renews.
```

The certificate and key files are stored in the specified locations. The certificate file, ***`fullchain.pem`***, contains the full certificate chain, including the domain's certificate and any necessary intermediate certificates. The key file, ***`privkey.pem`***, holds the private key associated with the certificate

It's important to note that the certificate has an expiration date, which in this case is 2023-08-19. To ensure the continued security of your website, it's crucial to renew the certificate before this date. However, it's worth mentioning that the current configuration does not enable automatic certificate renewal

To renew this certificate, you'll need to manually repeat the same ***`certbot`*** command before the expiration date. Keep in mind that renewing manual certificates requires the use of an authentication hook script (***`--manual-auth-hook`***), which you haven't provided in the current setup.

Additionally, the message provides some next steps and suggestions for supporting the Certbot project:

```Bash
NEXT STEPS:
- This certificate will not be renewed automatically. Autorenewal of --manual certificates requires the use of an authentication hook script (--manual-auth-hook) but one was not provided. To renew this certificate, repeat this same certbot command before the certificate's expiry date.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

These steps serve as a reminder that the current certificate will not be automatically renewed.

To support the project and help ensure its continued development, you can consider making a donation to the Internet Security Research Group (ISRG) or the Electronic Frontier Foundation (EFF), both of which play a significant role in advancing secure web encryption and digital freedom