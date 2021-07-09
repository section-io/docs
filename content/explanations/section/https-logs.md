---
title: HTTP Logs
description: An overview of the platform's HTTP logging functionality.
type: "docs"
keywords: monitoring, graphite, metrics, logs
weight: 1
aliases:
  - /logs/
  - /debugging/overview/
  - /graphite/
  - /topic-guides/platform-monitoring/http-logs/
---

## HTTP Logs

Clicking on "HTTP Logs"  in the left navigation bar opens up a view of Kibana. Kibana will allow you to search through your logs to dig deeper into trends you found in Graphite or Grafana. To open Kibana in its own window, click the “open in new window” button at the top of the Kibana frame.

On the Discover view in Kibana, you can either select items from the left nav, or type searches into the search bar. Here are a fields that are useful to know:

* **varnish_handling** - will add a column and show you whether a log was a hit or a miss.
* **varnish_handling:miss** - will show all logs that were misses
* **content_type** - shows you whether the content was image, html, js, etc
* **status** - shows response code (200, 3XX, 4XX, etc)
* **_type** - will indicate if the log was for varnish, origin proxy, last proxy, etc
* **scheme** - will indicate if the request was HTTP or HTTPS

You can then take these searches and turn them into different Graphs in the “Visualization” view. Then you can save these visualizations to a Dashboard to view later under the “Dashboard” view.

If you want to analyze your website using Graphite, start by grouping metrics such as error rates, cache hit and miss rates and then apply functions to help smooth data points for bigger trends or show variance between individual data sets.

### Related

* [Basic Logging and Search](/docs/debugging/how-tos/basic-logging/ "Basic Logging and Search")
* [Custom Logging and Search](/docs/debugging/how-tos/custom-logging/ "Custom Logging and Search")
* [Debugging Howtos](/docs/debugging/how-tos/ "Debugging Howtos")
* [Debugging Reference Guides](/docs/debugging/reference/ "Debugging Reference Guides")

