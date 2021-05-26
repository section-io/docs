---
title: "Check your current HTTPS setup"
description: ""
aliases:
  - /https/how-tos/check-your-current-https-setup/
  - /how-to/https/check-your-current-https-setup/
  - /ssl/how-tos/check-your-current-https-setup/
---

## Using the command line - OpenSSL

1. Open a terminal.
1. Run `openssl s_client -showcerts -connect www.example.com:443 </dev/null`, with your domain name.
1. If successful, you'll receive a complete output of what a browser uses to establish secure HTTP.

## Using an online tool - DigiCert

1. Browse to an online certificate checking service such as: https://www.digicert.com/help
1. Enter your domain name and initiate the check
1. Verify your setup receives a tick at the bottom of the test
