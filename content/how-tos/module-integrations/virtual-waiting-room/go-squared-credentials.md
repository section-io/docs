---
title: Acquire GoSquared Credentials
description: Using the GoSquared API for the user count.
keywords: Section, training, virtual waiting room, platform overview
weight: 1
aliases:
  - /modules/virtual-waiting-room/how-tos/go-squared-credentials/
  - /modules/virtual-waiting-room/references/go-squared-credentials/
---

## GoSquared Credentials File

`gosquared-visitor-count`

You need to add a file to the root of the repository called:
`gosquared-visitor-count`

The content of file should be:
`<threshold> <ID> <secret> varnish <hostname> <api_key>`

* Where “threshold” is the max number of customer you want on your site.
* Where “ID” comes from end of URL when you are logged into gosquared.
* Where “secret” is a string with no spaces that only you know.
* Where "hostname" is the first hostname(domain name) used in your Section Application.
* Where "api_key" is an api_key for your GoSquared project provided by Section engineering team.

Example:
`300 GSN-000000-M a000000000bc111111111d00000 varnish www.mysite.com jkfjijfejADFD`

The GoSquared ID will be provided by Section engineering team.
