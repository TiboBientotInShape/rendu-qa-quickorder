# Plan d'amélioration

## 1. Sécuriser les endpoints API (Priorité 1)
* **Amélioration :** Restreindre l'accès aux commandes via une vérification stricte du token utilisateur (corriger l'IDOR).
* **Justification :** Éviter toute fuite de données personnelles et se conformer au RGPD.

## 2. Protéger les mots de passe (Priorité 1)
* **Amélioration :** Créer des DTO (Data Transfer Objects) pour exclure le mot de passe de la réponse de l'endpoint `/users/me`.
* **Justification :** Empêcher le vol d'identifiants via l'interception de requêtes réseau.

## 3. Déplacer la validation financière côté serveur (Priorité 2)
* **Amélioration :** Le backend doit vérifier lui-même la validité des coupons et le respect du montant minimum avant de créer la commande en base.
* **Justification :** Les vérifications actuelles sont purement front-end et facilement contournables via les DevTools.

## 4. Gérer l'encodage des caractères (Priorité 3)
* **Amélioration :** Assainir (sanitize) les entrées du formulaire d'adresse pour supporter correctement les emojis ou les rejeter proprement avec une erreur 400.
* **Justification :** Éviter les crashs serveurs (500) non maîtrisés qui dégradent l'expérience utilisateur.

## 5. Améliorer la visibilité du champ Promo (Priorité 3)
* **Amélioration :** Afficher le champ "Code promotionnel" de façon plus évidente directement sous le sous-total du panier.
* **Justification :** Suite aux retours UX, les utilisateurs peinent à trouver l'emplacement pour utiliser leurs réductions.

## 6. Corriger le responsive design du Checkout (Priorité 4)
* **Amélioration :** Ajouter une marge inférieure dynamique (`margin-bottom`) sur les petits écrans au niveau du bouton de paiement.
* **Justification :** Rendre l'interface fluide et professionnelle pour les clients commandant depuis leur smartphone.