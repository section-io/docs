---
title: Troubleshoot Developer PoP Issues
description: How to deal with various issues that can arise while using DevPoP.
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, developer pop
aliases:
  - /developer-workflow/how-tos/troubleshoot-developerpop/
  - /how-to/developer-pop/troubleshoot-developerpop/
---

The Developer PoP is a still in beta and will occasionally have hiccups. This section details some common issues and how to deal with them.

#### Network connectivity and computer sleep
  Often if you put your computer to sleep with Minikube running, it will break Minikube's network adaptor, and you will get 503 errors without a clear cause when you resume operation. This will also prevent you from downloading proxy images as a part of a `git push`. In order to re-establish connectivity, you need to disconnect the network adapter and reconnect it. If using VirtualBox, do this by opening the VirtualBox UI, going to your VM's settings, clicking `network` and then changing the `attached to:` value from `NAT` to `not attached`, and then back to `NAT`. Toggling this will reset the adapter.

#### Problems with pods in a namespace
  Sometimes Minikube can fail at the namespace level — either by not properly provisioning all the containers it should, or failing to update existing containers after a new git push, or something else. If this happens, you can delete the namespace from the DevPop UI and push the repository back into Minikube by running `git push developer-pop` once the deleted namespace has disappeared from the DevPop UI. You can also accomplish this by renaming the git remote and initiating a `git push developer-pop`. This will create a new namespace and re-trigger all of the container provisioning. 

#### Minikube becomes unresponsive, or has other problems
  Sometimes, Minikube becomes unstable and stops responding to requests altogether. In this case, you'll want to begin this whole process over again with a `minikube delete` and a `minikube start`. Note that sometimes (especially if you start Minikube again very quickly after the initial delete), Minikube will spin up on another IP address (say `192.168.99.101` instead of `192.168.99.100`). This is fine, but you'll need to adjust your hostfile and your git remote if this occurs. Alternatively, if you restart your computer and then start Minikube again, it will return to the `193.168.99.100` address. Most Minikube problems not caused by some sort of configuration error can be fixed with a fresh boot of Minikube, so give this a shot if the source of the problem is unclear.
