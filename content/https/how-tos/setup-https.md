---
title: Set up HTTPS and HTTP/2
description: Guide for adding HTTPS and HTTP/2 to your website with Section using your own certificate or using our automated SSL certificates.
keywords: https, SSL, TLS, Let's Encrypt, EV, Extended Validation, SNI, Server Name Indication, website security, content delivery network, CDN
aliases:
  - /setup-https/
  - /how-to/setup-https/

---

When your application is first created it will be served over HTTP and via HTTPS using a default network certificate. Once we detect DNS has been changed on to our platform we will provide a signed and valid certificate through [Let's Encrypt](https://letsencrypt.org/).

If you have added [multiple domains](/docs/change-dns/#multiple-domains) to the application, a Let's Encrypt certificate will be provided for each domain. If you have provided your own custom certificate, you need to upload a certificate for each domain (even if they are listed as alternate names on the same certificate) using our [API](#certificate-api-upload). You can choose to upload a custom certificate for only some of the domains in the application if you choose, the others will use the Let's Encrypt certificate issues by Section.

Each certificate has a short validity period and will be renewed 30 days prior to expiry. If you require wildcards, multi hostname or extended validation (EV) certificates you will need to provide your own certificate.

## Add custom certificate through Section Console

To use a custom certificate for your application you will need to obtain a certificate and private key pair. For production use you should use a certificate signed by a trusted root Certificate Authority (CA). In development scenarios, you may find a [self-signed certificate is sufficient](https://en.wikipedia.org/wiki/Self-signed_certificate) ([Beginners guide](https://www.ssl.com/faqs/faq-what-is-ssl/)) ([Certificate Generation](https://www.thenativeweb.io/blog/2017-12-29-11-51-the-openssl-beginners-guide-to-creating-ssl-certificates/))

### 1) Get your properly-formatted certificate

You will need to ensure you have the public certificate in Base64-encoded DER-encoded (PEM) format. It will look something like this:

    -----BEGIN CERTIFICATE-----
    MIIF6DCCBNCgAwIBAgIQBBHej1O0YvalqGG3EuxrWTANBgkqhkiG9w0BAQsFADBw
    MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3
    ...
    tOiS1jXb8xWWRRZyxrZbpaybPN3qkrNdqxBlyuPIy2u0UKYuovcup8a9x7ZfoJsB
    I5JUNzQIPHaH0kP40DdTBNmczS4UiWaoY3pnlw==
    -----END CERTIFICATE-----

We have omitted most of the lines in the example but expect 30 or more in yours.

### 2) Specify any intermediate certificates

If your certificate is signed by a Certificate Authority, then it will typically have been signed by an intermediate certificate or two, not by the CA root certificate. As an example, the certificate chain for www.example.com looks like this:

    DigiCert (the CA root)
     \- DigiCert SHA2 High Assurance Server CA (an intermediate cert)
         \- www.example.com (the end-entity cert)

If you have any intermediate certificates in your chain you should have them in a separate file. You can and should omit the root certificate.

The certificate chain for www.example.com result would look like this:

public certificate at the top:

    -----BEGIN CERTIFICATE-----
    MIIF6DCCBNCgAwIBAgIQBBHej1O0YvalqGG3EuxrWTANBgkqhkiG9w0BAQsFADBw
    MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3
    ...
    tOiS1jXb8xWWRRZyxrZbpaybPN3qkrNdqxBlyuPIy2u0UKYuovcup8a9x7ZfoJsB
    I5JUNzQIPHaH0kP40DdTBNmczS4UiWaoY3pnlw==
    -----END CERTIFICATE-----

followed by any intermediate certificate(s):

    -----BEGIN CERTIFICATE-----
    MIIEsTCCA5mgAwIBAgIQBOHnpNxc8vNtwCtCuF0VnzANBgkqhkiG9w0BAQsFADBs
    ...
    0wGjIChBWUMo0oHjqvbsezt3tkBigAVBRQHvFwY+3sAzm2fTYS5yh+Rp/BIAV0Ae
    cPUeybQ=
    -----END CERTIFICATE-----

Again most lines have been omitted and replace with ...

The last input you require is your certificate’s corresponding RSA private key in PEM format. It will look slightly different, something like this:

    -----BEGIN RSA PRIVATE KEY-----
    MIICXAIBAAKBgQCqGKukO1De7zhZj6+H0qtjTkVxwTCpvKe4eCZ0FPqri0cb2JZf
    wmJG8wVQZKjeGcjDOL5UlsuusFncCzWBQ7RKNUSesmQRMSGkVb1/3j+skZ6UtW+5
    ...
    U9VQQSQzY1oZMVX8i1m5WUTLPz2yLJIBQVdXqhMCQBGoiuSoSjafUhV7i1cEGpb8
    37sJ5QsW+sJyoNde3xH8vdXhzU7eT82D6X/scw9RZz+/6rCJ4p0=
    -----END RSA PRIVATE KEY-----

It is important that the private key is **not password protected**. Also, unlike the default for some Base64 encoding tools, the line length must be 64 characters.

In most scenarios the openssl software can help produce the required files and convert them to the appropriate format.

### 3) Install the certificate in Section

Once you have your certificate and key in the formats described above, you can install them into Section.

Log in to [Aperture](https://aperture.section.io) for your application, and in the sidebar under the **Set up** header select **HTTPS**. Copy & paste the certificate files you prepared earlier into the input boxes as labeled, then click *Save Changes*. Make sure the certificates are in the proper order. For help on that, check out [our guide] (/docs/how-to/https/determine-tls-certificate-order)

This will deploy your certificate out to our delivery nodes.

Once you have saved your public certificates and private key, when you come back to the HTTPS page the private key will not be displayed on screen as it would be a security risk to display it.

## Upload a certificate using the API

### 1) To add an additional domain certificate  to your application via the API

`POST /account/{accountId}/application/{applicationId}/environment/{environmentName}/domain/{hostName}`

Note: Domains can only be added to a root application (ie pathPrefix of /). Domains added to this application's environment will also be used for the corresponding environment in the sub-apps.

If there is no body payload, the domain name will have a Let's Encrypt certificate provisioned for it. A custom certificate can be provided in this format:

    {
        "public_certificates": "string",
        "private_key": "string"
    }

### 2) To remove a domain via the API

`DELETE /account/{accountId}/application/{applicationId}/environment/{environmentName}/domain/{hostName}`

To add a custom certificate to an existing domain via the API:

`POST /account/{accountId}/domain/{hostName}/https`

with the following body payload:

    {
        "public_certificates": "string",
        "private_key": "string"
    }

### Server Name Indication

Parts of the Section platform are using shared infrastructure. One component important in this context is the TLS Offload Proxy, implicit in all Proxy Stacks. Its role is to accept end-user HTTP and HTTPS connections for multiple web applications on multiple domains, handle any TLS handshake and then route requests to the correct Proxy Stack.

For non-HTTPS requests, routing is easily performed by parsing the Host header present in any standard HTTP/1.1 request. For HTTPS it is a little more complicated.

Traditionally during an [SSL/TLS handshake](https://developer.mozilla.org/en-US/docs/Introduction_to_SSL#The_SSL_Handshake), the server provides its certificate (containing the domain names) to the client before the client has indicated which domain (or Host) its request is intended for.

Thankfully TLS has since introduced the Server Name Indication [SNI](http://en.wikipedia.org/wiki/Server_Name_Indication) extension which provides a mechanism for the client to specify the intended Host of its request before the server responds with its certificate. SNI allows the TLS Offload Proxy in Section to select the correct certificate to supply to the client and then continue routing the request to the correct Proxy Stack just as per a plain HTTP request.

When a certificate is provided in an application’s section.config.json file it is being used for HTTPS requests from SNI-enabled clients only. Some clients, eg old mobile browsers and most Windows XP browsers, do not support SNI and will not be able provide the necessary information for Section to offer the correct certificate for HTTPS requests.

By default these clients will receive a fall-back certificate which is not valid for the Host their request is intended for and these clients will report a security error. If you need to support older non-SNI-capable clients, contact Section support to discuss adding your application’s Host name to the fall-back certificate.
