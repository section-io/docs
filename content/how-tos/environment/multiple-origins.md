---
title: Run multiple origins in one environment
description: Set up Section so that it can deliver content from multiple origin servers
keywords: multiple origins, multiple upstreams, origin address, origin server, origin, cache, cached data, content delivery network, CDN
aliases:
  - /platform/environment/how-tos/multiple-origins/
  - /multiple-origins/
  - /how-to/multiple-origins/

---
#### A Guide to hooking up multiple origin servers to one Section environment and orchestrating incoming HTTP traffic distribution among them.

When you have a single origin or upstream server, your section.config.json file will look something like this:

    "origin": {
        "address": "origin.example.com",
        "host_header": "override.example.com"
    }

However, there are cases where it is useful to have two different upstream services — perhaps you want to make two backend systems appear on the same domain.

Section supports multiple origins in a single configuration which allows you to run multiple backends into one domain.

## Adding More than One Origin Server

Adding another backend service or origin to your configuration involves the following steps:


#### 1) Define Alternate Origins

To define multiple origins, we need to add configuration information about the additional origins to our `section.config.json` file.

Working from the case above, we can add a second origin by adding an `alernate_origins` block.

Here's an example of adding `origin2.example.com` to `section.config.json`

    "origin": {
        "address": "origin.example.com",
        "host_header": "override.example.com"
    },
    "alternate_origins": {
        "origin2_example_com": {
            "address": "origin2.example.com",
            "host_header": "origin2.example.com"
        }
    }

Note that the alternate origin definition is a named object. We advise naming the alternate origin similarly to the `address` field.

The `address` field tells Section the IP address or DNS name that it should connect to. You will also want to specify the `host_header` that will be used on the HTTP requests that Section makes to this upstream.

#### 2) Configure your Section proxy stack to forward requests to the alternate origin

Once you have established multiple origins by configuring your `section.config.json` file, you can choose to route incoming requests to different origins based on criteria of your choosing. When an incoming request hits the LastProxy(The final proxy in your chain), LastProxy looks for request headers and routes the request to the specified origin.

Generally speaking, this is done within the Varnish Cache  proxy. Here's an example using Varnish Cache VCL that you could incorporate into your `default.vcl`.

    sub vcl_recv {
        if (req.url ~ "sitemap.xml" ) {
            set req.http.section-origin = "origin2_example_com";
        }
    }

This `if` statement would be included in your existing `vcl_recv` function, or, as is allowed with vcl files, could be written as a part of a new vcl_recv block for the sake of organization.

This example says "If the requested URL contains sitemap.xml, then add a new header, `section-origin`, with the value `origin2_example_com`".

Now, when Section receives a request for sitemap.xml it will add the HTTP request header, which signals the LastProxy to forward the request to the specified alternative origin instead of your primary origin.
