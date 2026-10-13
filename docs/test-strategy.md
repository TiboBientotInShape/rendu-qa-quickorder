# Stratégie de test - QuickOrder

## 1. Périmètre (In Scope)
* Interface web utilisateur (Navigation, Ajout au panier, Checkout, Inscription/Connexion).
* API REST backend (Endpoints exposés via Swagger sur le port 5000).
* Logique métier (Application des réductions, montants minimums, calcul du total).

## 2. Hors périmètre (Out of Scope)
* Tests de charge et de performance (stress test).
* Intégration avec des passerelles bancaires réelles.
* Audit de sécurité de l'infrastructure (Pen-testing serveur).

## 3. Parcours critiques
1. Création de compte et Authentification sécurisée.
2. Ajout d'articles au panier et maintien de l'état de la session.
3. Validation de la commande (Checkout) avec calcul exact de la facturation.
4. Accès sécurisé aux données via l'API (authentification par clé).

## 4. Risques principaux
* **Financier :** Faille dans le calcul du panier ou utilisation de codes promos invalides.
* **Sécurité :** Fuite de données personnelles (RGPD) via l'API ou mots de passe non protégés.
* **Blocage :** Impossibilité pour un utilisateur de finaliser sa commande (perte de chiffre d'affaires).

## 5. Types de tests
* Tests fonctionnels manuels (UI).
* Tests API (via Swagger).
* Tests aux limites (quantités extrêmes, longueurs de champs).
* Tests d'erreurs (injections, mauvais formats).
* Tests de règles métier (horaires, minimum de commande).

## 6. Priorisation (Risque × Impact)
Priorité absolue accordée aux parcours de paiement et à la sécurité de l'API. Les bugs d'affichage esthétique ou les fonctionnalités secondaires (comme l'édition du profil) sont classés en priorité basse.