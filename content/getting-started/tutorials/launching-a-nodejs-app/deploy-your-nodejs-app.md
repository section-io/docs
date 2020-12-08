---
title: Deploy your Node.js app
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 3
---

Before you deploy, make sure you have [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/set-up-an-example-nodejs-app.md" >}}).

### Find the name of your app

Find the ID of your account:

```
sectionctl accounts
```

The output will look something like this:

```
| ACCOUNT ID | ACCOUNT NAME                      |
|------------|-----------------------------------|
| 1335       | g9ts24tx7gm8n12b2evf3.section.dev |
```

Note the number value in the account ID column – we're about to use it to list applications you have access to:

```
sectionctl apps list --account-id 1335
```

The output will look something like this:

```
| APP ID |    APP NAME                       |
|--------|-----------------------------------|
| 7171   | g9ts24tx7gm8n12b2evf3.section.dev |
```

The application name was automatically generated for you when you signed up.

Note the name of the application that is returned – you are going to use it in the final steps.

### Set up the SSL certificate for your domain

Section provides SSL certificates for your apps for free.

To set up this up so your app is available, run:

```
sectionctl certs renew --account-id 1335 --hostname g9ts24tx7gm8n12b2evf3.section.dev
```

(make sure to substitute your account ID and domain when you run this command)

### Deploy your app

Now your app is ready to deploy:

```
sectionctl deploy --account-id 1335 --app-id 7171
```

(make sure to substitute your account and app IDs when you run this command)

This will take a few minutes to upload and deploy your Node.js app to Section's edge.

### View your app running on Section

Plug the app name you saw above into your browser, and you should see your app running.

{{% notice tip %}}
Node.js Edge App Hosting is a new Section product, so it may have some rough edges. **If you see something that needs improvement, we'd love to [hear your feedback](https://support.section.io/hc/en-us/requests/new).**
{{% /notice %}}

### See the state of an application
You can use the following command to see the state of an application

```
sectionctl ps --account-id 1337 --app-id 7171
```

This will return the status of running app instances in the following format:

```
| APP INSTANCE NAME | APP STATUS |            APP PAYLOAD ID            |
|-------------------|------------|--------------------------------------|
| nodejs-flwp6-3b4  | Deploying  | 69be5c29-9f02-41dc-bed0-27cff1cbbbaf |
| nodejs-7xzhf-0d3  | Deploying  | 69be5c29-9f02-41dc-bed0-27cff1cbbbaf |
| nodejs-a8sfs-23e  | Running    | 2ea3e806-706d-4af2-bd8c-3d45ba4b634b |
| nodejs-sdfk5-54s  | Running    | 2ea3e806-706d-4af2-bd8c-3d45ba4b634b |
```

The example above shows:

- two running instances of the application on a previous version as indicated by the payload ID.
- two app instances being deployed with the latest version.

Once an app instance finishes deploying, its status will change from `Deploying` to `Running`, and replace the app instances running the older version:

```
| APP INSTANCE NAME | APP STATUS |            APP PAYLOAD ID            |
|-------------------|------------|--------------------------------------|
| nodejs-flwp6-3b4  | Running    | 69be5c29-9f02-41dc-bed0-27cff1cbbbaf |
| nodejs-7xzhf-0d3  | Running    | 69be5c29-9f02-41dc-bed0-27cff1cbbbaf |
```
