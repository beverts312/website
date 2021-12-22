---
title: OpenSSL
type: docs
---

[OpenSSL](https://www.openssl.org/) is a powerful CLI for working with certificates.  

|Description| Command |
|----------|---------------------------------|
|Read cert | `openssl x509 -in cert.pem -text` | 
|Create domain key | `openssl genrsa -out <your-domain>.key <2048 or 4096>` |
|Create a CSR | `openssl req -new -sha256 -key <your-domain>.key -out <your-domain>.csr` |  
|Create a Self Signed Cert | `echo 01 | sudo tee ca.srl > /dev/null && openssl req -newkey rsa:4096 -nodes -sha256 -keyout domain.key -x509 -days 365 -out domain.crt` |
