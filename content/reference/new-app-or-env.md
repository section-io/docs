---
title: Adding a New Domain to Section
description: Guide to choosing a new environment, new application, or adding a domain to an existing environment.
keywords: reverse proxy, CDN
aliases:
  - /platform/reference/new-app-or-env/
---

When you want to add a domain to Section, it is sometimes unclear where that domains should fit into your existing [account](/docs/platform/account/), [application](/docs/platform/application/), and [environment](/docs/platform/environment/) structure. This guide will help you decide whether it is most appropriate to create a new application, create a new environment, or add a new domain to an existing environment.

#### My new website is a staging/uat site for a production site that I have running or want to run on Section

The purpose of Section's application-environment structure is to streamline the configuration testing and promotion process for modules in your stack. With respect to configuration, the definition of an application is a git repository, and the definition of an environment is a branch within that repository. This makes testing changes to the staging environment and then promoting them to the production environment as simple as a git merge and push.

If you want to add a staging site to Section, the best solution for most use cases is to add a new environment to the same application (or use the Staging environment that comes by default whenever you create a new environment).

**Summary**: we recommend adding a new staging site to an existing application as a new environment.

#### I want to add a new website to Section that is similar to one or more sites I already have running on Section

Section maintains running containers for each module in your stack in each point of presence on a per environment basis. That means that if you assign www.example.com and www.demonstration.com to the same Section environment, the same containers will handle traffic for both sites. If you have a new site that has similar needs and configuration patterns to a site that is already running on section, then assigning both domains to the same environment greatly simplifies the overhead of managing them.

When two sites have the same URI patterns for resources and routes that should and should not be cached (i.e. both are set up for HTML caching and use the same routes for admin functionality or checkout), then it often makes sense to assign both of these domains to the same environment.

It is even possible to assign two domains to the same environment when the websites are running on different origin servers. Section supports routing requests to [alternate origins](/docs/platform/environment/how-tos/multiple-origins/) based on the incoming request's hostname or other criteria.

If the websites are mostly the same but have a few important differences, you can manage this as well within a single configuration by building hostname specific logic into your Varnish Cache Configuration:

    if (req.url ~ "/admin" && req.http.host == "www.example.com") {
      // Take action A
    } else if (req.url ~ "/admin" && req.http.host == "www.demonstration.com") {
      // Take action B
    }

**Summary**: If two websites have similar CDN/Edge compute needs, they should be mapped to the same environment.

#### I want to add a new website that is very different from all the sites I have running on Section

If you want to add a new site that has different needs from all the other sites you have running on Section, then creating a new application is often the best choice. As mentioned previously, one application corresponds to one git repository, so you will be able to manage the configuration for these two sites independently of one another. Some example use cases include:

1) Your new site is built in a different framework or has a different architecture such that you would need to write many site specific VCL directives (if using Varnish Cache).

2) Similar to the above, your new site is set up for a different kind of caching than your other sites. For example, site A is built for HTML caching via hole-punching, but site B caches HTML with ISE.

3) You want to run a different module configuration on the new site — such as adding or removing a WAF or image optimizer.

Note that it is possible to set up a new domain as another environment within the same application (Section supports multiple environments with names other than Staging or Production). While this allows all of your sites to share one git repository (a fact which does not particularly benefit you if the sites are different enough to not be mapped to the same environment), your sites will also share the same Kibana logs — meaning that logs from site A will be mixed in with logs from site B.

**Summary**: If two websites have different configuration needs or require different modules to run in the stack, these two domains should be in separate applications
