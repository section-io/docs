---
title: Grafana Metric Visualization
description: An overview of the Grafana tool and its application within the Section platform.
keywords: monitoring, Grafana, metrics, Varnish Cache handling
type: "docs"
aliases:
  - /monitoring/overview/grafana/
  - /grafana/
  - /topic-guides/platform-monitoring/grafana/
---

The Grafana view shows you aggregate level visualization using queries from Graphite. We’ve created 4 dashboards that can be accessed in the top right of the Grafana frame under the section "Content Delivery Grid."

{{% figure src="/docs/images/monitoring/navigate-grafana-metrics.png" %}}

You can also toggle the display and time frame for each of the graphs just above the "Content Delivery Grid" button.

You can open up Grafana in a new window for better viewing by clicking “Open in new window” button at the top of the frame.

![New window grafana](/docs/images/monitoring/grafana-new-window-aperture.png?height=600px)

#### Traffic Summary

The first view you will see is your "Traffic Summary," which is helpful for understanding your website's traffic overview. You will be able to see the amount of HTTP Requests served per minute and the corresponding bytes served per minute.

We also give you an overview of the HTTP responses served by status code, which is helpful for debugging errors. Following this chart is a break down of all client side errors (4xx status code) and server side errors (5xx status code).

#### Varnish Cache Overview

The “Varnish Cache Overview” dashboard, which is only has data viewable if you have a Varnish Cache module setup on your application. These charts go into detail on the hit, miss, pass ratios and help you understand how  many of your requests are able to be handled by Varnish Cache .

A “hit” means that the cache was able to respond to the request. A “miss” means that the cache was checked for the the content but it wasn’t there and did not respond to the request (and subsequently sent the request to the server). A “pass” means that the cache was not checked for the content and the request went straight to the server.

These charts give you a good high level understanding of how much content you are serving from the cache. The higher the number of cache hits, the faster your website loads and the less work is required by your servers. You can increase the overall cache hit count by caching more content, which can be managed in your [Varnish Cache configurations](/docs/basic-configuration/#varnish).

#### Varnish Cache Request Performance

The “Varnish Cache Request Performance” dashboard goes detail on time to serve and bandwidth by hit type, content type, and response type. Here we start to go into detail on time to serve and bandwidth by hit type, content type, and response type.

Hit type refers to Hit, Miss or Pass. With time to serve, you can start seeing the impact a cache hit has on speed to deliver content and bandwidth required by your servers.

Content type refers to what kind of content was requested: images, html, css, etc. This gives you a good idea of what type of content takes the longest to serve and requires to most work from your servers. It should provide a good starting indication of where to focus your efforts on which type of content to cache.

Response type refers to how your website responded to their request. A 200 code means that the content was delivered successfully. A 3XX means there was a redirect. Since redirects load two different objects, they require more time and resources to deliver than a 200. If you see an increase in 3XX codes, you should review your redirects and see if they are necessary or if they can be removed. 4XX and 5XX codes mean that the content was not delivered successfully and they should be reviewed in your Kibana logs to understand how to fix the issue.

#### Varnish Cache Hit Rates
The “Varnish Cache  Hit Rates” dashboard breaks down the overall hit rates by content type: HTML, Images, CSS, Javascript. This breaks down the overall hit rates by content type: HTML, Images, CSS, Javascript.

* HTML is the set of instructions required to load the page.
* Images are any images or icons you load.
* CSS is the style instruction for how to load images, text, and content on the page. And
* JS is small scripts your browser will run as when it is instructed to by the HTML.

For each content type, you can view your hit rates, volume of requests, and time to serve.
