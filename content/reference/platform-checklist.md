---
title: "Terminology"
description: ""
weight: 120
aliases:
  - /reference/terminology/
  - /platform/
  - /topic-guides/platform-monitoring/
  - /platform/overview/
  - /platform/reference/entities-and-nomenclature/
  - /entities-and-nomenclature/
  - /reference/entities-and-nomenclature/
---
Overview of the key entities and account structure referred to throughout Section.

| Component | Function | Description
|:--|:--|---|
| [Account](/docs/platform/account/ "Account overview") | Organization | Users can be associated with one or many accounts. Accounts represent organizations like businesses. The Account is the master structure of Section. Accounts may contain many Applications and Users. |
| [API](/docs/api/ "API overview") | API | Section JSON RESTful API to manage the users, accounts, applications, environments, domains and logging. |
| [Aperture](/docs/platform/reference/aperture/ "Aperture overview") | Dashboard | Section web portal to manage the users, accounts, applications, environments, domains and logging. |
| [Application](/docs/platform/application/ "Application overview") | Website configuration | Configuration for your content-delivery and proxy setup, monitors HTTP traffic from the client through your proxy stack to your origin and back again, and manages the state of your website content. Generally an Application is defined by the url for a website or web Application. Each Application may have multiple Environments (e.g. Production and Development) and can have multiple Users with access to the Environment(s) for that Application. |
| [Domains](/docs/dns/ "Domains overview") | www.yourdomain.com  mysecond-domain.com | Each application can also have multiple domains for any number of websites with the same proxy configuration setup, greatly simplifying the management process for many similar sites. |
| [Edge Proxy](/docs/platform/reference/edge-proxy/ "Edge Proxy overview") | Ingress / Edge Proxy | Every application proxy stack begins with the Edge proxy. |
| [Environment](/docs/platform/environment/ "Environment overview") | Staging, Development, Production etc  | Environment defines the functional space within which the Proxy Instance is working for the Application. Section means Users can seamlessly move a Proxy Stack configuration between Environments. An application supports multiple environments like staging, development, and production on git branches within the application repository. Each of these environments can have different proxy configurations. |
| [Instance](/docs/ "Instance overview") | Software & Configuration | Each User’s copy of the Proxy Stack for the application is referred to as an Instance. Generally, there will be multiple Instances of the Development Environment where there are multiple users working on the Proxy Stack for that Application. Usually, there will be only one Production instance and in normal development workflows, a limited number of instances for Test or Staging Environments. |
| [Modules](/docs/modules/ "Modules overview") | Software & Configuration | Section offers modules of open source and commercial software solutions that form a proxy stack. |
| [Proxy](/docs/platform/reference/entities-and-nomenclature/#proxy "Reverse Proxy overview") | Reverse Proxy | A Proxy or "Reverse Proxy” is the server handling requests within each environment e.g. Varnish Cache. A Proxy (or more technically correct “Reverse Proxy”) is the server handling requests within each environment (e.g. Varnish Cache ). The nature and configuration of the Proxy is subject to the changes a user may make in the respective environments. Section’s commands can then be called to synchronise the configuration of the Proxies between the Instances in each Environment. |
| [Proxy Stack](/docs/platform/reference/example-proxy-stacks/ "Proxy Stack overview") | Chained Proxies | Where more than one Proxy is “chained” together we refer to this as a Proxy Stack. Where more than one Proxy is “chained” together we refer to this as a Proxy Stack. E.g Combining two Proxies to work together such as Varnish Cache and Mod Security or Varnish Cache and Nginx would provide the user with a Proxy stack. |
| [Support](/docs/platform/support/ "Support overview") | Customer Engineers | Section is a managed platform and Customer Engineers are ready to support. |
| [User](/docs/platform/reference/entities-and-nomenclature/#users "User overview") | User management | Users can manage accounts, environments, applications etc. Users are defined by an email address. There may be many users per Account. A User may haver access to more than one Account. Each User may have access to multiple Environments within any Account. e.g. Development and Production|
