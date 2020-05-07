---
title: Sample Varnish Cache Snippets
description: A collection of Varnish Cache snippets to help get your Varnish Cache proxy up and running.
keywords: [Varnish, snippets, caching, HTTPS, blocking, Wordpress]
aliases:
  - /threat-x/
  - /topic-guides/advanced-config/sample-varnish-snippets/
---

## Varnish Cache Configuration

Advanced configuration is done via the Varnish Cache Control Language file `default.vcl`. You can access this file by going to Repository under the Configuration menu in the left nav of Section Console and then clicking on the Varnish Cache file.

To help you get started, we've written some VCL snippets that cover some basic aspects of functionality for you to review.

#### Cache Static Content

{{< gist section-io-gists 2a9e40238fffec56d3be >}}

#### Normalise Accept-Encoding

{{< gist section-io-gists 8ea78c06271d7e824431 >}}

#### Enforce HTTPS

{{< gist section-io-gists 02dba4113b8caf5da473 >}}

#### Block Access

{{< gist section-io-gists 12e0e35369e3b95ed996 >}}

#### Cache Everything

{{< gist section-io-gists 56391f3af9dff65dda36 >}}

#### Wordpress Caching

{{< gist section-io-gists 1a1ca70f1b0528442f8c >}}

For more information on how to write VCL, visit [Varnish](https://www.varnish-cache.org) documentation, where each version has its own user guide. Here is documentation for version [4.0](https://www.varnish-cache.org/docs/4.0/users-guide/vcl.html)
