---
title: Redirect a request
description: Guide to deliver a synthetic http 301 or 302 redirect using Varnish Cache.
keywords: varnish, Varnish Cache , cache, cached data, synthetic, redirect, 301, 302
aliases:
  - /modules/varnish-cache/how-tos/redirect-a-request/
---

## Overview

Varnish Cache allows you to create synthetic HTTP redirect responses with the use of [vcl_synth](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-synth). 

## Redirect syntax

Below is an example of how to deliver a synthetic redirect 301 response using VCL syntax 4.0. This example will deliver a 301 response with a location header to redirect to "/world" if a request matches the URI path "/hello"

{{< highlight js >}}
sub vcl_recv {
    if (req.url ~ "/hello") {
        return (synth(801, "/world"));
    }
}

sub vcl_synth {
    if (resp.status == 801) {
        set resp.http.Location = resp.reason;
        set resp.status = 301;
        return (deliver);
    }
}
{{< / highlight >}}
