---
tags: ['Bases']
---

# Formats

## Date

Toutes les dates utilisées dans nos APIs sont au format **ISO 8601**.

**En entrée de nos APIs** vous pouvez utiliser des dates avec timezone ou en UTC.

Exemple : `2020-09-20T09:00:00+02:00` ou `2020-09-20T07:00:00Z`


**En retour de nos APIs** toutes les dates seront au format UTC.

Exemple: `2020-09-20T07:00:00Z`

## Numéro de téléphone

Tous les numéros de téléphone doivent être dans un format international : `Indicatif + numéro`

Exemple: `+33610101010` ou `0033610101010`