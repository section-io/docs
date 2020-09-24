---
title: Optimize Bigcommerce with Section
description: A guide to optimize Bigcommerce on the Section platform.
keywords: bigcommerce, cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 10
aliases:
  - /how-to/bigcommerce/optimize/
  - /bigcommerce/optimize/
---

## Configure Caching and HTML Streaming


1.  Set the static caching and HTML Streaming features toggles to true.
```
sub vcl_recv {
    # Section feature toggles.
    if (!req.http.section-enable-static-caching) {
        set req.http.section-enable-static-caching = "true";
    }

    if (!req.http.section-enable-html-streaming) {
        set req.http.section-enable-html-streaming = "true";
    }
}
```

2.  Configure HTML Streaming by whitelisting paths.  
```
    # SWITCH for HTML streaming,
    if(req.http.section-enable-html-streaming == "true" && 
        (req.url ~ "(?i)^/(?=\?|&|$)" ||
         req.url ~ "\/sale\/shoes\/.*" ||
         req.url ~ "\/outlet\/promotion\/.*" || 
         req.url ~ "\/men\/new-arrivals\/.*" ||
         req.url ~ "\/outlet\/boys\/.*")){

```

## Location Optimization

Section can locate cached and HTML streamed content in the region closest to the customers end users. 

Such locations include:

1. Asia Pacific region.
2. Europe region.
3. North America region.

Contact Section support to for adjustments to locations: [contact us](/contact-us/).