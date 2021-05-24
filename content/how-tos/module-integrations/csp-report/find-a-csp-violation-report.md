---
title: Find a CSP violation report
description: Find a CSP violation report using Section logging
keywords: content delivery network, CDN, CSP, Report, security, reverse proxies, proxy, proxy template
weight: 1
aliases:
  - /modules/csp-report/how-tos/find-a-csp-violation-report/
---

## Overview

Utilize Section's powerful logging feature to quickly track down which part of a website or application is violating Content Security Policy directives.

### Step 1 - Setup CSP Report module

Follow the instructions from [this page for more details](/docs/modules/csp-report/tutorials/add-csp-report-to-your-proxystack/)

### Step 2 - Search Section logs for violations

1. Log into your Section portal and click `HTTP Logs` from the left nav-bar.

2. Replace the `*` in the search box with the following querie

```
_type:openresty-access-log AND uri_path:"/.well-known/csp_reporting"
```

3. Then add the field `Referrer` as a column.

![Show CSP violation reports in logs](/docs/images/csp-reporting-logging.png)

4. The referrer column will show you which part(s) of the web site or application is violating Content Security Policy directives. If there are a lot of violations, you can simply use Kibana's powerful Visualize feature to find the top offenders, we recommend using a Data Table and splitting the table by the top 5 `Referrers`

![Visualize CSP violation reports in logs](/docs/images/csp-reporting-logging2.png)
