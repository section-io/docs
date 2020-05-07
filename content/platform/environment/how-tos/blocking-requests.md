---
title: Block IP
description: How to block bots or spammers from your website to improve website performance via the Section Console UI or directly through config files.
keywords: bot, bot blocker, spammers, crawlers, website performance, webpage speed, website security, content delivery network, CDN
aliases:
  - /block-ip/
  - /blocking-requests/
  - /how-to/blocking-requests/

---

If visitors, crawlers, or spammers are degrading the performance of your site, it may be appropriate to block these from accessing your website content.

Rather than letting these requests be processed by Section and your origin server, you can block them as they enter Section.

There are two approaches to Blocking IP's.

1. IP Restrictions screen in Section Console web dashboard
2. section.config.json in Advanced Config & git workflow

The simplest interface to view/edit these values is available via "Configuration" > "IP Restrictions".

{{% notice info %}}
Note that blocking an IP within Section Console as described above adds the IP to the file ``section.config.json`` behind the scenes.
{{% /notice %}}

## 1. Block IP via Section Console IP Restrictions

Requests can be blocked by IP address or routing prefix.

![Block IPs](/docs/images/platform/ip-blacklist-add.gif)

For each requesting IP you wish to block requests from, click the "Add Another" button on the page and enter the address or range that you wish to block to the "IP address/CIDR block" text box. Once complete, press the "Save" button.

Within a few seconds Section will be blocking requests from your blacklist.

## 2. Manage your IP blacklist from within your application repository

The IP blacklist is stored in the ``section.config.json`` file in the root of the git repository for your web site. You can view this by going to <https://aperture.section.io/>, selecting your site and then going to the "Advanced Config" page.



{{< figure src="/docs/images/platform/advanced-config.gif" title="Simple proxy stack" >}}

The `ip_blacklist` field is applied to an environment (living at the same level as `origin` ). It is a list (array) of IP v4 addresses and/or [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation) routing prefixes.

The request blacklist is specified via an `ip_blacklist` property inside one of the `environment` objects found within the ``section.config.json`` file inside your Advanced Configuration tab of Section Console — for example:

    {
        "proxychain": [],
        "environments": {
            "Production": {
                "origin": {
                    "address": "origin.example.com"
                },
                "ip_blacklist": [
                    "192.0.2.1",
                    "198.51.100.0/24"
                ]
            },
            "Development": {
                "origin": {
                    "address": "origin.example.com"
                }
            }
        }
    }

The section.config.json file blacklist accepts individual IP addresses as well as entire subnets. This configuration file would block all requests from 192.0.2.1 and from the IP range of 198.51.100.0-198.51.100.255. The origin server would never even see the requests and the Section platform would deliver 403 forbidden errors directly to the (likely malicious) clients.

 If you prefer, you can create a [custom response]({{< ref "/debugging/reference/http-error-messages.md#custom-error-messages" >}}) to entities on the IP blacklist.
