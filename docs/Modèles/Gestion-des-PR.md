# Gestion des points-relais

Lors de la recherche de points-relais autour d'un point géographique, il est possible d'affiner les résultats en fonction de quatre critères:  

- Le code du transporteur
- Le type de point-relais 
- La catégorie de point-relais
- Un ensemble de colis

Les critères peuvent être sélectionnés en même temps pour une même demande. Il n’y a pas de contraintes sur la multi-sélection entre les types de point-relais et les catégories de retrait. 

## Code du transporteur
Le code du transporteur permet de filtrer la recherche en fonction du ou des transporteurs choisis.

*Ex:*
- Filtre sur un transporteur: 
```json
{
  "carrierCode": "bpost"
}
```
- Filtre sur plusieurs transporteurs: 
```json
{
  "carrierCode": ["bpost", "mondial-relay"]
}
```

## Type de point-relais

Le type de point-relais permet de filtrer la recherche en fonction du lieu de dépôt. Il est possible de choisir entre un `LOCKER` ou un bureau de poste (`POST-OFFICE`) par exemple. 

Code | Intitulé
---------|----------
 `PICKUP_POINT_AGENCY`|Agence de ramassage
 `PICKUP_POINT_POST_OFFICE`|Point-relais situé en agence La poste
 `PICKUP_POINT_RELAY_WITH_LOCKER`|Point relais avec Locker 
 `PICKUP_POINT_RELAY_WITHOUT_LOCKER`|Points relais sans Locker
 `PICKUP_POINT_ALL`|Tous les points relais possible

Default value : `PICKUP_POINT_ALL`

Types disponibles par transporteur:

Transporteur | Code | Types
---------|---------|----------
 Bpost| bpost|PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITH_LOCKER, PICKUP_POINT_RELAY_WITHOUT_LOCKER
 Chronopost | chronopost | PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITH_LOCKER, PICKUP_POINT_RELAY_WITHOUT_LOCKER
  Colissimo | colissimo | PICKUP_POINT_AGENCY, PICKUP_POINT_POST_OFFICE, PICKUP_POINT_RELAY_WITHOUT_LOCKER

*Ex:*
- Filtre par type:
```json
{
  "type": "PICKUP_POINT_AGENCY"
}
```
- Filtre par multiples transporteurs et type:
```json
{
  "carrierCode": ["bpost", "chronopost"],
  "type": {
    "bpost": "PICKUP_POINT_AGENCY",
    "chronopost": "PICKUP_POINT_RELAY_WITH_LOCKER"
  } 
}
```

## Catégorie de point-relais

La catégorie du point relais spécifique au transporteur, représente souvent une limite de poids / taille de stockage du point relais.

Catégories disponibles par transporteur:

Transporteur | Code | Catégories
---------|---------|----------
 Mondial relay | mondial-relay|24R, 24L, Drive
 Relais colis | relais-colis | RCStandard, RCMax
 Agrikolis | agrikolis | A1, A2, A3, A4
 Colissimo | colissimo | A2P, BPR, CDI, ACP, CMT, BDP


*Ex:*
- Filtre par catégories:
```json
{
  "carrierCode": ["mondial-relay"],
  "category": {
    "mondial-relay": ["24R", "24L"]
  } 
}
```
- Filtre par multiples transporteurs et catégories:
```json
{
  "carrierCode": ["mondial-relay", "relais-colis"],
  "category": {
    "mondial-relay": ["24R", "24L"],
    "relais-colis": ["RCMax"]
  } 
}
```

## Ensemble de colis

Il est possible de passer un ensemble de colis pour filter les points relais capablent d'accepter ces colis (poids et dimension).

*Ex:*
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

> ### A noter
>
> Le paramètre *category* ne peut pas être utiliser quand *packages* est fourni.
