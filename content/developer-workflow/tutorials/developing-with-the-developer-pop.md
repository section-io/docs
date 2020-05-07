---
title: Develop with the Developer PoP
description: How to get your local development environment setup to test Section CDN on your local machine.
keywords: content delivery network, CDN, virtual machine, vagrant, virtualbox, git, cli, local development, local machine, staging environment, developer pop
weight: 3
aliases:
  - /tutorials/developer-workflow/developing-with-the-developer-pop/
---

#### 1. Locally Override DNS to point at the Developer PoP

You will need to modify your **local host file** and point the **Hosted Name(s)** for your service at the IP address given by the command `minikube ip`.

    192.168.99.100    www.example.com

This will override the DNS endpoint for that domain and force traffic through the Dev PoP and then to your origin address.

Your origin could be your production webserver, production load balancer, development webserver — whatever you configured for in the Dev PoP UI.

Now when you browse to your site URL, the HTTP traffic will be flowing through the Developer PoP!

#### 2. Provision SSL certificate

If you visit your website at this point in the tutorial, you will likely see a browser security warning. While it is totally possible to skip this step, click through this warning and test your site without a problem, our Dev PoP can provision a certificate for your local cluster. On the top right hand side, click on the `download root certificate` button.

{{< figure src="/docs/images/dev/download-cert.png" title="Download Local Root Certificate" >}}

##### a) For Windows
Right click on the `section.io-developer-pop-root` certificate in your downloads folder and select `install certificate`. Click through the wizard and install the certificate. Once installed, you should see the `DO_NOT_TRUST_sectionio_root` in the security tab of your browser dev tools.
##### b) For Mac
Double-click on the certificate in your downloads folder and add it to the appropriate keychain. Once completed, you should be able to see `DO_NOT_TRUST_sectionio_root` under Category `certificates`. Right click on the certificate and select `Get Info`. Under the `Trust` section select the option `Always Trust` for `When using this certificate`. As with Windows, once installed properly the `DO_NOT_TRUST_sectionio_root` should appear in the security section of dev tools.

#### 3. Making changes to your configuration

Now that you have traffic flowing through the Dev PoP you will be able to change any configuration and see it live within a few seconds.

Using your favorite editor, open the repository you cloned from Section Console. Whether you have Varnish, PageSpeed, or a Web Application Firewall, you can change the configuration to see how your application will behave.

Once you have made changes to your config, you will want to push them to the Dev PoP to see them in action. Again we will be using a typical git workflow:

1. Stage your changes: `git add .`.
2. Commit your changes: `git commit -m "Some relevant message here"`.
3. Push your changes: `git push developer-pop`.
4. If you have syntax errors git will provide feedback. You may need to make adjustments and go back to step 1.
5. Go back to your browser, reload the page, and see what type of optimizations your changes made.

Congratulations! You have successfully set up the Section Developer PoP! See below for miscellaneous tips to help you get the most out of the software.

#### Further Reading
For a guide on [troubleshooting common Developer PoP issues]({{< relref "developer-workflow/how-tos/troubleshoot-developerpop.md" >}}).

For a guide on setting up [DevPoP with a local server]({{< relref "developer-workflow/how-tos/dev-pop-with-local-server.md" >}}).
