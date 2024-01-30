# Pickup point management

When searching for relay points in a geographical area, the results can be refined according to five criteria:

- The carrier code
- The type of relay point
- The relay point category
- A drop-off date for the package
- A set of packages

The criteria can be selected at the same time for the same request. Multiple relay point types and collection categories may be selected.

## Carrier code

The carrier code allows you to filter the search by the selected carrier(s).

_Eg:_

- Filter on a carrier:

```json
{
  "carrierCode": "bpost"
}
```

- Filter on several carriers:

```json
{
  "carrierCode": ["bpost", "mondial-relay"]
}
```

## The type of relay point

The type of relay point allows the search to be filtered according to the drop-off location. It is possible to choose between a `LOCKER` or a post office (`POST-OFFICE`) for example.

| Code                                | Title                                |
| ----------------------------------- | ------------------------------------ |
| `PICKUP_POINT_AGENCY`               | Collection agency                    |
| `PICKUP_POINT_POST_OFFICE`          | Relay point located in a post office |
| `PICKUP_POINT_RELAY_WITH_LOCKER`    | Relay point with Locker              |
| `PICKUP_POINT_RELAY_WITHOUT_LOCKER` | Relay point without Locker           |
| `PICKUP_POINT_DRIVE`                | Drive                                |

Default value: `PICKUP_POINT_RELAY_WITHOUT_LOCKER`

Types available by carrier:

| Carrier    | Code       | Types                                                                                                            |
| ---------- | ---------- | ---------------------------------------------------------------------------------------------------------------- |
| Bpost      | bpost      | PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITH_LOCKER, PICKUP_POINT_RELAY_WITHOUT_LOCKER |
| Chronopost | chronopost | PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITH_LOCKER, PICKUP_POINT_RELAY_WITHOUT_LOCKER |
| Colissimo  | colissimo  | PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITHOUT_LOCKER                                 |
| Geodis  | geodis  | PICKUP_POINT_AGENCY                                 |

_Eg:_

- Filter by type:

```json
{
  "type": ["PICKUP_POINT_AGENCY","PICKUP_POINT_RELAY_WITH_LOCKER"]
}
```

- Filter by multiple carriers and type:

```json
{
  "carrierCode": ["bpost", "chronopost"],
  "type": {
    "bpost": ["PICKUP_POINT_AGENCY","PICKUP_POINT_RELAY_WITH_LOCKER"],
    "chronopost": ["PICKUP_POINT_RELAY_WITH_LOCKER"]
  }
}
```

## The relay point category

The relay point category, specific to the carrier, often represents a weight/storage size limit for the relay point.

Categories available by carrier:

| Carrier       | Code          | Categories                   |
| ------------- | ------------- | ---------------------------- |
| Mondial relay | mondial-relay | 24R, 24L, Drive              |
| Relais colis  | Relais colis  | RCStandard, RCMax            |
| Agrikolis     | agrikolis     | A1, A2, A3, A4               |
| Colissimo     | colissimo     | A2P, BPR, CDI, ACP, CMT, BDP |

_Eg:_

- Filter by category:

```json
{
  "carrierCode": ["mondial-relay"],
  "category": {
    "mondial-relay": ["24R", "24L"]
  }
}
```

- Filter by multiple carriers and categories:

```json
{
  "carrierCode": ["mondial-relay", "relais-colis"],
  "category": {
    "mondial-relay": ["24R", "24L"],
    "relais-colis": ["RCMax"]
  }
}
```

## Drop-off date and non-working days

A theoretical drop-off date can be given for the packages in the relay point depending on your internal logistics lead time.

\*Example:
Your logistics lead time is 4 days, you can provide a drop-off date from **today's date + 4 days.\***

**By default the drop-off date is today + 3 days**

From this drop-off date, **a storage period of 14 days is added**if the relay point has temporary closure dates during the drop-off date + storing period, **this relay point is not returned**.

_Example:It is **31 August.** I search for a relay point without providing a drop-off date.**The default drop-off date is calculated as 3 September** and the end of the **storage period is 17 September**.
Only relay points that do not have a closing date during the period **3 to 17 September inclusive** will be returned._

## Set of packages

It is possible to send a set of packages to filter the relay points able to accept these packages by (weight and size).

_Eg:_

```json
 {
  "packages": [
    {
      "length": {
        "value": 15,
        "unit": "cm"
      },
      "width": {
        "value": 15,
        "unit": "cm"
      },
      "height": {
        "value": 1.2,
        "unit": "m"
      },
      "weight": {
        "value": 1,
        "unit": "kg"
      },
      "products": [
        {
          "type": "TYPOLOGY_GENERIC",
          "ean": "4dq86zd4q6zd4q64",
          "cug": "q56zd4q65d4q",
          "label": "Lampe",
          "quantity": 1
        }
      ],
      "quantity": 1
    }
 }
```

<!-- theme: warning -->

> ### Note
>
> The parameter _category_ cannot be used when _packages_ is provided.


## Pickup point type LOCKER with reservation 

To have relay points with reservation, you must pass the "packages" in the request POST/pickupPoint.

It is possible to specify the accessibility of the desired relay point with this parameters:
- pickUpPointAccessibility : accessibility of the pickup point
- boxCategoryAccessibility : accessibility of the box in the pickup point


_Eg:_

```json
 {
   ...
  "packages": [
    {
      "length": {
        "value": 15,
        "unit": "cm"
      },
      "width": {
        "value": 15,
        "unit": "cm"
      },
      "height": {
        "value": 1.2,
        "unit": "m"
      },
      "weight": {
        "value": 1,
        "unit": "kg"
      },
      "products": [
        {
          "type": "TYPOLOGY_GENERIC",
          "ean": "4dq86zd4q6zd4q64",
          "cug": "q56zd4q65d4q",
          "label": "Lampe",
          "quantity": 1
        }
      ],
      "quantity": 1
    }
  ],
 "pickUpPointAccessibility": "ACCESSIBLE",
 "boxCategoryAccessibility": "UPPER"
 ...
 }
```

