---
title: Filter HTTP logs by URI path
description: Filter HTTP logs by URI path
keywords: kibana, debugging, http logs, uri path
aliases:
  - /debugging/how-tos/filter-http-logs-by-uri-path/
---

### Overview

If you with to filter your HTTP Logs by a particular URI path, you'll first need to open up Kibana located under the **HTTP Logs** section for your application.

### Accessing logs

1. You'll first want to start out by searching for the URI path in the search bar by using the following syntax:
    * `uri_path:"/some/uri/path"`
    * *Note: do not include any query strings*
1. This is bring up a list of all logs where that URI path strictly equals the value to searched for.
1. To analyse the results you can do a few of the following:
    * Add the `_type` field as a column to view the different types of logs. E.g. **edge-access-log**, **varnish-ncsa-log**, or **last_proxy-access-log**.
    * Add the `status` filed as a column to see the status code each module delivered downstream.