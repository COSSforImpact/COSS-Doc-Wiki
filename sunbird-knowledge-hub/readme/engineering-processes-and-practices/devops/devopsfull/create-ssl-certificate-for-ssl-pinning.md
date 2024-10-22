---
icon: elementor
---

# Create SSL Certificate for SSL pinning

SSL pinning is a mechanism to ensure the application is talking to the "Real" server, and shouldn't susceptable to "Man in the Middle" attack.

Steps:

1. Get the original ssl certificate for the server
2. take the leaf certificate
3. attach it in the application

#### Getting SSL certificate <a href="#createsslcertificateforsslpinning-gettingsslcertificate" id="createsslcertificateforsslpinning-gettingsslcertificate"></a>

```
openssl s_client -servername dev.sunbirded.org -host dev.sunbirded.org -port 443 -showcerts
```



\


1. Check for the domain name, as highlighted above
2.  copy from \


    \-----BEGIN CERTIFICATE-----

    MIIGljCCBX6gAwIBAgIRAJU11K/RVD5pzOg+rvdI3IIwDQYJKoZIhvcNAQELBQAw

    gZAxCzAJBgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAO\
    BgNVBAcTB1NhbGZvcmQxGjAYBgNVBAoTEUNPTU9ETyBDQSBMaW1pdGVkMTYwNAYD\
    VQQDEy1DT01PRE8gUlNBIERvbWFpbiBWYWxpZGF0aW9uIFNlY3VyZSBTZXJ2ZXIg\
    Q0EwHhcNMTgxMjEwMDAwMDAwWhcNMTkxMjEwMjM1OTU5WjBiMSEwHwYDVQQLExhE\
    .......\
    ......\
    .....\


    \-----END CERTIFICATE-----
3. save it as `leaf.crt`
