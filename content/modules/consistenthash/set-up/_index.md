---
title: Set up
description: Getting Started Guide
keywords: Section, training, platform overview
weight: 1.5
---

## Overview

This tutorial will guide you through the process of adding the Consistent Hashing module to your proxy stack with default configuration files. This tutorial assumes you've cloned your application's git repository to your local machine.

### Step 1 - Updating section.config.json

1. Add the following object to your **proxystack** array in your **section.config.json** file located in the root of your repository.

```
{
    "name": "consistenthash",
    "image": "consistenthash:1.0.0"
}
```

{{% notice note %}}
Typically this is added downstream of the module you want to load balance traffic to based on the consistent hash.
{{% /notice %}}

### Step 2 - Adding default files

1. Create a `consistenthash` directory in the root of your repository.
1. Create the following files under the **consistenthash** directory:
    * server.conf

### Step 3 - Populate the server.conf file

The `server.conf` file contents:

```nginx

# Use HTTP 1.1 to allow for keepalive connections
proxy_http_version 1.1;

# Pass the request host header through to the upstream
proxy_set_header Host $host;

# Allow http connections to be kept open
proxy_set_header Connection '';

# Pass the origin server response header through rather than allowing nginx to set it to "nginx"
proxy_pass_header Server;

location / {
  proxy_pass "http://consistenthash_uri_next_hop_upstream";
}
```

This default config implements the consistent hash based on the URI path of the HTTP request in the proxy_pass directive, but you can use the following values for other forms of consistent hashing:

* `consistenthash_uri_next_hop_upstream` - consistent hash based on the URI path.
* `consistenthash_client_ip_next_hop_upstream` - consistent hash based on the originating Client IP address.
* `next_hop_upstream` - no consistent hashing applied.

### Step 4 - Deploy

Commit your changes and push them to the desired branch you are working on. If you run into any issues please contact support@section.io.