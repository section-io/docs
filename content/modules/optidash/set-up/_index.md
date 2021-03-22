---
title: Set up
description: Adding Optidash to your Section proxy stack.
keywords: content delivery network, CDN, optidash, image optimization, reverse proxies, proxy, proxy template
weight: 1
aliases:
  - /modules/optidash/tutorials/add-optidash-to-your-proxystack/
  - /modules/kraken/tutorials/add-kraken-to-your-proxystack/
  - /modules/kraken/tutorials/
---

## Overview

This tutorial will guide you through the process to adding the Optidash module to your proxy stack with default configuration files. This tutorial assumes you've cloned your application's git repository to your local machine.

### Step 1 - Updating section.config.json

1. Add the following object to your **proxystack** array in your **section.config.json** file located in the root of your repository.

```
{
    "name": "optidash",
    "image": "optidash:1.0"
}
```

{{% notice note %}}
You can add this module at any index in your proxystack array. We'd recommend adding this module behind Varnish Cache.
{{% /notice %}}

### Step 2 - Adding default files

1. Create a `optidash` directory in the root of your repository.
1. Create the following files under the **optidash** directory:
    * optidash.json

### Step 3 - Populate the optidash.json file

The `optidash.json` file will have the following format :

```
{
    "api_key": "REDACTED",
    "lossless": false,
    "enabled": true,
    "ttl": 604800,
    "cache_version": "v1",
    "s3": {
        "key": "REDACTED",
        "secret": "REDACTED",
        "region": "ap-southeast-2",
        "bucket": "section-kraken"
    }
}
```

The `api_key` and `api_key_secret` will be provided to you by Section. You can contact us at support@section.io.

You can learn more about the different settings [Optidash advanced settings](/docs/modules/optidash/how-tos/optidash-advanced-config/).

### Step 4 - Deploy

Commit your changes and push them to the desired branch you are working on. If you run into any issues please contact support@section.io.