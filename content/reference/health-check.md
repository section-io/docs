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

Section uses a health check that queries the path `/.well-known/section-io/aee-hc/healthz?ts=<timestamp>` to check for health of the entire stack of modules and it's ability to handle HTTP traffic. The health check is validating the Section edge components, and Section's ability to communicate with your origin from each PoP, it is **not** checking the health of your origin.

If your Section environment has multiple domain names associated, the health check will use the first domain name, sorted alphabetically, preferring domain names that are confirmed to have the DNS record directed to Section.

Section uses multiple remote-agents throughout the world to query the environment and then the individiual health responses are aggregated. An individual health response is calculated according to the following conditions:

|Scenario|Healthy|
|--- |--- |
|Response timeout|Ignored|
|DNS fails to resolve|Ignored|
|TLS handshake fails (excluding certificate validation)|NOT healthy|
|**Any** response status code sent by the origin|Healthy|
|Response status code is `409` and headers contain `section-ingress: not-configured`|NOT healthy|
|Response status code is an error, e.g. `500` through to `599`|NOT healthy|
|Response status code is any number and does not meet the above conditions|Healthy|

You can read more about [custom debugging headers here](/docs/debugging/reference/debug-headers/).

## Example

You can use the following example to query your environment and confirm if your environment is healthy to handle HTTP traffic :

```bash
curl --head 'https://apps.manibatra.xyz/.well-known/section-io/aee-hc/healthz?ts=12345' \
--header 'section-debug: true' \
--max-time 42

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
