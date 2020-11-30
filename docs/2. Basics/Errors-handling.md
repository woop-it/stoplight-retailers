---
tags: ["Basics"]
---

# Errors handling

Error responses from API contain the detail of what's been wrong. Response format is described like following :

```json
{
  "statusCode": 400,
  "error": "Bad Request",
  "message": "Invalid request payload JSON format"
}
```

This is a list of possible error responses :

| Code HTTP | Status       | Description                                                                 |
| --------- | ------------ | --------------------------------------------------------------------------- |
| `400`     | Bad Request  | Missing or incorrect element in request body                                |
| `401`     | Unauthorized | You are not llowed to acces this element                                    |
| `404`     | Not found    | The requested element has not been found or does not exist                  |
| `403`     | Forbidden    | Impossible action (1)                                                       |
| `409`     | Conflict     | Specified ID already exists. The ID is unique and cannot be generated twice |
| `504`     | xxx          | Response time exceeds max time set by the caller (2)                        |

(1) Woop platform acts as a link to broadcast error code(s) given back by carrier(s). Technical and business constraints must be reviewed (weights, sizes and distances).

(2) Woop platform acts as a link to broadcast response time of carriers platforms. Woop platform response time is added to carriers one.
