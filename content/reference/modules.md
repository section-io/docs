---
title: Modules
description: Information on which modules and reverse proxies are available to use on Section edge platform.
keywords: content delivery network, CDN, varnish, turpentine, modsecurity, reverse proxies, proxy, proxy template
aliases:
  - /modules/
  - /proxy-list/
  - /reference/proxy-list/
  - /modules/pagespeed/
  - /modules/pagespeed/set-up/
  - /modules/pagespeed/how-tos/
  - /modules/pagespeed/how-tos/debugging-pagespeed/
  - /modules/pagespeed/how-tos/enable-and-disable-filers/
  - /modules/pagespeed/how-tos/pagespeed-advanced-config/
  - /modules/pagespeed/how-tos/pagespeed-and-varnish-cache/
  - /modules/pagespeed/how-tos/turn-pagespeed-on-and-off/
weight: 150
ordersectionsby: "title"
---

Section offers a number of different modules that can be used in your edge deployment.

Section also allows you to build your own modules and run custom workloads on our edge network throughout the world. You can get started with building your own module with the example module assets provided by Section : **[Module Build Assets](https://github.com/section/module-build-assets)**.

A module template is a combination of the module software (eg. Varnish Cache) and a set of default files to configure the module (eg. the `default.vcl` file).

If you want to experiment with different modules you can use our [Developer Workflow](/docs/developer-pop/) to run your edge deployment on your local machine.

## Available Modules

| Module | Function | Description
|:--|:--|---|
| [Cloudinary](/docs/explanations/modules/cloudinary/ "Cloudinary overview") | Image Optimization | On-the-fly image manipulation and optimization. |
| [Optidash](/docs/explanations/modules/optidash/ "Optidash overview") | Image Optimization | Optimize images and reduce page weight and load time. |
| [ModSecurity](/docs/explanations/modules/modsecurity/ "ModSecurity") | Web Application Firewall | Open source Web Application Firewall. |
| [Node.js](/docs/explanations/modules/nodejs/ "Node.js overview") | Edge Compute | Node.js Javascript application module running on Section compute edge. |
| [OpenResty](/docs/explanations/modules/openresty/ "OpenResty overview") | Edge Compute | Nginx and Lua based scriptable web platform. |
| [Radware Bot Manager](/docs/explanations/modules/radware-bot-manager/ "Radware Bot Manager overview") | Bot Management | Non-human bot traffic detection and management. |
| [Signal Sciences](/docs/explanations/modules/signal-sciences/ "Signal Sciences overview") | Web Application Firewall | Real-time protection for an application under attack and integrates into devops toolchains. |
| [SiteSpect](/docs/explanations/modules/sitespect/ "SiteSpect overview") | A/B Testing | Javascript and Tag Free A/B testing. |
| [Templarbit Shield](/docs/explanations/modules/templarbit/ "Templarbit Shield overview") | Web Application Firewall | Intelligent application protection. |
| [ThreatX](/docs/explanations/modules/threat-x/ "ThreatX overview") | Web Application Firewall | Web Application Firewall based on dynamic rules. |
| [Varnish Cache](/docs/explanations/modules/varnish-cache/ "Varnish overview") | Cache | Latest version of Varnish Cache completely customizable. |
| [Virtual Waiting Room](/docs/explanations/modules/virtual-waiting-room/ "Virtual Waiting Room overview") | Traffic Management | Manage user experience during extreme traffic events. |

{{% children %}}
