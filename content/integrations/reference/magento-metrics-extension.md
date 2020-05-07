---
title: Magento Metrics
description: Guide for Section Magento Metrics extension that provides visibility into the impact caching has on your website.
keywords: magento, varnish, Varnish Cache , metrics, magento extension, cache, page speed, webpage speed
aliases:
  - /magento-metrics-extension/
  - /reference/magento-metrics-extension/

---

Section has an extension for Magento customers that allows business managers to access Section site metrics. These metrics provide visibility into the impact caching has on your website, without having to login to the Section application. You can get the extension for your Magento website by going to the [Magento Marketplace](https://marketplace.magento.com/sectionio-metrics.html).

There are three metrics we show in the extension: Overall Cache Hit, HTML Cache Hit, and HTTP Response Codes. The extension in Magento is meant to give you an overview on the current status, but by having a developer look into your [Varnish Cache configuration settings](/docs/basic-configuration/#varnish) or your logs in the in the Section application, you can improve all of these metrics.

## Overall Cache Hit
Overall Cache Hit count shows the number of cache hits from all content types. A cache hit is when a customer requests content from your site (whether it's an image, html document, etc) and the cache is able to respond to that request. The chart shows successful responses (responses with a 200 HTTP response code) in 4 hour increments over the previous 7 days. The timezone is based on the location of the Magento user.

The more often the cache can answer your customer requests, the higher the overall cache hit count. The higher the number of cache hits, the faster your website loads and the less work is required by your servers. This means you can earn more revenue by providing a better experience for your customers, and you can save money by not having to purchase additional servers with Magento.

You can increase the overall cache hit count by caching more content. To setup caching, login to Section Console account and add [configurations for Varnish](/docs/basic-configuration/#varnish).


## HTML Cache Hit
HTML Cache Hit count shows the number of cache hits for HTML documents. HTML documents are a set of instructions used to create the webpage and determine how all other content types get loaded on the page. The chart shows successful responses (responses with a 200 HTTP response code) in 4 hour increments over the previous 7 days. The timezone is based on the location of the Magento user.

As with overall cache hit, the more often the cache can answer requests for the HTML document, the higher the HTML cache hit count. The higher the number of HTML cache hits, the faster your website loads and the less work is required by your servers. HTML documents are generated for you by Magento and they consume a significant amount of your server resources. By focusing on HTML document caching as the first type of content you try to optimize, you are focusing on the content type that can make the biggest initial improvement to both your performance and server resources. This means you can earn more revenue by providing a better experience for your customers, and you can save money by not having to purchase additional servers with Magento.

To increase the HTML cache hit count, you should start serving these documents from the cache instead of from your server. To setup caching, login to Section Console account and add [configurations for Varnish](/docs/basic-configuration/#varnish).

## HTTP Status Codes
HTTP status codes show how your website responded to a customer request. The extension in Magento is meant to give you an overview, but we recommend that a developer look into the logs in the Section application in order to review the codes as described below in order to make improvements. The chart shows responses by type in 4 hour increments over the previous 7 days. The timezone is based on the location of the Magento user. Here is what each of the response types mean and what you should do about them:

A 200 code is a normal response, which means the customer can get the content they requested (such as your full website page, an image on the page, etc). You want as many 200 codes as possible, as it means a good experience for your customers.

A 3XX code typically means there was a redirect of some kind. This does not mean anything is broken, however, it may mean longer loading times for your customers as at least two items need to be served instead of one (the original and the redirect). You will want to review your 3XX codes and make sure the redirects you have setup for your website are necessary, and then remove the unnecessary ones. You can also update marketing campaigns to point traffic directly to the end destination instead of continuing to point to a site that will trigger a redirect.

A 4XX or 5XX code means that your customer’s request was not answered and can indicate broken links or application error. The difference between a 4XX and a 5XX has to do with why the error took place, and a developer can dig into each error to find out the reason. The most common error in the bucket is a 404 which means that the page was not found. You can [setup custom error messages]({{< relref "debugging/reference/http-error-messages.md#custom-error-messages" >}}) in Section to give your customers a better experience when this does happen until you fix the link.

A 7XX code has to do with the connection, and may be the result of problems with the connection your customer is using to make the request and not the result of your website.
