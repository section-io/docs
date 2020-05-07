---
title: Clear Kraken cache
description: How to clear Kraken Cache?
keywords: Section, training, platform overview
weight: 1
---


## Overview

There are two ways for clearing Kraken cache.

- Clear the entire Cache
- Clear a particular image from the cache.

### Clear the entire Cache

In the [advanced configuration](/docs/modules/kraken/reference/kraken-advanced-config/) settings for Kraken you can change the following parameter

`"cache_version" : "v1"`
Updating the "cache_version" will clear the entire Kraken cache.

### Clear a particular image from the cache.

To clear the cache for an individual URL you can use our API: https://aperture.section.io/api/ui/#!/Proxy/proxyStatePost with the `proxyName` as Kraken and the URL of the image as the `banExpression`.
You can also clear the cache for the URL using the Section Console. This feature is an option available under `Clear Cache > kraken`

{{% figure src="/docs/images/kraken-cache-clear.png" %}}

When using Kraken behind Varnish be sure to [clear the Varnish cache]({{< relref "modules/varnish-cache/how-tos/clearing-the-cache.md" >}})  to see the updated image.
