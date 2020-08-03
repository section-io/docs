---
title: Deploy your Node.js app
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 1
---

Before you deploy, make sure you have [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-node.js-app/set-up-an-example-node.js-app.md" >}}).

### Tell Section about your new app

List applications you have access to, and environments for each:

```
section apps
```

Tell Section about your new app:

```
section apps create --name nextjs-blog --environments production
```

### Deploy your app

Now your app is ready to deploy:

```
section deploy --name nextjs-blog --environment production
```

### View your app running on Section

You can now view yoru app running on Section:

> [nextjs-blog.section.dev](https://nextjs-blog.section.dev)

### The Section CLI is now configured.

Next: [deploy your Node.js app]({{< relref "getting-started/tutorials/launching-a-node.js-app/deploy-your-node.js-app.md" >}}).
