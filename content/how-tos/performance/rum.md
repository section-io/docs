---
title: Set up Real User Monitoring
description: Section real user monitoring
keywords: content delivery network, CDN, rum, performance, baseline, testing
aliases:
  - performance-techniques/how-tos/rum/
  - /rum/
  - /how-to/rum/

---
Section offers free real user monitoring for any customer that signs up and begins their trial. This enables you to see how your own visitors are experiencing your website performance with the use of a simple JavaScript snippet. Data includes:

* Back end, front end, and full page load time
* Throughput
* Traffic by user agent (browser, device type)

## Setting up RUM in Section

To add RUM to your website, simply [login to your Section account](https://aperture.section.io/) and go to "Real User Monitoring" under "Set Up" in the left navigation. All you need to do is paste the `script` tag above your `</head>` tag in any HTML document you want to track.

## Adding with Google Tag Manager

To add the Section RUM script within Google Tag Manager, please follow the steps below:

1) Get the RUM script from [your Section account](https://aperture.section.io/) and go to "Real User Monitoring" under "Set Up" in the left navigation.

2) Login to your Google Tag Manager account and navigate to the container with your domain you wish to add the script to.

3) Click on the red **New Tag** button.

{{% figure src="/docs/images/add-tag.png" %}}

4) Name the tag “Section RUM”.

5) Under **Tag Configuration** choose custom HTML.

6) Paste the RUM script into the area that appears.

7) Under **Triggering** choose **All Pages**. Click save.

{{% figure src="/docs/images/gtm.png" %}}

8) In the upper right-hand corner, click **Publish** and continue to publish all changes.

9) Once you've completed these steps, you're ready to start collecting performance metrics.

## Set up RUM with Classifications

Section RUM can also provide user statistics subdivided by page classifications, giving you pageload statistics for specific page classifications and site-wide statistics.

### To setup RUM with page classifications:

#### 1) Decide what classifications you want

In order to build out the rest of your RUM script, you need to decide what page classifications you want to collect data for. Our available classifications are: `Home`,`Product`, `Checkout`, `Category`, and `Uncategorised`.

**Note**: *Make sure you do not change the spelling of 'Uncategorised'. It will not collect the data*

If you choose to enable them all, these classifications give you statistical metrics on your home page, your individual product pages, your product category pages, and your checkout process. Uncategorised collects metrics on everything that doesn't fall into one of those classifications.

#### 2) Add HTML body classnames for each one of your classifications

By the end of this step, all the pages you want tracked need to have a classification-specific class on their HTML body that identifies them to our RUM script. For example, all Product pages need to have some product class, all Category pages need to have a category class, etc.

If you are setting up RUM for a Magento application, you probably already have body classes you can use for this. These classnames are included below in the example code for Step #5. If you are using Magento, you'll want to verify that your bodies have these classes and then proceed to the next step.

If you're not using Magento but already have classes that appear consistently on the bodies of your pages, feel free to use those and proceed to the next step as well.

If you don't have any consistently applied body classes, you'll need to make some. A good classname for your Product classification would be something like `rum-product`. All that matters is that it makes sense and consistently appears on all pages that you want under that classification. Add these to the appropriate pages.

#### 3) Create a folder in your repository (found under Advanced Configuration) named `rum`.

**Note**: *In order to do this, you will need to pull down your configuration repository onto your local machine. Folders and files cannot be created in the UI*.

#### 4) Create a JavaScript file inside `rum` with the same name as your Hostname/Production domain name.

 If your Production domain name is `www.example.com`, then your JS file should be `www.example.com.js`. Similarly, if you are using a bare domain such as `abc.com`, then your JS file should be named `abc.com.js`.

#### 5) Tailor this template to fit your classifications and insert into your JS file:

```
(function (w) {

  var pageUrl = w.location.pathname;

  var pageName = "Uncategorised";

  if (bodyHasClass("cms-home")) {
    pageName = "Home";
  } else if (bodyHasClass("catalog-category-view")) {
    pageName = "Category";
  } else if (pageUrl.match("/checkout")) {
    pageName = "Checkout";
  } else if (bodyHasClass("catalog-product-view")) {
    pageName = "Product";
  } else {
    pageName = "Uncategorised";
  }

  w.sq_pagetype_override = pageName ;

  function bodyHasClass(className) {
    return document.getElementsByTagName("BODY")[0].classList.contains(className);
  }
})(window);
```

**Double Note**: *Don't change the spelling of Uncategorised*

The only sections you should need to configure are the if-statements. The pageName variable will default to `Uncategorised`, but that default is overwritten if any if-statement resolves to true. The `bodyHasClass()` method will inspect the body for a given class and return a boolean, but you're free to make the if-logic pass in any other way that makes sense. In the example above, `Checkout` pages are identified by URL matching as opposed to HTML classnames. What matters is that pageName is set to the right value.

#### 6) Contact Section

In order to go-live with your new RUM, you'll need a Section engineer. Email us at `support@section.io`.

## Viewing your metrics

To view your real user monitoring metrics [login to your Section account](https://aperture.section.io/) and go to "Monitoring" under "Real time" in the left navigation. From there you can click on "Real User Monitoring" in the left hand corner of the screen to view your Data

{{% figure src="/docs/images/grafana.png" title="Real User Monitoring in Grafana" %}}
