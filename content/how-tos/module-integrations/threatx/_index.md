---
title: Set up ThreatX
description: Adding ThreatX to your Section proxy stack.
keywords: content delivery network, CDN, waf, web applicatio firewall, threatx, reverse proxies, proxy, proxy template
weight: 1
aliases:
  - /modules/threat-x/set-up/
  - /modules/threatx/tutorials/
  - /modules/threatx/tutorials/add-threatx-to-your-proxystack/
---

## Overview

This tutorial will guide you through the process to adding the ThreatX module to your proxy stack with default configuration files.

## Setting up Threat X in Section

You can add Threat X to your Section setup Content Delivery Grid very quickly. There are a few phases to this process.

When creating your application you will want to select the **Threat-X** on the second page of the setup process.

{{% figure src="/docs/images/select-threatx2.png" %}}

If you already have an application on Section add the following object to your **proxystack** array in your **section.config.json** file located in the root of your repository.

```
{
    "name": "threatx",
    "image": "threatx:latest"
}
```

{{% notice note %}}
You can add this module at any index in your proxystack array. We'd recommend adding this module as the first module in the proxy stack.
{{% /notice %}}

### Step 2 - Adding default files

1. Create a `threatx` directory in the root of your repository.
1. Create the following files under the **threatx** directory:
    * proxy-features.json

### Step 3 - Populate the proxy-features.json file

The `proxy-features.json` file will have the following format :
```
{
    "environment_variables": [
      "CUSTOMER=<customer_name>",
      "API_KEY=<api_key>"
    ]
}
```

Contact Section support at support@section.io. Our engineers will organize an account with Threat X. The Section team will provide you with credentials to populate the file and access the Threat X management console.

### Step 4 - Deploy

Commit your changes and push them to the desired branch you are working on. Now, when you select the **Advanced Config** option in the left sidebar you  will see the newly added **threatx** folder under your root directory. If you run into any issues please contact support@section.io


### Step 5 - Switch to auto blocking

Threat X will then be running on your site, inspecting your traffic. This period is referred to as "baselining" and allows the system to form a behavioral map of what good, normal traffic looks like for your website.
After a while, look at the threats that are hitting your site with a representative from Threat X. Together you will assess the results of baselining mode and look for any false positives - this is where Threat X has detected an attack that could be a result of intended behavior or bugs in your site. As a last step the Threat X module will be switched from inspection mode to blocking mode.

____

You are now setup with ThreatX as part of your Section proxy stack. If you have any questions reach please contact section support at support@section.io

____
