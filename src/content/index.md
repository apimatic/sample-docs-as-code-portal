---
title: Welcome
description: Getting started with the Swagger Petstore API
---

Welcome to the Swagger Petstore documentation.

The Petstore is a sample API for a store that sells pets. It covers the three
things most APIs need: managing a catalogue (`/pet`), placing orders against it
(`/store`), and the accounts that place them (`/user`).

## Base URL

All requests go to:

```
https://petstore3.swagger.io/api/v3
```

## Your first request

Fetch every pet that is still up for adoption:

```bash
curl "https://petstore3.swagger.io/api/v3/pet/findByStatus?status=available" \
  -H "Accept: application/json"
```

Browse the full endpoint reference in the **API** section, or read
[Authentication](/authentication) first if you plan to write data.
