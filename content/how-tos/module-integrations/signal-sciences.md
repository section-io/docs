---
title: Set up Signal Sciences
description: Adding Signal Sciences to your Section proxy stack.
keywords: content delivery network, CDN, waf, web applicatio firewall, Signal Sciences, reverse proxies, proxy, proxy template
weight: 1
aliases:
  - /modules/signal-sciences/set-up/
  - /modules/signal-sciences/tutorials/
  - /modules/signal-sciences/tutorials/add-signal-sciences-to-your-proxystack/
---

## Overview

This tutorial will guide you through the process to adding the Signal Sciences module to your proxy stack with default configuration files.

## Setting up Signal Sciences when setting up an application

When creating your application you will want to select the **Signal Sciences** on the second page of the setup process.

{{% figure src="/docs/images/select-sigsci.png" %}}

## Setting up Signal Sciences on an existing application

### Step 1 - Adding default files

1. Clone the application repository by selecting the **Advanced Config** option in the left sidebar and copying the repo URL.

{{% figure src"/docs/images/clone-sigsci.png" %}}

2. Create a `sigsci` directory in the root of your repository.
3. Create the following files under the **Signal Sciences** directory:
    * proxy-features.json

### Step 2 - Populate the proxy-features.json file

The `proxy-features.json` file will have the following format :
```
{
  "environment_variables": [
    "SIGSCI_ACCESSKEYID=access_key",
    "SIGSCI_SECRETACCESSKEY=secret_access_key"
  ]
}
```

Contact Section support at support@section.io. Our engineers will organize an account with Signal Sciences. The Section team will provide you with credentials to populate the file and access the Signal Sciences management console.

### Step 3 - Deploy

Commit your changes and push them to the desired branch you are working on. Now, when you select the **Advanced Config** option in the left sidebar you will see the newly added **sigsci** folder under your root directory. If you run into any issues please contact support@section.io

### Step 4 - Update your proxy stack config file

 Add the following object to your **proxystack** array in your **section.config.json** file located in the root of your repository.

```
{
    "name": "sigsci",
    "image": "sigsci:latest"
}
```

{{% notice note %}}
You can add this module at any index in your proxystack array. We'd recommend adding this module as the first module in the proxy stack.
{{% /notice %}}

____

You are now setup with Signal Sciences as part of your Section proxy stack. If you have any questions reach please contact section support at support@section.io

___
