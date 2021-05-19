---
title: API Tokens
description: API tokens usage with the Section API
keywords: Section, training, platform overview, api keys
weight: 2
aliases:
  - /api/api-keys/

---
## Using an API Token

Use your API Token by adding it to your requests in the `Section-Token` header.

```bash
curl -H "Section-Token: YOUR-API-TOKEN-HERE" https://aperture.section.io/api/v1
```

API Tokens can also be used to authenticate git when accessing the Section config repository for your application.  
When git prompts for your username, enter `section-token`, and use the API Token value as the password.
