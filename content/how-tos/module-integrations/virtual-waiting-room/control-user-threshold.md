---
title: Control User Threshold
description: How to increase/decrease concurrent user count on the site?
keywords: Section, training, platform overview
weight: 1
aliases:
  - /modules/virtual-waiting-room/how-tos/control-user-threshold/
---

## Overview

The Virtual Waiting Room module offers an easy to use interface to control the max number of concurrent users on the site.

### Increase/Decrease user threshold

The maximum number of concurrent users can be increased/decreased easily by using the counter under the Control Visitor Count section.

{{% figure src="/docs/images/vwr_config.png" %}}

This can also be controlled directly by changing the *threshold* value in the **[Advanced Configuration](/docs/modules/virtual-waiting-room/reference/virtual-waiting-room-advanced-configuration/)**  and the **[GoSquared Credentials file](/docs/modules/virtual-waiting-room/reference/go-squared-credentials/)**

{{% notice note %}}
The default behavior is to force all users to be rechecked if you reduce the number of users allowed on your site. This may cause some users currently on the site to be put into the waiting room. If you uncheck *Apply threshold to existing users?* option, user's currently on the site won't be kicked off. It will only naturally decrease. This values always defaults to on.
{{% /notice %}}
