---
title: Set up a Magento 2 app on Section
description: A guide for setting up a Magento 2 app on the Section platform.
keywords: cache, https, website performance, page speed, webpage speed, website security, content delivery network, CDN
weight: 10
aliases:
  - /integrations/how-tos/magento-setup/set-up-magento-2/
  - /how-to/magento-setup/magento-2/
---

The following is a guide to going live on Section with a Magento 2 application.

### 1) Download the Section extension.

#### a) Via the Magento Marketplace
  To get started with Section and Varnish Cache directly from the Magento Admin portal, you first must download the "Instant Global Cache" extension from the [Magento Marketplace](https://marketplace.magento.com/sectionio-metrics.html).

#### b) Via the command line
  Add `"sectionio/metrics": "dev-master"` to your `composer.json` file and run `composer update`. This assumes that your application is configured to pull from Packagist.

### 2) Connect your Magento application to your Section account.   

Once the extension is added, click on Reports in the left Nav. A Section option should now be listed among your reports.

{{% figure src="/docs/images/magento-extension-location.png" %}}

#### a) Set up via the Admin portal
Inside the Section reports view, you will see fields requesting your Section credentials. If you've already created an account on our platform, enter those credentials here. Othewise, You can also create an account from here in the Magento portal or on our website: [section.io/sign-up/] (https://www.section.io/sign-up/). When you create your login, we will also send you an email to verify your email address. This is required for us to setup your application.

#### b) Set up via the command line  
In order to link your Section account to your Magento application via the command line, you need to have already created an account( [section.io/sign-up/](https://www.section.io/sign-up/)). Once your account is created and the Section extension is installed inside your app, your magento binary should have access to the `sectionio:setup` command. From the root of your application, run `bin/magento sectionio:setup <username> <password> <account_id> <application_id>`. A successful execution produces no output. If it executed successfully, you should see your account information displayed in the Section reports tab within your admin portal. *Note*: After running this command, run `bin/magento setup:upgrade` and `bin/magento setup:di:compile`.

### 3) Set up your application and Varnish Cache .

When you are logged in on your Magento Admin Portal with your Section credentials, we will determine if you already have an application setup with us. If you do, we will show you the accounts you have with us. If you do not, we will create an application for you.

If you do not have Varnish Cache  as your chosen Full Page Cache Caching Application, we will show an error message for you to update this. To update this field, go to Stores -> Configuration (under Settings) -> Advanced -> System. Then toggle the Caching Application under Full Page Cache to Varnish Cache .

{{% figure src="/docs/images/magento-cache-settings.png" %}}

Now you have a Section application created with Varnish Cache 4 and Varnish Cache  setup as your Full Page Cache solution in Magento.

### 4) Import Magento Varnish Cache  configuration

#### a) Import via the Admin portal
On the Section extension, you will see a Management section. The first button says “Update Varnish Cache configuration.” Clicking this button will pull in the recommended Magento VCL (Varnish Cache Configuration Language) into your Section application to optimize your caching for Magento.

{{% figure src="/docs/images/magento-extention-management.png" %}}

#### b) Import via the command line

You can also import your vcl configuration using the `bin/magento sectionio:updatevcl` command. The effect of this is identical to the "Update Varnish Cache configuration" button described above. As with the other CLI commands, success is silent.

### 5) Provision a free Section certificate (optional)

There is also a button to pull in free HTTPS certificate. This will ensure your website has the green padlock next to the url. This is a free certificate included with your Section application that we will managed on your behalf, to include procurement, installation, and renewal. Please ensure your website has an endpoint exposed to the internet so we can validate the certificate before you go live.

**note:** if you do not perform this step, you will need to upload a custom certificate to the Section portal in order to maintain HTTPS. (See [our guide]({{< relref "how-tos/https-tls/upload-a-custom-certificate.md" >}}) )

### 6) Change DNS and Go Live!

To go live with Varnish Cache and your Section application, you will need to change a DNS record to point to Section. Detailed instructions can be found [here](https://www.section.io/docs/change-dns/#dns-hosting-with-your-current-provider). You can also find more information from your hosting provider as to where to go to make this change. Once you have made the change, you can click verify to see if the change was successful and traffic is currently flowing through Section.

## Additional Settings: Include CMS in Product Purges

When a product is updated either via checkout event, image update, description change or other similar event, Magento clears the cache for all pages where that product is mentioned, including the home page, category pages, and product pages. Although it is important to clear cache when product information changes, often this internal cache-clearing protocol clears the cache on non-product pages unnecessarily, exposing your origin to additional traffic and slowing down response times.

Although the Section Magento extension forwards all cache-clearing directives to your cloud Varnish Cache instances out of the box, it can be configured to ignore cache clear requests for CMS pages. To enable this feature, navigate to Stores->Configuration->Advanced->System->Full Page Cache->Section settings. Here you can toggle whether CMS pages are included in automated cache purges.

Note: enabling this feature means that if you change key elements of a product like the name, other pages that feature the product will need to be manually cleared. Overall, this configuration option will have a positive benefit on site performance at the cost of some manual overhead. Whenever you update a product, you need to clear the relevant caches in the admin console.  


  [free Turpentine Magento extension]: http://www.magentocommerce.com/magento-connect/turpentine-varnish-cache.html
  [official instructions]: https://github.com/nexcess/magento-turpentine/wiki/Installation
  [lastest Section cli bridge here]: https://github.com/section-io/varnish-cli-bridge/releases/latest
  [Configure and use Varnish]: http://devdocs.magento.com/guides/v2.0/config-guide/varnish/config-varnish.html
  [Install Varnish]: http://devdocs.magento.com/guides/v2.0/config-guide/varnish/config-varnish-install.html
  [Configure Varnish Cache and your web server]: http://devdocs.magento.com/guides/v2.0/config-guide/varnish/config-varnish-configure.html
  [Configure Magento to use Varnish]: http://devdocs.magento.com/guides/v2.0/config-guide/varnish/config-varnish-magento.html
