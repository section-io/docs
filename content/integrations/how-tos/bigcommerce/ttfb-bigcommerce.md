---
title: TTFB Bigcommerce with Section
description: TTFB for Bigcommerce on the Section platform.
keywords: TTFB, bigcommerce, cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 10
aliases:
  - /how-to/bigcommerce/ttfb/
  - /bigcommerce/ttfb/
---

## Time To First Byte (TTFB)

Time To First Byte is an important metric for user experience as people do not wait for slow pages to load. 

1. TTFB is a metric of the time taken for a user to receive the first byte.
2. Start render time is crucial because it represents the time the user is waiting while looking at a blank screen.
3. There is a high correlation between start render time and bounce rate, so significantly improving this metric has tangible business benefits.

## HTML Streaming

HTML Streaming uses Varnish ESI and OpenResty to punch a hole in the HTML DOM and can stream the HTML behind the title tag, but allows the loading and caching of the head of the document.

4. Dynamically cache parts of HTML document without caching elements of the page that are unique to the user.
5. HTML streaming improves load time metrics and user experience without requiring complex application changes.
6. Achieves faster page load times.
7. HTML streaming dramatically improves the start render time on applications that are not yet caching their entire HTML document. 
8. Unlike dynamic content caching, HTML streaming does not require an intensive implementation time or code changes to your origin and can very quickly realize most of the gains of dynamic content caching within hours of enabling the feature with the help of Section's engineers.
9.  HTML Streaming is fast to implement because it does not require changes to your origin and you don’t need to learn more advanced caching strategies or advanced VCL.

### Before Section HTML Streaming

Using a standard store and testing from Sydney Australia. 

Before HTML Streaming is enabled TTFB is approximately 1500ms on the homepage of a Bigcommerce site using the permanent URL. 

![Before HTML Streaming](/docs/images/screenshots/stream/ttfb.png)

### After Section HTML Streaming

After HTML Streaming and caching is enabled TTFB is approximately 190ms on the homepage.


{{% notice note %}}
After Section caching and HTML Streaming is enabled, from Australia, we generally see an approximately 80-90% improvement in TTFB.
{{% /notice %}}

![After HTML Streaming](/docs/images/screenshots/stream/ttfb-section.png)