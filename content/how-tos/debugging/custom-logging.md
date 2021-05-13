---
title: Custom Logging
description: Set up Section so that it can log custom information in Varnish
keywords: custom logging, logging, Edge logging, Varnish Cache logging, Kibana, Elastic Search, content delivery network, CDN
aliases:
  - /debugging/how-tos/custom-logging/
  - /custom-logging/
  - /how-to/custom-logging/

---
#### A Guide to logging custom information using Varnish Cache or at the Edge.

To help with debugging Section allows several ways to log custom information then allow this information to be recorded and searchable in Kibana.

{{< youtube FpUrkuFI_uc >}}


#### 1) Log using HTTP response header

Any `section-io-tag` HTTP response header received by Edge will be logged and indexed in Kibana edge-access-log documents as the `section_io_tag` field. This header can be set by origin or any proxy upstream of Edge.

You will see it under `Edge-access-log` documents in Kibana as `section_io_tag`

{{% figure src="/docs/images/section_io_tag.png" %}}

This is a HTTP header and is therefore visible downstream, so care should be taken with what information is presented in this header to prevent security issues.


#### 2) Log using Varnish Cache std.log

Varnish Cache 4.1+ VCL can call `std.log("section-io-cache-tag:CUSTOM_VALUE_HERE");` in `sub vcl_deliver` and the value specified will be indexed in Kibana `varnish-ncsa-log` documents as the `section_io_cache_tag` field. This is not a HTTP header and is therefore not visible upstream or downstream. 

Here is an example usage where an origin response header named `origin-information` is captured and logged in `sub vcl_deliver` then removed so it is not visible downstream:
    
    import std;
    sub vcl_deliver {
        std.log("section-io-cache-tag:" + resp.http.origin-information);
        unset resp.http.origin-information;
    }


If the value of `origin-information` header was `Hello again!` you would see following in Kibana.

{{% figure src="/docs/images/section_io_cache_tag.png" %}}

Note: Varnish Cache is setup to only log these custom values from `sub vcl_recv` and `sub vcl_deliver`. Logging information from other subroutines such as `sub vcl_backend_response` will be ignored. 


