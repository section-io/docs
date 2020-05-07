---
title: Deleting an Application
description: Guide for deleting your application.
keywords: application, deleting an application
aliases:
  - /how-to/account-management/deleting-an-app/
---

<!-- Here you will find instructions on how to [split your application](#splitting-applications) into multiple content delivery network configurations, as well as how to [delete an application](#deleting-applications) if you wish to start afresh.

## Splitting Applications

A new Section application is configured to handle all HTTP requests on its associated domain, e.g. www.example.com. Many websites, though, will serve different types of responses (e.g. static assets versus user-tailored pages) or even different applications (e.g. a public e-commerce store and a CMS admin site).

These different resources and applications typically have different requirements. It may be redundant to process static CSS requests through a web application firewall (WAF). It could be harmful to operate a caching proxy in front of an authenticated admin-only site.

Most of these scenarios can be catered for with conditional logic in the WAF or cache configuration to decide which requests to handle and which rules are applicable. Conditional configuration like this can quickly grow and become difficult to maintain leading to mistakes, or fear of making changes.

Section allows the URL space of a domain to be subdivided and routed to discrete Section applications with independent configurations, unique proxy stacks, and potentially different origin servers. For example, this means that all URLs beginning with www.example.com/images/ could be handled by one Section application with Varnish Cache  while all other requests could be handled by another application with only ModSecurity.

Only the domain name, HTTPS configuration, and points-of-presence are shared between split applications.

Splitting an application always begins from the first application created for a domain which handles all requests for all URLs. A new application can be created from this original by specifying the prefix of all the URLs that the new application will be responsible for. The new application will start with a configuration identical to the original to ensure live traffic continues to operate unchanged but the new application can then be modified independently to introduce new behaviours.

A split application with a prefix will still observe the original URLs with the prefix still present. Section does not remove the prefix from the URL or modify the HTTP conversation in any other way.

The original application with no-prefix (also considered the / root prefix) can be split multiple times if a different URL prefix is used for each new split application. A split application with a prefix can be further split by specifying a more specific prefix. The follow model is possible:

-   www.example.com/ - original application

> -   www.example.com/admin/ - the admin-only site
> -   www.example.com/assets/ - static assets
>
> > -   www.example.com/assets/images/ - static images only

See the Split option under Overview for your application in Section Console for some more detail.

A split application can later be [deleted](#deleting-applications) and requests for its URL prefix will resume being handled by the original application.

All applications handling requests for a given domain must be within the same Section account. -->

Sometimes you may wish to start an application from scratch or simply remove an unused application.

#### 1) Navigate to application's Overview Page
and click on Actions, then select Delete Application from the drop down menu. Note, if your site is currently live on the Section platform you may wish to point the DNS record for the site away from us before deletion, as deleting the application will cause an outage until you create a new one to replace it.

{{% figure src="/docs/images/delete-app.png" %}}

You will then need to confirm this action by typing in the full name for the application.

{{% figure src="/docs/images/delete-application-confirm.png" %}}
