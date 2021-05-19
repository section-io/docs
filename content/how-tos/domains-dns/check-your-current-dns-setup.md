---
title: "Check your current DNS setup"
description: ""
weight: 3
aliases:
  - /dns/how-tos/make-bare-domain-cname/
  - /dns/how-tos/check-your-current-dns-setup/
  - /how-to/dns/check-your-current-dns-setup/
---

## From a terminal

1. Run `dig +trace www.yourdomain.com`. If you are unable to run this command locally, leverage an online tool such as <a href="http://www.kloth.net/services/dig.php" title="Kloth online dig service" target="kloth">Kloth</a>.
 {{%expand "Click to expand an example" %}}

```
$ dig +trace www.example.com

; <<>> DiG 9.11.0-P5 <<>> +trace www.example.com
;; global options: +cmd
.                       488165  IN      NS      f.root-servers.net.
.                       488165  IN      NS      g.root-servers.net.
.                       488165  IN      NS      h.root-servers.net.
.                       488165  IN      NS      i.root-servers.net.
.                       488165  IN      NS      j.root-servers.net.
.                       488165  IN      NS      k.root-servers.net.
.                       488165  IN      NS      l.root-servers.net.
.                       488165  IN      NS      m.root-servers.net.
.                       488165  IN      NS      a.root-servers.net.
.                       488165  IN      NS      b.root-servers.net.
.                       488165  IN      NS      c.root-servers.net.
.                       488165  IN      NS      d.root-servers.net.
.                       488165  IN      NS      e.root-servers.net.
.                       488165  IN      RRSIG   NS 8 0 518400 20171018050000 20171005040000 46809 . Gqx4rurS7g34OaTMZuVqeULR0YKkHJSDbeq6MhUrf2Zs9k4S+EfYYTun 9qcns+xkDlrHkcrPYMQpOjRTLHXasaZnWcnr+t2ok7MlGefnLT8OCZBh UDcDw0gO/0V4oPn6R9dkTA7l2ZOaQl5UdHh1E6GRynr5JDaqZp5R0iX3 PZaaR9oL9GxvTW5cED4C5auIVt4TCOLSuaeotMyuuNKlVUXZkAXGHKtz Nqpzj0cm+NWMATzqOHT1yJzh9BoB1POZdMNIhsksyyX3idDu4VAQIrwR zeQdHPIZhrJ4Hc+7JVEkLC6tXI56GVb+eBlFY1Q6q0M1zWi7+DjcGJJU fjsVzA==
;; Received 1097 bytes from 75.75.75.75#53(75.75.75.75) in 17 ms

com.                    172800  IN      NS      a.gtld-servers.net.
com.                    172800  IN      NS      b.gtld-servers.net.
com.                    172800  IN      NS      c.gtld-servers.net.
com.                    172800  IN      NS      d.gtld-servers.net.
com.                    172800  IN      NS      e.gtld-servers.net.
com.                    172800  IN      NS      f.gtld-servers.net.
com.                    172800  IN      NS      g.gtld-servers.net.
com.                    172800  IN      NS      h.gtld-servers.net.
com.                    172800  IN      NS      i.gtld-servers.net.
com.                    172800  IN      NS      j.gtld-servers.net.
com.                    172800  IN      NS      k.gtld-servers.net.
com.                    172800  IN      NS      l.gtld-servers.net.
com.                    172800  IN      NS      m.gtld-servers.net.
com.                    86400   IN      DS      30909 8 2 E2D3C916F6DEEAC73294E8268FB5885044A833FC5459588F4A9184CF C41A5766
com.                    86400   IN      RRSIG   DS 8 1 86400 20171018170000 20171005160000 46809 . H3HKSPmogdfIznmPZO9Qjo33Kk2kxds6Qc79ti2DcBhqfnKWLcdrlYIO hh4lXFlGQZc8ySrfXg2BZ0n1YKqea9HrktCHQsdEhJywZM/avD7EfMdW Woc/4pofkuoYF4gQ8fGSEOO9fQaCqS2SqokzKAR3aDDv7crK5pPfX/nz mqbPclm6jq63um4I0cjgnIM5ceoV6UM4m9sFqaTDXfqqWafQMfIXy2s1 RqxtWt4J0naFOFFNH2SkdHN6gngQDCDPXRJfXnzMof7F3qXWMvWS1uKR OSleF+6B/cJMve+nJqrGnwzktVkDNVqQ8bfl7kwO1peiNZqJ9FIpPz6r 1hpmVA==
;; Received 1175 bytes from 198.97.190.53#53(h.root-servers.net) in 97 ms

example.com.            172800  IN      NS      a.iana-servers.net.
example.com.            172800  IN      NS      b.iana-servers.net.
example.com.            86400   IN      DS      31589 8 1 3490A6806D47F17A34C29E2CE80E8A999FFBE4BE
example.com.            86400   IN      DS      31589 8 2 CDE0D742D6998AA554A92D890F8184C698CFAC8A26FA59875A990C03 E576343C
example.com.            86400   IN      DS      43547 8 1 B6225AB2CC613E0DCA7962BDC2342EA4F1B56083
example.com.            86400   IN      DS      43547 8 2 615A64233543F66F44D68933625B17497C89A70E858ED76A2145997E DF96A918
example.com.            86400   IN      DS      31406 8 1 189968811E6EBA862DD6C209F75623D8D9ED9142
example.com.            86400   IN      DS      31406 8 2 F78CF3344F72137235098ECBBD08947C2C9001C7F6A085A17F518B5D 8F6B916D
example.com.            86400   IN      RRSIG   DS 8 2 86400 20171011042652 20171004031652 5528 com. CdiFjCZayrnvnBJLJkIu4Y3ze0Tt1Ee0EQGncFteAVlMynR+OZLVj3yl x5gR8eoz60J2GJBitaRF7ShIThqFJANhZj2UNVgGTj2MwIoKdSYa9RzW MFl5jDtccwPQlz9ExQRsKdhWvR+NmHzxZGL8i3Jn1mlYy/zlDBhcOnT1 PVs=
;; Received 595 bytes from 2001:503:231d::2:30#53(b.gtld-servers.net) in 61 ms

www.example.com.        86400   IN      A       93.184.216.34
www.example.com.        86400   IN      RRSIG   A 8 3 86400 20171015151339 20170924131703 15819 example.com. UGzI8J1fpRC4ckqAGmRngSfcWuu3W8q+d6JusiM8JG0ofH3YAdsHH0lF jWt5vyb/VUVEy/9VBU9bg97EokbTivETfESA3kIePbUtm5RGMPs+rTO0 KwyOqU5LzmHtwJTrYHzkN8QxTBZfX77//PGoiVfZturMLZxNIO6jg9Ke Vcf7Mao=
example.com.            86400   IN      NS      b.iana-servers.net.
example.com.            86400   IN      NS      a.iana-servers.net.
example.com.            86400   IN      RRSIG   NS 8 2 86400 20171015113637 20170924071703 15819 example.com. MwSG+cV2YIqswOOkBXVNmMUx4jVg3sGe4cOrRjmAg8fwNfx/OxC7QUbt vjeseYXDtYECEfVKjaPlPh8P7YhlI1WQvm3QVYf3z0avd67UYBJPZH7i h++xg6X+n3uBtYigkgIJ4l7fTZ9bYwEyEwFuqVjkiYOEkIH4MBjeCVeM NUtIyCQ=
;; Received 544 bytes from 199.43.133.53#53(b.iana-servers.net) in 43 ms
```
{{% /expand%}}

1. Check your output. The last section contains most of the useful information.

Notice the line `www.example.com.        86400   IN      A       93.184.216.34`. This means that the DNS lookup retrieved an A record pointing to 93.184.216.34 for the "www" subdomain. All queries for www.example.com will be instructed to visit that IP address. The record has a TTL of 86400 seconds, meaning that DNS servers are instructed to cache this value for 24 hours and any DNS changes will take up to that long to be completely propagated globally.

Another feature of interest is the following: `example.com.            86400   IN      NS      b.iana-servers.net.`. This specifies the name servers for your DNS hosting company and the place where your DNS configuration is managed.

After a successful DNS change onto Section, your main website domain (**www.example.com**) should have a CNAME record (or an ALIAS record in the case of a bare domain) pointing towards the section CNAME record visible on the DNS tab in the Section portal. For example:

    www.example.com.        86400   IN      CNAME       www.example.com.c.section.io   
