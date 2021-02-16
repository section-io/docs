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

When you are ready to start creating more advanced configurations for your proxies, you can start editing the configuration files directly. All of the files in your repository can be accessed by visiting *Advanced Config* under the *Application Edge* menu in the left nav of Aperture. For more information on more basic configurations done through our GUI, check out [quick configuration](/docs/topic-guides/basic-configuration).

In the repository you can see all the files in your repository, commits to those files, stats, and a branching diagram. All of your advanced configuration for any of your reverse proxies will be done by editing the files here.

Inside Advanced Config, you should see one folder for every reverse proxy running on your application and one 'section.config.json' file, where you can add additional reverse proxies to your stack. **If you want to add a new reverse proxy your stack, check out our [guide](/docs/how-to/install-a-new-proxy).**

![Advanced Config](/docs/images/dev/advanced-config-git.png)

## Working locally

Because your Section configuration is a git repository, you can also clone it locally to work with as well as using the web editor.  This is particularly helpful if you want to do local development with our [Developer Pop](/docs/developer-workflow/).

Copy the URL from the *Advanced Config* page labelled *Clone with HTTPS* and use this to run `git clone <url-from-advanced-config>`.

### Git Authentication

There are two ways to authenticate git.  If you log into Aperture with a username & password you can just use those credentials to also authenticate git.  If you access Aperture via SSO, or you don't want to use your main credentials for git, you can also authenticate with an API token. If you don't already have an API token, [follow these instructions to create one](/docs/api/api-tokens/#creating-an-api-token). Once that is done you can authenticate git using `section-token` as the username and the token value as the password.