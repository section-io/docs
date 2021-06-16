---
title: "Bare Domains"
description: "How to set up bare domains with the Section platform."
type: "docs"
aliases:
  - /dns/reference/bare-domains/
  - /threat-x/
  - /topic-guides/dns/bare-domains/
---

Bare domains (sometimes called naked domains, or apex domains) present a challenge to DNS, because they do not permit the use of CNAME records at the zone apex.

Your website runs on as a bare domain if you are using a name like `https://example.com`. Notice there is no prefix like "www." or "shop." before example.com.

In most situations, we recommend moving off your bare domain so that your website uses a prefix. There are advantages to doing this:

1. You'll get better manageability of your DNS.
1. Your security may be improved.

There's a good discussion on this topic here: https://www.yes-www.org/why-use-www/

## Common Misconceptions About Moving from a Bare Domain to a Subdomain

As engineers, here are some of the common questions we are faced with.

### My SEO people say that moving the domain will kill SEO

This isn't correct. If you redirect your bare domain traffic to a domain with a prefix (eg. HTTP redirect example.com to www.example.com) using HTTP 301 redirects, search engines will update their indexes accordingly.

### My marketing people say that "the brand" is the domain name without a prefix

This doesn't matter either. They can continue to use the bare domain in printed materials, and links on the Internet, without any effect on user experience, when HTTP 301 redirects are put in place.

## I Can't Convince the Team, and I Really Need Bare Domains

That's fine. There are some DNS providers that allow you to fake the CNAME at the zone apex.

Ask your DNS provider if they support `ALIAS` records. This is where the DNS provider actually does the CNAME lookup on the DNS server. So instead of responding with a CNAME record for the user to look up, they do the lookup first. They then respond with the A records.

If your DNS provider doesn't support `ALIAS` records, then you need to move DNS hosting. Section provides a high quality, global, anycast-based DNS service free of charge to our users. You could use our DNS hosting, or any provider that supports `ALIAS` records at the zone apex.

If you have any questions, please ask in the Community Slack Channel. Join us at https://yxorp.section.io.