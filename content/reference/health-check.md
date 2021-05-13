---
title: Health Checks
description: Explanation of built-in health checks in the Section platform
keywords: health, health-check, environment, edge
aliases:
  - /health-checks/
  - /reference/health-checks/
  - /docs/platform/reference/health-checks/
  - /platform/reference/health-checks/
---

Section platform has a default built-in HTTP health check that monitors the health of the environment across multiple locations in the world.

Section uses a health check that queries the path `/.well-known/section-io/aee-hc/healthz?ts=<timestamp>` to check for health of the entire stack of modules and it's ability to handle HTTP traffic.

Section uses multiple remote-agents throughout the world to query the environment and then the individiual health responses are aggregated. An individual health response is calculated according to the following conditions :

|Scenario|Healthy|
|--- |--- |
|error: timeout|irrelevant|
|error: dns|irrelevant|
|error: tls, note: that this does not validate the certificate|false|
|Anything other than a HTTP 200 OK from the Remote Agent|irrelevant|
|headers contains section-origin-status and the value is not 000 and not empty|true|
|status: 409 and headers contains section-ingress: not-configured|false|
|status: 5-- where -- is any number|false|
|status is any number and does not meet the above conditions|true|

You can read more about [custom debugging headers here](/docs/debugging/reference/debug-headers/).

## Example

You can use the following example to query your environment and confirm if your environment is healthy to handle HTTP traffic :

```bash
curl --head 'https://apps.manibatra.xyz/.well-known/section-io/aee-hc/healthz?ts=12345' \
--header 'section-debug: true' \
--max-time 30

HTTP/2 404
date: Tue, 27 Apr 2021 04:53:20 GMT
content-type: text/html
content-length: 6118
vary: Accept-Encoding
vary: Accept-Encoding
etag: "60878fc3-17e6"
section-origin-dns-failure: false
section-origin-status: 404
section-origin-time-seconds: 0.271
section-io-id: 51a17b0c4b0f233e711ad1a1b256c2fd

```

In the above example we query an environment with the hostname **apps.manibatra.xyz**. The above response is deemed healthy according to the conditions mentioned above.
