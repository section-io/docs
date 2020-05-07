---
title: Create a Free Certificate using Let's Encrypt
description: How to provision a free SSL certificate in Section portal.
keywords: SSL, certificate, custom, upload, update, CDN configuration
aliases:
  - /how-to/https/create-a-free-tls-certificate-using-letsencrypt/
  - /ssl/how-tos/create-a-free-tls-certificate-using-letsencrypt/
---

## Get started

Log into your Section Console dashboardand under **Set up** navigate to the **HTTPS** page.

{{< figure src="/docs/images/https/https-aperture.gif" title="HTTPS in Section Console" >}}


## Select domain

{{< figure src="/docs/images/https/https-pulldown.gif" title="HTTPS Pulldown" >}}

The SSL information for the first domain in this application will automatically load. If you have setup multiple domains on a single application, click the drop down box "Select your domain" and select the domain you wish to upload a certificate for. 

## Provision certificate

Click the "**Renew certificate**" button. 

If you previously used a custom certificate, click the "**Switch to Let's Encrypt**" button.
Let's Encrypt will run validation tests over the domain then provision a new certificate once validation is complete.

If you have only recently performed [Go-Live ]({{< relref "getting-started/tutorials/going-live/_index.md" >}}) (pointed DNS at Section) the validation process might require multiple attempts, as DNS propagation can take some time. So if your free certificate doesn't provision straightaway, click the "Renew certificate" button again in a few minutes. If it still doesn't provision after 3 or 4 attempts, contact our support team. 

Once the certificate has been provisioned, it will automatically renew every 3 months.

## AAAA DNS records 
Domains that use both A and AAAA records will need to remove the AAAA record before attempting to provision the certificate. 
This is because Section platform uses IPv4 and AAAA records are IPv6 which will be not pointing at Section platform leading to provision failure.