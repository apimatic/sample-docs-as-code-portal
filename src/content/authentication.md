---
title: Authentication
description: How to authenticate against the Petstore API
---

Reading the catalogue is open to anyone. Creating, updating or deleting anything
requires credentials.

## API key

Pass your key in the `api_key` header:

```bash
curl "https://petstore3.swagger.io/api/v3/pet/1" \
  -H "api_key: special-key"
```

## OAuth 2.0

The write endpoints are also reachable with an OAuth 2.0 implicit-flow token:

| Scope        | Grants                           |
| ------------ | -------------------------------- |
| `read:pets`  | Reading pets you own             |
| `write:pets` | Creating and modifying your pets |

```bash
curl -X POST "https://petstore3.swagger.io/api/v3/pet" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"fluffy","photoUrls":[],"status":"available"}'
```

Tokens are issued by `https://petstore3.swagger.io/oauth/authorize`.
