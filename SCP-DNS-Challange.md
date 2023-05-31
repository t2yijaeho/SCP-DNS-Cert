# DNS Challange on SCP

To complete the DNS challenge on the Samsung Cloud Platform (SCP), please follow the steps provided below

## ***Step 1. Obtain the DNS ID***

To retrieve the registered domain ID, execute the following command in the terminal:

```Bash
scpc dns list-dns-domain-v2
```

This command will retrieve a comprehensive list of domains that have been registered through the SCP DNS service. The output will include domain ID, domain names, registration dates, expiration dates, and other relevant information.

Here's an example of the command output:

```Bash
ubuntu@T3SCP:~$ scpc dns list-dns-domain-v2 | jq
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

## ***Step 2. Create DNS TXT Record***

Once you have the DNS ID, you can create the DNS TXT record.

Create a CLI request JSON file using the following command:

***Replace `<ACME CHALLANGE VALUE>` actual challenge value created during the issuance of the certificate and `<DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>` with the specific ID of the domain for which you want to retrieve information***

```Bash
cat <<EOF >req-txt-record.json
{
  "reqVo": {
    "dnsRecordMapping": [
      {
        "preference": 1,
        "recordDestination": "<ACME CHALLANGE VALUE>"
      }
    ],
    "dnsRecordName": "_acme-challenge",
    "dnsRecordType": "TXT",
    "ttl": 333
  },
  "dnsDomainId": "<DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>"
}
EOF
```

Next, create the TXT DNS record using the following command:

```Bash
scpc dns create-dns-record-v2 --input-json file://req-txt-record.json
```

An example output of the command will be:

```Bash
ubuntu@T3SCP:~$ scpc dns create-dns-record-v2 --input-json file://req-txt-record.json | jq
{
 "projectId": "PROJECT-XXXXXXXX-XXXXXXXXXXXXX_X",
 "resourceId": "DNS_DOMAIN_RECORD--XXXXXXXXXXXXXXXXXXXXX",
 "requestId": "REQ-XXXXXXXXXXXXXXXXXXXXX"
}
```

To list the registered DNS record, use the following command:

***Replace `<DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>` with the actual ID of the domain you want to retrieve information for***

```Bash
scpc dns list-dns-record-v2 --dns-domain-id <DNS_DOMAIN_SERVICE-XXXXXXXXXXXX>
```

Here's an example output of the command:

```Bash
ubuntu@T3SCP:~$ scpc dns list-dns-record-v2 --dns-domain-id <DNS_DOMAIN_SERVICE-XXXXXXXXXXXX> | jq
{
  "totalCount": 1,
  "contents": [
    {
      "dnsRecordId": "DNS_DOMAIN_RECORD--XXXXXXXXXXXXXXXXXXXXX",
      "dnsRecordName": "_acme-challengee",
      "dnsRecordType": "TXT",
      "ttl": 333,
      "dnsState": "ACTIVE",
      "recordDestinations": [
        "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
      ]
    }
  ]
}
```

## ***Step 3. Verify DNS Record Propagation***

To ensure that the DNS TXT record has propagated correctly, follow the steps below:

Execute the following command in the terminal to verify the TXT record for the ***`_acme-challenge.xxxxx.com`*** domain:

```Bash
dig _acme-challenge.xxxxx.com TXT
```

Here's an example output of the command:

```Bash
ubuntu@T3SCP:~$ dig _acme-challenge.xxxxx.com TXT

; <<>> DiG 9.18.12-0ubuntu0.22.04.1-Ubuntu <<>> _acme-challenge.xxxxx.com TXT
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63606
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;_acme-challenge.xxxxx.com.     IN      TXT

;; ANSWER SECTION:
_acme-challenge.xxxxx.com. 0    IN      TXT     "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"

;; Query time: 40 msec
;; SERVER: 172.20.144.1#53(172.20.144.1) (UDP)
;; WHEN: Tue May 30 16:49:22 KST 2023
;; MSG SIZE  rcvd: 124
```

The output provides the following information:

- The status of the query is ***`NOERROR`*** indicating that the record was found
- The ANSWER SECTION displays the TXT record value associated with the ***`_acme-challenge.xxxxx.com`*** domain
- The Query time shows the time taken for the DNS query to complete.
- The SERVER field specifies the DNS server used for the query
- Ensure that the displayed TXT record value matches the one you provided during the creation of the DNS record. This confirms that the DNS record has propagated successfully
- Note: The specific values shown in the example output will vary based on your configuration

If you receive an ***`NXDOMAIN`*** status, it means that the TXT record has not propagated yet or there may be an issue with the DNS configuration. Here are some steps you can take to troubleshoot the issue:

1. Wait for some time and try again later: DNS propagation can take time, so it's possible that the record hasn't propagated to all DNS servers yet. Wait for some time, usually up to hours, and then retry the command

2. Check your DNS settings: Ensure that you have correctly set up the TXT record with the appropriate value. Double-check the domain name, record name (_acme-challenge), and record type (TXT). Verify that you have entered the correct information in your DNS provider's settings.

3. Change your DNS server: In some cases, the DNS server you are using may not have updated its records yet. You can try changing your DNS server to a different one that is known for fast propagation. Popular public DNS servers include Google DNS (8.8.8.8, 8.8.4.4) and Cloudflare DNS (1.1.1.1, 1.0.0.1). Consult your operating system or network settings to change the DNS server configuration

By following these steps and ensuring the correct DNS configuration, you can verify the propagation of the DNS TXT record