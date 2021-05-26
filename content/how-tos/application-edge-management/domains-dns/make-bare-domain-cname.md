---
title: Make bare domain CNAME records
description: Guide for creating CNAME records for bare domains.
keywords: DNS, DNS records, DNS hosting, bare domain, naked domain and root domain
aliases:
  - /how-to/dns/make-bare-domain-cname/

---

Bare Domains are DNS records without www, also called Zone Apex, Naked Domain and Root Domain. In order to go live on Section, you need to setup a CNAME record pointing to the Section platform. While this is simple to do for any subdomain such as www, creating a CNAME record for a bare domain can cause some problems. This is because a CNAME record trumps all other records and can cause issues with MX records — potentially leading to broken email etc.

There are several workarounds to this problem:

1.  Switch to running your site on “www”. This means that users will type in www.domain.com to get to your website. You would then setup a HTTP 301 redirect from the bare domain to the www version so that users (and SEO) are automatically redirected to the “www” site. With this configuration fully in place, the bare domain points to the origin, www points to Section, and the origin servers redirects to the www. For a deeper discussion of the impact of serving your website off of the www instead of the bare domain, see [this article](/docs/dns/reference/bare-domains/).

2.  Use a DNS provider that supports a special `ALIAS`/`ANAME` record type at the bare domain. These records are like CNAME records but do not cause the issues described above. If your DNS hosting provider does not support ALIAS/ANAME records, you can switch to [Section hosted DNS](/docs/dns/how-tos/set-up-dns-on-section/).

For technical background on CNAME’s and the bare domains see: [RFC 1034 section 3.6.2](https://tools.ietf.org/html/rfc1034#section-3.6.2).
