---
title: Process ESI Directives in JSON responses
aliases:
  - /how-to/varnish-cache/configure-varnish-cache-to-process-esi-directives-in-json-responses/
---

If you use Varnish Cache  for Content composition using Edge Side Includes you may need to configure Varnish Cache  to process ESI directives in files that don't look like XML.

For example, if you are using ESI in an AJAX call that returns some JSON, you might need to enable disable Varnish's XML check.

To do this:

1. Create a file in the **varnish** directory named **proxy-features.json**.
1. Add the following content:
```
{
  "feature/esi_disable_xml_check": true
}
```.
1. Commit the file.
1. Push your changes to the Developer PoP or Section Console.

{{% notice note %}}
Whilst this change will take effect in the Developer PoP, you may need to contact support for this to take effect in production.
{{% /notice %}}