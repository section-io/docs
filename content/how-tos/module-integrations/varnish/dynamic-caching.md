---
title: Configure Dynamic Content Caching
description: An overview of the different ways to cache dynamic content on the platform.
keywords: dynamic caching, caching, cache
aliases:
  - /modules/varnish-cache/how-tos/dynamic-caching/
  - /topic-guides/dynamic-caching/
  - /modules/varnish-cache/reference/dynamic-caching/

---

Caching is so effective at boosting website performance because delivering web content involves extreme repetition. Web servers receive requests for identical static assets and HTML documents thousands (or hundreds of thousands) of times per day. Caching allows the web server delegate this repetition to the caching layer and only respond to a small fraction of these requests. Eliminating this repetition makes your web server significantly more efficient and can drastically reduce server costs.  

This simple formula becomes more complicated, however, when a website introduces authenticated content. These assets are no longer identical — they have important personal information unique to the user making the request. When authentication is involved, caching becomes dangerous. The last thing you want is session leakage: a situation in which one user's personal information is cached and served to another user. Below are two techniques that have been developed to maximize caching while avoiding the potential downfalls of dealing with authenticated content.

## Intelligent Session Establishment (ISE)

Because of the significant risks around caching authenticated content, Varnish Cache  does not cache backend responses with any set-cookie headers by default. It also does not look up responses in cache for any requests with cookies on them. The thinking here is that if a backend is responding with a set-cookie header, the response is likely to have some authenticated, user-specific content, or if a client has a cookie, then they're asking for the same. This makes sense in theory, but the problem is that many modern web development frameworks set cookies on non-authenticated responses, greatly reducing Varnish's caching rate out of the box. To Varnish Cache , a much higher percentage of modern web traffic looks uncacheable than actually is.

Intelligent Session Establishment is a technique that solves this problem by using Varnish Cache Configuration Language (VCL) to cache and look up in cache the traffic that Varnish Cache  thinks is authenticated but actually is not.

In order to implement this, you need to know a few things about your platform. The first thing you need to know is the actual cookie that establishes your session. Once you know this, you can specifically instruct Varnish Cache  to pass over any traffic that has or is setting this cookie, but cache ones that have or are setting other cookies. Next, you need to know what routes you want Varnish Cache  to treat as uncacheable no matter what. This would be routes like '/checkout' or '/admin'. Once you have written VCL excluding these two types of requests, you can instruct Varnish Cache to cache other kinds of traffic.

For more information on implementing ISE, [check out this article](https://community.section.io/t/a-novel-way-to-cache-html/79).

## Hole-Punching

Even though authenticated pages clearly have user-specific and therefore uncacheable personal information, they also have a lot of generic and reusable resources on them. User account pages, for example, are literally designed to display unique personal data, but they also reuse much of the same HTML and CSS for every customer. As long as we're sending a user account page via a single response, though, we miss out on caching all this generic content.

Hole-punching is a design pattern that solves this problem by loading the authenticated and unauthenticated content for a single page with different requests. To implement hole-punching for a user account page, for example, you would configure the application to respond to such a request with the generic HTML document and other reusable resources, and then load the user-specific information with additional requests — either AJAX or ESI calls (Edge Side Includes). This way, you can cache the generic content and leave the authenticated content completely alone.

## HTML Streaming

No matter how session-specific and customized a page is, typically the head of the HTML document for a given URL is the same for every user. From a website optimization perspective, anything that is reliably the same can be cached. HTML Streaming is a technique that leverages this consistent repetition of the head tag in order to optimize delivery. With HTML streaming implemented, our platform separates out the head and body of incoming HTML documents and then caches the head portion. For all subsequent requests for that URL, Varnish Cache  delivers the HTML head immediately with an embedded ESI tag which requests the body.

Beyond the obvious performance benefits of caching a piece of the HTML document, HTML streaming offers extremely fast time-to-first-byte on pages that cannot be cached according to traditional methods.

## Summary

ISE is a technique that is implemented at the Section level and allows us to cache as many valid responses as possible. Hole-punching is a design pattern implemented on your origin application that separates authenticated and unauthenticated information into separate requests to allow for maximum caching. HTML streaming offers quick time-to-first-bytes by selectively caching HTML documents.

For implementation questions on any of these, contact our engineering team at `support@section.io`
