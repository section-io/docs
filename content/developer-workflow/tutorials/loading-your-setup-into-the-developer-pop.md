---
title: Load Setup Into Developer PoP
description: How to get your local development environment setup to test Section CDN on your local machine.
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, local machine, staging environment, developer pop
weight: 2
aliases:
  - /tutorials/developer-workflow/loading-your-setup-into-the-developer-pop/
  - /docs/developer-workflow/tutorials/loading-your-setup-into-the-developer-pop/
---

<!-- Run `minikube service -n section-shared developer-pop`. Your browser will open when the endpoint for the service becomes ready. -->

#### 1. Clone application's git repository

Clone your application's git repository located in the **Advanced Config** menu in the Section portal.

{{< figure src="/docs/images/dev/bootcamp-url.png" title="URL from GIT repo" >}}

Clone with `git clone <url-from-advanced-config>`

![how to clone a repo](/docs/images/dev/advanced-config-git.png)



#### 2. Add the Dev PoP remote to your repository
  * Open the Dev Pop UI: `minikube service -n section-shared developer-pop`

{{< figure src="/docs/images/dev/get-ready-section.png" title="Section app ready to connect to Section Console" >}}

#### Connect Section Console

{{< figure src="/docs/images/dev/connect-aperture.png" title="Connect to Section Console button" >}}

#### Grant Access

> The application section.io-Developer-PoP is requesting access to your Section accounts.

> Upon approval, your browser will be redirected to the following URL with an access token appended:

> http://192.168.99.102:32080/app/aperture-connected.html
> Allow access?

{{< figure src="/docs/images/dev/grant-access.png" title="Grant Access" >}}

#### Operations

  * Click on the Operations tab.

{{< figure src="/docs/images/dev/operations.png" title="Operations" >}}

#### Add Dev PoP Remote to Local Application Repository

Enter the git commands you see here inside the repository you cloned down in Step 1.

```
cd www.site.com
git remote add developer-pop http://<IP-From-Operations-Tab>:30090/www.site.com.git
```
{{% notice tip %}}
  Replace www.site.com with your domain which is visible in the Section portal. It won't actually break anything if you leave it as "site".
{{% /notice %}}

#### 3. Push your configuration files to the Developer PoP
  Once you have added the git remote you can push to the Dev PoP by running: `git push developer-pop`

```
git push developer-pop
Counting objects: 176, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (132/132), done.
Writing objects: 100% (176/176), 306.64 KiB | 38.33 MiB/s, done.
Total 176 (delta 37), reused 176 (delta 37)
remote: Resolving deltas: 100% (37/37), done.
remote:
remote: varnish image not found, pulling from repository
remote: modsecurity image not found, pulling from repository
remote: Pulling required proxy images, please try again shortly
To http://192.168.99.101:30090/www.site.com.git
 ! [remote rejected] Production -> Production (pre-receive hook declined)
error: failed to push some refs to 'http://192.168.99.101:30090/www.site.com.git'
```


{{% notice tip %}}
  If you get this message "Pulling required proxy images, please try again shortly", that means that your machine does not have the proxy images locally and has begun downloading them. 
{{% /notice %}}

Your terminal will look as though it has exited the process and nothing is happening, but the downloads are going on behind the scenes. 

Try `git push developer-pop` every few minutes until the downloads are complete and the push goes through. The length of this process will depend entirely on the speed of your internet connection and the power of your computer.

```
➜  bootcamp.section.io git:(Production) git push developer-pop
Counting objects: 176, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (132/132), done.
Writing objects: 100% (176/176), 306.64 KiB | 61.33 MiB/s, done.
Total 176 (delta 37), reused 176 (delta 37)
remote: Resolving deltas: 100% (37/37), done.
remote: Validating configuration for proxy varnish...
remote: Validating configuration for proxy modsecurity...
To http://192.168.99.101:30090/www.site.com.git
 * [new branch]      Production -> Production
```

{{< figure src="/docs/images/dev/services.png" title="Services in Dev PoP" >}}

#### Expand Services

{{< figure src="/docs/images/dev/expanded.png" title="Expanded Dev PoP" >}}

#### 4. Configure origin server details
Now that your configurations are running on the Dev Pop, you will need to configure your origin server details to tell the Dev Pop where to pass the HTTP request. 

Use the Dev Pop UI's **Services** tab where you will find information about the repository you just pushed up. A page refresh might be needed.

#### (a) Connect Dev PoP to Section Console
 Make sure to connect your Dev PoP to your [Aperture account]({{< relref "developer-workflow/how-tos/connect-to-aperture.md" >}}) and **import** the Environment configurations.

1. Click on **Import** under the *Operations* column in the **Services** tab.
2. Select the **Environment** you want to test. i.e Production
3. Click on **Import** to finish importing the configurations.

{{< figure src="/docs/images/dev/import-env.gif" title="Import ENV" >}}

{{% notice tip %}}
To Import an Application and its Environments you must be invited as a User for that Account. This is done via Section Console: Account > Manage Users > Invite User. 
{{% /notice %}}

#### (b) Configure the service manually
In the **Operations** column of the table, there will be a button for you to "Configure" that service. Do this if you do not have a Section account. It will bring up a modal asking for the following information:

1. Hosted Name: This is the host headers for your application (e.g. www.example.com).
2. Origin Address: This is the either a domain name or IP address that points directly to your load balancer or webserver.
3. Origin Host Header: This is the host header the egress will use to send upstream (typically it's the same as your hosted name).


Now, you're all set. [Let's see your new Developer PoP in action.]({{< relref "developer-workflow/tutorials/developing-with-the-developer-pop.md" >}}).

  [git]: http://git-scm.com/
  [Vagrant]: http://docs.vagrantup.com/v2/installation/
  [Minikube]: https://github.com/kubernetes/minikube/releases/tag/v0.21.0
  [VirtualBox]: http://www.virtualbox.org/
