---
tags: ["Basics"]
---

# Versioning

A versioning system based on **HTTP Header** is used on all APIs.

`x-api-version` header must be sent in each call with the **targeted API version**.

Example :

```json
{
  "x-api-version": "1.3.0"
}
```

_Version numbers follow a convention. Follow this link for more details on Semantic Versioning : [semver](https://semver.org/)_.
