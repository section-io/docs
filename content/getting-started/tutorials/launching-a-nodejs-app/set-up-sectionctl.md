---
title: Set up the Section CLI tool
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 1
---

### Download and install `sectionctl`

Go to GitHub [to download the latest release](https://github.com/section/sectionctl/releases/latest) of `sectionctl` for your platform.

On Linux this looks like:

```
wget https://github.com/section/sectionctl/releases/download/v1.6.1/sectionctl-v1.6.1-linux-amd64.tar.gz
tar zxvf sectionctl-v1.6.1-linux-amd64.tar.gz
```

Then place the executable on your path and ensure it's executable.

On Linux this looks like:
```
mv sectionctl /usr/local/bin/sectionctl
chmod +x /usr/local/bin/sectionctl
```

### Configure authentication

To set up credentials so the CLI tool works, run:

```
sectionctl login
```

This will prompt you for your Section username and password, and securely store them where `sectionctl` can find them.

### The Section CLI is now configured and ready to use

Next: [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-nodejs-app/set-up-an-example-nodejs-app.md" >}}).

{{% notice tip %}}
Node.js Edge App Hosting is a new Section product, so it may have some rough edges. **If you see something that needs improvement, we'd love to [hear your feedback](https://support.section.io/hc/en-us/requests/new).**
{{% /notice %}}
