---
title: "Configurations with GIT"
description: ""
weight: 1
aliases:
  - /topic-guides/advanced-configuration/
  - /topic-guides/advanced-config/
  - /platform/reference/configurations-with-git/
---

## Configuration

When you are ready to start creating more advanced configurations for your proxies, you can start editing the configuration files directly. All of the files in your repository can be accessed by visiting Repository under the Configuration menu in the left nav of Section Console. For more information on more basic configurations done through our GUI, check out [quick configuration](/docs/topic-guides/basic-configuration).

In the repository you can see all the files in your repository, commits to those files, stats, and a branching diagram. All of your advanced configuration for any of your reverse proxies will be done by editing the files here.

Inside Advanced Config, you should see one folder for every reverse proxy running on your application and one 'section.config.json' file, where you can add additional reverse proxies to your stack. **If you want to add a new reverse proxy your stack, check out our [guide](/docs/how-to/install-a-new-proxy).**
