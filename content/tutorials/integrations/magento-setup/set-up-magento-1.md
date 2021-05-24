---
title: Set up and optimize Magento 1 on Section
description: Guide set up a Magento 1 application on Section
keywords: cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 20
aliases:
  - /integrations/how-tos/magento-setup/set-up-magento-1/
  - /how-to/magento-setup/magento-1/
---
## Options to optimize HTML:

1.  HTML Streaming - https://www.section.io/html-streaming/
2.  Anonymous User Caching (Recommended) - https://community.section.io/t/a-novel-way-to-cache-html/79
3.  Turpentine - Detail below

## Set up Varnish Cache Caching

Magento 1.9 and earlier does not support Varnish Cache out of the box. Support is instead provided by the [free Turpentine Magento extension].

The Turpentine extension issues commands required for correct operation to a management port intended for Varnish Cache. A special “bridge” program listens on this port, and makes the Section platform look like a normal Varnish Cache instance (Instead of a globally distributed platform that runs Varnish Cache for you).

Follow the **[official instructions](https://github.com/nexcess/magento-turpentine/wiki/Installation)** in order to install Turpentine. Since Varnish Cache itself is already configured inside Section you’ll only need to complete the ‘Install this plugin’ steps.

1.  Sign up & create an application at Section using the final DNS name that your site will be accessed as.
2.  Download, install & configure the varnish-cli-bridge.
3.  Follow the standard Magento+Turpentine instructions, with some exceptions (see below).
4.  Apply the Varnish Cache configuration from within Turpentine Configuration, to update Section.
5.  Update your public DNS records to direct traffic to Section for your site.

---

### Create an application

Section provides a customized Varnish Cache image already configured for Magento Turpentine. Create your application using the Stack “Varnish Cache v3 Magento Turpentine”.

---

### Set up the varnish-cli-bridge

This program will listen for Varnish Cache commands and foward them to the Section hosted Varnish Cache platform.

#### Download

Download the **[lastest Section cli bridge here](https://github.com/section-io/varnish-cli-bridge/releases/)**. You will want the **varnish-cli-bridge-vN.N.N-linux-amd64.tar.gz** file.

#### Collect configuration details

There are 3 pieces of information required to run the bridge:

1.  API endpoint: This URL uniquely identifies your application within Section. Most often, you’ll need the “Production Varnish Cache Proxy API endpoint” from the Configuration &gt; API page in Section’s management portal.
2.  API username: This is a username that has permission to perform API actions.
1.  API password: This is a password for the specified user to perform API actions.

#### Run as a service

We have an **[Upstart](http://upstart.ubuntu.com/) [script available](https://github.com/section-io/varnish-cli-bridge/blob/master/upstart.conf)** to to run the bridge as a service.

Install Upstart if it is not already installed on your server. Copy the script above with the new name “varnish-cli-bridge.conf” into /etc/init/. Change the endpoint, username & password to match your application.

    # Step 1: Install Bridge
    cd /tmp
    curl  --remote-name --location https://github.com/section-io/varnish-cli-bridge/releases/download/v0.2.4/varnish-cli-bridge-v0.2.4-linux-amd64.tar.gz
    tar xvzf varnish-cli-bridge-v?.?.?-linux-amd64.tar.gz
    cp ./varnish-cli-bridge /usr/local/bin/varnish-cli-bridge

    # Step 2:Setup bridge to run
    cd /etc/init
    curl --location https://github.com/section-io/varnish-cli-bridge/raw/master/upstart.conf --output varnishclibridge.conf

    # Step 3: edit the file "/etc/init/varnishclibridge.conf" with your specific details
    vi varnishclibridge.conf

    # Step 4: State the Varnish Cache cli bridge as a service
    start varnishclibridge

    # Step 5:Check bridge log for success - Should see a line like this -> main.go:159: Listening on '127.0.0.1:6082'.
    tail /var/log/varnish-cli-bridge.log

Otherwise, use whatever solution is available with your distribution to run the binary as a service.

#### Configure Turpentine to talk to the bridge

In your Magento admin portal, you will want to navigate to the Turpentine "Varnish Cache Options" section. Here we will be updating the `Server List` option with the endpoint for the Varnish Cache CLI Bridge you just installed. Add the entry `127.0.0.1:6082` to the list and hit "Save Config" in the upper right hand corner.

{{% figure src="/docs/images/turpentine-server-list.png" %}}

If you get an error (sample error in picture below), you should revisit the bridge installation process and ensure you have done that correctly.

{{% figure src="/docs/images/turpentine-error.png" %}}

---

### Deviations from official Turpentine instructions

#### Installation

See the **[turpentine installation guide](https://github.com/nexcess/magento-turpentine/wiki/Installation)**.

Step 1-3: Skip these steps. There is no need to install or configure a local Varnish Cache server.

#### Configuration

See the **[turpentine configuration guide](https://github.com/nexcess/magento-turpentine/wiki/Configuration)**.

No special configuration is required to use Turpentine with the bridge & Section.

#### Upload Turpentine configuration to Section

The configuration must be applied/uploaded into Section by manually hitting the Apply Varnish Cache Configuration button on the Cache Management page.

#### Testing

There are 2 recommended tests to validate your implementation:

1.  Test Pages Are Coming From Cache - Reload your browser 3-5 times on a single page, You should start to see multiple Varnish Cache ID’s in the HTTP response headers (In a browser debugger such as Chromes debugger) and see page response times around ~50-100ms
2.  Test Bans Are Reaching the Section Platform - Using a Product page on your site refresh 3-5 times to ensure pages are in cache. Once the page is in cache, Add a product to your shopping cart. This will cause Turpentine to send a Ban statement to Section to clear out the block on all pages for the user that contains the shopping cart. You should see the shopping cart updated successfully on page refresh.
