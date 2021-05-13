---
title: View response metrics by region
description: A guide to testing the time_taken_ms response times across different regions.
keywords: webpage test, testing, speed, regions
aliases:
  - debugging/how-tos/view-response-metrics-by-region/
---

## Overview

This is a guide to help you test the response times in milliseconds across different regions. You will be utilizing the Kibana/HTTP Logs view to break down the `time_taken_ms` field on the edge-access-log type by the `geoip.country_code2` field.

### Step 1 - Creating the visualization

1. Visit your Section portal and view the **HTTP Logs** section of your application. This will open up the Kibana view in it's default state.
1. Proceed to click the visualize tab in the upper nav bar which will prompt you to **Create a visualization**. 
1. Select the **Line Chart** option followed by **From a new search**.

{{% notice note %}}
The Kibana view can be opened up in a new tab by clicking the "Open in a new window" button. This is useful if you wish to share the visualization with a colleague. 
{{% /notice %}}

### Step 2 - The search term

You should be viewing a line chart with a single data point and the term "*" in the search input. For this visualization we will want to only view the **edge-access-log**. Copy and paste the following into the search box to view only the edge logs:

`_type:edge-access-log`

### Step 3 - Defining the X-Axis

You will now configure the X-Axis to display the data over a period of time. 

1. On the left hand side of the screen you will want to select **X-Axis** under the **Select buckets type** drop down. 
1. Select **Date Histogram** as the **Aggregation**.
1. Hit the green play button to view the results.

{{% notice note %}}
At this time you are viewing the total number of edge-access-logs (Count metric) over a period of time. 
{{% /notice %}}

### Step 4 - Defining the Y-Axis

You will now configure the Y-Axis to display the average time taken in milliseconds for the edge logs.

1. On the left hand side of the screen you will want to select **Y-Axis** under the **metrics** section.
    * The Y-Axis is already configured to show the **Count** metric as we previously saw while defining the X-Axis.
1. Configure the **Aggregation** to show the **Average** value instead of Count and this will prompt you to select a field. Here we will find the **time_taken_ms** option to select.
1. Hit the green play button again to view the results of the average time_taken_ms for ALL edge logs.

### Step 5 - Splitting the lines

You are now viewing the average time_taken_ms value over your selected time frame for all edge logs. Next steps will be to split the lines by country code.

1. On the left hand nav under the X-Axis configuration click the **Add sub-buckets** option.
1. Select the **Split Lines** option which will add a second layer to the X-Axis. 
1. In the **Sub Aggregation** option box select the **terms** option.
1. This will prompt you to select another field, this time you will select the **geoip.country_code2** field.
1. Above the **Sub Aggregation** select box, there is an arrow which allows you to make this aggregation the main aggregate. Select the **up arrow**.
1. Hit the green play button again to view the results of the average time_taken_ms for edge logs broken down by the top 5 country codes during your selected time frame.

### Additional notes

{{% notice note %}}
You can include more than the default 5 results by increasing the **Size** option under the **geoip.country_code2** aggregate configuration.
{{% /notice %}}

{{% notice note %}}
If you are interested in a select few country codes, then you can append search terms to your global search. For example:

`_type:edge-access-log AND (geoip.country_code2:US OR geoip.country_code2:AU)`
{{% /notice %}}