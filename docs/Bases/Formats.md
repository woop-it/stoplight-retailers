---
tags: ['Bases']
---

# Formats

## Date

All dates used in the API are in the format **ISO 8601**.

**For API input** dates with time zone or UTC information should be used.
If the time zone is not sent, the date will be treated as UTC.

*Example: `2020-09-20T09:00:00+02:00` or `2020-09-20T07:00:00Z`*


**For API input** all dates must be in UTC format.

*Example: `2020-09-20T07:00:00Z`*

## Telephone numbers

All telephone numbers must be in international format: `Country code + number`

*Example: `+33610101010` or `0033610101010`*