---
title: Running Minikube with a Local Origin
description: A guide for connecting a local development server to the Developer PoP
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, local machine, staging environment, developer pop
aliases:
  - /developer-workflow/how-tos/dev-pop-with-local-server/
  - /how-to/developer-pop/dev-pop-with-local-server/
---

Although Minikube functions functions best when pointed at an origin server with a publicly available IP address, it is possible to connect DevPop to a local development server. The source of complexity here is dealing with the network bridge between the host machine and the Minikube virtual machine. The following is a set of directions for implementing this using virtual box and a local server running on port 80, but the necessary configuration may vary if you have an alternative setup.

1. Start your local server on port 80.
1. Start Minikube.
1. Once Minikube is running and it's network has been established, you should be able to visit your localhost server on both `127.0.0.1` and `192.168.99.1` (If not, subsequent steps will not work). If successful, this means that the Minikube VM can access your host machine's localhost on `192.168.99.1`.
1. In the DevPop UI, add both `192.168.99.1` and the relevant hostname (such as `www.example.com`) as the origin for the Section configuration you wish to run in front of your origin server.
1. In your hostfile, map the hostname you set in the previous step (`www.example.com`) to the IP address of Minikube (likely `192.168.99.100` — verify by running `minikube ip` in your command line).
1. Visit your hostname `www.example.com` in your browser. If everything is configured correctly, then your browser will send the request to DevPoP on `192.168.99.100`, which will then pass it to the local origin server running on `192.168.99.1`. Note that this request must be made over HTTP and not HTTPS.
