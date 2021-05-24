---
title: Make a Custom Grafana Dashboard
description: Create custom dashboards that are specific to your application.
keywords: data visualization, Grafana
aliases:
  - /monitoring/how-tos/make-grafana-dashboard/
  - /how-to/make-grafana-dashboard/
---
## Grafana - Custom Dashboards

It may be helpful for you to create a custom dashboard that is specific to your application. You can create your own dashboard by either starting from scratch or duplicating an existing dashboard.

### Creating a dashboard from scratch

To create a dashboard from scratch:  

1. Click on the **Grafana** logo in the left hand corner.  
2. Open the **Dashboards** dropdown.  
3. Click on **New**.  
4. Select the type of panel you want to display (Graph, singlestat, table, pie chart, etc).
5. Click on the **Panel Title** and then click on th edit button as depicted below:

{{% figure src="/docs/images/monitoring/create-new-graphana-dashboard.gif" %}}

6. From here, simply designate the desired metrics to display. A completed example is pictured below:
![Create New Dashboard](/docs/images/monitoring/new-grafana-dashboard-metrics.png?height=450px)
This screenshot contains several features of interest:

  a) Note that the **Queries to** dropdown must be changed to **Graphite**. This connects the dashboard to the graphite metrics associated with your account.

  b) In order to query the data set and see a visualization, you will need to specify a query. Below the Queries to source tab, you will see an empty query with a **select metric** option. Click here to begin enumerating the query. Section already provides dashboards for a number of common queries by default, but you can use this technique to visualize any relevant metrics that are not already being reported. For help determining what metrics are available, visit our [documentation on Graphite](/docs/monitoring/overview/graphite/)

  c) Grafana dashboards can perform and visualize multiple queries simultaneously. This allows you to compare two separate metric values, such as 4xx and 5xx errors.

Finally, save your changes by clicking the **Save** icon on the top of the screen.

### Duplicating an existing dashboard

To create a dashboard from an existing dashboard:  

1. Click on **Dashboard settings** at the top of the screen  
2. Click on **Save as...**
3. Rename the new dashboard  
4. Click **save**.

In order for these changes to be permanent you **MUST** remove the `system` tag from this dashboard. To do this:  

1. Click on **Dashboard settings** once again  
2. Click on **Make editable**. This will allow you to make changes in the dashboard.  
3. In the section called **Tags**, you will want to remove the **system** tag (image below).


![Creating Copy of New Dashboard](/docs/images/monitoring/create-dashboard-duplicate.png?height=500px)
