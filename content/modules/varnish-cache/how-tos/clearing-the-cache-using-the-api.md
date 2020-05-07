---
title: How to clear the cache using the API
aliases:
  - /how-to/varnish-cache/clearing-the-cache-using-the-api/
---

1. From the management console, click **API** in the top menu. This will bring you to a UI for all our API routes grouped by category.
![API Link](/docs/images/varnish-cache/api-option.png?height=80px)
1. Scroll through the list, Click **Show/Hide** on the **Proxy** group, then click on the **POST** method ending with **state**.
![Varnish Cache Clear API Method](/docs/images/screenshots/swagger-ui/highlight-varnish-cache-clear-api-operation.png?height=350px)
1. Here, you'll see an interface to help build your API call. Enter your **account id**, **application id**, **environment name**, and **proxy name**.<br/>These can be obtained from the URL in the management console (go to your Section Console homepage and look at the URL - the numbers go accountId -> applicationId -> environmentId). Your **proxy name** is probably `varnish`, but you can also clear cache for other caching proxies.
![Varnish Cache Clear API Example Inputs](/docs/images/screenshots/swagger-ui/example-varnish-cache-clear-api-inputs.png?height=350px)
1. Click **Run**.
1. Now, you'll see a generated request/response cycle for your cache-clear. Pay attention to the response, and notice that the varnish ban expression is appended to the end of the URL as a query string. From here, you can start making automated cache clearing API calls from within your system! Note that these API requests are authenticated using HTTP basic auth and your Section Console credentials. To replicate the API calls made from Swagger outside of the portal, simply add --user user@example.com:your_password.    
