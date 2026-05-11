#  TP1 Redis : Système de Cache E-commerce

## Projet : ShopFast — Plateforme E-commerce Algérienne

---

## 1. Introduction

Dans ce TP, nous avons implémenté une couche de cache basée sur **Redis** afin d’améliorer les performances d’une plateforme e-commerce (ShopFast).

L’objectif principal est de :
- Réduire la charge sur la base de données
- Accélérer les temps de réponse
- Améliorer l’expérience utilisateur

Nous avons utilisé différentes structures Redis et le pattern **Cache-Aside**, ainsi que la gestion des sessions et un système de classement en temps réel.

---

##  2. Structures de données utilisées

###  Hash
Utilisé pour représenter les produits et le panier utilisateur.

✔ Avantages :
- Accès rapide aux champs d’un objet
- Idéal pour les entités structurées

---

###  List
Utilisée pour l’historique de navigation utilisateur.

✔ Avantages :
- Données ordonnées
- Historique facile à gérer (LPUSH / LRANGE)

---

###  Set
Utilisé pour les catégories de produits.

✔ Avantages :
- Évite les doublons
- Permet des opérations ensemblistes

---

###  Sorted Set
Utilisé pour le classement des ventes.

✔ Avantages :
- Tri automatique par score
- Parfait pour leaderboard

---

##  3. Cache-Aside Pattern

###  Principe

1. Vérifier dans Redis
2. Si HIT → retourner la donnée
3. Si MISS → requête DB + stockage dans Redis + retour

---

###  Schéma logique

Client → Redis ?  
  ├── HIT → retour immédiat  
  └── MISS → DB → stockage Redis → retour

---

##  4. Résultats de performance

| Métrique        | Sans Cache | Avec Redis |
|----------------|-----------|------------|
| Temps moyen     | 3200 ms   | 120 ms     |
| Charge DB       | Élevée    | Faible     |
| Performance     | Lente     | Très rapide |

---

###  Cache Hit / Miss

- Cache HIT → réponse instantanée
- Cache MISS → accès DB + mise en cache

✔ Plus le taux de HIT est élevé, meilleures sont les performances

---

##  5. Gestion des sessions

Les sessions utilisateur sont stockées dans Redis avec un TTL de 30 minutes.

### ✔ Fonctionnalités :
- Création de session
- Renouvellement automatique (sliding expiration)
- Suppression de session

###  Avantages :
- Sessions rapides et centralisées
- Expérience utilisateur améliorée

---

##  6. Leaderboard (Classement des ventes)

Implémenté avec **Sorted Set Redis**.

### ✔ Fonctionnalités :
- Incrément des ventes
- Classement global
- Top produits

###  Avantages :
- Mise à jour en temps réel
- Très performant (O(log N))

---

##  7. Pipeline & Transactions

###  Pipeline
Permet d’exécuter plusieurs commandes Redis en batch.

✔ Avantages :
- Réduction des appels réseau
- Gain de performance

---

###  Transactions (MULTI/EXEC)

✔ Avantages :
- Atomicité des opérations
- Protection contre les conflits concurrents

---

##  8. Problèmes rencontrés

###  Redis redémarrage
- Perte des données mémoire
- Solution : RDB / AOF persistence

---

###  Cohérence cache / DB
- Données parfois obsolètes
- Solutions :
  - Invalidation du cache
  - TTL adapté
  - Write-through strategy

---

###  TTL trop court
- Augmente les cache misses
- Charge la base de données

---

##  9. Conclusion

Ce TP nous a permis de comprendre l’importance de Redis dans une architecture e-commerce moderne.

Nous avons appris à :
- Utiliser les structures Redis efficacement
- Implémenter un cache performant (Cache-Aside)
- Gérer les sessions utilisateurs
- Construire un leaderboard temps réel
- Optimiser les performances avec pipeline et transactions

 Redis permet une amélioration significative des performances et de la scalabilité des systèmes web.


