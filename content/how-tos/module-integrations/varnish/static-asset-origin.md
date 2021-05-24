---
title: Configure static asset origin
description: Use VCL to configure a layer 7 load balancer for static assets.
keywords: content delivery network, CDN, load balancer, VCL, HTTP
aliases:
  - /modules/varnish-cache/how-tos/static-asset-origin/
  - /load-balancer/Static-asset-origin/
  - /topic-guides/load-balancer/static-asset-origin/
  - /modules/varnish-cache/reference/static-asset-origin

---

## Static asset origin

Below is an example of how to configure your Content Delivery Grid to direct all requests for static assets to a separate origin.

Prerequisites:

* Section account
* Section application running Varnish
* A separate origin for your static assets (e.g. S3 bucket)

In your `default.vcl` file you can set a header that's recognizable in Section `last-proxy` to determine which origin address and host header to make the request with. So you are going to need to define that origin first in your `section.config.json` file located in the root of your applications git repo. You will be adding a key called `alternate_origins` under `environments.Production`.

#### `section.config.json`

    ...
    "environments": {
        "Production": {
            "origin": {
                "address": "203.0.113.1"
            },
            "alternate_origins": {
                "assets_example_com": {
                    "address": "203.0.113.2",
                    "host_header": "assets.example.com"
                },
            }           
        },
    ...

#### `default.vcl`

Next we need to tell Varnish Cache when to use and how to define this origin for static assets. We will be using the name we defined in your `section.config.json`.

    sub vcl_recv {
        ...
        if (req.url ~ "/some-unique-url-for-static-assets") {
            set req.http.section-origin = "assets_example_com";    
        }
        ...
    }

*Note:* If your origin only accepts traffic on port 80 and you are requesting this resource over HTTPS, you will need to set the `X-Forwarded-Proto` to `http`.

    set req.http.X-Forwarded-Proto = "http";

#### Overview

This use case is especially helpful if you are requesting your static assets on the same domain (e.g. `www.example.com`) to utilize HTTP/2, but want to take the load off your default origin when requesting static assets. Section handles all the internals of actually making the request to your `assets` origin and all you have to do is configure your reverse proxy setup in your git repo!
