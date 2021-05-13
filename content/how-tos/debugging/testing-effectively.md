---
title: Recommended Test Suite
description: A recommended battery of tests to ensure optimal performance.  
keywords: webpagetest, performance testing, metrics, website performance, page speed, webpage speed, website security
aliases:
  - /debugging/how-tos/testing-effectively/
  - /testing/
  - /how-to/testing/testing-effectively/

---

The following steps will enable you to prime the CDN caches and follow a process that identifies caching issues for resolution ahead of actual customer traffic:

#### **1 Load your site's Homepage 3-4 times**

This will ensure that assets are stored in cache and any optimizations that are being applied are activated

#### **2 Browse to another page (eg product page)**

If your site is an ecommerce site add a product to cart (or perform a similar action that personalizes the users experience)

**Test checklist item:** Confirm that add to cart action works

#### **3 Browse back to the Homepage**

This tests the experience when a user has performed some actions elsewhere and returns to a cached / optimized page

**Test checklist item:** Confirm that user still has products in cart and page rendering looks normal

#### **4 Login to your sites User portal**

If your site has an area for users to manage their username and password and other account related settings login now

**Test checklist item:** Confirm that login works and user portal rendering looks normal

#### **5 Browse back to the Homepage**

This tests that your site renders properly after logging in when browsing a cached / optimized page.

**Test checklist item:** Confirm that the page displays the user logged in status correctly

#### **5a (Optional) Load the Homepage in a new Incognito window**

Loading your website in an Incognito window (in Chrome browser for example) simulates a new user that is not related to your existing user on the site. This enables you to confirm that things like cart/logged in status are unique per user.

**Test checklist item:** Confirm that the page displays correctly and that the page does not have any cart items or logged in status

#### **6 Complete Checkout/Key call to action**

Complete the primary call to action on your site to ensure that users can complete this step without any issues.

**Test checklist item:** Confirm that an order / booking / inquiry has been placed and that your user has received any confirmation emails as appropriate

#### **7 Login to your sites Admin (CMS) portal and reload 3-4 times**

Tests that the user portal of your site is functioning when assets may have been cached / optimized

**Test checklist item:** Ensure that you can perform 1-2 of your most common CMS functions

### Testing Complete - Go live!
Now that you have followed the above process, you have tested the core functionality of your site. Through the above process it's critical to focus on the functional elements of testing. Seeing actual user performance will only be relevant when you have actual users on your website.
