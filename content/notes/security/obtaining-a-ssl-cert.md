---
title: Obtaining a SSL Certificate 
type: docs
---

There a a variety of ways to obtain a 
Most domain registrars will sell you an ssl cert for anywhere from $5 to $30 a year.  

A friend recently showed me [ZeroSSL](https://zerossl.com/) which provides FREE certificates and you can do the whole process in your browser with a few clicks. 
The only downside is they expire after 90 days. If you are trying to get a certificate so that you can use a custom domain with AWS Api Gateway (which is not integrated with there Certificate Management Service or Route53 as of Nov 2016), you will need to generate your CSR locally and you can do the rest of the steps from the ZeroSSL UI. This is because ZeroSSL by default provides 4096-bit keys and AWS requires 2048-bit keys.  

## Obtaining a cert for use with Amazon API Gateway  
First off its pretty frustrating Amazon hasn't integrated route53, api gateway, and cloudfront properly so that this is just a few clicks...but its not that go so here is the quick and dirty version:

To do this:  
1. Create a domain key - `openssl genrsa -out <your-domain>.key 2048`  
2. Create the CSR - `openssl req -new -sha256 -key <your-domain>.key -out <your-domain>.csr`  
3. Go to the [online tool](https://zerossl.com/free-ssl/#crt)  
4. Paste in your CSR  
5. Click Next and verify that it properly extracts the domain(s) you want from the CSR  
6. You will need to verify your domain ownership, form me DNS was an easier approach (I use route53)  
7. Click next a few more times and you can download your cert  
When you go to add the cert in AWS you will see it asks for a "certificate chain", wtf is this I asked myself. 
Turns out this is packaged in your cert you downloaded. 
The top section is your "certificate body", bottom section is "certificate chain", "certificate private key" is the thing you created in step 1.
