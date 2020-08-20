# Versionning

Un versioning par **header Http** est utilisé sur toutes nos APIs.

Le header `x-api-version` doit être envoyé à chaque appel avec **la version d'api ciblée**.

Exemple :
```json
{
  "x-api-version": "1.4.0"
}
```

*Les numéros de versions suivent la convention [semver](https://semver.org/)*.

## Versions disponibles

- #### **1.4.0** 

