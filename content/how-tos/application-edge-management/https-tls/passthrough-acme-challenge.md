---
title: Passthrough ACME Challenge HTTP Request
description: How to configure Section to passthrough the ACME Challenge route
keywords: SSL, certificate, custom, upload, acme, acme challenge
aliases:
  - /https/how-tos/passthrough-acme-challenge/
---
## Context

If you wish to configure the Section platform to pass the ACME Challenge route through to your origin please follow the following steps. Please note that enabling this feature will render the Section provided Let's Encrypt SSL certificates unusable.  

## Steps

Follow the below steps to deploy this change:

1. Locate the `section.config.json` file in the root of your Section git repository.
1. Locate environment block (in this example we'll be using Production).

```json
...
"environments": {
    "Production": {
    "origin": {
        "address": "origin.example.com",
        "enable_sni": true
    },
...
```

1. Add the following key/value to the origin block: `"proxy_acme_challenge": true`

```json
...
"environments": {
    "Production": {
    "origin": {
        "address": "origin.example.com",
        "enable_sni": true,
        "proxy_acme_challenge": true
    },
...
```

1. Commit your changes and push to your desired branch.
