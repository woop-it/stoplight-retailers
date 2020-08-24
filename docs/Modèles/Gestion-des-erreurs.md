# Gestion des erreurs

The beginning of an awesome article...

Les réponses erreur des API comprennent le détail de ce qui s'est mal passé. Le format de la réponse est décrit comme suit :

```json
{
    "statusCode": 400,
    "error": "Bad Request",
    "message": "Invalid request payload JSON format"
}
```

Voici la liste des erreurs API possible : 

Code HTTP| Statut| Description
---------|-------|------------
`400`| Bad Request| Éléments manquants et/ou incorrect dans le body de la requête
`401`| Unauthorized| Vous n'êtes pas autorisé à accéder à cet élément
`404`| not found| L'élément demandé n'existe pas ou n'est pas reconnu
`403`| xxx| Action impossible (1)
`409`| Conflict| l'identifiant indiqué existe déjà. L'identifiant est unique est ne peut être généré une deuxième fois
`504`| xxx| Temps de réponse dépasse le temps de réponse maximal configuré par l’appelant (2)



(1) La plateforme Woop agissant comme passerelle à propager le(s) code(s) d’erreur retourné(s) par le(s) plateforme(s) transporteur. Les contraintes techniques et métier sont en cause (poid(s), taille(s), distance(s), temporelle(s)) 

(2) La plateforme Woop agissant comme passerelle à propager le temps de réponse de la plateforme des transporteurs. Le temps de traitement de la plateforme Woop s'additionne au temps de réponse des plateformes transporteur..

