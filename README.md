# DNS and Certificates on Samsung Cloud Platform(SCP)

## Register a domain

To search for and register an available domain name, you can utilize the SCP DNS service. SCP DNS offers a comprehensive solution for managing domain names, allowing you to easily search for and secure a domain for your specific needs. By following the steps outlined below, you can successfully search for an available domain name and register it using SCP DNS:

### ***1. Access the SCP DNS service***

Begin by logging into your SCP account and navigating to the SCP DNS service webpage provided by Samsung Cloud Platform

### ***2. Search for an available domain***

Utilize the domain search functionality provided by SCP DNS. Enter the desired domain name into the search field to check its availability. SCP DNS will query the relevant domain databases to determine if the domain is currently registered or if it is available for registration.

### ***3. Review the search results***

SCP DNS will display the search results, indicating whether the domain name is available or already registered by another party. Take note of the availability status and any alternative suggestions or variations provided by the service.

### ***4. Select and register the domain***

If the desired domain name is available, proceed with the registration process. Follow the instructions provided by SCP DNS to provide the necessary registration details, such as contact information and any additional DNS configurations required

### ***5. Complete the registration***

Review the registration details and confirm that they are accurate. Proceed with the payment process as specified by SCP DNS to finalize the registration. Ensure that you complete any necessary verification steps or agreements as prompted

### ***6. Domain activation***

Once the registration process is successfully completed and payment is confirmed, SCP DNS will initiate the activation of the domain. This process may take a short period of time, during which the domain will be configured and made accessible

By utilizing the SCP DNS service, you can easily search for available domain names and complete the registration process in a seamless manner. Ensure that you follow all necessary steps and provide accurate information to secure the desired domain for your online presence

### Verrify the registered domain

***[Get Domain Information(CLI)](Get-Domain-Info.md)***

### ***Warning: Privacy Risks and Lack of DNSSEC Protection***

It is imperative to exercise caution and prioritize privacy and security when dealing with domain names and internet communications. Failing to implement privacy protection configurations and neglecting the use of Domain Name System Security Extensions (DNSSEC) can potentially expose personal information such as names, email addresses, and phone numbers to the public

To mitigate these risks and protect your sensitive data, it is crucial to be aware of the following concerns:

***Privacy Protection Configuration***: Take proactive measures to shield personal information associated with domain registrations. Failing to do so can result in this data being publicly accessible through WHOIS database queries or other means. Ensure you configure appropriate privacy settings within your domain management system

***Lack of DNSSEC on SCP***: It is essential to note that the Samsung Cloud Platform (SCP) does not provide DNSSEC protection by default. DNSSEC is a vital security measure that protects against unauthorized modifications or tampering of DNS records. Without DNSSEC, your domain may be vulnerable to attacks such as DNS cache poisoning or DNS spoofing. Consider enabling DNSSEC within your domain's DNS settings

By heeding this warning and taking proactive steps to address privacy risks and implement DNSSEC, you can significantly reduce the likelihood of your personal information becoming exposed to the public. Neglecting these precautions can compromise the confidentiality and security of your online presence

## Create a Certificate

Create a certificate issued by a publicly trusted Certificate Authority(CA) with DNS authorization

In order to obtain a public certificate from the nonprofit organization Internet Security Research Group (ISRG), it is advisable to install the software tool called ***`certbot`***. Certbot facilitates the process of generating and managing SSL/TLS certificates, ensuring secure communication over the internet

By following the steps outlined below, you can successfully obtain a public certificate through the use of certbot:

### ***1. Install the certbot software tool on your system***

This can typically be accomplished by executing the appropriate installation command provided by your operating system or package manager

***[Get Certbot (Official Guide)](https://eff-certbot.readthedocs.io/en/stable/install.html)***

***[Install Certbot on Ubuntu (Step-by-Step Guide)](Certbot-Install-Ubuntu.md)***

### ***2. Launch the certbot and follow instructions***

Once certbot is installed, launch the application and follow the prompts to initiate the certificate generation process

***[Get Certification Manually (Official Guide)](https://eff-certbot.readthedocs.io/en/stable/using.html#manual)***

***[Launch Certbot on Ubuntu (Step-by-Step Guide)](Certbot-Launch-Ubuntu.md)***

### ***3. Challange DNS ownership***

During the certificate generation process, you will be required to provide certain information, such as the domain name for which the certificate is being issued. Ensure that you have administrative control over the domain and can verify your ownership.

Certbot will communicate with the Let's Encrypt certificate authority, which is operated by ISRG, to verify your domain ownership and request the certificate. This involves a series of steps to validate your control over the domain

***[DNS Challange (Official Guide)](https://letsencrypt.org/docs/challenge-types/#dns-01-challenge)***

***[DNS Challange on SCP (Step-by-Step Guide)](SCP-DNS-Challange.md)***

### ***4. Verify Certificate and cryptographic Keys***

Upon successful verification, certbot will retrieve the generated certificate and associated keys. These files are crucial for establishing secure connections and ***must be safeguarded appropriately***

## Register the certificate on SCP

### ***1. Prepare Certificate and Key Files***

Before proceeding with the registration process, it is crucial to ensure that you have the necessary certificate and key files in the correct formats. This ensures a smooth registration process

### ***2. Register the Certificate***

Once you have prepared the certificate and key files, follow SCP's guides and procedures to register the certificate on SCP

## Deploy the certificate

Deploy the certificate created in the previous steps

Finally, you can configure your web server or application to utilize the obtained certificate, enabling encrypted connections and ensuring the trustworthiness of your online presence

- The deployment process can vary depending on the specific web server or application you are using

- Consult the documentation or support resources for your web server or application for instructions on how to deploy the certificate

- Generally, the deployment process involves configuring the web server or application to use the obtained certificate and private key

- This typically includes specifying the paths to the certificate and key files in the server/application configuration.

- Restart or reload the web server or application to apply the configuration changes.
