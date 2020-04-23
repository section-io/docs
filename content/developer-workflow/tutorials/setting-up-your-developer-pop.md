---
title: Set-up Section Developer PoP
description: How to get your local development environment setup to test Section Edge Compute on your local machine.
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, local machine, staging environment, developer pop
weight: 1
aliases:
  - /tutorials/developer-workflow/setting-up-your-developer-pop/
---

Section Developer PoP runs on Kubernetes. Minikube is a miniature, prepackaged Kubernetes cluster that works locally on a desktop Microsoft Windows, Mac or Linux computer.

Minikube runs in the free and open source [VirtualBox].

1. Verify that you have installed VirtualBox
1. Download and install <a href="https://github.com/kubernetes/minikube/releases/tag/v1.6.2" target="Minikube" title="Minikube v1.6.2 download">Minikube v1.6.2</a>. Version 1.6.2 is the Section supported version of Minikube. https://github.com/kubernetes/minikube/releases/tag/v1.6.2
1. Download and install <a href="https://kubernetes.io/docs/tasks/tools/install-kubectl" target="kubectl" title="kubectl v1.16.2 download">kubectl v1.16.2</a>. Version v1.16.2 is the Section supported version of kubectl. https://kubernetes.io/docs/tasks/tools/install-kubectl
1. Start minikube: `minikube start`
1. Initialize the Developer PoP

**Start Minikukbe**

`minikube start`

Minikube will start as below on Ubuntu 18.04.

```
minikube start
🙄  minikube v1.6.2 on Ubuntu 18.04
✨  Automatically selected the 'virtualbox' driver (alternates: [none])
💿  Downloading VM boot image ...
    > minikube-v1.5.1.iso.sha256: 65 B / 65 B [--------------] 100.00% ? p/s 0s
    > minikube-v1.5.1.iso: 143.76 MiB / 143.76 MiB [-] 100.00% 4.14 MiB p/s 35s
🔥  Creating virtualbox VM (CPUs=2, Memory=2000MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.16.2 on Docker '18.09.9' ...
💾  Downloading kubeadm v1.16.2
💾  Downloading kubelet v1.16.2
🚜  Pulling images ...
🚀  Launching Kubernetes ... 
⌛  Waiting for: apiserver
🏄  Done! kubectl is now configured to use "minikube"
```

**Initialize the Developer PoP**

```
minikube ssh "docker run --rm --net=host -v /var/lib/minikube:/var/lib/minikube:ro sectionio/section-init"
```

{{% notice info %}}
Depending on the speed of your internet connection and the power of your computer, the initiation of the Developer PoP can take several minutes.
{{% /notice %}}


**Initialize Namespaces**

```
Unable to find image 'sectionio/section-init:latest' locally
latest: Pulling from sectionio/section-init
96ac93103c33: Pull complete
7f806fcb5e6c: Pull complete
9f61142fa1a0: Pull complete
fd79b6758639: Pull complete
c99a605ef53e: Pull complete
Digest: sha256:6619bbb259d0b4f20f8064385a4dad3b1529f825f76ae10867cae11d6a092332
Status: Downloaded newer image for sectionio/section-init:latest
namespace "section-bootstrap" created
serviceaccount "section-bootstrap" created
clusterrolebinding "section-bootstrap-cluster-admin" created
deployment "bootstrap" created
namespace "section-shared" created
service "developer-pop" created
```

**Developer PoP Ready**

Now your Developer PoP base is ready, but it has not yet launched any of the specific proxies in your configuration.

Let's change that by **[loading your Section setup into the Developer PoP]({{< relref "developer-workflow/tutorials/loading-your-setup-into-the-developer-pop.md" >}})**.


**Time to Setup**

After each one of these terminal commands, you will need to wait a few moments for Minikube to fully launch all the Section containers.

If you, for example, try and do the git pushes in the next section immediately after completing the `minikube ssh` command above, you may find that the git daemon or some other relevant component has not yet come online.

In this case, just wait for a few minutes — the exact time depends upon the speed of your internet connection and specifications of your machine.

{{% notice tip %}}
Disable repeating messages about the **kubectl** component you won't need: `minikube config set WantKubectlDownloadMsg false`
{{% /notice %}}


  [VirtualBox]: http://www.virtualbox.org/

Next, [loading your Section setup into the Developer PoP]({{< relref "developer-workflow/tutorials/loading-your-setup-into-the-developer-pop.md" >}})
