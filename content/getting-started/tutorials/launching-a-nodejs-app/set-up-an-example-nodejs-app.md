---
title: Set up an example Node.js app
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 2
---

Next, we're going to set up a [NuxtJS](https://nuxtjs.org) app for you to deploy to Section's Edge App Hosting.

## Setup

First, let’s make sure that your local development workspace is ready.

- If you don’t have Node.js installed, [install it from here](https://nodejs.org/en/). You’ll need Node.js version 10.14 or later.
- You’ll be using your own text editor and terminal app for this tutorial.

If you are on Windows, we recommend [downloading Git for Windows](https://gitforwindows.org/) and use Git Bash that comes with it, which supports the UNIX-specific commands in this tutorial.

### Set up a demo app

To set up a demo app, open your terminal, `cd` into the directory you’d like to create the app in, and run the following command:

```
git clone https://github.com/section/nodejs-example
```

### Run the development server

You now have a new directory called `nodejs-example`. Let’s `cd` into it:

```
cd nodejs-example
```

Pull down the dependencies and build your app by running:

```
npm install
npm run-script build
```
{{% notice info %}}
The Section platform expects you have run both of these commands before you can deploy your app.
{{% /notice %}}

Then, run the following command:

```
npm run-script start
```

This starts your app’s development server on port 8080.

Let’s check to see if it’s working. Open [http://localhost:8080](http://localhost:8080) from your browser.

### Your app is now ready to deploy

Next: [deploy your Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/deploy-your-nodejs-app.md" >}}).

{{% notice tip %}}
Node.js Edge App Hosting is a new Section product, so it may have some rough edges. **If you see something that needs improvement, we'd love to [hear your feedback](https://support.section.io/hc/en-us/requests/new).**
{{% /notice %}}
