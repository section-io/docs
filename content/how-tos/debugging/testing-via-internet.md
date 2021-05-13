---
title: Run WebPagetest On Your Website
description: A guide on testing the performance of your site using webpagetest.
keywords: webpage test, testing, synthetic
aliases:
  - /debugging/how-tos/testing-via-internet/
  - /how-to/testing/testing-via-internet/
---

This is a guide to help you run some basic tests against your website using [webpagetest.org](http://webpagetest.org), a free real browser synthetic testing agent.

While synthetic tests do not necessarily provide an accurate indication of how fast your site will be in the hands of your users, they can be useful to help you understand which items you can work on to the improve performance of individual pages. By focusing on key pages, you can improve the overall performance of your website.

These tests assumes you have [signed up](https://www.section.io/sign-up) with Section and that you have [added your application](https://www.section.io/docs/create-application/).

Check out our [set of recommended tests](/docs/how-to/testing-effectively/) for help ensuring that you've covered all your bases.

### Test without Section

Visit [webpagetest.org](http://webpagetest.org) and run a test against a sample page from your website. Run 5 tests with first and repeat views from a location which may be relevant to your users. This should give you a good picture of your origin's performance without the benefits of Section.

{{% figure src="/docs/images/webpagetestbasic.png" %}}

### Test with Section

#### **1  Find the cname Record for Your Application**

Visit your Section portal and view the Change DNS settings. Also found under the Repository settings if you have not selected to use Section hosted DNS offering.

You should see something like:    www.website.com.c.section.io

Copy this as you will need it for the next step.

#### **2  Set Webpagetest to Test the Site Running Through Section**

At the home screen of webpagetest, select the "Script" tab and enter a DNS reroute so that webpage test thinks the origin server for your website is at Section.

{{% figure src="/docs/images/webpagetestscript.png" %}}

You may also need to set webpagetest so that it ignores any SSL errors assuming you have a cert installed on your website which you have not yet installed on Section.

{{% figure src="/docs/images/webpagetestssl.png" %}}

Run another 5 tests with first and repeat views.

#### **3 Review Your Results**

You should be able to see the Section markers in the responses for the items.  Select one of the webpagetest waterfalls and click on the response.  The Section id provides you with confirmation that the test has traversed the Section platform.

{{% figure src="/docs/images/webpagetestsection.png" %}}

#### **4 Optimize Your Website Performance**

Now you can modify your VCL in Section platform and re run multiple tests for caching or modify the page to serve entirely HTTPS so you can take advantage of Section HTTP/2 platform.

The cache hit headers will be apparent on the responses you see in webpagetest.

You can also then correlate the responses to your logs and metrics in Section portal.  Simply take a copy of the Section ID for a particular response anc copy and paste it into the query frame in Kibana in Section portal.  This will provide you with detail for that particular request and how it was dealt with at the Section platform.

{{% figure src="/docs/images/webpagetestlogs.png" %}}


#### **5 Rinse and Repeat**

This process can allow you to see the impact you can have on your website with Section.  As you progressively improve the configuration in Section you should be able to see these changes reflected in your webpagetest results.

Once you have made your DNS change, these tests become even more simple as the script you entered will no longer be required.
