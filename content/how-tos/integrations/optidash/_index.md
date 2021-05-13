---
title: Set up Optidash
description: Adding Optidash to your Section proxy stack.
keywords: content delivery network, CDN, waf, web applicatio firewall, Optidash, reverse proxies, proxy, proxy template
weight: 1
aliases:
  - /modules/optidash/set-up/
---
# Overview
This tutorial will guide you through the process to adding the Optidash module to your proxy stack with default configuration files. This tutorial assumes you’ve cloned your application’s git repository to your local machine.

##Step 1 - Updating section.config.json
Add the following object to your proxystack array in your section.config.json file located in the root of your repository.
{
    "name": "optidash",
    "image": "optidash:1.0"
}
You can add this module at any index in your proxystack array. We’d recommend adding this module behind Varnish Cache.

## Step 2 - Adding default files
Create a optidash directory in the root of your repository.
Create the following files under the optidash directory:
optidash.json

## Step 3 - Populate the optidash.json file
The optidash.json file will have the following format :

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
The api_key and api_key_secret will be provided to you by Section. You can contact us at support@section.io.

You can learn more about the different settings Optidash advanced settings.

## Step 4 - Deploy
Commit your changes and push them to the desired branch you are working on. If you run into any issues please contact support@section.io.