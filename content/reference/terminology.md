---
title: Terminology
description: Definition of terms used by Section.
keywords: account management, proxy, proxy configuration, reverse proxies, content delivery network, CDN
aliases:
  - /platform/reference/entities-and-nomenclature/
  - /entities-and-nomenclature/
  - /reference/entities-and-nomenclature/
---

Overview of the key entities and account structure referred to throughout Section

## Account

The Account is the master structure of Section. Accounts may contain many Applications and Users.

## Application

Generally an Application is defined by the url for a website or web Application. Each Application may have multiple Environments (e.g. Production and Development) and can have multiple Users with access to the Environment(s) for that Application.

## Environment

Environment defines the functional space within which the Proxy Instance is working for the Application. Section means Users can seamlessly move a Proxy Stack configuration between Environments.

## Users

Users are defined by an email address. There may be many users per Account.

A User may haver access to more than one Account.

Each User may have access to multiple Environments within any Account. e.g. Development and Production

## Instance

Each User’s copy of the Proxy Stack for the application is referred to as an Instance. Generally, there will be multiple Instances of the Development Environment where there are multiple users working on the Proxy Stack for that Application. Usually, there will be only one Production instance and in normal development workflows, a limited number of instances for Test or Staging Environments.

{{% figure src="/docs/images/peterman-account.png" title="Account Example" %}}

## Proxy

A Proxy (or more technically correct “Reverse Proxy”) is the server handling requests within each environment (e.g. Varnish Cache ). The nature and configuration of the Proxy is subject to the changes a user may make in the respective environments. Section’s commands can then be called to synchronise the configuration of the Proxies between the Instances in each Environment.

## Proxy Stack

Where more than one Proxy is “chained” together we refer to this as a Proxy Stack. E.g Combining two Proxies to work together such as Varnish Cache  and Mod Security or Varnish Cache  and Nginx would provide the user with a Proxy stack.
