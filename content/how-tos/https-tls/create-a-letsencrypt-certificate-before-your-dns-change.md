---
title: "Create a Let's Encrypt Certificate Before your DNS Change"
description: ""
aliases:
  - /https/how-tos/create-a-letsencrypt-certificate-before-your-dns-change/
  - /how-to/https/create-a-letsencrypt-certificate-before-your-dns-change/
  - /ssl/how-tos/create-a-letsencrypt-certificate-before-your-dns-change/ 
---

If you would like to create your free TLS certificates before you make your DNS change, you need to configure your server.

## For users of Nginx

1. Obtain the CNAME record for your application. You'll see this on the DNS menu in the Section management console.
1. Add this block to your server's configuration, replacing `yourdomain.c.section.io` with the CNAME you obtained above:

	```
	location /.well-known/acme-challenge/ {
	  proxy_set_header Host $host;
	  proxy_pass http://yourdomain.c.section.io;
	}
	```

1. Click **Renew Certificate** on the HTTPS menu within the Section management console.

## For users of Apache

1. Obtain the CNAME record for your application. You'll see this on the DNS menu in the Section management console.
1. Add this block to your server's configuration, replacing `yourdomain.c.section.io` with the CNAME you obtained above:

	```
	<Location "/.well-known/acme-challenge/">
	  ProxyPreserveHost On
	  ProxyPass "http://yourdomain.c.section.io"
	</Location>
	```

1. Click **Renew Certificate** on the HTTPS menu within the Section management console.