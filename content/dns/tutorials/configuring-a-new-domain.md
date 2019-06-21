---
title: Configuring a new domain
description: How to configure a new domain under an existing Section application.
keywords: dns, domain configuration
---

## Overview

This tutorial will walk you through the steps needed to add a domain to an existing Section application. If you wish to set up an entirely separate application for this domain please follow the [getting started guide]({{< relref "getting-started/tutorials/going-live" >}}).

### Step 1 - Adding the domain

1. Navigate to the **DNS** section of your existing Section application.
1. Click the **Add domain** button and input the desired domain.
1. Hit save.

This will configure the Section platform to route all requests for your desired domain through this applications module stack.

### Step 2 - Configuring DNS

You will need to make the DNS record for the domain you added point to the CNAME record automatically generated for that specific domain for traffic to flow through the Section platform.

Assume we added **www.example.com**

1. Navigate to your DNS hosting provider.
1. Add a CNAME record for **www.example.com**
    * The value will be **www.example.com.c.section.io**
1. Save your changes.

You can test these configurations by utilizing [dig](https://linux.die.net/man/1/dig) to perform a DNS lookup to ensure the domain is pointed to your Section record. You can also use a web based tool to [perform DNS lookups](https://www.whatsmydns.net/#CNAME/www.example.com).

Example dig command: `dig +trace www.example.com @8.8.8.8`

{{% notice note %}}
All domains added to the Section platform will generate a unique CNAME record. This CNAME record follow the naming convention domain.c.section.io.
{{% /notice %}}

### Step 3 - SSL Certificate

Follow the how to guide on [provisioning an SSL certificate]({{< relref "https/how-tos/create-a-free-tls-certificate-using-letsencrypt.md" >}}).
