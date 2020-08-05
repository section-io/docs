---
title: Set up the Section CLI tool
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 2
---

## Setup

First, let’s make sure that your local development workspace is ready.

- If you don’t have Node.js installed, [install it from here](https://nodejs.org/en/). You’ll need Node.js version 10.13 or later.
- You’ll be using your own text editor and terminal app for this tutorial.

If you are on Windows, we recommend [downloading Git for Windows](https://gitforwindows.org/) and use Git Bash that comes with it, which supports the UNIX-specific commands in this tutorial.

### Create a Next.js app

To create a Next.js app, open your terminal, `cd` into the directory you’d like to create the app in, and run the following command:

```
npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"
```

### Run the development server

You now have a new directory called nextjs-blog. Let’s cd into it:

```
cd nextjs-blog
```

Then, run the following command:

```
npm run dev
```

This starts your Next.js app’s "development server" on port 3000.

Let’s check to see if it’s working. Open [http://localhost:3000](http://localhost:3000) from your browser.

### Add a Procfile

Add a Procfile, so Section knows how to start your app:

```
echo 'server: npx next start' | tee Procfile
```

### The Section CLI is now configured.

Next: [deploy your Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/deploy-your-nodejs-app.md" >}}).
