---
title: Basic Logging
description: Basic logging and search using Kibana
keywords: custom logging, logging, Edge logging, Varnish Cache logging, Kibana, Elastic Search, content delivery network, CDN
aliases:
  - /basic-logging/
  - /how-to/basic-logging/

---

In this document and video we get a basic demo of how to search the HTTP Logs in Section's dashboard called Section Console.

Use the Kibana 4 HTTP Logs to debug the proxy stack for possible issues with origin or the application in Section.

{{< youtube -NMpG78Dj1w >}}

* Intro 0:00
* First time setup 1:33
* Basics 2:17
* Filters 3:26
* Manual search 5:28
* Tip 1 - faster work flow 6:52
* Tip 2 - CSV exporter 7:24

### HTTP Logs

Login to Section's dashboard Section Console and click the HTTP Logs link.

{{% figure src="/docs/images/debugging/basic1.png" %}}

### HTTP Logs Screen

Open the HTTP Logs screen and view Kibana wrapped inside an iframe in Section Console.

{{% figure src="/docs/images/debugging/basic2.png" %}}

### Launch HTTP Logs in Full Window

Click the Open in New Window button which opens HTTP Logs Kibana screen in a full browser window. You are now in the Discover tab.

{{% notice info %}}
It is useful to open Kibana HTTP Logs in full screen so you can copy and paste URLs for logs
{{% /notice %}}

{{% figure src="/docs/images/debugging/basic3.png" %}}

### Adjust the time period

Click the top right hand corner of the Kibana screen next to the Clock or time icon which by default is 15 minutes.

{{% figure src="/docs/images/debugging/basic4.png" %}}

### Expand time period filter pane

Clicking expands the time period filtering and defaults to Quick.

{{% figure src="/docs/images/debugging/basic5.png" %}}

#### Quick time period filters explained

The Quick section has options like Today, This Week, Last Hour, Last 4 Hour etc.

{{% notice info %}}
Section only keeps Kibana 4 HTTP Logs for the most recent 7 days.
{{% /notice %}}

{{% figure src="/docs/images/debugging/basic6.png" %}}

#### Relative time period filters explained

The Relative filter pane in Kibana allows custom relative filters. i.e. 18 minutes from now, 75 minutes from now, 275 minutes from now.

{{% figure src="/docs/images/debugging/basic7.png" %}}

#### Absolute time period filters explained

Absolute searches are useful for selecting a range of time between two dates. This can be useful for investigating a known incident.

{{% figure src="/docs/images/debugging/basic8.png" %}}

### Kibana tabs: Discover, Visualize, Dashboard & Settings

Along the top of the HTTP Logs screen to the right of the Kibana logo are 4 tabs: Discover, Visualize, Dashboard & Settings.

{{% figure src="/docs/images/debugging/basic9.png" %}}

### Kibana Settings

Click on the Kibana Settings tab and select the Indices and a log pattern. You can now see all fields in the index which we can use the make reports in the main Discover tab.

{{% figure src="/docs/images/debugging/basic10.png" %}}

## Demo Search on Edge Access edge-access.log

We will now do a demo search on the edge access log.

The Edge Access log is the first log in the Section proxy stack and is often a useful log to investigate the interface between Section and the origin server.

{{% figure src="/docs/images/debugging/edge1.png" %}}

### Select _type edge-access.log

Select the edge-access.log by selecting the popular _type filter and then click on the magnifying glass icon. This adds a search filter for the edge proxy. 

{{% figure src="/docs/images/debugging/edge-log-animated.gif" %}}
