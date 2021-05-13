---
title: Searching HTTP logs using section-io-id
description: Searching in Kibana using section-io-id
keywords: custom logging, logging, Edge logging, Varnish Cache logging, Kibana, Elastic Search, content delivery network, CDN
aliases: 
  - /debugging/how-tos/search-logs-using-section-io-id/
---

In this document and video we show you how to search the HTTP Logs in Section's dashboard by using the value of the `section-io-id' HTTP response header which is present on every response served by Section platform.

### Obtain the section-io-id header value.

If you are using a broswer, you shoulw be able to open up broswer Dev-Tools -> Network, load the page then you should see all the requests the browser made.
Find the request that is of interest and click it. Under Headers, look for the  `section-io-id` response header. It should look something like this:

```
section-io-id: 97031a48002326276ebc1aef2eb40f2d
```
Copy just the value, e.g `97031a48002326276ebc1aef2eb40f2d` then follow the instructions below to search for logs associated with that response.


### Searching in Kibana

{{< youtube FpUrkuFI_uc >}}

* Intro 0:00
* Search by section.io ID 0:49
* Edge proxy 2:17
* Varnish logs 2:58
* WAF 3:34
* Origin proxy 3:56
* Filter by ID 4:14
