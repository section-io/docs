---
title: Block a request
description: Guide to block a request using Varnish Cache.
keywords: varnish, Varnish Cache, block, 403

---

## Overview

Varnish Cache allows you to create synthetic HTTP responses with the use of [vcl_synth](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-synth). This can be used to deliver a [403 forbidden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403) status code. These config changes are typically made under **Advanced Config -> varnish -> default.vcl** for the respective branch.

## VCL syntax

Below is an example of how to deliver a synthetic 403 response using VCL syntax 4.0. This example will deliver a 403 response if the request matches the URI path "/admin":

{{< highlight js >}}
sub vcl_recv {
    if (req.url ~ "/admin") {
        return (synth(803, "Forbidden"));
    }
}

sub vcl_synth {
    if (resp.status == 803) {
        set resp.status = 403;
        return (deliver);
    }
}
{{< / highlight >}}

{{% notice note %}}
This is just an example of how to block a request using Varnish Cache. You can utilize many different patterns to block a request. E.g. check for user agents, country codes (example below), IP addresses, etc.
{{% /notice %}}

### Blocking traffic based on GEO Region

The section.io platform performs GEO region lookup at the Edge and sets a custom header `section-io-geo-country` that contains the ISO 3166-1 alpha-2 country code such as US for the United States, or AU for Australia. There are also a number of other header that are set which can be useful. 
See: https://www.section.io/docs/edge-proxy/#ip-geolocation 

You can then use the `section-io-geo-country` header to block traffic in Varnish.

{{< highlight js >}}
sub vcl_recv {
	if(req.http.section-io-geo-country == "XX") {
		return (synth(403, "Forbidden"));
	}
}
{{< / highlight >}}

Replace XX with the country code to block.You can block multiple countries by using | e.g.req.http.section-io-geo-country == "XX|YY|ZZ"
