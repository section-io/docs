---
title: Generate a 404 response 
description: Guide to deliver a synthetic http 404 or 410 response using Varnish Cache.
keywords: varnish, Varnish Cache , cache, cached data, synthetic, redirect, 301, 302
aliases:
  - /modules/varnish-cache/how-tos/respond-with-a-404/
---

## Overview

Varnish Cache allows you to create synthetic HTTP responses with the use of [vcl_synth](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-synth). This can be used to deliver a 404 not found or 410 permanently removed status code for a particular asset.

## VCL syntax

Below is an example of how to deliver a synthetic 404 response using VCL syntax 4.0. This example will deliver a 404 response if the request matches the URI path "/hello.jpg"

{{< highlight js >}}
sub vcl_recv {
    if (req.url ~ "/hello.jpg") {
        return (synth(804, "Not Found"));
    }
}

sub vcl_synth {
    if (resp.status == 804) {
        set resp.status = 404;
        return (deliver);
    }
}
{{< / highlight >}}

Note: You can use 410 instead of 404 to deliver a [HTTP 410](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/410)
