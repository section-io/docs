---
title: Set up Wallarm
description: Set up the Wallarm module
keywords: module, security, wallarm
weight: 1.5
---

# wallarm-module

Based on https://github.com/wallarm/docker-wallarm-node

## Getting started

You need an account by either logging in or signing up using the Wallarm web app https://my.wallarm.com/

Once you have an account navigate the the user management section https://my.wallarm.com/settings/users?status=all&orderBy=name&order=asc. We will be cerating a user with the following details:

* type: `Deploy`
* Name: `Section Deploy`
* email: `wallarm_deploy@example.com`
* password: `generate_a_secure_password`

Save the credentials for later.

## Deploying on Section

Clone your Section application repository to your local machine and create a `wallarm` directory in the root of the repository with the following files:

* `geo.conf`
* `server.conf`
* `wallarm.json`

Add the following to your proxychain object in `section.config.json`:

```
{
    "name": "wallarm",
    "image": "wallarm:2.18.1.1"
}
```

Contents for the files are as followed.

### geo.conf

This file is used to define the Wallarm mode (either blocking or monitoring). This is also where the whitelisting functionality lives for the Wallarm WAF. If you wish to whitelist an IP address simply add a line item to the geo block. E.g. `97.118.185.230 off;`

```
geo $remote_addr $wallarm_mode_real {
    # Please replace <WALLARM_MODE> below by the request filtering mode: 
    # off to disable request processing
    # monitoring to process but not block requests
    # block to process all requests and block the malicious ones
    default monitoring;
    # IP addresses and rules for US cloud scanners
    23.239.18.250 off;104.237.155.105 off;45.56.71.221 off;45.79.194.128 off;104.237.151.202 off;45.33.15.249 off;45.33.43.225 off;45.79.10.15 off;45.33.79.18 off;45.79.75.59 off;23.239.30.236 off;50.116.11.251 off;45.56.123.144 off;45.79.143.18 off;172.104.21.210 off;74.207.237.202 off;45.79.186.159 off;45.79.216.187 off;45.33.16.32 off;96.126.127.23 off;172.104.208.113 off;192.81.135.28 off;35.235.101.133 off;34.94.16.235 off;35.236.51.79 off;35.236.87.46 off;35.236.16.246 off;35.236.110.91 off;35.236.61.185 off;35.236.14.198 off;35.236.96.31 off;35.235.124.137 off;35.236.100.176 off;34.94.13.81 off;35.236.55.214 off;35.236.127.211 off;35.236.126.84 off;35.236.3.158 off;35.235.112.188 off;35.236.118.146 off;35.236.1.4 off;35.236.20.89 off;
    # IP addresses and rules for European cloud scanners
    139.162.130.66 off;139.162.144.202 off;139.162.151.10 off;139.162.151.155 off;139.162.156.102 off;139.162.157.131 off;139.162.158.79 off;139.162.159.137 off;139.162.159.244 off;139.162.163.61 off;139.162.164.41 off;139.162.166.202 off;139.162.167.19 off;139.162.167.51 off;139.162.168.17 off;139.162.170.84 off;139.162.171.141 off;139.162.172.35 off;139.162.174.220 off;139.162.174.26 off;139.162.175.71 off;139.162.176.169 off;139.162.178.148 off;139.162.179.214 off;139.162.180.37 off;139.162.182.156 off;139.162.182.20 off;139.162.184.225 off;139.162.185.243 off;139.162.186.136 off;139.162.187.138 off;139.162.188.246 off;139.162.190.22 off;139.162.190.86 off;139.162.191.89 off;85.90.246.120 off;104.200.29.36 off;104.237.151.23 off;173.230.130.253 off;173.230.138.206 off;173.230.156.200 off;173.230.158.207 off;173.255.192.83 off;173.255.193.92 off;173.255.200.80 off;173.255.214.180 off;192.155.82.205 off;23.239.11.21 off;23.92.18.13 off;23.92.30.204 off;45.33.105.35 off;45.33.33.19 off;45.33.41.31 off;45.33.64.71 off;45.33.65.37 off;45.33.72.81 off;45.33.73.43 off;45.33.80.65 off;45.33.81.109 off;45.33.88.42 off;45.33.97.86 off;45.33.98.89 off;45.56.102.9 off;45.56.104.7 off;45.56.113.41 off;45.56.114.24 off;45.56.119.39 off;50.116.35.43 off;50.116.42.181 off;50.116.43.110 off;66.175.222.237 off;66.228.58.101 off;69.164.202.55 off;72.14.181.105 off;72.14.184.100 off;72.14.191.76 off;172.104.150.243 off;139.162.190.165 off;139.162.130.123 off;139.162.132.87 off;139.162.145.238 off;139.162.146.245 off;139.162.162.71 off;139.162.171.208 off;139.162.184.33 off;139.162.186.129 off;172.104.128.103 off;172.104.128.67 off;172.104.139.37 off;172.104.146.90 off;172.104.151.59 off;172.104.152.244 off;172.104.152.96 off;172.104.154.128 off;172.104.229.59 off;172.104.250.27 off;172.104.252.112 off;45.33.115.7 off;45.56.69.211 off;45.79.16.240 off;50.116.23.110 off;85.90.246.49 off;172.104.139.18 off;172.104.152.28 off;139.162.177.83 off;172.104.240.115 off;172.105.64.135 off;139.162.153.16 off;172.104.241.162 off;139.162.167.48 off;172.104.233.100 off;172.104.157.26 off;172.105.65.182 off;178.32.42.221 off;46.105.75.84 off;51.254.85.145 off;188.165.30.182 off;188.165.136.41 off;188.165.137.10 off;54.36.135.252 off;54.36.135.253 off;54.36.135.254 off;54.36.135.255 off;54.36.131.128 off;54.36.131.129 off;
}
```

### server.conf

This files defines the upstream definiton and initalizes the Wallarm nginx module. No customization is needed for this file.

```
wallarm_mode $wallarm_mode_real;
wallarm_acl default;
wallarm_instance 1;

location / {
    proxy_set_header X-Forwarded-For $http_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
    proxy_set_header Host $host;
    proxy_pass http://next_hop_upstream;
}
```

### wallarm.json

This is the customer specific configuration file to authenticate the running container with the Wallarm cloud and where we will be using the credentials generated for the deploy user in the Getting Started section. The `api_host` component is important to get correct based on the region your Wallarm account is registered with. The default is `api.wallarm.com` and note the domain name in the browser navigation for the Wallarm portal to get a hint of which API endpoint to use. More info here: https://docs.wallarm.com/admin-en/api-en/#api-endpoint

Options for api_host:

* `api.wallarm.com` for the EU cloud
* `us1.api.wallarm.com` for the US cloud

```
{
    "api_user": "your_deploy_user_email",
    "api_secret": "your_deploy_user_password",
    "api_host": "api.wallarm.com",
    "acl_enable": false
}
```

`acl_enable` is an optional boolean parameter which enables IP based blocking, see docs here: https://docs.wallarm.com/admin-en/configure-ip-blocking-en/
It is disabled by default. 

## Validating the deployment

Check the nodes Section in the Wallarm portal to ensure nodes are getting registered after deployment and kick off a note to @vgartvich in #wallarm-section to let him know we've deployed agents for customer X.