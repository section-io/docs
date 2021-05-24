---
title: Device based origin selection
description: Use VCL to configure a layer 7 load balancer for different devices.
keywords: content delivery network, CDN, load balancer, VCL, HTTP
aliases:
  - /modules/varnish-cache/how-tos/device-based-origin/
  - /modules/varnish-cache/how-tos/deliver-a-synthetic-response/
  - /Device-based-origin/
  - /topic-guides/load-balancer/device-based-origin/
  - /modules/varnish-cache/reference/device-based-origin/

---

## Device based origin selection

Below is an example of how to configure your Content Delivery Grid to direct requests to different origins based on the requesting user's device type.

Prerequisites:

* Section account
* Section application running Varnish
* A separate origin with content for different devices

In your `default.vcl` file you can set a header that's recognizable in Section `last-proxy` to determine which origin address and host header to make the request with. So you are going to need to define that origin first in your `section.config.json` file located in the root of your applications git repo. You will be adding a key called `alternate_origins` under `environments.Production`.

#### `section.config.json`

    ...
    "environments": {
        "Production": {
            "origin": {
                "address": "203.0.113.1"
            },
            "alternate_origins": {
                "mobile_device": {
                    "address": "203.0.113.2"
                }
            }           
        },
    ...

#### `default.vcl`

Next we tell Varnish Cache to use this origin for requests if we detect the User-Agent as a mobile device. Use the origin names defined in `section.config.json`.

    sub devicedetect {
        # The VCL here is just an example, it is not a exhaustive device detection logic.
        if (req.http.User-Agent ~ "(?i)samsung|iphone|ipod|pixel") {
            set req.http.device-type = "mobile";
        }
    }

    sub vcl_recv {
        ...
        call devicedetect;
        if ( req.http.device-type == "mobile" ) {
            set req.http.section-origin = "mobile_device";
        }
        ...
    }

*Note 1:* Requests from non-mobile devices will be directed at the default origin of `203.0.113.1`.
*Note 2:* If you are caching responses, make sure to `hash_data(req.http.section-origin)` to split the cache based on origin.

#### Overview

This use case is especially helpful if you are serving unique content to different devices or just to keep load off your default origin when the request is from a mobile device. Section handles all the internals of actually making the request to your `mobile_device` origin and all you have to do is configure your reverse proxy setup in your git repo!
