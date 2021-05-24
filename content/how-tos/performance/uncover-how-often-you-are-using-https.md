---
title: Uncover how often you are using HTTPS
description: Guide for evaluating your website performance and how to use Section to make improvements.
keywords: cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 3
aliases:
  - /performance-techniques/tutorials/performance-evaluation/uncover-how-often-you-are-using-https/
  - /topic-guides/performance-evaluation/uncover-how-often-you-are-using-https/
---

## What is HTTP(S)?

HTTP is a protocol for how web requests are handled. HTTPS is an enhanced version of that protocol to add security by encrypting your customers data so it is protected from threats. You can see when a webpage has HTTPS because the url will show a green padlock.

## Why is it important?

The percentage of requests that have HTTPS show how often your customer data is protected. If this ratio is low, you are putting your customers’ data at a higher risk for incident.  Websites which serve entirely over HTTPS can also take advantage of the performance benefits of HTTP/2 and will be ranked higher by Google in search results.

## How can I see my HTTP(S) requests?

You can view your websites breakdown of HTTP vs HTTPS under Real-Time -> HTTP Logs. To build a nice pie chart, you want to filter by `_type:edge-access-log` which limits the count to only requests to the edge proxy and then split by `scheme` which indicates HTTP or HTTPS. You can see the example for Bootcamp [Bootcamp HTTP vs HTTPS Ratio Piechart][1].

[1]: https://aperture.section.io/account/1/application/1/kibana/#/visualize/create?_a=(filters:!(),linked:!f,query:(query_string:(analyze_wildcard:!t,query:'*')),vis:(aggs:!((id:'1',params:(),schema:metric,type:count),(id:'2',params:(filters:!((input:(query:(query_string:(analyze_wildcard:!t,query:'_type:edge-access-log'))))),row:!t),schema:split,type:filters),(id:'3',params:(field:scheme,order:desc,orderBy:'1',size:5),schema:segment,type:terms)),listeners:(),params:(addLegend:!t,addTooltip:!t,isDonut:!f,shareYAxis:!t),type:pie))&indexPattern=account1-app1-*&type=pie&_g=() 

![Kibana HTTPS Ratio](/docs/images/http(s)-ratio-kibana.png?height=400px)