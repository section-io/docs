---
title: Debugging
description: Information on Section logs including what information gets passed through logs.
keywords: logs, kibana, elasticsearch, website performance, page speed, webpage speed, website security, content delivery network, CDN
aliases:
  - /logs/
  - /reference/logs/
weight: 300

---

## Debugging with logs

Section is built with operational visibility in mind. One aspect of this is providing you with access to detailed logs of your site's behavior on the Section platform. You can find your logs by clicking the **HTTP Logs** link below the **Real Time** section in Section Console's left-hand side navigation menu.

All web access logs for all traffic flowing through the Section proxies are stored in Elasticsearch and retained for 7 days. We provide you with direct access to Elastic's Kibana tool for querying your log data.

{{< youtube -NMpG78Dj1w >}}

### Basic Logging and Search

In [Basic Logging](/docs/debugging/how-tos/basic-logging/) we cover the basics of HTTP Logs for debugging using Kibana in Section Console dashboard.

### Custom Logging and Search

In [Custom Logging](/docs/debugging/how-tos/custom-logging/) we cover custom HTTP Logs for debugging on Kibana in Section Console dashboard.

### Tutorial

Please review our training [videos on youtube](https://www.youtube.com/watch?v=-NMpG78Dj1w&list=PLfMFVnIIzktEZqFAmwqam5Q1KoOH3-N8u).

## Security Concerns

Section records logs of the URLs and query strings of all requests. If your site uses the URL or query string to transmit sensitive information, please be aware that this data will be captured in the logs. If possible, consider changing your design to send the sensitive information in the request body, or unlogged request headers, instead. See also the [The OWASP Foundation's recommendations on query strings](https://owasp.org/www-community/vulnerabilities/Information_exposure_through_query_strings_in_url) and [CWE-598: Information Exposure Through Query Strings in GET Request](https://cwe.mitre.org/data/definitions/598.html) for more information.

## Table of Contents

{{% children depth="3" %}}
