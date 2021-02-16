# Pickup points management

During pickup point searching around a geographic location, it's possible to refine the results according to three criterias :  

- The carrier code
- Pickup point type 
- Pickup point category

Criterias can be selected at the same time for a unique request. There are not constraints on multi-selection between pickup point types and categories.

## Carrier code
The carrier code allows you to filter the search according to the selected carrier(s).

*Ex:*
- Filter on a carrier: `?carrierCode=bpost``.
- Multi-carrier filter: `?carrierCode=bpost&carrierCode=dpd`.

## Pickup point type

The pickup point type allows filtering the research according to delivery place. It is possible to choose between a `LOCKER` or a post office (`POST-OFFICE`) for example. 

Code | Label
---------|----------
 `PICKUP_POINT_AGENCY`|Pick up agency
 `PICKUP_POINT_POST_OFFICE`|Pickup point located in a post office
 `PICKUP_POINT_RELAY_WITH_LOCKER`|Pickup point with locker
 `PICKUP_POINT_RELAY_WITHOUT_LOCKER`|Pickup point without locker
 `PICKUP_POINT_ALL`|All available pickup points

Default value : `PICKUP_POINT_RELAY_ALL`

## Pickup point category

The category specifies the support for pickup point types depending on a carrier. Each pickup point is able to take a product typology, accepting a size and a maximum volume. 

Code | Label
---------|----------
 `PICKUP_POINT_STANDARD`|Standard pickup point
 `PICKUP_POINT_XL`|XL pickup point 
 `PICKUP_POINT_XXL`|XXL pickup point 
 `PICKUP_POINT_DRIVE`|Drive pickup point

Default value : `PICKUP_POINT_STANDARD`

*Ex:*
- Filter by category: `?category=PICKUP_POINT_STANDARD``.
- Multi-category filter: `?category=PICKUP_POINT_STANDARD&category=PICKUP_POINT_XL`.
- Filter by carriers and categories: `?carrierCode=bpost&carrierCode=dpd&category[bpost]=PICKUP_POINT_STANDARD&category[bpost]=PICKUP_POINT_XL&category[dpd]=PICKUP_POINT_STANDARD`.