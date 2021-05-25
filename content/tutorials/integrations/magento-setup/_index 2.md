---
title: Magento
description: Guide for evaluating your website performance and how to use Section to make improvements.
keywords: cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 10
aliases:
  - /how-to/magento-setup/
---

Magento is a popular eCommerce platform that needs extensive performance tuning.

Section delivers huge speed improvements to all versions of Magento through full page caching (HTML and static assets) using Varnish Cache .

## Different Approaches for Different Magento Versions

For [Magento 2.x](/docs/integrations/how-tos/magento-setup/set-up-magento-2/ "Magento 2.x") , support for Varnish Cache to cache page content is integrated into Magento. Section offers ["Instant Global Cache"](/docs/integrations/how-tos/magento-setup/set-up-magento-2/ "Instant Global Cache"), an extension that will let you get setup with Varnish Cache and distribute it globally on Section’s CDN directly from the Magento Admin portal.

For [Magento 1.x](/docs/integrations/how-tos/magento-setup/set-up-magento-1/ "Magento 1.x Varnish cache clear"), Varnish Cache support is provided by HTML Streaming, Anonymous user caching or the free Turpentine Magento extension.


