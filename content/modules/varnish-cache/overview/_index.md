---
title: Overview
description: A high level overview of how Section runs Varnish Cache
keywords: [Varnish,caching]
aliases:
  - /topic-guides/section-and-varnish/
weight: 1
---

## How Varnish Cache works on Section

Section implements a pure and unchanged version of the Varnish Cache.

At every opportunity, the implementation of Varnish Cache on the Section platform has been designed to be as close as possible to how it would be if you had installed Varnish Cache yourself locally.

Section uses the official Varnish Cache distributions published by Varnish Cache. Section does not use custom-compiled builds of Varnish Cache.

Varnish Cache is started, listening on port 80.

Varnish Cache VCL can found in the **default.vcl** file in the corresponding subdirectory of your Section application repository.

Assuming Varnish Cache is the first proxy in your proxy stack, Varnish Cache will receive connections from the **Section TLS Offload Proxy** with two additional HTTP request headers.

1. **X-Forwarded-For** containing the downstream client IP address and any intermediate proxy IP addresses.
2. **X-Forwarded-Proto** which will specify either HTTP or HTTPS depending on the protocol with which the downstream client connected.

Issuing cache invalidation requests to Varnish Cache sends a ban command to the Varnish Cache management interface. Section accepts any valid Ban expression and passes it to Varnish Cache unaltered.

We also provide some convenience tools to help with removing particular URL's from the cache, see our [Cache Clearing]({{< relref "modules/varnish-cache/how-tos/clearing-the-cache.md" >}})  documentation for more details.

Requesting the Varnish Cache Log executes varnishlog for each Varnish Cache instance and returns the results.

varnishncsa is also running, logging request and response details, including cache effectiveness. This data is used to drive the charts seen in Section Console.

### Table of contents

{{% children page="modules/varnish-cache" depth="3" %}}
