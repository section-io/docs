---
title: Determine TLS Certificate Order
description: How to determine custom TLS certificate order
keywords: SSL, certificate, custom, upload, update, CDN configuration
aliases:
  - /https/how-tos/determine-tls-certificate-order/
  - /how-to/https/determine-tls-certificate-order/
  - /ssl/how-tos/determine-tls-certificate-order/ 
---
## Getting started

Download or unzip the certificates in to a directory somewhere on your computer.
The certificates should be PEM encoded and will look like the following in a text editor.

    -----BEGIN CERTIFICATE-----
    /* contents of certificate */
    -----END CERTIFICATE-----


You will require Openssl to be installed. To check if you have Openssl installed, open a command prompt and type:

    openssl version

You should see output like `OpenSSL 1.0.2l  25 May 2017`

In your command prompt go to the directory where you placed the certificates.


## Determine domain certificate

You will need to determine which certificate is the one issued to your site(s).

Run the following command in your command prompt window where `certificate1.pem` is the file name of a certificate you are testing:

    openssl x509 -noout -subject -in certificate1.pem

If the certificate is the site certificate, you will see the domain of your site in the output. e.g.

    subject= /CN=www.yoursite.com


If your domain is listed as a Subject Alternate Name(SAN) on a certificate you won't see it under subject using the above method.
You will need to examine the rest of the certificate.

For linux/mac based command prompt, run:

    openssl x509 -text -noout -in certificate1.pem | grep "DNS"

For windows based command prompt, run:

    openssl x509 -text -noout -in certificate1.pem | findstr "DNS"

You should see a list of SAN domains on that certificate. If that list contains your domain name, then this certificate is your domain certificate.


## Determine intermediate certificate order

Each certificate contains information about its issuer. The issuer is the next link in the SSL chain.
The SSL chain will be `domain certificate -> intermediate ceritificate(s) -> root certificate`

Determine the intermediate certificate of your domain certificate by examining the issuer of your domain cert with the following command.

    openssl x509 -noout -issuer -in certificate1.pem

You should see output such as `issuer= /C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3`

Then you can compare this against the subject of the other certificate files to find one that matches the issuer above.

    openssl x509 -noout -subject -in certificate2.pem

If this is the correct intermediate certificate, you will see a matching subject to the issuer of the domain certificate. `subject= /C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3` This is your first intermediate certificate. So the certificate chain so far is `certificate1.pem -> certificate2.pem`.

Now look at the issuer of certificate2.pem

    openssl x509 -noout -issuer -in certificate2.pem

If this is the only intermediate certificate in the chain, the issuer will result in a Root issuer e.g. `issuer= /O=Digital Signature Trust Co./CN=DST Root CA X3`. If you don't see an issuer that contains "Root CA" then there is likely another intermediate certificate. Examine the issuer of each certificate you have and match it with the subject of the next intermediate certificate until you see the issuer is a Root CA. This resulting order is your SSL chain.
