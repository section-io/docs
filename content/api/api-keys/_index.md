---
title: API Keys
description: API Key usage with the section API
keywords: Section, training, platform overview, api keys
weight: 2

---
## Introduction
Section allows you to create an API key belonging to your user. This API key will have the same permissions 
as your user has at the time of creation. When your user is deleted, this key will persist.

## Creating an API Key

You can create an api with your user by making the following request:

```bash
curl -u username:password -XPOST -d '{"query":"mutation {  createUserAPIToken}"}' https://aperture.section.io/new/authorized/graphql_api/query
```

Where you should replace `username` and `password` with your section username/password for basic authentication.

## Using an API Key
Use your API Key by adding it to your requests in the Section-Token header.

```bash
curl -H "Section-Token: API-KEY-HERE" aperture.section.io/api/v1
```
