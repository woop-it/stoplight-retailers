---
tags: ["Basis"]
---

# Versioning

Versioning by **header HTTP** is used in all APIs.

The header `x-api-version` must be sent for each call with **the target API version**.

Example:

```json
{
  "x-api-version": "1.4.0"
}
```

_Version numbers follow the convention. Follow the link for more details on Semantic Versioning: [semver](https://semver.org/)_.
