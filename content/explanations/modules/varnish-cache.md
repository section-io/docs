---
title: Varnish Cache
description: A high level overview of how Section runs Varnish Cache
keywords: [Varnish,caching]
aliases:
  - /modules/varnish-cache/
  - /topic-guides/section-and-varnish/
  - /modules/varnish-cache/overview/
  - /modules/varnish-cache/reference/
  - /modules/varnish-cache/reference/available-versions/
  - /modules/varnish-cache/reference/section-varnish-fact-sheet/
weight: 1
---

## What does it do

Section implements a pure and unchanged version of the Varnish Cache.

At every opportunity, the implementation of Varnish Cache on the Section platform has been designed to be as close as possible to how it would be if you had installed Varnish Cache yourself locally.

Section uses the official Varnish Cache distributions published by Varnish Cache. Section does not use custom-compiled builds of Varnish Cache.

Varnish Cache is started, listening on port 80.

Varnish Cache VCL can found in the **default.vcl** file in the corresponding subdirectory of your Section application repository.

Assuming Varnish Cache is the first proxy in your proxy stack, Varnish Cache will receive connections from the **Section TLS Offload Proxy** with two additional HTTP request headers.

1. **X-Forwarded-For** containing the downstream client IP address and any intermediate proxy IP addresses.
2. **X-Forwarded-Proto** which will specify either HTTP or HTTPS depending on the protocol with which the downstream client connected.

Issuing cache invalidation requests to Varnish Cache sends a ban command to the Varnish Cache management interface. Section accepts any valid Ban expression and passes it to Varnish Cache unaltered.

We also provide some convenience tools to help with removing particular URL's from the cache, see our [Cache Clearing]({{< relref "/how-tos/module-integrations/varnish/clearing-the-cache.md" >}})  documentation for more details.

Requesting the Varnish Cache Log executes varnishlog for each Varnish Cache instance and returns the results.

varnishncsa is also running, logging request and response details, including cache effectiveness. This data is used to drive the charts seen in Aperture.

## Fundamentals

* Varnish Cache is a HTTP caching reverse proxy.
* "Varnish Cache decides whether it can store the content or not based on the response it gets back from the backend".
* the origin or backend can instruct Varnish Cache to cache the content with the HTTP response header Cache-Control.
* Varnish Cache by default does not cache cookies or other sensitive client side content.
* Varnish Cache has a conservative approach to caching to avoid the cache leaking sensitive data i.e. shopping cart or personalization information.
* Varnish Cache policies can be changed by Varnish Configuration Language (VCL).
* VCL is a flexible and power language that can handle a wide range of use cases.  
* delivery from cache is usually in milliseconds.
* Varnish Cache is highly performant, is usually twice as fast as a backend server and Varnish Cache is usually constrained by networks.

Source: [Varnish 6.3 Official Docs - Starting Varnish](https://varnish-cache.org/docs/6.3/tutorial/starting_varnish.html)

## Varnish Cache Basics

The Varnish Configuration Language (VCL) is a domain-specific language for caching HTTP requests. The language is specific to the domain of caching HTTP requests and responses.

* Varnish Configuration Language (VCL) implements a state machine.
* Varnish Cache uses VCL (Varnish Configuration Language) to run as a ‘state machine’.
* Various Varnish Cache states are thought of, and implemented as subroutines.
* Varnish Cache includes built-in subroutines via builtin.vcl.
* VCL has functions, legal return actions and variables.
* VCL functions can be extended by *vmods* (Varnish Cache modifications).
* Varnish Cache on Section has a preinstalled set of [vmods](https://github.com/nigoroll/varnish-modules).
* Each URL in the cache is hashed and accessible via a hash key based on host-headers, IP or other criteria via VCL logic or VMODs.

## Varnish Cache Receive and Respond

The two most important Varnish states or subroutines or subs are "received request"`vcl_recv` and "backend response" `vcl_backend_response`.

* "received request" `vcl_recv`
* "backend response" `vcl_backend_response`

## Varnish Cache Flow

![Varnish Cache Flow Diagram](http://book.varnish-software.com/4.0/_images/simplified_fsm.svg)

Source: [Varnish Software Book](https://info.varnish-software.com/the-varnish-book)

## Varnish Cache Flow Described

Each HTTP request flows by switching between Varnish Cache states such as `recv`, `hit`, `miss` or `pass` by calling `return` functions which use VCL logic to determine which state is next. For each state `recv` there is a VCL subroutine `vcl_recv`.

| State | Subroutine | Name | Description
|:--|:--|:--|---|
| [recv](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-recv "vcl_recv") | [vcl_recv](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-recv "vcl_recv") | **Received** | HTTP request is completely received, parsed and can then be inspected and modified by this routine. `vcl_recv` subroutine is terminated by calling `return()` and can `fail`, `synth`, `restart`, `pass`, `pipe`, `hash`, `purge` and `vcl(label)`.|
| [hash](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-hash "vcl_hash") | [vcl_hash](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-hash "vcl_hash") |  **Hash** | Creates a unique hash key for each cached object. By default, the builtin `vcl_hash` uses hostname or IP address and adds the requested URL to the cache hash. `vcl_hash` always runs the `lookup` action on the hash key and determines the next state / sub-routine i.e. `hit`, `miss`, `pass` or `purge` etc. |
| [hit](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-hit "vcl_hit") | [vcl_hit](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-hit "vcl_hit") | **Hit** | Called by `vcl_hash` via the lookup operation, `vcl_hit` finds or "hits" a cache object. High hit rates are optimal for website performance.|
| [miss](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-miss "vcl_miss") | [vcl_miss](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-miss "vcl_miss") | **Miss** | If a requested object is not found by a lookup of the cache hash key, it is declared a miss by the `vcl_miss` subroutine. `vcl_miss` decides if a document should be retrieved from a backend by returning `fetch`. |
| [pass](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-pass "vcl_pass") | [vcl_pass](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-pass "vcl_pass") | **Pass** | "Called upon entering pass mode. In this mode, the request is passed on to the backend, and the backend's response is passed on to the client, but is not entered into the cache. Subsequent requests submitted over the same client connection are handled normally". |
| [pipe](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-pipe "vcl_pipe") | vcl_pipe | **Pipe** | Pipes a HTTP request direct to backend or origin, passing back and forwards with no other VCL running. Basically turns Varnish into a dump TCP/IP proxy. |
| [fetch](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-backend-fetch "vcl_backend_fetch") | [vcl_backend_fetch](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-backend-fetch "vcl-backend-fetch") | **Backend Fetch** | `vcl_backend_fetch` can be called from `vcl_miss` or `vcl_pass`. It typically alters the request before it gets to the backend or origin. |
| [response](https://book.varnish-software.com/4.0/chapters/VCL_Basics.html#vcl-vcl-backend-response "vcl_backend_response") | [vcl_backend_response](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-backend-response "vcl-backend-response") | **Backend Response** | `vcl_backend_response` is designed to avoid caching cookies and other probably undesired data. Called after response headers are retrieved from the backend/origin. Returns `vcl_deliver`.|
| [deliver](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-deliver "vcl_backend_deliver") | [vcl_deliver](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-deliver "vcl-deliver") | **Deliver** | Usually the last exit point for HTTP request flows and is often used to add or remove debug-headers. Cached content is ready to be delivered to client of user. |
| [synth](https://book.varnish-software.com/4.0/chapters/VCL_Subroutines.html#vcl-vcl-backend-fetch "vcl_synth") | [vcl_synth](https://varnish-cache.org/docs/trunk/users-guide/vcl-built-in-subs.html#vcl-synth "vcl_synth") | **Synth** | `vcl_synth` is called to deliver a synthetic object, generated in VCL and not fetched from the backend. |

## Varnish Cache Modifications

Varnish Cache modifications or vmods pre-installed on Section. This is a collection of modules ("vmods") extending Varnish VCL used for describing HTTP request/response policies with additional capabilities.

| VMOD | Name | Description
|:--|:--|---|
| [cookie](https://varnish-cache.org/docs/trunk/reference/vmod_cookie.html?highlight=cookie "cookie") | Cookie | HTTP request is received and can then be inspected and modified by this routine. |
| [vsthrottle](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_vsthrottle.rst "vsthrottle - Throttling VMOD") | Throttling VMOD | A Varnish Cache vmod for rate-limiting traffic on a single Varnish Cache server. Offers a simple interface for throttling traffic on a per-key basis to a specific request rate. |
| [header](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_header.rst "Header VMOD for Varnish") | Header VMOD for Varnish Cache | Varnish Cahce Module for manipulation of duplicated HTTP headers, for instance multiple Set-Cookie headers. |
| [saintmode](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_saintmode.rst " Saint mode backend director") |  Saint mode backend director | Saintmode lets you deal with a backend that is failing in random ways for specific requests. It maintains a blacklist per backend, marking the backend as sick for specific objects. When the number of objects marked as sick for a backend reaches a set threshold, the backend is considered sick for all requests. Each blacklisted object carries a TTL, which denotes the time it will stay blacklisted. |
| [softpurge](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_softpurge.rst "Softpurge") | Softpurge | Softpurge is cache invalidation in Varnish that reduces TTL but keeps the grace value of a resource. It is not safe to use with Varnish Cache 5.0 onwards, use vmod-purge from Varnish Cache 5.2 instead. |
| [tcp](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_tcp.rst "TCP vmod") | TCP vmod | The TCP vmod opens for access and modification of client TCP connection attributes from VCL. |
| [var](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_var.rst "var") | var | This VMOD implements basic variable support in VCL. |
| [xkey](https://github.com/nigoroll/varnish-modules/blob/master/docs/vmod_xkey.rst "xkey") | xkey - Surrogate keys support for Varnish Cache | This vmod adds secondary hashes to objects, allowing fast purging on all objects with this hash key. |
| [bodyaccess](https://github.com/nigoroll/varnish-modules/blob/master/src/vmod_bodyaccess.c "Body access") | Body access | Undocumented VMOD giving access to body objects. |

## Builtin VCL

* The built-in standard [Varnish builtin.vcl](https://github.com/varnishcache/varnish-cache/blob/master/bin/varnishd/builtin.vcl)

>"Make sure you understand this: Your own VCL-configuration will not overwrite this builtin configuration, it will just be prepended to each sub. Unless your VCL code executes a terminating statement (e.g. return(pass)) it will continue into these default subs."

Source: [Varnish Examples](https://varnish-cache.org/trac/wiki/VCLExamples)

## Varnish Cache Resources

* [Varnish Software Book](https://info.varnish-software.com/the-varnish-book): [Intro](https://book.varnish-software.com/4.0/chapters/Introduction.html)
* [Varnish Blog](https://info.varnish-software.com/blog?hsLang=en-us)
* [Varnish Latest Official Docs](https://varnish-cache.org/docs/trunk/)
* [Varnish Source Code](https://github.com/varnishcache/varnish-cache)
* [Varnish modifications](https://github.com/nigoroll/varnish-modules)

This document is inspired by [Integralist](https://www.integralist.co.uk/posts/fastly-varnish/)

## Available versions

### Varnish Cache v6.0

- Varnish Cache  6.0.0
- Std VMOD - <https://www.varnish-cache.org/docs/6.0/reference/vmod_std.generated.html>
- Cookie, Header, Softpurge, Var, and Xkey VMODs - <https://github.com/varnish/varnish-modules#readme>

### Varnish Cache v5.2

- Varnish Cache  5.2.1
- Std VMOD - <https://www.varnish-cache.org/docs/5.2/reference/vmod_std.generated.html>
- Cookie, Header, Softpurge, Var, and Xkey VMODs - <https://github.com/varnish/varnish-modules#readme>
- UUID VMOD - <https://github.com/Sharecare/libvmod-uuid#readme>

### Varnish Cache v5.1

- Varnish Cache  5.1.3
- Std VMOD - <https://www.varnish-cache.org/docs/5.1/reference/vmod_std.generated.html>
- Cookie, Header, Softpurge, Var, and Xkey VMODs - <https://github.com/varnish/varnish-modules#readme>
- UUID VMOD - <https://github.com/Sharecare/libvmod-uuid#readme>

### Varnish Cache v4.1

Varnish Cache  4.1 is available if you need this version

- Varnish Cache  4.1.9
- Std VMOD - <https://www.varnish-cache.org/docs/4.1/reference/vmod_std.generated.html>
- Cookie, Header, Softpurge, Var, and Xkey VMODs - <https://github.com/varnish/varnish-modules#readme>
- UUID VMOD - <https://github.com/Sharecare/libvmod-uuid#readme>

### Varnish Cache  v4.0

Varnish Cache  4.0 is available if you need this version

- Varnish Cache  4.0.3
- Std VMOD - <https://www.varnish-cache.org/docs/4.0/reference/vmod_std.generated.html>
- Cookie VMOD - <https://www.varnish-cache.org/vmod/cookie>
- Maxmind GeoIP VMOD - <https://www.varnish-cache.org/vmod/maxmind-geoip>
- Header VMOD - <https://www.varnish-cache.org/vmod/header-manipulation>
- UUID VMOD - <https://github.com/Sharecare/libvmod-uuid#readme>

### Varnish Cache v3

If you have a need to run Varnish Cache 3, eg. you have existing v3 VCL you want to run in Section, pick this one. This proxy also has ESI enabled to support the [Magento Turpentine extension]

- Varnish Cache  3.0.5
- Cookie VMOD - <https://www.varnish-cache.org/vmod/cookie>
- Maxmind GeoIP VMOD - <https://www.varnish-cache.org/vmod/maxmind-geoip>
- Header VMOD - <https://www.varnish-cache.org/vmod/header-manipulation>

*Varnish is a registered trademark of Varnish Software AB and its affiliates*

### Table of contents

{{% children page="modules/varnish-cache" depth="3" %}}
