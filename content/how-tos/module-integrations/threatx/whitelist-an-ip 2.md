---
title: Whitelist an IP Address or a CIDR Range
description: How to Whitelist an IP address/CIDR range in ThreatX?
keywords: Section, training, platform overview
weight: 1
aliases:
  - /modules/threat-x/how-tos/whitelist-an-ip/
---

## Overview

By whitelisting an IP address or a CIDR range you can instruct Threat-X to not inspect requests from those IPs. The ThreatX portal allows you to easily whitelist an IP Address or a CIDR range.

## Whitelist an IP Address/CIDR range

As first step you will have to log into the ThreatX portal at x.threatx.io and access `Settings > IWAF` from the navbar.

![ThreatX Nav IWAF](/docs/images/threatx/threatx_nav_iwaf.png)

Select the **Whitelist** tab and click on  **Add Entry** in the top right corner.

![ThreatX - Whitelist](/docs/images/threatx/threatx_whitelist.png)

This will present you with a pop to add the IP address or the CIDR range. Add and click **Submit**.

![ThreatX - Whitelist entry](/docs/images/threatx/add_whitelist_entry_threatx.png)

{{% notice note %}}
If you are whitelisting an entry previously in the blacklist make sure that you remove it from the blacklist.
{{% /notice %}}
