<img width="724" height="700" alt="12-class-diagram-online-shopping" src="https://github.com/user-attachments/assets/464dc8ec-fcbe-4cf6-aaa5-cffbbcb0c3b0" />
Le diagramme UML présenté modélise le fonctionnement d’un système complet de commerce en ligne. Il décrit les principales entités du système, leurs attributs, ainsi que les relations qui existent entre elles. L’objectif est de représenter toutes les étapes du processus d’achat, depuis la connexion de l’utilisateur jusqu’à la création d’une commande et son paiement.

🔹 1. WebUser

La classe WebUser représente l’utilisateur qui accède à la plateforme en ligne.
Elle contient les informations nécessaires à l’authentification, telles que l’identifiant de connexion et le mot de passe.
Elle possède également un attribut state, basé sur l’énumération UserState (New, Active, Blocked, Banned), qui indique l’état du compte utilisateur.

Chaque WebUser peut être associé à un seul Customer et peut posséder éventuellement un ShoppingCart (0..1), représentant le panier en cours.

🔹 2. Customer

La classe Customer représente le client réel.
Elle contient les données personnelles : adresse, téléphone et email.
Un Customer est obligatoirement associé à un unique Account (1..1), qui gère ses opérations financières et commandes.

🔹 3. Account

La classe Account joue un rôle central dans le système.
Elle représente le compte commercial du client : adresse de facturation, date d’ouverture, date de fermeture et état (ouvert ou fermé).

Un Account peut être lié à :

0 ou 1 ShoppingCart (panier actif)

plusieurs Orders (1..*)

plusieurs Payments (1..*)

Cela reflète le fait qu’un client peut passer plusieurs commandes et effectuer plusieurs paiements.

🔹 4. ShoppingCart (Panier)

La classe ShoppingCart représente le panier actif d’un client.
Elle contient la date de création et regroupe les articles que le client souhaite acheter avant de passer la commande.

Un ShoppingCart contient :

plusieurs LineItem (lignes d’articles)

Il est associé :

à 1 WebUser (facultatif pour utilisateurs temporaires)

à 1 Account

🔹 5. Order (Commande)

La classe Order représente une commande validée par le client.
Elle contient des informations telles que :
numéro de commande, date, adresse de livraison, statut (OrderStatus) et total.

Une commande :

est liée à 1 Account

contient plusieurs LineItem

peut être associée à 0 ou plusieurs Payments

Les statuts possibles (OrderStatus) sont : New, Hold, Shipped, Delivered, Closed.

🔹 6. Payment (Paiement)

La classe Payment représente une transaction effectuée par le client.
Elle contient l’identifiant du paiement, la date, le montant payé et des détails éventuels.

Un Payment :

est obligatoirement lié à 1 Account

peut être associé à une ou plusieurs commandes, ou à aucune (par exemple un prépaiement).

🔹 7. LineItem (Ligne d’achat)

La classe LineItem représente une ligne d’article dans une commande ou un panier.
Elle contient la quantité et le prix unitaire.

Elle est utilisée dans deux cas :

dans le ShoppingCart (panier)

dans un Order (commande)

Chaque LineItem est lié à un seul Product.

🔹 8. Product (Produit)

La classe Product représente un produit proposé à la vente.
Elle contient un identifiant, un nom et un fournisseur.
Un produit peut apparaître dans plusieurs LineItem, dans différentes commandes ou paniers.

✅ Conclusion générale

Ce diagramme UML décrit de manière cohérente l’ensemble du processus d’achat dans une plateforme de commerce en ligne.
Il couvre tous les éléments essentiels : utilisateurs, clients, comptes, paniers, produits, commandes et paiements.
Les relations montrent clairement le flux logique :
WebUser → Customer → Account → ShoppingCart / Order → LineItem → Product → Payment
