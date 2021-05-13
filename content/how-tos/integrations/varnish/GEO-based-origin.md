---
title: Configure GEO-based origin selection
description: Use VCL to configure a layer 7 load balancer for differnet GEO locations.
keywords: content delivery network, CDN, load balancer, VCL, HTTP
aliases:
  - /modules/varnish-cache/how-tos/geo-based-origin/
  - /GEO-based-origin/
  - /topic-guides/load-balancer/geo-based-origin/
  - /modules/varnish-cache/reference/geo-based-origin/
---

## GEO based origin selection
Below is an example of how to configure your Content Delivery Grid to direct requests to different origins based on the requesting user's GEO location.

Prerequisites:

* Section account
* Section application running Varnish
* A separate origin with content for users of different GEO locations

In your `default.vcl` file you can set a header that's recognizable in Section `last-proxy` to determine which origin address and host header to make the request with. So you are going to need to define that origin first in your `section.config.json` file located in the root of your applications git repo. You will be adding a key called `alternate_origins` under `environments.Production`.

#### `section.config.json`

    ...
    "environments": {
        "Production": {
            "origin": {
                "address": "203.0.113.1"
            },
            "alternate_origins": {
                "US_origin": {
                    "address": "203.0.113.2"
                },
                "AU_origin": {
                    "address": "203.0.113.3"
                }
            }           
        },
    ...

#### `default.vcl`

Next we tell Varnish Cache to use this origin for requests depending on the GEO IP country code. Use the origin names defined in `section.config.json`.

    sub vcl_recv {
        ...
        if ( req.http.section-io-geo-country-code ~ "(?i)^(US|CA)$" ) {
            set req.http.section-origin = "US_origin";
        } elsif ( req.http.section-io-geo-country-code ~ "(?i)^(AU|NZ)$" ) {
            set req.http.section-origin = "AU_origin";
        }
        ...
    }

*Note 1:* Requests not from US/CA/AU/NZ will be directed at the default origin of `203.0.113.1`.
*Note 2:* If you are caching responses, make sure to `hash_data(req.http.section-origin)` to split the cache based on origin.

#### Overview

This use case is especially helpful if you are serving unique content to different geographic locations, such as offers only available in certain regions or pages in different languages or currencies or just to keep load separated between different origins. Section handles all the internals of actually making the request to origins for each region and all you have to do is configure your reverse proxy setup in your git repo!
