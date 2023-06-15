# Get Domain Information

To obtain a list of registered domains, you can use the following command in the SCP command-line interface:

```Bash
scloud dns list-dns-domain-v2
```

This command allows you to retrieve a comprehensive list of domains that have been registered through the SCP DNS service. The output will include details such as domain names, registration dates, expiration dates, and other relevant information.

```Bash
ubuntu@SCP:~$ scloud dns list-dns-domain-v2 | jq
{
  "totalCount": 1,
  "contents": [
    {
      "dnsDomainId": "DNS_DOMAIN_SERVICE-xxxxxxxxxxxxx",
      "dnsDomainName": "xxxxx.com",
      "dnsEnvUsage": "PUBLIC",
      "dnsDomainType": "HOSTING_MANAGED",
      "startDate": "2023-05-17T00:00:00.000000+09:00",
      "expiredDate": "2024-05-17T00:00:00.000000+09:00",
      "autoExtension": false,
      "dnsState": "ACTIVE",
      "linkedRecordCount": 0,
      "region": "Global"
    }
  ]
}
```

To obtain detailed information about a specific registered domain, you can use the following command:

***Replace `<DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>` with the actual ID of the domain you want to retrieve information for***

```Bash
scloud dns detail-dns-domain-v2 --dns-domain-id <DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>
```

This command will provide you with more in-depth details about the specified registered domain, including administrative contact information, domain renewal, and other relevant data

```Bash
ubuntu@Matia-Odyssey:~$ scloud dns detail-dns-domain-v2 --dns-domain-id DNS_DOMAIN_SERVICE-XXXXXXXXXXXX | jq
{
  "projectId": "PROJECT-XXXXXXXX-XXXXXXXX-XXXXXXXX-XXXXXXXX",
  "createdBy": "XXXXXXXX",
  "createdDt": "2023-05-17T08:57:42.335000+09:00",
  "modifiedBy": "XXXXXXXX",
  "modifiedDt": "2023-05-17T10:54:51.503000+09:00",
  "dnsDomainId": "DNS_DOMAIN_SERVICE-XXXXXXXX",
  "dnsDomainName": "XXXXXXXX.com",
  "dnsEnvUsage": "PUBLIC",
  "dnsDomainType": "HOSTING_MANAGED",
  "startDate": "2023-05-17T00:00:00.000000+09:00",
  "expiredDate": "2024-05-17T00:00:00.000000+09:00",
  "registeredByLastName": "XXXXXXXX",
  "registeredByFirstName": "XXXXXXXX",
  "registeredByEmail": "XXXXXXXX@gmail.com",
  "firstKoAddress": "XXXXXXXX",
  "koDetailAddress": "XXXXXXXX",
  "firstEnAddress": "XXXXXXXX",
  "enDetailAddress": "XXXXXXXX",
  "secondEnAddress": "",
  "secondKoAddress": "",
  "countryType": "DOMESTIC",
  "postalCode": "XXXXXXXX",
  "dnsDescription": "",
  "koCompanyName": "XXXXXXXX",
  "enCompanyName": "XXXXXXXX",
  "registeredByTelno": "XXXXXXXX",
  "autoExtension": false,
  "dnsState": "ACTIVE",
  "linkedRecordCount": 0
}
```

You can obtain detailed information about a registered domain using the WHOIS database with WHOIS lookup tools. These tools provide comprehensive information about domain registrations, including registrant details, registration dates, expiration dates, and domain status. By conducting a WHOIS lookup on a registered domain, you can gather additional insights about its ownership and registration history

```Bash
ubuntu@XXXXX:~$ whois XXXXX.com
 Domain Name: XXXXX.COM
 Registry Domain ID: XXXXXXXXXXXXXXXX_DOMAIN_COM-VRSN
 Registrar WHOIS Server: whois.whois.co.kr
 Registrar URL: http://www.whois.co.kr
 Updated Date: 2023-05-17T15:35:04Z
 Creation Date: 2023-05-16T23:57:53Z
 Registry Expiry Date: 2024-05-16T23:57:53Z
 Registrar: Whois Corp.
 Registrar IANA ID: 100
 Registrar Abuse Contact Email: abuse@whois.co.kr
 Registrar Abuse Contact Phone: +82.15884259
 Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
 Name Server: NS1.SAMSUNGSDSCLOUD.COM
 Name Server: NS2.SAMSUNGSDSCLOUD.COM
 DNSSEC: unsigned
 URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2023-05-29T23:06:19Z <<<

For more information on Whois status codes, please visit https://icann.org/epp

NOTICE: The expiration date displayed in this record is the date the
.
.
.

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
Domain Name : XXXXX.com
Registry Domain ID: XXXXXXXXXXXXXXXX_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.whois.co.kr
Registrar URL: http://www.whois.co.kr
Updated Date: 2023-05-17T15:35:04Z
Creation Date: 2023-05-16T23:57:53Z
Registrar Registration Expiration Date: 2024-05-16T23:57:53Z
Registrar: Whois Corp.
Registrar IANA ID: 100
Registrar Abuse Contact Email: abuse@whois.co.kr
Registrar Abuse Contact Phone: +82.15884259
Reseller:
Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
Registry Registrant ID:
Registrant Name:
Registrant Organization:
Registrant Street:
Registrant City:
Registrant State/Province:
Registrant Postal Code:
Registrant Country:
Registrant Phone:
Registrant Phone Ext:
Registrant Fax:
Registrant Fax Ext:
Registrant Email:
Registry Admin ID:
Admin Name:
Admin Organization:
Admin Street:
Admin City:
Admin State/Province:
Admin Postal Code:
Admin Country:
Admin Phone:
Admin Phone Ext:
Admin Fax:
Admin Fax Ext:
Admin Email:
Registry Tech ID:
Tech Name:
Tech Organization:
Tech Street:
Tech City:
Tech State/Province:
Tech Postal Code:
Tech Country:
Tech Phone:
Tech Phone Ext:
Tech Fax:
Tech Fax Ext:
Tech Email:
Name Server: ns1.samsungsdscloud.com
Name Server: ns2.samsungsdscloud.com
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System:<EUGPSCoordinates>http://wdprs.internic.net/
>>> Last update of WHOIS database:<EUGPSCoordinates>2023-05-30T08:<EUGPSCoordinates>06:<EUGPSCoordinates>32Z <<<

For more information on Whois status codes, please visit https://icann.org/epp
```
