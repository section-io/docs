---
title: Install A New Proxy
description: How to install a new proxy within an existing proxy configuration.
keywords: proxy, installation
aliases:
  - /how-tos/environment/install-a-new-proxy/
  - /platform/environment/how-tos/install-a-new-proxy/
  - /how-to/install-a-new-proxy/

---
## The section.config.json file
The config files dictates the order that traffic will flow through the proxy chain — be aware of the location you put the new reverse proxy in.

For example, if your application is setup with Varnish Cache 4.0.3, you should see this at the top of your config file:

	"proxychain": [
	        {
	            "name": "modsecurity",
	            "image": "modsecurity:2.2.7"
	        }
	    ]

## 1) Add the proxy to your environment's section.config.json file
Let's add Varnish Cache 6.0.0 to the example above. You can find a list of current proxies [here]({{< relref "reference/modules.md" >}})

To add a proxy, we need to insert a json object containing the proxy's name and image (the specific version of the proxy you want). After adding the Varnish Cache proxy, our file looks like:

	"proxychain": [
	        {
	            "name": "modsecurity",
	            "image": "modsecurity:2.2.7"
	        },
	        {
	            "name": "varnish",
	            "image": "varnish:6.0.0"
	        }
	    ],

Note that different proxies have different ways of specifying the image.  

## 2) Deploy your new configuration

Section has a git-ops workflow. Deployment is via git commits. Free and open source proxy Modules like Varnish do not require Section engineers. 

However, paid proxies like Kraken or ThreatX require Section engineering initialization and setup at the beginning of a proxy life-cycle. After initial setup, normal git-ops will trigger deployment of changes to environments such as Production or Staging. 

If you need to contact a Section engineer please send us a [support ticket](https://support.section.io/hc/en-us/requests/new).
