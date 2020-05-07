---
title: Overview
description: Using the ThreatX Web Application Firewall (WAF) inside Section.
keywords: WAF, web application firewall, security, Layer 7 attacks
aliases:
  - /topic-guides/threat-x/
weight: 1

---

Because Section is the only CDN that allows you to choose the reverse proxies that run in your stack, you can choose to bring the Web Application Firewall created by the security experts at ThreatX into your web site's delivery infrastructure.

## About ThreatX

ThreatX is a reverse proxy that inspects and adapts to web site attacks that can infiltrate your web site and cause problems for your business.

Because ThreatX doesn't simply rely upon statically defined rule sets like old WAFs (and CDNs based on those old WAFs) you can expect a higher degree of security.

This also means that there's a lower cost to maintain that level of security, because the adaptive nature of the platform means that you don't need to spend time and money on in-house security experts to keep your rules up to date.

Of course, you can still rely on ThreatX for virtual patching, which is one of the most sought after features in a WAF.


## Other things to note

Naturally, you can see ThreatX is on your site by looking at the Overview page in Section Console, Section management console.

The Section platform writes a log for each HTTP request that passes through ThreatX. These will be available in our powerful Kibana interface alongside logs from all of the other proxies in your stack.
