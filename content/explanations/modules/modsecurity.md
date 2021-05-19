---
title: ModSecurity
description: A discussion of how Modsecurity integrates with Section and an overview of how to get started.
keywords: [Modsecurity, firewall]
aliases:
  - /modules/modsecurity/
  - /topic-guides/advanced-config/modsecurity-config/
  - /modules/modsecurity/overview/
  - /modules/modsecurity/reference/
  - /modules/modsecurity/reference/available-versions/
weight: 1
---

## Modsecurity Configuration

The initial configuration in a repository starts ModSecurity’s SecRuleEngine in DetectionOnly mode (this writes log entries but never executes any disruptive actions) with rules from base\_rules & optional\_rules. This is a great starting point, as you can immediately see possible threats without stopping legitimate traffic to your site.

*Note:* Whilst many tutorials and guides use *Symbolic Links* to have content appear in the rules/activated\_rules directory, symbolic links complicate the use of source control & local development. It is recommended to copy files instead, and *never* use symbolic links in any Section configuration.

To add a new rule set, copy the rule set .conf file into your rules/activated\_rules directory.

To remove a rule set, delete the corresponding .conf file from your rules/activated\_rules directory.

To edit a rule set, edit the text content of the corresponding .conf in your rules/activated\_rules directory.

There is also a GUI tool under Configuration&gt;Proxy in the application portal to help enable and disable rule sets.

For documentation see [Modsecurity](http://www.modsecurity.org/documentation.html) and [OWASP Modsecurity Rule Set Project](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project).

### How ModSecurity work on Section

At every opportunity, the implementation of ModSecurity on the Section platform has been designed to be as close as possible to how it would be if you had installed ModSecurity yourself locally.

Section uses the official ModSecurity distributions published by [Trustwave] running upon Apache. Section does not use custom-compiled builds of modsecurity.

ModSecurity will be initialized with the configuration found in the modsecurity.conf file, and matching rule files at rules/activated\_rules/\*.conf under the corresponding subdirectory of your Section application repository.

*Note:* Like other proxies in Section, ModSecurity will sit between a TLS offload system accepting incoming connections, and an outbound proxy making upstream connections. Two additional HTTP request headers will be added to carry connection information, X-Forwarded-For containing the downstream client IP address and any intermediate proxy IP addresses, and also X-Forwarded-Proto which will specify either http or https depending on the protocol with which the downstream client connected.

### High Availability & ModSecurity State

To achieve high availability & performance in production, Section will run multiple instances of your ModSecurity proxy stack. It’s important to consider that each instance is unaware of the internal state of other running instances.

A set of client requests will likely be spread across different instances, and any rules that track state (using setvar, setuid, setsid, etc) will likely act differently in a distributed environment.

### Enabling Protection

Every rule set can have false positives in new environments and any new installation should initially run with Detection only. After running ModSecurity in detection only mode for a while, review the logs and decide if any further modifications to the rule sets should be made before switching to protection mode.

To enabled protection edit the modsecurity.conf file and change the setting for SecRuleEngine from DetectionOnly to On.

## Available versions

### ModSecurity 2.7

- apache 2.4.7
- modsecurity 2.7.7
- OWASP ModSecurity Core Rule Set ([commit c63affc9dfa6294ecf8782ae4d1f1fb2c9fd5a18]) included by default
