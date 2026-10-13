# Rapport d'anomalies (Bug Reports)

## Bug 01 : Validation silencieuse des coupons expirés
* **Contexte :** Web UI, parcours client connecté.
* **Préconditions :** Avoir un article dans le panier, connaître un code expiré (ex: EXPIRED10).
* **Étapes :** 
  1. Se rendre dans le panier. 
  2. Saisir `EXPIRED10` dans le champ code promo. 
  3. Cliquer sur Appliquer.
* **Résultat attendu :** Un message d'erreur indique que le coupon est invalide ou périmé.
* **Résultat obtenu :** Le coupon s'applique avec succès et déduit le pourcentage du total.
* **Preuve :** Non requise.
* **Sévérité :** Majeure.
* **Priorité :** Haute.

## Bug 02 : Contournement du montant minimum de commande
* **Contexte :** Web UI, parcours client.
* **Préconditions :** Avoir un panier avec un sous-total inférieur au minimum requis (ex: 11.90€ pour un minimum de 20€).
* **Étapes :** 
  1. Aller sur la page Checkout. 
  2. Descendre jusqu'au bouton de confirmation. 
  3. Cliquer sur le bouton.
* **Résultat attendu :** Le bouton est désactivé ou l'action est bloquée par le serveur.
* **Résultat obtenu :** La commande est validée avec succès malgré le non-respect du minimum.
* **Preuve :** Non requise.
* **Sévérité :** Majeure.
* **Priorité :** Haute.

## Bug 03 : Faille IDOR sur l'historique des commandes API
* **Contexte :** API Swagger (`/orders/{id}`).
* **Préconditions :** Être authentifié avec la clé démo.
* **Étapes :** 
  1. Exécuter un GET sur `/api/orders/2` (ou un ID n'appartenant pas à l'utilisateur connecté).
* **Résultat attendu :** Erreur 403 Forbidden.
* **Résultat obtenu :** Renvoi du statut HTTP 200 avec les informations personnelles de la commande d'un autre client.
* **Preuve :** Non requise.
* **Sévérité :** Critique.
* **Priorité :** Urgente.

## Bug 04 : Mots de passe renvoyés en clair par l'API
* **Contexte :** API Swagger (`/users/me`).
* **Préconditions :** Être authentifié.
* **Étapes :** 
  1. Exécuter un GET sur `/api/users/me`.
* **Résultat attendu :** Le JSON de réponse contient les infos du profil en excluant le mot de passe.
* **Résultat obtenu :** Le mot de passe de l'utilisateur est lisible en clair dans le champ "password" du JSON.
* **Preuve :** Non requise.
* **Sévérité :** Critique.
* **Priorité :** Urgente.

## Bug 05 : Panier non vidé après déconnexion
* **Contexte :** Web UI, gestion des sessions.
* **Préconditions :** Avoir des articles dans le panier.
* **Étapes :** 
  1. Se déconnecter. 
  2. Se reconnecter avec un autre compte (ou naviguer en tant qu'invité).
* **Résultat attendu :** Le panier est vide pour la nouvelle session.
* **Résultat obtenu :** Les articles de la session précédente sont toujours présents dans le panier.
* **Preuve :** Non requise.
* **Sévérité :** Moyenne.
* **Priorité :** Moyenne.

## Bug 06 : Crash de l'application (500) avec des emojis dans l'adresse
* **Contexte :** Web UI, Checkout.
* **Préconditions :** Avoir un panier prêt à être payé.
* **Étapes :** 
  1. Dans le champ adresse de livraison, taper "12 rue de Paris 🏢". 
  2. Valider la commande.
* **Résultat attendu :** Commande validée ou rejetée proprement (erreur 400).
* **Résultat obtenu :** Crash serveur, renvoi d'une erreur HTTP 500 (Internal Server Error) dans la console.
* **Preuve :** Non requise.
* **Sévérité :** Majeure.
* **Priorité :** Moyenne.

## Bug 07 : Cumul abusif des codes promotionnels
* **Contexte :** Web UI, panier.
* **Préconditions :** Avoir un panier bien rempli, connaître deux codes promos.
* **Étapes :** 
  1. Entrer un premier code et l'appliquer. 
  2. Entrer un deuxième code et l'appliquer.
* **Résultat attendu :** Le deuxième code remplace le premier, ou un message indique que les codes ne sont pas cumulables.
* **Résultat obtenu :** Les réductions s'additionnent de manière illimitée sur le total.
* **Preuve :** Non requise.
* **Sévérité :** Majeure.
* **Priorité :** Haute.

## Bug 08 : Chevauchement UI du bouton de paiement sur mobile
* **Contexte :** Web UI, simulation mobile (DevTools).
* **Préconditions :** Être sur la page de Checkout avec une largeur d'écran < 400px.
* **Étapes :** 
  1. Ouvrir DevTools et passer en vue iPhone 12. 
  2. Scroller en bas du checkout.
* **Résultat attendu :** Le bouton de validation est bien espacé du reste du texte.
* **Résultat obtenu :** Le bouton chevauche les conditions générales ou le pied de page, rendant le clic difficile.
* **Preuve :** Non requise.
* **Sévérité :** Mineure.
* **Priorité :** Basse.