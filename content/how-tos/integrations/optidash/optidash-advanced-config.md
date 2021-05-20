---
title: Optidash Advanced Configuration
description: Settings Available for the Optidash module
keywords: Section, training, platform overview
weight: 1
aliases:
  - /modules/optidash/how-tos/optidash-advanced-config/
  - /modules/kraken/reference/optidash-advanced-config/
---

## Optidash Module Settings

Once your application has been set up with Optidash you will find the following settings under `Advanced Config > Optidash` in the Section Console (Aperture portal). 
```
{
    "api_key": "REDACTED",
    "lossless": false,
    "enabled": true,
    "ttl": 604800,
    "cache_version": "v1",
    "s3": {
        "key": "REDACTED",
        "secret": "REDACTED",
        "region": "ap-southeast-2",
        "bucket": "section-kraken"
    }
}
```

---


- `"lossless" : "true/false"`

Enable disable lossy compression.

- `"quality" : 1 - 100`

 This options will only be used if the LOSSY option is set to true. Can be a number in the range of 1 - 100. If the quality option is not provided it will default to "auto" where Optidash will optimize the images based on their characteristics.

- `"compression" : "ultra"`

Overrides `lossless` and `quality` settings and provides lower quality and smaller images even compared to the lowest `quality` setting. This option is only recommended for sites that do not care about the image quality and require maximise image size reduction.

- `"cache_version" : "v1"`

You can update the "cache_version" to clear the entire Optidash cache.


- `"ttl" : <time>`

Sets as cache-control maxage in the response headers sent downstream


- `"enabled" : true/false`

You can enable/disable image optimization by changing the value for the "enabled" option. When in a disabled state the module acts as a reverse proxy.

- `"s3" : {}`

Section provides storage for optimized images. If you want the optimized images to be stored in your own S3 bucket we can set it up for you.

- `"optimize_paths" : ["/images/", "/media/"]`

You can provide a list of path prefixes for which you want the Optidash module to attempt optimization. The Optidash module optimizes by default the image extensions **png,jpeg,jpg,gif and webp**. For any other assets you can use the above feature. For example using a prefix */images* as shown above will instruct the Optidash module optimize all images which have the prefix */images* in their URL.

### Image Resizing

Section Optidash module can use querystrings to resize using the following strategies: auto, exact, fill, fit, landscape, portrait. See Optidash docs for details: https://docs.optidash.ai/operations/resizing

Querystring paramaters accepted:
- `width` - positive integer
- `height` - positive integer
- `mode` - Image resizing mode, default is auto

Note: legacy parameter from previous solution
- `strategy`  - string indicating strategy to be used

Example auto mode:
`www.example.com/image.png?mode=auto&width=100`

Legacy strategy usage:
`www.example.com/image.png?strategy=auto&width=100&height=200`


### Bypass optimization

Section Optidash module will not optimize an image when the request contains the header:

- `Optidash-Optimized: false`
