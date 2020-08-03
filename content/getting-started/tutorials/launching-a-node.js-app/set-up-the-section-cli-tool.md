---
title: Set up the Section CLI tool
description: A step-by-step guide on how to launch a Node.js app on Section.
keywords: guide, getting started, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 1
---

### Download and install the Section CLI tool

Go to GitHub [to download the latest release](https://github.com/section-io/section-cli/releases/latest) of `section-cli` for your platform.

On Linux this looks like:

```
wget https://github.com/section-io/section-cli/releases/latest/download/section-cli-linux-amd64
```

Then place the executable on your path and ensure it's executable.

On Linux this looks like:
```
mv section-cli-linux-amd64 /usr/local/bin/section
chmod +x /usr/local/bin/section
```

### Configure authentication

To set up credentials so the CLI tool works, run:

```
section login
```

This will:

 - Open your browser, taking you to [create a new token](https://aperture.section.io/settings/tokens/new)
 - Ask you to name your token
 - Show you the token once and only once – make sure you copy it somewhere safe
 - Writes the token to `~/.netrc`, in the format:
   ```
   machine aperture.section.io
     login you@domain.example
     password 286755fad04869ca523320acce0dc6a4
   ```
 - Warn you if your `.netrc` file is world readable.

### The Section CLI is now configured and ready to use

Next: [set up an example Node.js app]({{< relref "getting-started/tutorials/launching-a-node.js-app/set-up-an-example-node.js-app.md" >}}).
