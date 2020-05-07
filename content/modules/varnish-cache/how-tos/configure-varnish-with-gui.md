---
title: Varnish Cache Quick Config
aliases:
  - /how-to/varnish-cache/configure-varnish-with-gui/
---

Learning VCL can be a tricky thing so we have made a GUI that let's you cache your static assets and HTML documents without knowing VCL.

In the left hand side of your Section Console dashboard there is a section called *Quick Config* which contains the toggles and inputs to configure Varnish Cache.

{{< figure src="/docs/images/varnish-cache/quick-config.gif" title="Varnish Cache Quick Config" >}}

### Configure static asset caching

Static asset caching is enabled by default to cache your statics for 6 hours and retain your origin cache control headers for the browser cache. Below is a list of file extensions that we cache by default:

* css
* js
* jpeg
* png
* gif
* ico
* swf
* woff

There are 3 settings for static caching as well the first is the TTL (Time to Live) which tells Varnish Cache how long to cache your static assets for, the second is a toggle to remove the query strings for all static assets to increase your cache hit rate, and the third is a setting to set the **cache-control** header for browser caching.

**Note:** be careful with the browser cache setting as it becomes difficult to invalidate the browser cache if you don't have some type of version control for your static assets.

### Configure HTML caching

The first thing you'll notice is a toggle to enable and disable HTML caching for quick and easy incident management in the case of an emergency.

When HTML caching is enabled it will by default cache all of your HTML documents that are fetched with a GET request. This is great for sites that are completely static and do not have any customized or authenticated sections or content, for example a shopping cart or customized nav bar per authenticated user.

In order to configure your site for a pattern we like to call ISE (Intelligent Session Establishment) you'll need to have a basic understand of Regexes and how your application establishes a session with a Cookie.

The first option you'll need to configure are the routes you never want to be cached like admin routes or cart routes. You'll need to construct a Regex that matches on all of your non-cacheable routes. Here is an example:

```
(/admin|/cart|/user)
```

So this pattern will match the following routes and not cache them (these are all examples of routes that will not be cached):

* /admin
* /admin/test.html
* /test/admin/abc/123.html
* /cart
* /cart/checkout
* /user/1

The second option you'll need to configure is the Cookie(s) that identify a users session. This is usually established when a user adds something to their cart, logs in tho their account, etc. These cookies are generally set on a POST request which forces the user out of the caching behavior. This is also configured with a Regex in case you have multiple cookies that establish a user's sessions.

```
(frontend|logged_in_user)
```

**Note:** Only HTTP GET requests will be cached with this pattern.
