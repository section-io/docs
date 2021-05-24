---
title: Setting and unsetting HTTP headers
description: Varnish Cache gives you the ability to modify, add, and remove HTTP headers on the request and response object.
keywords: http headers
aliases:
  - /modules/varnish-cache/how-tos/set-and-unset-headers/
---

## Overview

Varnish Cache gives you the ability to modify, add, and remove HTTP headers on the request and response object.

## Request Headers

The [vcl_recv](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-recv) sub routine is called at the beginning of a request and this is where we will be modifying the request headers. We will be adding the header `hello` with value of `world`, and removing the `user-agent` header.

```js
sub vcl_recv {
    ...

    set req.http.hello = "world";
    unset req.http.user-agent;

    ...
}
```

{{% notice note %}}
The **req.http** object is how to access any request header and is only readable from **vcl_recv** and **vcl_deliver**.
{{% /notice %}}

## Response Headers

The [vcl_backend_response](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-backend-response) sub routine is called once Varnish Cache has received the response headers from the upstream service. We will be modifying the header `cache-control` and setting the value to `public, max-age=600`, and removing the `server` header.

```js
sub vcl_backend_response {
    ...

    set beresp.http.cache-control = "public, max-age=600";
    unset beresp.http.server;

    ...
}
```

{{% notice note %}}
The **beresp.http** object is how to access any response header and is only readable from **vcl_backend_response** and **vcl_deliver**.
{{% /notice %}}