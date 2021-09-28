# Gestion des points-relais

Lors de la recherche de points-relais autour d'un point géographique, il est possible d'affiner les résultats en fonction de trois critères:  

- Le code du transporteur
- Le type de point-relais 
- La catégorie de point-relais

Les critères peuvent être sélectionnés en même temps pour une même demande. Il n’y a pas de contraintes sur la multi-sélection entre les types de point-relais et les catégories de retrait. 

## Code du transporteur
Le code du transporteur permet de filtrer la recherche en fonction du ou des transporteurs choisis.

*Ex:*
- Filtre sur un transporteur: `?carrierCode=bpost`
- Filtre sur plusieurs transporteurs: `?carrierCode=bpost&carrierCode=dpd`

## Type de point-relais

Le type de point-relais permet de filtrer la recherche en fonction du lieu de dépôt. Il est possible de choisir entre un `LOCKER` ou un bureau de poste (`POST-OFFICE`) par exemple. 

Code | Intitulé
---------|----------
 `PICKUP_POINT_AGENCY`|Agence de ramassage
 `PICKUP_POINT_POST_OFFICE`|Point-relais situé en agence La poste
 `PICKUP_POINT_RELAY_WITH_LOCKER`|Point relais avec Locker 
 `PICKUP_POINT_RELAY_WITHOUT_LOCKER`|Points relais sans Locker
 `PICKUP_POINT_ALL`|Tous les points relais possible

Default value : `PICKUP_POINT_RELAY_ALL`



## Catégorie de point-relais

La catégorie indique la prise en charge des types de point-relais en fonction d'un transporteur. Chaque point de retrait est capable d'accueillir une typologie de produit acceptant une taille et un volume maximum. 

Code | Intitulé
---------|----------
 `PICKUP_POINT_STANDARD`|Point relais standard
 `PICKUP_POINT_XL`|Point relais XL 
 `PICKUP_POINT_XXL`|Point relais XXL 
 `PICKUP_POINT_DRIVE`|Points relais drive

Default value : `PICKUP_POINT_STANDARD`

*Ex:*
- Filtre sur une catégorie: `?category=PICKUP_POINT_STANDARD`
- Filtre sur plusieurs catégories: `?category=PICKUP_POINT_STANDARD&category=PICKUP_POINT_XL`
- Filtre par transporteurs et catégories: `?carrierCode=bpost&carrierCode=dpd&category[bpost]=PICKUP_POINT_STANDARD&category[bpost]=PICKUP_POINT_XL&category[dpd]=PICKUP_POINT_STANDARD`