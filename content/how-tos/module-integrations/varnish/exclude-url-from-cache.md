---
title: Exclude URL from Varnish cache
aliases:
  - /modules/varnish-cache/how-tos/exclude-url-from-cache/
---

Requests to particular URLs can be excluded from Varnish cache.

### Exclude a particular URL

Use the following code snippet to exclude an exact match to a URL. This code is for VCL4.0.

``` vcl
sub vcl_recv {
    if (req.url == "/example.html") {
        return(pass);
    }
}

sub vcl_backend_response {
    if (bereq.url == "/example.html") {
        set beresp.uncacheable = true;
        set beresp.ttl = 120s;
        return(deliver);
    }
}
```


### Exclude a URL pattern

You can also use regex expressions to exclude URLs based on a pattern.
The following code block will match any request URL that contains `/URL_path/`.

``` vcl
sub vcl_recv {
    if (req.url ~ "/URL_path/") {
        return(pass);
    }
}

sub vcl_backend_response {
    if (bereq.url ~ "/URL_path/") {
        set beresp.uncacheable = true;
        set beresp.ttl = 120s;
        return(deliver);
    }
}
```