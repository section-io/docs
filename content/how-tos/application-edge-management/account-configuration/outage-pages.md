---
title: Set up Outage Pages
description: Set up Section so that it can serve an outage page during maintenace
keywords: custom outage mapge, maintenance, custom html, content delivery network, CDN, scheduled maintenance.
aliases:
  - /how-tos/environment/outage-pages/
  - /platform/environment/how-tos/outage-pages/
  - /reference/outage-pages/

---

# A guide to setup custom outage pages

Section has an Outage Page feature that will allow multiple HTML pages to be uploaded on to the platform and displayed during maintenance or other planned down times.

## 1) Design an outage page

The Outage Page feature is designed for HTML only. We recommend keeping the HTML simple.
Any static assets linked in the HTML should be hosted off domain, such as on AWS S3.

## 2) Upload an outage page

You can place one or more HTML files in the `outage_pages` folder in your application repository. If this folder does not exist, you can create it.
Each HTML file that is uploaded in to the repo will show up under the Outage Page portal page which you will find on the left hand side nav bar.

For example, if you uploaded the following 3 files into the `outage_pages` folder:

{{% figure src="/docs/images/outage_page_00.png" %}}

You should see them displayed in the Outage Page portal as per the screenshot.

{{% figure src="/docs/images/outage_page_01.png" %}}

## 3) Enable/disable outage page

When you wish to enable outage mode and display one of your uploaded outpage pages, simply check the box next to the page you wish to display and click "Engage".
You will be prompted to confirm the action. Once confirmed, all requests to the site will be served the outage page. Please be aware that a deployment time of around 30 seconds is expected when you click confirm.

When you are ready for users to see the site again, click the Disengage button.

## 4) Outage page for specific Domains or URLs

Right now the Outage Page portal covers all domains and URLs on a Section environment.
If you wish to only display an outage page for a select domain or URL path, you will need to do so using Varnish Cache.
See this [community article](https://community.section.io/t/how-to-display-a-custom-maintenance-page-using-varnish/112) for details.
