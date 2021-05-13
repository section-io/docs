---
title: "Platform"
description: ""
weight: 120
aliases:
  - /platform/
  - /topic-guides/platform-monitoring/
  - /platform/overview/
---

| Component | Function | Description
|:--|:--|---|
| [Account](/docs/platform/account/ "Account overview") | Organization | Users can be associated with one or many accounts. Accounts represent organizations like businesses. |
| [API](/docs/api/ "API overview") | API | Section JSON RESTful API to manage the users, accounts, applications, environments, domains and logging. |
| [Aperture](/docs/platform/reference/aperture/ "Aperture overview") | Dashboard | Section web portal to manage the users, accounts, applications, environments, domains and logging. |
| [Application](/docs/platform/application/ "Application overview") | Website configuration | Configuration for your content-delivery and proxy setup, monitors HTTP traffic from the client through your proxy stack to your origin and back again, and manages the state of your website content. |
| [Domains](/docs/dns/ "Domains overview") | www.yourdomain.com  mysecond-domain.com | Each application can also have multiple domains for any number of websites with the same proxy configuration setup, greatly simplifying the management process for many similar sites. |
| [Edge Proxy](/docs/platform/reference/edge-proxy/ "Edge Proxy overview") | Ingress / Edge Proxy | Every application proxy stack begins with the Edge proxy. |
| [Environment](/docs/platform/environment/ "Environment overview") | Staging, Development, Production etc  | An application supports multiple environments like staging, development, and production on git branches within the application repository. Each of these environments can have different proxy configurations. |
| [Modules](/docs/modules/ "Modules overview") | Software & Configuration | Section offers modules of open source and commercial software solutions that form a proxy stack. |
| [Proxy](/docs/platform/reference/entities-and-nomenclature/#proxy "Reverse Proxy overview") | Reverse Proxy | A Proxy or "Reverse Proxy” is the server handling requests within each environment e.g. Varnish Cache. |
| [Proxy Stack](/docs/platform/reference/example-proxy-stacks/ "Proxy Stack overview") | Chained Proxies | Where more than one Proxy is “chained” together we refer to this as a Proxy Stack. |
| [Support](/docs/platform/support/ "Support overview") | Customer Engineers | Section is a managed platform and Customer Engineers are ready to support. |
| [User](/docs/platform/reference/entities-and-nomenclature/#users "User overview") | User management | Users can manage accounts, environments, applications etc. |

### Table of contents

{{% children depth="3" %}}