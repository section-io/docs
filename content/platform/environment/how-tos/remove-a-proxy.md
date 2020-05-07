---
title: Removing a module from your proxy stack
description: How to remove a proxy/module within an existing proxy configuration.
keywords: proxy, installation, removal

---

## The section.config.json file
This file in the root of your git repository found under the Advanced config menu in Section Console, defined which proxies/modules are running for your environment dictated by the git branch.

For example, if your application is setup with Varnish Cache 6.1.1 and Kraken 2.0.0, you should see this at the top of your config file:

	"proxychain": [
	        {
	            "name": "varnish",
	            "image": "varnish:6.1.1"
	        },
			{
				"name": "kraken",
				"image": "kraken:2.0.0"
			}
	    ]

## 1) Removing a proxy/module
If you'd wish to remove a proxy/module from your proxy stack, you can simply remove the object from the proxychain array in your section.config.json file.

After removing the Kraken module, our file looks like:

	"proxychain": [
	        {
	            "name": "varnish",
	            "image": "varnish:6.1.1"
	        }
	    ],

## 2) Deploy your new configuration
Once you've made the above changes to your configuration files, you can simply commit and push your changes to the desired branch and the Section platform will remove this module from your HTTP delivery chain.
