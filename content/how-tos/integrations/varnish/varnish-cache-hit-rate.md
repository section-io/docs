---
title: Improve Varnish Cache Hit Rate
description: Guide for understanding Varnish Cache  hit rate, metrics, and logs.
keywords: varnish, Varnish Cache , cache, cached data, hit rates, Varnish Cache hit rates, vcl, Varnish Cache configuration language, metrics
aliases:
  - /modules/varnish-cache/how-tos/varnish-cache-hit-rate/
  - /varnish-cache-hit-rate/
  - /how-to/varnish-cache-hit-rate/

---

The Varnish Cache  project provides some high level instructions on [improving cache hit rate](https://varnish-cache.org/docs/4.0/users-guide/increasing-your-hitrate.html).

The following describes the work flow with Section metrics and development processes to achieve optimal cache hit ratios.

> 1.  Review Section Varnish Cache metrics
> 2.  Review http logs
> 3.  Make changes to VCL locally
> 4.  Confirm change has been effective -> Logs
> 5.  Promote changes to Production
> 6.  Confirm change has been effective -> Metrics
> 7.  Rinse and repeat

## Review Varnish Cache Metrics

Your Section [Varnish Cache metrics](/docs/metrics-overview/) provide an overview of cache hit ratios for all asset types in addition to cache hit ratios by type.

You can use these metrics to identify an object type for which you would like the cache hit ratio to be improved.

## Review HTTP Logs

Use the Kibana logs to review the HTTP requests. For more information about these logs please check out the docs [here](/docs/logs/).

## Make Changes to VCL

Modify your local VCL file. Save and fire the requests at your local instance. See [Local Development](/docs/how-tos/integrations/varnish/basic-configuration/).

Review logs again to confirm a change in the cache hit behavior for the target assets.

## Promote Changes to Production

If required you can test the application locally to confirm the VCL changes have not affected the functionality of the application adversely for users.

Sync your Section repo with production and confirm cache hit rates are improving by reviewing your metrics.

## Rinse and Repeat

Until you hit a desirable cache hit rate across the site.

---


### **Completed all 7 steps?**

Awesome! Steps 5 through 7 are meant to be an iterative process. Focus on big wins first using your metrics evaluation. Then after you’ve improved those areas, you can focus on other areas to fine tune.


### **How do I know if I’ve been successful?**

* You have improved your Cache Hit Rate
* You have ensured your most requested content is being cached
* You have increased the ratio of HTTPS on your site
* Because you’ve achieved these three goals, you see your customers bouncing less frequently and viewing more pages on your website - which will translate into more revenue for you! Congrats!

### **Need Help?**

Section is here to help with setup and can be reached by emailing contact@Section. If you want help with configuration you can ask us about consulting engagements, and if you want a fully managed service please contact us for a quote.

