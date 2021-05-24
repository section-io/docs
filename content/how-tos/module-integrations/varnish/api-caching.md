---
title: API Caching
description: How-to use Varnish to cache an API.
keywords: API, API caching, varnish, Varnish Cache, JSON, JSON API caching
aliases:
  - /modules/varnish-cache/how-tos/api-caching/
  - /api-caching/

---

## Overview

Varnish Cache can be used to cache an API. By caching a JSON RESTFul API an application running on the edge can be made to run faster.

This how-to describes using the Varnish Module on the Section platform to cache an Application Programming Interface (API).

For example, an application running in a [Section Node.js Module]({{< ref "modules/nodejs/_index.md" >}}) on the Edge can cache commonly used API routes in a "varnishapi" Varnish Cache Module.

### section.config.json

The section.config.json could look like;

{{< highlight js >}}

    "proxychain": [
        {
            "name": "varnishstatic",
            "image": "varnish:6.1.1"
        },
        {
            "name": "varnishhtml",
            "image": "varnish:6.1.1"
        },
        {
            "name": "nuxt",
            "image": "nodejs:10.11.0"
        },
        {
           "name": "varnishapi",
           "image": "varnish:6.1.1"
        }
    ],
{{< / highlight >}}


In our example we will cache the following routes;

{{< highlight bash >}}
/api
{{< / highlight >}}

But, will pass all other routes to other proxies;

{{< highlight bash >}}
/
{{< / highlight >}}



### VCL syntax

Example VCL is used in the "varnishapi" module to cache API's.

{{< highlight bash >}}
sub vcl_recv {

    if (req.method != "GET" && req.method != "HEAD" && req.method != "PURGE") {
        return (pass);
    }
    #rest / soap apis or magento should pass
    if (req.url ~ "^/api/(rest|soap|v2_soap)") {
        return(pass);
    }
    #all except /api/+ should look for cache
    elseif (req.url ~ "/api/.+") {
      return(hash);
    }
    if (req.http.Authorization) {
        return (pass);
    }

    return(pass);
}


sub vcl_backend_response {
    if (bereq.method != "GET" && bereq.method != "HEAD" && bereq.method != "PURGE") {
        set beresp.uncacheable = true;
        set beresp.ttl = 120s;
        return (deliver);
    }

    if (bereq.url ~ "/api/(rest|soap|v2_soap)") {
        set beresp.uncacheable = true;
        set beresp.ttl = 120s;
        return (deliver);
    }
    elseif (bereq.url !~ "/api/.+") {
        set beresp.uncacheable = true;
        set beresp.ttl = 120s;
        return (deliver);
    }
    if (beresp.status != 200) {
        # Do not cache non-200 responses
        set beresp.ttl = 120s;
        set beresp.uncacheable = true;
        return (deliver);
    } else {
        if (bereq.url ~ "^/api") {
            unset beresp.http.Set-Cookie;
            set beresp.ttl = 4h;  # cache for 4 hours
            set beresp.grace = 4h;
            return (deliver);
        }
    }
    return (deliver);

}

sub vcl_deliver {
    if (obj.hits > 0) {
        #set resp.http.section-io-cache = "Hit";
    } else {
       #set resp.http.section-io-cache = "Miss";
    }
     # Debug custom header
    if (obj.hits > 0) {
        set resp.http.CUSTOMER-API-Cache = "HIT";
    } else {
        set resp.http.CUSTOMER-API-Cache = "MISS";
    }

}


sub vcl_hash {
    # Purpose: Split cache by HTTP and HTTPS protocol.
    hash_data(req.http.X-Forwarded-Proto);
}


{{< / highlight >}}

{{% notice note %}}
Replace CUSTOMER-API with a custom header i.e. Section or MyAwesomeAPP.
{{% /notice %}}
