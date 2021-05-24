---
title: Set up CSP Report
description: Training area, Section platform overview.
keywords: Section, training, platform overview
weight: 2
aliases:
  - /modules/csp-report/tutorials/add-csp-report-to-your-proxystack/
  - /modules/csp-report/how-tos/
---
---
title: Set up CSP Report
description: CSP Report
weight: 1.5
aliases:
  - /modules/csp-report/set-up/
  - /modules/csp-report/tutorials/
  - /modules/csp-report/tutorials/add-csp-report-to-your-proxystack/
---

## Guide to add CSP Report to your module stack

This tutorial will guide you through the process of adding the CSP Report module to your proxy stack with default configuration files. This tutorial assumes you've cloned your application's git repository to your local machine.

### Step 1 - Setup Openresty in your proxy stack

Follow the instructions from [this page for more details](/docs/modules/openresty/how-tos/)

### Step 2 - Add CSP Report to Openresty

1. Create a folder under the `openresty` folder called `csp`, then copy the files from [this Git Repository](https://github.com/section/csp-report/tree/master/csp) into the new folder. You should end up with the following files in your Section repository.

```
/openresty/csp/csp.json
/openresty/csp/csp.lua
/openresty/csp/csp_init.lua
```

2. Add the following line to Openresty's `init.lua` file
```
cspInit = require("/opt/proxy_config/csp/csp_init")
```

3. Use the following location blocks in Openresty's `server.conf` file
``` nginx
location = /.well-known/csp_reporting {
  rewrite_by_lua_block {
    csp.respondToReport()
  }
}

location / {
  header_filter_by_lua_block {
    csp.injectHeader() 
  }

  proxy_pass "http://next_hop_upstream";
}
```

### Step 3 - Configure the JSON file

Edit `/openresty/csp/csp.json` which should look like the following:
``` json
{
    "Content_Security_Policy_Report_Only": "<Insert policy here> report-uri https://www.yoursite.com/.well-known/csp_reporting",
    "inject_headers": true
}
```
and populate the `Content_Security_Policy_Report_Only` property with your desired CSP policy. Make sure the `report-uri` is updated to use the domain on which this module is setup.

The `inject_headers` boolean is used to toggle whether the `Content_Security_Policy_Report_Only` property is injected as a `Content-Security-Policy-Report-Only` HTTP response header to all responses. You can set this to false to disable the injection.

### Step 4 - Deploy

Commit your changes and push them to the desired branch you are working on. If you run into any issues please contact support@section.io.

### Table of contents

{{% children depth="3" %}}