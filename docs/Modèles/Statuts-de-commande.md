# Statuts de commande

Au cours de son cycle de vie la commande passe tour à tour par plusieurs statuts.

### Parcours d'une commande


### Liste des statuts de livraison possible

Statut | Intitulé | Description
---------|----------|----------
 `ORDER_CREATED`|Commande enregistrée|La commande a bien été enregistrée coté woop.
 `ORDER_UPDATED`|Commande modifiée|La commande a été modifiée.
 `ORDER_TO_BE_QUOTED`|En attente de devis|La demande de devis a été envoyée aux transporteurs.
 `ORDER_QUOTED`|Devis en cours d'analyse|Les devis reçus sont en cours d'analyse par le système d'orchestration. 
 `ORDER_QUOTE_TO_BE_CONFIRMED`|En attente de confirmation|Le devis en attente de confirmation de la part des transporteurs. 
 `ORDER_TO_BE_SENT_TO_CARRIER`|Livraison à confirmer|Le devis est sélectionné et est en attente d'un identifiant de livraison.
 `ORDER_TO_DELIVER`|Commande à livrer|La commande est prête à être livrer par le transporteur retenu.
 `ORDER_BEING_DELIVERED`|Livraison en cours|Livraison de la commande en cours. 
 `ORDER_DELIVERED`|Commande livrée|La commande a bien été livrée.
 `ORDER_WITH_NO_CARRIER_ELIGIBLE`|Aucun transporteur|Aucun transporteur retenu lors de l'orchestration.
 `ORDER_WITH_NO_CARRIER_AVAILABLE`|Transporteurs indisponibles|Aucun transporteur disponnible pour les devis envoyés. Toutes les réponses sont négatives. 
 `ORDER_WITH_NO_QUOTE`|Aucun devis|Aucun devis reçu de la part des transporteurs sollicités.
 `ORDER_DELIVERY_UNCOMPLETED`|Livraison non finalisée|Livraison en cours n'est pas finalisée. 
 `ORDER_TO_BE_COMPLETED`|Commande à compléter|Commande à compléter avec informations manquantes.
 `ORDER_CANCELLED`|Commande annulée|La commande a été annulée.
 `ORDER_REFUSED_DELIVERY`|Commande refusée|La commande a été refusée par les transporteurs. 
 
### Gestion des retours et des erreurs