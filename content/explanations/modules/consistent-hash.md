---
title: Consistent Hash
description: Consistent Hash Module overview
weight: 1
aliases:
  - /modules/consistenthash/
---

## What does it do

This module is built on the Section OpenResty module and provides a more robust upstream definition by load balancing traffic using an internal consistent hash to select the right upstream node.

Available hashed key values:

* True-Client-IP
* URI Path

See the [set up guide]({{< relref "modules/consistenthash/set-up/_index.md" >}}) to implement this module into your module stack.