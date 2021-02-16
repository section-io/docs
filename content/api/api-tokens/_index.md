---
title: API Tokens
description: API Key usage with the section API
keywords: Section, training, platform overview, api keys
weight: 2
aliases:
  - /api/api-keys/

---
## Introduction
Section allows you to create an API key belonging to your user. This API key will have the same permissions 
as your user has at the time of creation. When your user is deleted, this key will persist.

## Creating an API Token

Go to the [User Setting page](https://aperture.section.io/new/configure/user) by clicking on your profile picture in the top right then select [API Tokens](https://aperture.section.io/new/configure/user/tokens).

![Create API Token](/docs/images/api-token-create.png)

Enter a description for what this API token will be used for and then click the *Add* button.

![Create API Token Result](/docs/images/api-token-create-after.png)

Copy the token value and store it somewhere securely.  As the warning says, this value cannot be retrieved later. If you loose this value you will need to create a new token and delete the old one.

The tokens you have created will be listed on this page, and can be deleted by clicking the *X* button next to the token description.

## Using an API Token
Use your API Token by adding it to your requests in the Section-Token header.

```bash
curl -H "Section-Token: API-TOKEN-HERE" aperture.section.io/api/v1
```

Tokens can also be used to authenticate git when accessing the Section config repository for your application.  When git prompts for your username enter `section-token` and use the token value as the password.
