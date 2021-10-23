# KeyChain
tags: #encryption #pki #signature

`KeyChain` class provides access to private keys and their corresponding certificate chains in credential storage.

Step to access
1. Receive callback from an `X509KeyManager` that a private key is requested.
2. Call `choosePrivateKeyAlias` to allow the user to select from a list of currently available private keys and corresponding certificate chains. The chosen alias will be returned by the callback `KeyChainAliasCallback#alias`, or null if no private key is available or the user cancels the request.
3. Call `getPrivateKey(Context, String)` and `getCertificateChain(Context, String)` ti retrieve the credentials to return to the corresponding `X509KeyManager` callbacks.

An application may remember the value of a selected alias to avoid prompting user again. If the alias is no longer valid, null will be returned on lookups using that value.

An application can request the installation of private keys and certificates via the `Intent` provided by `createInstallIntent()`. Private keys installed via this `Intent` will be accessible via `choosePrivateKeyAlias(Activity, KeyChainAliasCallback, String[],  Principal[], Uri, String)` while CA certificates will be trusted by all applications through default `X509TrustManager`.

## X.509 Certificates
Is the most well-known public-key certificates, version 3 defined in 1995. The structure:

This key pairs are used to authenticate the local side of a secure socket. During secure socket negotiations, implementations call methods in this interface to:
- determine the set of aliases that are available for negotiations based on the criteria presented.
- select the best alias based on the criteria presented.
- obtain the corresponding key material for given aliases.

X509ExtendedKeyManager should be used in favor of this class

![](attachments/Pasted%20image%2020211022201100.png)

Example:
```pem
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:04:54:08:f9:ff:10:92:e1:69:fe:49:8f:78:d3:6d:dc:47
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Let's Encrypt, CN = R3
        Validity
            Not Before: Jul 15 08:01:49 2021 GMT
            Not After : Oct 13 08:01:48 2021 GMT
        Subject: CN = *.wikipedia.org
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (256 bit)
                pub:
                    04:a5:9a:47:b2:d3:fc:a7:df:de:f6:cb:45:62:0a:
                    d3:c1:a7:38:de:20:bd:d7:10:7d:58:73:de:8d:a1:
                    99:70:0c:dd:ab:91:3f:0e:83:97:1b:4f:a2:99:f3:
                    f8:30:73:ef:da:be:91:25:18:7a:d6:da:bf:e5:e9:
                    72:a3:41:31:7a
                ASN1 OID: prime256v1
                NIST CURVE: P-256
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier:
                08:0E:29:26:07:E9:B4:5B:63:2D:86:5D:F6:E2:5A:8C:CD:6A:D0:A7
            X509v3 Authority Key Identifier:
                keyid:14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6

            Authority Information Access:
                OCSP - URI:http://r3.o.lencr.org
                CA Issuers - URI:http://r3.i.lencr.org/

            X509v3 Subject Alternative Name:
                DNS:*.m.mediawiki.org, DNS:*.m.wikibooks.org, DNS:*.m.wikidata.org, DNS:*.m.wikimedia.org, DNS:*.m.wikinews.org, DNS:*.m.wikipedia.org, DNS:*.m.wikiquote.org, DNS:*.m.wikisource.org, DNS:*.m.wikiversity.org, DNS:*.m.wikivoyage.org, DNS:*.m.wiktionary.org, DNS:*.mediawiki.org, DNS:*.planet.wikimedia.org, DNS:*.wikibooks.org, DNS:*.wikidata.org, DNS:*.wikimedia.org, DNS:*.wikimediafoundation.org, DNS:*.wikinews.org, DNS:*.wikipedia.org, DNS:*.wikiquote.org, DNS:*.wikisource.org, DNS:*.wikiversity.org, DNS:*.wikivoyage.org, DNS:*.wiktionary.org, DNS:*.wmfusercontent.org, DNS:mediawiki.org, DNS:w.wiki, DNS:wikibooks.org, DNS:wikidata.org, DNS:wikimedia.org, DNS:wikimediafoundation.org, DNS:wikinews.org, DNS:wikipedia.org, DNS:wikiquote.org, DNS:wikisource.org, DNS:wikiversity.org, DNS:wikivoyage.org, DNS:wiktionary.org, DNS:wmfusercontent.org
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
                  CPS: http://cps.letsencrypt.org

            CT Precertificate SCTs:
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : F6:5C:94:2F:D1:77:30:22:14:54:18:08:30:94:56:8E:
                                E3:4D:13:19:33:BF:DF:0C:2F:20:0B:CC:4E:F1:64:E3
                    Timestamp : Jul 15 09:01:49.274 2021 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:46:02:21:00:88:0F:F3:F1:BC:A3:AD:B8:7B:FD:C2:
                                A6:6A:4B:7C:1F:35:18:7B:3F:18:F6:43:29:46:F6:C2:
                                DD:15:63:C1:5D:02:21:00:CF:E0:1F:3D:E7:4A:37:C6:
                                CD:E5:BC:CD:99:FE:9C:F1:F7:EA:04:2D:97:DA:C2:74:
                                A6:30:37:57:F0:32:82:73
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : 6F:53:76:AC:31:F0:31:19:D8:99:00:A4:51:15:FF:77:
                                15:1C:11:D9:02:C1:00:29:06:8D:B2:08:9A:37:D9:13
                    Timestamp : Jul 15 09:01:50.105 2021 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:37:BC:8F:6A:BA:FA:AC:0B:3B:4C:3F:C8:
                                C2:AB:EA:3B:60:DE:A8:AB:44:72:E5:43:6A:E0:0A:24:
                                32:49:7F:30:02:20:11:AF:F7:67:43:81:07:C7:FB:B6:
                                89:55:0B:74:58:61:76:FB:62:FF:F4:C9:D0:C6:A7:43:
                                63:98:4C:F5:4C:7E
    Signature Algorithm: sha256WithRSAEncryption
         8e:f4:d1:85:9c:96:e8:63:d0:38:fd:7a:cc:d5:ad:b2:06:b4:
         4a:cf:3d:5a:b9:c2:28:3d:58:57:8a:55:42:ec:99:d3:ca:4f:
         ec:97:c0:10:73:77:43:5c:74:be:7e:2a:89:d8:fa:86:2f:8d:
         d3:57:99:67:3a:f6:28:6c:d1:26:29:ce:cf:7e:96:bd:34:0e:
         86:98:b3:0b:2e:28:dc:5b:46:77:32:a7:d9:b1:e6:de:e9:9a:
         2b:5d:03:f2:e0:07:12:03:d9:03:a8:ef:47:60:16:55:2a:32:
         53:c9:b3:4c:54:99:e0:98:d6:5f:1a:94:1c:6c:c5:e9:13:f7:
         08:c7:b6:b5:dd:d8:2b:b5:b7:2e:ba:cb:0b:2d:be:50:c6:85:
         0d:22:46:5e:e6:5f:b7:d4:86:45:d8:a4:bf:80:18:6e:46:96:
         d1:76:93:f5:40:e2:15:18:be:e0:cb:5f:cd:d0:4f:fa:ca:76:
         68:ba:94:c4:1d:1a:0e:3d:3b:ef:ed:1e:29:38:1d:22:bb:8b:
         96:71:55:b7:e4:8b:31:34:ec:63:09:e9:1c:d8:2f:f8:9a:b7:
         78:dc:33:c9:4e:84:85:03:0b:c5:52:af:9e:b0:6a:dc:fe:9e:
         89:2f:17:40:69:74:74:65:37:38:b4:28:23:01:01:81:19:23:
         23:cd:75:a0
```

Standard attributes of issuer:
* country,
* organization,
* organizational unit,
* distinguished name qualifier,
* state or province name,
* common name (e.g., "Susan Housley"), and
* serial number



