---
title: Debug Headers
description: Use  debug headers provided by Section to debug a response.
keywords: debug headers, errors, Edge debug, content delivery network, CDN
aliases:
  - /debug-headers/
  - /how-to/debug-headers/

---
#### Overview

Section provides a range of debug-headers that are disabled by default. These headers can be enabled by sending the `section-debug` header set to any value. Section provides the following debug headers :

- section-origin-status
- section-origin-failure
- section-origin-dns-failure
- section-origin-time-seconds

#### section-origin-status

- When no bytes are received from the origin web server (e.g. DNS failures) `s​ection-origin-status` header is set to "000".

- When a response is received from the origin web server `section-origin-status` is set to upstream status when the upstream-status is a single status code and the last value when the upstream-status is an array of response codes (e.g. due to retries)

#### section-origin-failure

When no bytes/response is received from the origin web server and Section can resolve the DNS for the origin web server (a request to the origin is made) `section-origin-failure` header is set to `true` else it is not set.

#### section-origin-dns-failure

When Section is unable to resolve the DNS of the origin web server `section-origin-dns-failure header` is set to `true` else it is set to `false`.

#### section-origin-time-seconds

This header indicates in seconds the time taken by the Section platform to receive the entire response from the origin web server.
