---
title: Whitelist Section traffic to origin infrastructure
description: Whitelist Section traffic to origin infrastructure
keywords: whitelist, origin traffic
aliases: 
  - /platform/environment/how-tos/whitelist-section-traffic-on-origin/
---

### Overview

Section's platform runs on a multitude of hosting providers which means we do not provide a static set of IP addresses. This can be a problem if you wish to whitelist Section traffic to your origin infrastructure.

### Alternative method

If you wish to whitelist our servers we suggest using a shared secret key header that is send by Section's platform as part of all requests to the origin, and the origin can choose to block requests that do not have that header present.

The best way to achieve this is with [HTTP Basic Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication).

You can also use a secret key header like so (E.g. in VCL):

{{< gist section-io-gists 3851c1e787652a01c5178f40232eef05 >}}