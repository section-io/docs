---
title: Proxy Contract
description: Requirements to run a reverse proxy on Section.
keywords: reverse proxy, CDN
aliases:
  - /proxy-contract/
  - /reference/proxy-contract/
  - /platform/reference/proxy-contract/
  - /docs/platform/proxy/proxy-contract/

---

# Proxy Requirements

The following defines the interaction between the proxy container and the Section proxy hosting platform:

## Essential

* Proxy should listen on TCP port 80 for HTTP/1.1 on its public interface — never HTTPS or any other port. It may listen on other ports on its loopback interface for internal use only.
* Proxy must connect upstream to `next-hop:80` as HTTP, never HTTPS. The platform will ensure "next-hop" resolves to the next proxy in the chain or the origin — whichever is next upstream.
  * The proxy must resolve the `next-hop` name first via `/etc/hosts` and then via the nameservers and other options defined by [/etc/resolv.conf](http://man7.org/linux/man-pages/man5/resolv.conf.5.html). All other DNS resolution (e.g. external resolvers) are unsupported and will be blocked by the firewall.
* Proxy must handle logs according to these requirements:  
   * All HTTP access must be written to the container's stdout stream in either JSON format or [LTSV](http://ltsv.org/) format.
   * All diagnostic or error logs must be written to the container' stderr stream.
   * Log files should not be used. They will not be accessible outside the proxy and the proxy is responsible managing file growth.
* An executable at `/opt/section/validate.sh` will be executed by Section Console during the git push pre-receive hook to validate that the user's proxy configuration is correct.
  * This executable must exist, even if it takes no action. It does not need to be a shell script, any file with this name and appropriate file mode is acceptable.
  * The user's configuration for the proxy will be available in the `/opt/proxy_config/` directory.
  * The process must return a zero exit code and zero output if config is valid.
  * The process must return non-zero exit code if config is invalid and output reason for validation failure to the stderr stream.
  * The script will have zero network connectivity so the process will not be able to issue requests to external services as part of the validation.

## Optional

 * Proxy should expect that `/opt/proxy_config/` directory will contain the configuration for this proxy. This will be the proxy-specific subdirectory from the Section Application git repository. Assume the directory contents are read-only.

## Things you can rely on

 * Proxy can expect `X-Forwarded-Proto` request header will equal `https` for HTTPS connections from the User-Agent. Assume HTTP otherwise.
 * Proxy can expect `X-Forwarded-For` request header will be present. A `True-Client-IP` request header will also be present and contain a single IP representing the downstream client's address extracted from the `X-Forwarded-For` header.
 * Proxy should configure HTTP/1.1 keep-alive to be enabled for both downstream and upstream connections.

## Additional Considerations

* The proxy image will be published in a publicly accessible docker repository. This repository allows your image to be downloaded to both production servers and section.io users using the Developer PoP.
