---
title: Kraken Advanced Configuration
description: Settings Available for the Kraken module
keywords: Section, training, platform overview
weight: 1
---

## Kraken Module Settings

Once your application has been set up with Kraken you will find the following settings under `Advanced Config > kraken` in the Section Console. We will go over these settings under Operations.

{{< gist section-io-gists c720b97f695ccabccf75c39239deb0c6 >}}

---


- `"lossy" : "true/false"`

Enable disable lossy compression.

- `"quality" : 1 - 100`

 This options will only be used if the LOSSY option is set to true. Can be a number in the range of 1 - 100. If the quality option is not provided it will default to "auto" where Kraken will optimize the images based on their characteristics.



- `"cache_version" : "v1"`

You can update the "cache_version" to clear the entire Kraken cache.


- `"ttl" : <time>`

Sets as cache-control maxage in the response headers sent downstream


- `"enabled" : true/false`

You can enable/disable image optimization by changing the value for the "enabled" option. When in a disabled state the module acts as a reverse proxy.

- `"s3" : {}`

Section provides storage for optimized images. If you want the optimized images to be stored in your own S3 bucket we can set it up for you.

- `"optimize_paths" : ["/images/", "/media/"]`

You can provide a list of path prefixes for which you want the Kraken module to attempt optimization. The Kraken module optimizes by default the image extensions **png,jpeg,jpg,gif and webp**. For any other assets you can use the above feature. For example using a prefix */images* as shown above will instruct the Kraken module optimize all images which have the prefix */images* in their URL.

### Image Resizing

Section Kraken module can use querystrings to resize using the following strategies: auto, exact, fill, fit, landscape, portrait. See Kraken docs for details: https://kraken.io/docs/image-resizing

Querystring paramaters accepted:
- `strategy`  - string indicating strategy to be used
- `width` - positive integer
- `height` - positive integer
- `background` - hex value of background, only used for fill strategy

Example simple usage:
`www.example.com/image.png?strategy=auto&width=100&height=200`

Example advanced usage:
`www.example.com/image.png?strategy=fill&width=100&height=200&background=000000`
