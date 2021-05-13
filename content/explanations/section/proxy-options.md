---
title: Proxy Options
weight: 5
aliases:
  - /getting-started/overview/developer-ready/
  - /tutorials/overview/proxy-options/
---

Unlike Legacy CDNs which generally are fixed on a single proxy, Section allows you to choose the proxies that suit your application architecture.

Depending on your needs, you can run a single module or combine multiple modules for enhanced performance benefit:

* **Performance**: Varnish Cache  (versions 3, 4, 5, 6). Google's PageSpeed. Nginx, and Nginx+Lua.
* **Scalability**: Varnish Cache . Nginx.
* **Availability**: Varnish Cache . Nginx+Lua.
* **Security**: ModSecurity. ThreatX. Signal Sciences.

These are just some of the reverse proxies that are available to you. Pick the right combination and painlessly change them as your requirements change.

All of these proxies are available throughout the entire [development lifecycle]({{< relref "explanations/section/developer-ready.md" >}}).
