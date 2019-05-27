---
title: Getting started with NodeJS on Section
description: Using Section's NodeJS module.
keywords: content delivery network, CDN, node, nodejs, edge compute, proxy
---

Section's NodeJS module allow you to deploy your own NodeJS code at the Edge. Below are the following steps you will need to take to get the NodeJS module up and running within your [Section](https://www.section.io) application.

## Step 1: Add NodeJS module to Section application

Pull your Section application repository to your local machine. In the root of your repository, add a folder titled `nodejs`. Then edit `section.config.json` file in the root directory and add the following lines under proxy:

```
{
    "name": "nodejs",
    "image": "nodejs:10.11.0"
}
```

## Step 2: Define URL paths to be served by the Node module.

Create a new file under the `nodejs` directory named `server.conf`. This is an Nginx configuration file where you can add location blocks to direct HTTP requests either at the NodeJS module or bypass it.

For a location to be server by the nodejs module you will need the following Nginx location block.

```
location /examplePath1/ {
    proxy_set_header X-Forwarded-For $http_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
    proxy_set_header Host $host;
    include /etc/nginx/section.module/node.conf;
}
```

For all requests to be served by the NodeJS module, you can replace `location /examplePath/` with `location /`

If you would like to bypass the NodeJS module for certain URL paths, use the following location block:

```
location ~ "/examplePath2/" {
    proxy_set_header X-Forwarded-For $http_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
    proxy_set_header Host $host;
    proxy_pass http://next-hop;
}
```

## Step 3: Setting up your NodeJS app 

Your NodeJS application will live entirely in the `nodejs` folder and needs to satisfy the following requirements.

[NodeJS Contract](/docs/how-content/reference/nodejs-contract/)


## Step 4: Deploy to the Edge

`git push` all your changes to the origin branch of the Section repository to trigger the deployment process. This can take a while depending on a number of factors such as the size of all the node modules required to run the NodeJS application.  



