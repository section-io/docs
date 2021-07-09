---
title: HTTP Error Messages
description: How to review http response codes. How to upload a custom error page for your website with Section.
type: "docs"
keywords: website performance, error message, http response code, content delivery network, CDN
aliases:
  - /debugging/reference/http-error-messages/
  - /custom-errors/
  - /http-error-messages/
  - /reference/http-error-messages/

---

Have a look in Chrome's development tools, on the network tab, to discover the HTTP response code for a request.

### HTTP 522

This is a modified [HTTP 502](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#502) status code and means that we had trouble establishing a TCP connection to your server.

Here are some things to check:

1. Is your server running? Sometimes your web server (for example, Apache or nginx) may not be running. It may be refusing TCP connections.
1. Is your origin server address correct? Try browsing directly to your server IP (you may need to override DNS with hosts file entries). If not, [update your origin address]({{< relref "how-tos/application-edge-management/account-configuration/change-origin.md" >}}).

### HTTP 524

This is a modified [HTTP 504](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#504) status code and means your application took too long to respond.

Here are some things to check:

1. Is your server under heavy load? Perhaps you could [improve your cache hit rate]({{< relref "/how-tos/module-integrations/varnish/varnish-cache-hit-rate.md" >}}).

### HTTP 508

The HTTP status code that Section edge serves if there appears to be a cyclic loop (i.e., egress requests back to edge).

Here are some things to check:

1. Is your origin configured as another environment on the Section platform?

## Custom Error Messages

If you would like to customise what HTML we return in case of specific HTTP error codes you can place a file in the `custom_errors` folder in your application repository.

The repository is initialized with a `custom_errors` folder containing a `500.html.sample` file.

{{% figure src="/docs/images/custom-errors.png" %}}

To customise the HTML returned in case of a 500 error the file should be renamed to `500.html` and the HTML inside customized to what they want. Other error codes can be implemented in the same way, eg. `503.html`, `404.html`, etc.

Customising error pages for 502 and 504 errors will also customise error pages for 522 and 524 error codes.

Only valid nginx error codes can be used, that is codes between 300 and 599 excluding 499. Any other files in that folder will be ignored.
