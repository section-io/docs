---
title: Clear Optidash cache
description: How to clear Optidash Cache?
keywords: Section, training, platform overview
weight: 1
aliases:
  - /modules/optidash/how-tos/how-to-clear-cache/
  - /modules/kraken/how-tos/how-to-clear-cache/
---


## Overview

There are two ways for clearing Optidash cache.

- Clear the entire Cache
- Clear a particular image from the cache.

### Clear the entire Cache

In the [advanced configuration](/docs/modules/optidash/how-tos/optidash-advanced-config/) settings for Optidash you can change the following parameter

`"cache_version" : "v1"`
Updating the "cache_version" will clear the entire Optidash cache.

### Clear a particular image from the cache.

To clear the cache for an individual URL you can use our API: https://aperture.section.io/api/ui/#!/Proxy/proxyStatePost with the `proxyName` as Optidash and the URL of the image as the `banExpression`.

You can also clear the cache for the URL using the Section Console (formerly known as Aperture portal). This feature is an option available under `Clear Cache > Optidash`

When using Optidash behind Varnish be sure to [clear the Varnish cache]({{< relref "/how-tos/module-integrations/varnish/clearing-the-cache.md" >}})  to see the updated image.

