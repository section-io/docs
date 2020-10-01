---
title: Extract domain based metrics
description: How to extract domain level metrics for your own consumption
keywords: data, API
aliases:
  - /how-to/extract-domain-based-metrics/
---

## Extract domain based metrics

In addition to standard platform metrics you can enable domain based metrics extraction.

Email support@section.io to have this enabled on your account.

Once enabled this will allow you to connect to a metrics endpoint to extract data.
(Interesting fact: The endpoint is a prometheus source, you could federate this and point your own prometheus infrastructure at this location)

### Data available

This endpoint provides the following data:
HTTP Requests and Bytes used by Account
HTTP Requests and Bytes used by Application
HTTP Requests and Bytes used by Environment
HTTP Requests and Bytes used by Module (Not normally needed)

### Process to extract domain based metrics

When logged into Section Console you can browse to the following uri (Replace ACCOUNTID with your own account ID): `https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query_range`

Metrics names available:

* `section_http_bytes_rate:by_module_name_and_hostname`
* `section_http_count_rate:by_module_name_and_hostname`

Labels:

`section_io_account_id`

`section_io_application_id`

`section_io_environment_id`

`section_io_module_name`

* “`private-ingress`” This is the first customer visible layer that incoming clients (eg browsers) connect to, Use this when looking for usage totals
* “`varnish`” Metrics from a module in the stack named “varnish” which is commonly the caching layer (may or may not be included in a customers configuration)

`hostname`
* Domain name of the incoming client

Example queries:

All data for Account:
`https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query_range?query=section_http_request_count_rate%3Aby_module_name_and_hostname%7Bsection_io_module_name%3D%22private-ingress%22%2C%20section_io_account_id%3D%221949%22%7D*60&start=1595446578.479&end=1595468178.479&step=60&_=1595467942570`

Restrict to specific domain:
`https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query_range?query=section_http_request_count_rate%3Aby_module_name_and_hostname%7Bsection_io_module_name%3D%22private-ingress%22%2C%20section_io_application_id%3D%227210%22%2C%20hostname%3D%22www.example.com%22%7D*60&start=1595461225.853&end=1595468425.853&step=60&_=1595467942575`

Examples with curl:
When using curl / remote systems ensure you had created a username and password in the Section Account that you are querying and included this in the uri as per below:

`curl -g --user username:password “https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query_range?query=section_http_request_count_rate%3Aby_module_name_and_hostname%7Bsection_io_module_name%3D%22private-ingress%22%2C%20section_io_account_id%3D%221949%22%7D*60&start=1595446578.479&end=1595468178.479&step=60&_=1595467942570”`

Summarise all data for the last 24hrs for a specific domain:

`curl -g --user username:password "https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query_range?query=sum(sum_over_time(section_http_request_count_rate%3Aby_module_name_and_hostname%7Bhostname%3D%22www.example.com%22%2Csection_io_account_id%3D%22ACCOUNTID%22%2Csection_io_module_name%3D%22private-ingress%22%7D%5B86400s%5D))*(60)&start=1601437080.527&end=1601523480.527&step=86400&_=1601509374478"`


Query API is also available:
`https://aperture.section.io/account/ACCOUNTID/prometheus/api/v1/query?query=section_http_request_count_rate%3Aby_module_name_and_hostname%7Bsection_io_module_name%3D%22private-ingress%22%2C%20section_io_application_id%3D%227210%22%2C%20hostname%3D%22www.example.com%22%7D*60`



### Notes:

1. The step function you specify has impacts on how fast (or slow) your query will respond. Follow these guidelines:
    1. Never make step less than 60 seconds as this will not increase granularity of results 
    2. If pulling a 60 second step don't request more than 2-3hrs of data
    3. If pulling 24hr usage try a step of 1hr of more
2. Expect 7 days of metric retention



