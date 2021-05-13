---
title: HTTP Error Messages
description: How to review http response codes. How to upload a custom error page for your website with Section.
keywords: website performance, error message, http response code, content delivery network, CDN
aliases:
  - /debugging/reference/http-error-messages/
  - /custom-errors/
  - /http-error-messages/
  - /reference/http-error-messages/

---

If your origin server is down or running slowly, you or your users might be presented with the following screen:

{{% figure src="/docs/images/generic-error-http.png" %}}

This page is show where Section responds with a HTTP 502 or HTTP 504 response code.

Have a look in Chrome's development tools, on the network tab, to discover the HTTP response code.

### HTTP 502

[HTTP 502](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#502) means that we had trouble establishing a TCP connection to your server.

Here are some things to check:

1. Is your server running? Sometimes your web server (for example, Apache or nginx) may not be running. It may be refusing TCP connections.
1. Is your origin server address correct? Try browsing directly to your server IP (you may need to override DNS with hosts file entries). If not, [update your origin address]({{< relref "how-tos/environment/change-origin.md" >}}).

### HTTP 504

[HTTP 504](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#504) means your application took too long to respond.

Here are some things to check:

1. Is your server under heavy load? Perhaps you could [improve your cache hit rate]({{< relref "how-tos/integrations/varnish/varnish-cache-hit-rate.md" >}}).

## Custom Error Messages

If you would like to customise what HTML we return in case of specific HTTP error codes you can place a file in the `custom_errors` folder in your application repository.

The repository is initialized with a `custom_errors` folder containing a `500.html.sample` file.

{{% figure src="/docs/images/custom-errors.png" %}}

To customise the HTML returned in case of a 500 error the file should be renamed to `500.html` and the HTML inside customized to what they want. Other error codes can be implemented in the same way, eg. `503.html`, `404.html`, etc.

Only valid nginx error codes can be used, that is codes between 300 and 599 excluding 499. Any other files in that folder will be ignored.
