---
title: Deploy your Node.js app
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 3
---

Before you deploy, make sure you have [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/set-up-an-example-nodejs-app.md" >}}).

### Find the name of your app

List applications you have access to, and environments for each:

```
section apps
```

The output will look something like this:

```
Name => Environments
--------------------

paranoid-android => Production
```

The application name was automatically generated for you when you signed up.

Note the name of the application that is returned – you are going to use it in the next step.

### Deploy your app

Now your app is ready to deploy:

```
section deploy paranoid-android --environment Production
```

### View your app running on Section

You can now view your app running on Section:

{{% notice tip %}}
Node.js Edge App Hosting is a new Section product, so it may have some rough edges. **If you see something that needs improvement, we'd love to [hear your feedback](https://support.section.io/hc/en-us/requests/new).**
{{% /notice %}}
