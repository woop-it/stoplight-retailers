---
tags: ["Basics"]
---

# Formats

## Date

All dates in API are in **ISO 8601** format.

**As API input** you have to use dates with timezone information or UTC.

_Example : `2020-09-20T09:00:00+02:00` or `2020-09-20T07:00:00Z`_

**As API output** all dates will be in UTC format.

_Example: `2020-09-20T07:00:00Z`_

## Phone number

All phone numbers are in international format : `country code + number`

_Example: `+33610101010`_
