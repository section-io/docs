---
title: Blacklist an IP address or a CIDR range
description: How to blacklist an IP address or a CIDR range in ThreatX?
keywords: Section, training, platform overview
weight: 1
aliases:
  - /modules/threat-x/how-tos/blacklist-an-ip/
---

## Overview

The ThreatX portal allows you to easily block an IP Address or a CIDR range by adding it to blacklist.

## Blacklist an IP Address/CIDR range

As first step you will have to log into the ThreatX portal at x.threatx.io and access `Settings > IWAF` from the navbar.

![ThreatX Nav IWAF](/docs/images/threatx/threatx_nav_iwaf.png)

Select the **Blacklist** tab and click on  **Add Entry** in the top right corner.

![ThreatX - Blacklist](/docs/images/threatx/threatx_blacklist.png)

This will present you with a pop to add the IP address or the CIDR range. Add and click **Submit**.

![ThreatX - Blacklist entry](/docs/images/threatx/add_blacklist_entry_threatx.png)

{{% notice note %}}
If you are blacklisting an entry previously in the whitelist make sure that you remove it from the whitelist.
{{% /notice %}}