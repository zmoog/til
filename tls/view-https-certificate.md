# View HTTPS Certificate

Sometime it is useful inpect the certificate used by a website or API endpoint:

```shell
$ openssl s_client -connect arduino.cc:443 < /dev/null | openssl x509 -noout -text
depth=3 O = Digital Signature Trust Co., CN = DST Root CA X3
verify return:1
depth=2 C = US, O = Internet Security Research Group, CN = ISRG Root X1
verify return:1
depth=1 C = US, O = Let's Encrypt, CN = R3
verify return:1
depth=0 CN = arduino.cc
verify return:1
poll errorCertificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:19:ff:2f:2d:d1:c5:71:5c:3e:6a:3e:ee:1d:8b:31:5b:37
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=US, O=Let's Encrypt, CN=R3
        Validity
            Not Before: Jul 13 12:16:57 2021 GMT
            Not After : Oct 11 12:16:56 2021 GMT
        Subject: CN=arduino.cc
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:c1:ff:10:5a:4f:da:cb:1c:a6:b7:4c:00:01:89:
                    b0:e2:d7:00:17:05:93:ab:b8:c8:75:57:46:e6:c8:
                    9e:b3:e4:c9:7d:3e:8e:df:91:98:04:87:da:24:7d:
                    5b:2d:75:55:94:e1:c9:b7:6b:95:03:2d:24:4a:7f:
                    2a:63:7b:85:ab:d2:e6:d7:ff:1e:8b:b9:d9:d5:9a:
                    55:b4:b4:2d:68:0a:02:e1:73:be:11:49:8c:2e:71:
                    8b:53:d9:86:d4:12:d4:62:46:86:49:e8:98:6c:35:
                    2e:8c:dc:78:1d:2d:97:cf:f7:49:0f:c4:14:c8:4c:
                    0d:57:54:8a:f9:c9:f3:cc:bb:2f:e1:f5:12:34:95:
                    88:37:7e:12:cf:63:7c:8a:25:4e:7e:70:5f:8f:7b:
                    71:de:aa:1d:31:cd:88:26:83:c9:67:f5:17:c7:46:
                    fe:aa:47:3e:68:89:5b:fd:04:32:35:f4:3f:72:e5:
                    1a:5b:78:d3:a7:19:85:06:97:38:d2:a1:f9:59:1d:
                    a5:58:4b:fd:30:b6:30:15:45:29:4e:af:5d:cc:30:
                    e5:4a:ac:e3:12:68:43:5f:04:9e:ec:bd:1a:67:1a:
                    17:67:c7:8e:2f:b0:d6:59:1d:b7:e2:9e:5f:0d:ba:
                    89:b7:e3:f9:52:c8:ce:21:64:40:fa:b2:7b:75:03:
                    6b:81
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage: 
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier: 
                90:80:54:7A:9B:38:62:E9:05:B1:13:CE:B1:30:43:3B:B4:84:C0:E9
            X509v3 Authority Key Identifier: 
                keyid:14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6

            Authority Information Access: 
                OCSP - URI:http://r3.o.lencr.org
                CA Issuers - URI:http://r3.i.lencr.org/

            X509v3 Subject Alternative Name: 
                DNS:arduino.cc
            X509v3 Certificate Policies: 
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
                  CPS: http://cps.letsencrypt.org

            1.3.6.1.4.1.11129.2.4.2: 
                ......v.\.C....ED.^..V..7...G..s..^........z..q......G0E.!.........~<.7.7*n~sS.PS.....B..... 4.Q.&G.qO..02m.F..|^!.....v.@.iE.w..\./.w0".T..0.V..M..3.../ ..N.d....z..p......H0F.!..y......(>,.A.....+'...9P<pf...e.!....C@..2..\Wen.t.>.5...w......,F
    Signature Algorithm: sha256WithRSAEncryption
         03:cf:23:c1:da:d0:ed:72:77:20:f5:33:e6:13:3b:50:fa:1e:
         ec:6f:38:54:2c:fb:22:19:8b:66:28:f9:31:3d:3d:ca:9a:a4:
         4c:8a:34:15:31:a1:63:43:f5:ae:b1:4d:ee:b5:9f:d5:a7:81:
         fd:cc:14:74:fc:cb:1a:d1:c8:93:73:e5:51:0b:71:d6:ae:02:
         b0:eb:f4:53:14:d8:ea:76:4a:a2:4f:d6:1c:2b:d2:a9:63:6b:
         67:be:76:f1:98:d5:e3:99:3e:c7:75:4f:33:8e:4d:ad:16:60:
         b0:1d:c4:c5:de:1c:c6:be:5e:b2:ca:ae:ec:65:f0:2c:ae:a5:
         84:03:fb:d6:2a:07:71:a5:b6:69:7c:df:48:c6:52:5f:12:0c:
         0b:17:a9:d4:7e:cb:f4:50:9c:fd:1e:65:00:0b:d4:71:33:b6:
         62:76:4c:e5:6b:29:cf:34:79:f4:54:6e:7d:75:ef:61:7b:62:
         55:cf:63:8a:78:3e:45:6a:a4:07:22:58:1a:9a:b3:14:83:9a:
         07:e1:7e:c5:c5:ca:df:26:f4:ac:f7:c6:d5:1a:f5:db:69:78:
         32:49:da:76:19:f0:2b:63:7c:c5:d5:05:4f:d7:0a:cc:b2:88:
         18:6e:e8:f5:f3:8d:06:13:ab:d0:52:92:78:63:30:cc:b3:d2:
         bb:9f:97:db
```
