---
title: "Platform Monitoring"
description: "An overview of the ways Section monitors your application internally and the tools we provide to access that information"
aliases:
  - /threat-x/
  - /topic-guides/platform-monitoring/
---

Section provides two different ways to gather information and metrics about your app's performance on the platform. First of all, we keep detailed logs of every request that passes through our system. These logs are queryable through the Kibana instance associated with your application and remain in our system for seven days. Because of their high detail but relatively short lifespan, these logs are ideal for debugging but not very effective at establishing long term trends or comparing past and present performance data.

The second type of metrics we provide last for 13 months and are queryable through your application's Grafana instance or through Graphite's GUI directly. While these metrics provide much less detail relative to the first type, their longevity allows for long term trends to be established.

This section of the documentation is largely devoted to Monitoring, or observing and identifying trends in performance primarily using the second type of logs. For information on using Kibana for debugging and other information gathering, please see [our debugging documentation](/docs/debugging).

{{% children depth="3" %}}
