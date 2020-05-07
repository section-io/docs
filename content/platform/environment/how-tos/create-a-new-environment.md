---
title: Create a New Environment
description: A guide to adding an environment to an existing applications
keywords: environment, application
aliases:
  - /how-to/account-management/create-a-new-environment/
weight: 2
---

This is a guide for setting up a new environment within an existing Section application.

### 1) Log Into Section Console

### 2) Click on the Application in which you want the new environment
  The number of options that appear here will vary depending on the number of applications associated with your account.

![Select Application](/docs/images/select-app.png?height=190px)
### 3) Click on the **Create Environment** button

{{% figure src="/docs/images/environment-button.png" %}}

### 4) Fill in **New Environment Name**
  This **environment name** becomes the name of a git branch within your application repository for the new environment's config. For a thorough explanation of how Section applications and environments use git, see our [overview](/docs/topic-guides/account-management).

### 5) Fill in **Hostname**
  Although Section supports many domains on a single environment, creating a new environment only requires one. If you want to associate your new environment with multiple domains, you can do so once the environment is up and running.  
