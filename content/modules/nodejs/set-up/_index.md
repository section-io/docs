---
title: Set up
description: Using Section's Node.js module.
keywords: content delivery network, CDN, node, nodejs, edge compute, proxy
aliases:
  - /modules/nodejs/tutorials/
  - /modules/nodejs/tutorials/getting-started/
---

Section's Node.js module allows you to deploy your own Node.js code at the Edge. Below are the following steps you will need to take to get your Node.js app up and running within your [Section](https://www.section.io) application.

## Step 1: Add Node.js module to Section application

Pull your Section application repository to your local machine. In the root of your repository, add a directory titled `nodejs`. Then edit `section.config.json` file in the root directory and insert the following object into the proxychain object located in the json file. This can be inserted at the index you prefer:

```
{
    "name": "nodejs",
    "image": "nodejs:10.11.0"
}
```

## Step 2: Define URL paths to be served by the Node.js module.

Create a new file under the `nodejs` directory named `server.conf`. This is an Nginx configuration file where you can configure location blocks to route traffic to either the Node.js process or the next module in your proxy stack.

To route traffic to your Node.js process you'll need to use the following Nginx configuration in the location block.

```
location /examplePath1/ {
    proxy_set_header X-Forwarded-For $http_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
    proxy_set_header Host $host;

    # This sends the request to the local Node.js server.
    include /etc/nginx/section.module/node.conf;
}
```

For all requests to be routed to the Node.js process, you can replace `location /examplePath/` with `location /`

If you would like to bypass the Node.js process for certain URL paths, use the Nginx configuration location block:

```
location ~ "/examplePath2/" {
    proxy_set_header X-Forwarded-For $http_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
    proxy_set_header Host $host;

    # This sends the request to the upstream module or origin web server.
    proxy_pass http://next-hop;
}
```

## Step 3: Setting up your Node.js app

Your Node.js application will live entirely in the `nodejs` directory and needs to satisfy the following requirements:

[Node.js Contract]({{< relref "modules/nodejs/_index.md" >}})

Here is an example application that will work out of the box with Section Node.js module. [Node.js Example Nuxt App](https://github.com/section/nodejs-example)

## Step 4: Deploy to the Edge

Commit all your changes to your Section repository and desired branch/environment to trigger the deployment process. This can take a while depending on a number of factors such as the size of all the Node.js modules required to run the Node.js application.
