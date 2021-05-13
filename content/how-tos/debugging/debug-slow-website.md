---
title: Debugging a slow website
description: A guide to understanding the reason for an unexpected website slowdown.
keywords: Kibana, Elastic Search, content delivery network, CDN
aliases:
  - /debugging/how-tos/debug-slow-website/
---

## Overview
When investigating a website slowdown, you first want to determine whether the slowdown is originating within the Section platform or at the origin server. The following guide will help you create a visualization of website performance data.

### Step 1 - Creating the visualization

1. Visit your Section portal and view the **HTTP Logs** section of your application. This will open up the Kibana view in it's default state.
1. Proceed to click the visualize tab in the upper nav bar which will prompt you to **Create a visualization**.
1. Select the **Line Chart** option followed by **From a new search**.

{{% notice note %}}
The Kibana view can be opened up in a new tab by clicking the "Open in a new window" button. This is useful if you wish to share the visualization with a colleague.
{{% /notice %}}

### Step 2 - Defining the X-Axis

You will now configure the X-Axis to display the data over a period of time.

1. On the left hand side of the screen you will want to select **X-Axis** under the **Select buckets type** drop down.
1. Select **Date Histogram** as the **Aggregation**.
1. Hit the green play button to view the results.

### Step 3 - Defining the Y-Axis

You will now configure the Y-Axis to display the average time taken in milliseconds for the edge logs.

1. On the left hand side of the screen you will want to select **Y-Axis** under the **metrics** section.
1. Configure the **Aggregation** to show the **Average** value instead of Count and this will prompt you to select a field. Here select the **time_taken_ms** option.
1. Hit the green play button again to view the results of the average time_taken_ms for ALL  logs.

### Step 4 - Splitting the lines

You are now viewing the average time_taken_ms value over your selected time frame for all  logs. Next steps will be to split the lines by log type to pinpoint the cause of the slowdown.

1. On the left hand nav under the X-Axis configuration click the **Add sub-buckets** option.
1. Select the **Split Lines** option which will add a second layer to the X-Axis.
1. In the **Sub Aggregation** option box select the **terms** option.
1. This will prompt you to select another field, this time you will select the **_type** field.
1. Above the **Sub Aggregation** select box, there is an arrow which allows you to make this aggregation the main aggregate. Select the **up arrow**.
1. Hit the green play button again to view the results of the average time_taken_ms for each module type.

Here is an example of the finished product with clear increases in LastProxy access log times. This is a strong indicator for a slowdown at the origin application:

{{% figure src="/docs/images/debugging/origin-slowdown.png" %}}

### Next Steps:

If you see a pattern of clear increases in LastProxy time_taken_ms values that resembles the above screenshot, the slowdown is likely being caused by the origin server and not Section. From here, look into origin server logs and an origin server monitoring solution such as New Relic if available.

If the above investigation reveals increased time_taken_ms values for Edge, Varnish Cache, or another module in your stack but a stable LastProxy value, this could indicate an degradation of service within the Section platform. In this case email support@section.io to immediately receive support from an engineer.

​
