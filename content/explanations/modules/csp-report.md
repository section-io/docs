---
title: CSP Report
description: Using the CSP Report module inside Section.
keywords: CSP, content, security, policy, XSS, injection
aliases:
  - /modules/csp-report/
  - /csp-report/
  - /topic-guides/csp-report/
  - /modules/csp-report/overview/
  - /modules/csp-report/reference/
weight: 1

---

## What does it do

Automatically detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection.

From https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP

> A primary goal of CSP is to mitigate and report XSS attacks. XSS attacks exploit the browser's trust of the content received from the server. Malicious scripts are executed by the victim's browser because the browser trusts the source of the content, even when it's not coming from where it seems to be coming from.

> CSP makes it possible for server administrators to reduce or eliminate the vectors by which XSS can occur by specifying the domains that the browser should consider to be valid sources of executable scripts.

The CSP Report module allows users to easily insert and modify security policies and track which part of a site/application has experienced policy breaches.

---
