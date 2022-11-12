

### Windows Powershell


### Encryptying Insecure File Transfers

*Encrypt*

``` JavaScript
openssl enc -aes-256-cbc -pbkdf2 -k strongPass <input.txt >input.txt.enc
```

*Decrypt*

``` JavaScript
openssl enc -d -aes-256-cbc -pbkdf2 -k strongPass <input.txt.enc >input.txt
```



