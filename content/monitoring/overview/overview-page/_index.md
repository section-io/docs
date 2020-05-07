---
title: Section Console Overview Page
description:
keywords: metrics, grafana, graphite, kibana, varnish, modsecurity, website performance, website security, content delivery network, CDN
aliases:
  - /metrics-overview/
  - /topic-guides/platform-monitoring/overview-page/
---

Each Section environment has its own **overview page**. The overview page displays general information about the environment's module stack and HTTP request flow, any recent errors between Section and the origin server, and a number of links to more detailed information about the environment such as DNS information and HTTP logs.
#### Module Stack

All module stack configurations running on Section begin with the edge module (the very first module that incoming HTTP requests hit when they enter Section) and ends with the LastProxy (the last module that incoming HTTP requests pass through before leaving Section and hitting your origin server). The modules in between can be configured to perfectly suite your needs using your environment's [advanced configuration](/docs/modules/). On the overview page, we display a graphic detailing the proxies currently running in your environment's configuration and their current order.
{{% figure src="/docs/images/monitoring/bootcamp-proxy-stack.png" %}}

#### HTTP Traffic Summary

We also show you an overview graph that can be toggled between three metrics: Number of HTTP responses served per minute, Breakdown of error requests for the last hour, and Downstream response bandwidth served per minute. This data is pulled from [Graphite](/docs/monitoring/overview/graphite) in the **Metrics** view, so you can go here to dig deeper into the data.

{{% figure src="/docs/images/monitoring/bootcamp-http-response-count.png" %}}

Number of HTTP responses served per minute gives you a quick sense of the overall volume of traffic hitting your website, including all HTML content and all static resources like images & CSS files. This view is great for a general, low-resolution picture of how your site is doing.

Clicking the **Error Responses** button below the HTTP graph brings up a breakdown of all error responses served to your users in the last hour, separated out into 3XX (Redirections), 4XX (Client request errors) & 5XX (Server errors) errors. This graph provides a simple way to detect a recent increase in errors served. (#logs).

Downstream response bandwidth served per minute shows you the total amount of bandwidth sent to your customers. This represents the volume of data sent, as opposed to the count (represented by the number of HTTP requests). If you see this increasing but your number of HTTP responses staying the same, then you may have increased the average size of content being requested. You can review the bandwidth by file type in **Metrics** to see what may be causing this increase.

In addition to the overview graph, we also show data depending on whether your application is set up with [Varnish](#varnish) or [Modsecurity](#modsecurity).

#### Varnish

For Varnish Cache we show Cache hit, pass and misses for the last hour and Upstream request bandwidth served per minute.

{{% figure src="/docs/images/varnish-cache-hit-miss-pass.png" %}}

Cache hit, pass and misses for the last hour shows the breakdown of how Varnish Cache  handled your requests.  The higher the hit percentage, the faster your website will perform and the less work required by your servers.


Upstream request bandwidth served per minute shows the volume of data sent by the origin. The more content you cache using Varnish, the lower this will be. By lowering this number you decrease the amount of work required by your servers.

#### Modsecurity

For Modsecurity we show Intercepts, audits and passes % for the last hour and Upstream request bandwidth served per minute.

{{% figure src="/docs/images/modsecurity-audits-intercepts.png" %}}

Intercepts, audits and passes % for the last hour shows you the breakdown of how Modsecurity handled your requests. Intercepted means that modsecurity blocked the request (a function that must be activated in your configuration). Audits means that modsecurity looked at the request based on the rules you have turned on. Passes means that modsecurity did not look at the request.

Upstream request bandwidth served per minute shows the volume of data sent by the origin. The more malicious requests you block using Modsecurity, the lower this will be. By lowering this number you decrease the amount of work required by your servers.

#### Other Modules

Depending on your configuration, you may see additional icons here for other modules such as Openresty, Kraken, or a Web Application Firewall. The overview page does not provide metrics for these additional modules like it does for Varnish and ModSecurity.  

To dig into metrics further for Varnish, ModSecurity, or another module in your stack, go to the Metrics tab within you r Section portal and visit our [Monitoring documentation](/docs/monitoring) and our [Debugging documentation](/docs/).
