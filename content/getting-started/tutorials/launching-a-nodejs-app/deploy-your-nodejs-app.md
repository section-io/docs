---
title: Deploy your Node.js app
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 3
---

Before you deploy, make sure you have [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/set-up-an-example-nodejs-app.md" >}}).

### Tell Section about your new app

List applications you have access to, and environments for each:

```
section apps
```

Tell Section about your new app:

```
section apps create nextjs-blog
```

This will create a new app on section, with a single environment, `Production`.

You can create multiple enviroments by using the `--environments` option:

```
section apps create nextjs-blog --environments Production,Staging,UAT
```

### Deploy your app

Now your app is ready to deploy:

```
section deploy nextjs-blog --environment Production
```

### View your app running on Section

You can now view your app running on Section:

> [nextjs-blog.section.dev](https://nextjs-blog.section.dev)
