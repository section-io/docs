---
title: Serve stale content while the backend is offline
description: How to configure Varnish Cache to serve stale content
keywords: CDN, content delivery network, performance, stale content
aliases:
  - /modules/varnish-cache/how-tos/configure-varnish-cache-to-serve-content-while-the-backend-is-offline/
  - /origin-shield/
  - /stale-content/
  - /varnish-grace/
  - /how-to/varnish-cache/configure-varnish-cache-to-serve-content-while-the-backend-is-offline/
---

Configuring Varnish Cache to serve stale content is very useful for when your origin crashes. This behavior is achievable when running Varnish Cache as a reverse proxy within the Section Content Delivery Grid.

#### Prerequisites

Make sure you have an [account on Section](https://www.section.io/sign-up/), and have selected Varnish Cache to run in your proxy stack.

_Note: This guide will be using VCL 4 syntax, so if you are interested in VCL 3 syntax please reach out to us at support@section.io and we can provide you instructions to upgrade your Varnish instance to support VCL 4_

## Set up

_This guide assumes you know basic VCL and the flow of HTTP traffic through Varnish Cache._

### Step 1 - `vcl_backend_response`

We will need to add logic within `vcl_backend_response` to begin the process for serving stale content.

You will need to check for the backend response status, from your origin server, for any "5XX" errors and return `abandon`. You will also need to set the grace period of the object.

    sub vcl_backend_response {
        if (beresp.status >= 500 && beresp.status <= 599) {
            return (abandon);
        }

        ...

        set beresp.grace = 24h;
    }

### Step 2 - `vcl_synth`

In `vcl_synth` we need to check the `resp.status` for a 503 code as this is the code set by `return(abandon)`. If this is the case, we will utilize `restart` to run through the VCL code again.

    sub vcl_synth {
        if (resp.status == 503) {
            return (restart);
        }

        ...
    }

### Step 3 - `vcl_hit`

This part is where we actually tell Varnish Cache to serve stale content. If you are not using your own `sub vcl_hit` then this is the built in `sub vcl_hit` routine. A great explanation of the following code is provided in the [Varnish docs](https://varnish-cache.org/docs/trunk/users-guide/vcl-grace.html#the-effect-of-grace-and-keep)

{{< highlight js >}}
   sub vcl_hit {
     if (obj.ttl >= 0s) {
          // A pure unadulterated hit, deliver it
          return (deliver);
     }
     if (obj.ttl + obj.grace > 0s) {
          // Object is in grace, deliver it
          // Automatically triggers a background fetch
          return (deliver);
     }
     // fetch & deliver once we get the result
     return (miss);
}
{{< / highlight >}}

## Testing

You can test this logic, by enabling maintenance mode on your server which will serve some type of 500 error. Keep in mind if the request is not in the cache before your origin goes down, the end user will still receive an error.
