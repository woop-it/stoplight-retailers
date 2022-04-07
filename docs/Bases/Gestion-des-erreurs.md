---
tags: ["Basis"]
---

# Error handling

The API error responses include details of what went wrong. The format of the response is described as follows:

```json
{
  "statusCode": 400,
  "error": "Bad Request",
  "message": "Invalid request payload JSON format"
}
```

The following is a list of possible API errors:

| HTTP code | Status       | Description                                                                                             |
| --------- | ------------ | ------------------------------------------------------------------------------------------------------- |
| `400`     | Bad Request  | Missing and/or incorrect elements in the body of the request                                            |
| `401`     | Unauthorised | You are not authorised to access this item                                                              |
| `404`     | Not found    | The requested item does not exist or is not recognised                                                  |
| `403`     | Forbidden    | You cannot perform this action (1)                                                                      |
| `409`     | Conflict     | The indicated identifier already exists. The identifier is unique and cannot be generated a second time |
| `504`     | Timeout      | Response time exceeds the maximum response time configured by the caller (2)                            |

(1) The Woop platform acts as a gateway to distribute error codes returned by carriers. The technical and business constraints are to be reviewed (weights, sizes and distances).

(2) The Woop platform acts as a gateway to distribute the response time of the carrier platform. The processing time of the Woop platform is added to the carrier response time.
