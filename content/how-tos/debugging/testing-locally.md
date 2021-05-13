---
title: Test Website Performance Locally
description: A guide on testing a Section configuration on your local machine before go-live.
keywords: webpage test, testing, synthetics, local testing
aliases:
  - /debugging/how-tos/testing-locally/
  - /how-to/testing/testing-locally/
---

Instead of using WebPageTest, you may wish to test the site through Section locally using your own browser. You can achieve this by changing how DNS to the site is resolved on your local test machine.

Check out our [set of recommended tests](/docs/how-to/testing-effectively/) for help ensuring that you've covered all your bases.

### **1 Obtaining a test IP**
For our managed customers, our engineers will provide you with a test IP and you can skip to part 2.

For self serve customers, to find out the IP address of the Section platform for your site, run the following command from a command prompt

nslookup site_domain.c.section.io
For www.example.com that would be, nslookup www.example.com.c.section.io

This will give you one or more IP addresses. e.g. 203.0.113.1

### **2 Find local DNS lookup file**
Open the test machine's 'hosts' file in a text editor. This will need to be done as an administrator or with root privilege.

Default locations:
Windows:  C:\Windows\System32\Drivers\etc\hosts
MacOS and Linux:  /etc/hosts


### **3 Change local DNS lookup file**
Add a DNS entry into the file that will tell your test machine to send requests for that domain to the Section platform instead of performing a DNS lookup.

For the example from point 1) and 2) this would look like:
203.0.113.1 www.example.com

Then save the file.

### **4 Test on browser**
Now open a new browser tab or window and navigate to the site with dev tools open.
Requests served from the section will always have a section-io-id response header.
Please note that if you have not uploaded an SSL certificate for the site on to our platform and try to navigate to a HTTPS page, your browser will display a warning about an insecure site, this is expected and not a problem for testing.
You can by-pass this warning in Chrome by clicking Advanced then Proceed to site.
The warning will disappear once you have either uploaded a custom SSL certificate or after you have pointed DNS at our platform and have provisioned our free SSL certificate.

{{% figure src="/docs/images/testing_section_header.png" %}}

If this header isn't present, check that the HOST file is correctly edited and saved. You may also need to flush the DNS cache of the browser. For Chrome enter the following in the address bar: chrome://net-internals/#dns  then clear the host cache.

If you still do not see a section-io-id, contact our support team through which ever channel is available to your support plan.


We recommend focusing on functional testing of the site, such as user login, add to cart, checkout etc.

Performance testing when the site is not live on our platform can yield varying results due to the cache being cold from lack of real world traffic. Remember that the busier a site is, the better it should perform as the cache will be better populated.
