---
title: Change your Origin Address
description: Guide for changing the origin address of a Section application.
keywords: origin address, origin server, origin, cache, cached data, content delivery network, CDN
aliases:
  - /platform/how-tos/environment/change-origin/
  - /howto-change-origin/
  - /how-to/change-origin/

---

Section is a proxy service, so at the end of the day, any requests for your site that have not been offloaded by the cache or redirected or blocked by the firewall will be passed on to be served by your webserver. The address of this server (or the address of the load balancer in front of your servers) is the origin address.

When your first setup your site on Section we resolve the DNS of the hostname you enter and set that as the origin address. This origin address is stored in a JSON file in the root of the git repository for your application. You can view this by going to <https://aperture.section.io/>, selecting your site and then going to the “Advanced Config” page.

![Change Origin Repository](/docs/images/change-origin-repository.png?height=410px)

This gives you a view of the git repository for your site. From there you can open `section.config.json`.

This is the configuration file for your site on Section. It contains the proxy stack you have configured and environment specific configuration settings.

Each environment has its own section in the file where you can specify config options for that environment. There are a number of possible config settings but for now the one we are interested in is `origin.address`.

![Change Origin Config File](/docs/images/change-origin-configfile.png?height=410px)

To change the address of your production environment Click the Edit button on the page. This will open the online file editor. From there you can change the value of the origin address to the new IP address or CNAME. To save the change, put a description in the Commit Message field (remember, this is all git) and click Commit. This will do a git commit & push which will trigger a deploy to the Section delivery nodes to apply the new orgin address.

Within a few seconds Section will be serving requests from your new webserver.

We will direct all http requests to port 80 and all https requests to port 443 on your origin server. We do not support any other origin ports.

## Override the `Host` request header sent to the origin

Normally, the same `Host` request header sent by the User-Agent will be forwarded to the origin server as-is. However if your origin expects a different `Host` request header, an override can be specified in the `section.config.json` file.

The alternate Host request header should be specified via a `host_header` property inside the `origin` object, for example:

    "origin": {
        "address": "origin.example.com",
        "host_header": "override.example.com"
    }

## Removal of X-Forwarded-Proto and other request headers
Some origin servers and load balancers don't handle certain request headers like `X-Forwarded-Proto` correctly. You can remove them by editing your `section.config.json` by adding a `remove_request_headers` key for each origin.

    "origin": {
        "address": "origin.example.com",
        "remove_request_headers": [
            "x-forwarded-proto"
        ]
    }

## Disable persistent connections between Section and the origin

By default, if your origin allows [HTTP/1.1 persistent connections](https://tools.ietf.org/html/rfc7230#section-6.3) Section will maintain a number of connections open between our reverse proxies and your origin web servers to reduce the cost of performing a TCP 3-way handshake (or more for TLS connections) for each HTTP request forwarded to the origin. This is also known as HTTP Keep-alive.

While persistent connections are generally recommended for the best performance, there are occasional scenarios where you may need to disable it. For example, if you origin load balancer injects a sticky-session cookie only for the first response on a given connection because it assumes one connection equals one browser.

To disable the persistent connection behavior, add a `disable_keepalive` property to the relevant `origin` in your `section.config.json` file.

    "origin": {
        "address": "origin.example.com",
        "disable_keepalive": true
    }

## Leverage alternate origin locations

A common customer requirement is to send a portion of traffic to an alternate origin location. This is often used to segment the uri space or flag a specific type of request to be sent to an alternate location to the standard origin.

An examples of this use case would be to send any request to /assets/images/.\* in your application to an S3 bucket instead of your origin application servers.

To implement this feature there are 2 elements to configure, Please see our Alternate origin documentation here: https://www.section.io/docs/multiple-origins/

## Enable SNI

If your origin has SNI enabled and serves multiple secure(HTTPS) websites using different SSL certificates then you should `Enable SNI` under `Origins` > `Common Settings` in the Section Console.

{{% figure src="/docs/images/enable-sni.png" %}}

This will enable our platform to pass the server name through TLS/SNI when establishing a connection with your origin.

This option is turned off by default.
