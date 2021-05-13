---
title: DNS with multiple domains
description: Guide for configuring DNS with multiple domains.
keywords: DNS, DNS records, DNS hosting, multiple domains
aliases:
  - /dns/reference/dns-with-multiple-domains/
  - /dns/
  - /hosted-dns/
  - /change-dns/
  - /how-to/dns/dns-with-multiple-domains/

---

The Section platform will only accept requests with a domain name that is explicitly added to an environment. For example, if you add www.example.com to Section as **www.example.com** but then choose to create a **blog.example.com** CNAME record pointing at **www.example.com.c.section.io.**, visitors to `http://blog.example.com` will receive an error page displaying **HTTP 409 Conflict**.

This is because blog.example.com has not been explicitly associated with a Section environment.In this case you would need to add **blog.example.com** to a Section environment and then create a **blog.example.com.c.section.io** CNAME record for **blog.example.com** in your DNS hosting console. The same is true if you register a bare domain record such as **example.com**. Each domain must be specified in full in order for the request to be accepted by Section.  

If you would like your Section application to respond to multiple domains, you can add them on bottom of the the Domains page under *Domains*. You can also add or delete additional domains via our API by using the following commands:

`POST /account/{accountId}/application/{applicationId}/environment/{environmentName}/domain/{hostName}`

`DELETE /account/{accountId}/application/{applicationId}/environment/{environmentName}/domain/{hostName}`

Please review our [HTTPS setup page](/docs/setup-https) to ensure all of your domains are properly covered by either our automated HTTPS or your own custom certificates to prevent certificate errors.

If the additional domain names should redirect to the canonical domain name to improve search engine ranking, this can be achieved with a basic Varnish Cache configuration, for example:

    vcl 4.0;

    sub vcl_recv {
      return (synth(700, ""));
    }

    sub vcl_synth {
        if (resp.status == 700) {
            set resp.status = 302; # or 301 if preferred
            set resp.http.Location = "https://canonical-domain.example.com" + req.url;
            return(deliver);
        }
    }
