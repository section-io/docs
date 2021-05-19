---
title: Understanding Cache Effectiveness
description: Guide for evaluating your website performance and how to use Section to make improvements.
keywords: cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 1
aliases:
  - /performance-techniques/tutorials/performance-evaluation/understand-if-your-varnish-cache-is-effective/
  - /topic-guides/performance-evaluation/understand-if-your-varnish-cache-id-effective/
---

Whenever a request reaches a Varnish Cache instance, one of four outcomes occurs: hit, miss, pass, or synth.

A key metric when evaluating website performance is **cache hit rate**. Cache hit rate is a measure of how effectively the cache is responding to customer requests.

A **hit** means that the cache responded to the request with a cached resource.

A **miss** means that the cache tried to respond to the request with a cached resource but could not do so because it did not have a copy of the requested resource in its memory.

A **pass** means that the cache did not even try to look up a response for the requested resource — often users specifically instruct Varnish Cache to pass on urls that should never be served from cache like `/checkout`, but there are other causes as well.

From a performance standpoint, the goal is to increase Hit % and decrease Miss and Pass %.

**Why do you care?:**

Whenever the cache answers a customer request, that means the request did not need to be answered by your website origin server. Having a large percentage of cache hits results in performance benefits and reduced costs.

From a performance standpoint, Varnish Cache's quick lookup and response time combined with the geographic distribution of Section's platform means that your users are quickly served a response from a server close to their geographical location.

This improves time-to-first-byte and keeps latency low.

From a cost-savings perspective, every request that receives a response from cache does not need to connect to your origin server, greatly reducing load. With a finely-tuned caching configuration, your origin only needs to respond to requests for personalized actions such as checkout and and account pages.  

**How do you see it?:**

This is the first chart we show you on the Section dashboard. To see this in action on our demo bootcamp application, go to **[Section Bootcamp Overview dashboard](https://aperture.section.io/account/1/application/1/environment/Production/overview)**.

{{% figure src="/docs/images/varnish-cache-usage-metrics.png" %}}

For more detailed information, such as the absolute number of requests and size of those requests, you can view **[Trending Metrics](https://aperture.section.io/account/1/application/1/grafana-web)**. For more in-depth guidance on using our Monitoring tools, see [the monitoring section](/docs/monitoring/) of our documentation.
