---
title: Connect Developer PoP to Aperture
description: How to get your local development environment setup to test Section CDN on your local machine.
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, local machine, staging environment, developer pop
aliases:
  - /developer-workflow/how-tos/connect-to-aperture/
  - /how-to/developer-pop/connect-to-aperture/
---

{{% notice info %}}
DIf you don't have an Aperture account and want to use the devpop to simply test reverse proxies, feel free to skip this section.*
{{% /notice %}}

In the upper right hand corner of the devpop UI, there is a **Connect to Aperture** button. When clicking this it will redirect you to Aperture and prompt you to login and authorize the devpop. If you are successful then the **Connect to Aperture** button will be replaced with a blinking blue icon followed by your email address.

This will enable an **Import** button on the **Operations** column of the services table, which will open up a modal prompting you to select the application you want to import.
