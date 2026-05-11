#  TP4 Neo4j — UniConnect DZ

##  Contexte

Ce projet consiste à modéliser un réseau social universitaire avec Neo4j.

Objectif :
- Représenter les relations entre étudiants
- Optimiser les requêtes de graphe
- Implémenter des recommandations

---

##  1. Modélisation du graphe

###  Nœuds
- Etudiant
- Cours
- Club
- Entreprise
- Competence

### 🔹 Relations
- CONNAIT
- SUIT
- MEMBRE_DE
- MAITRISE
- A_STAGE_CHEZ

 Avantage :
- Représentation naturelle des relations complexes

---

##  2. Requêtes principales

###  Amis d’amis
- Simple avec Cypher (2 hops)
- Très complexe en SQL (JOIN multiples)

---

###  Profil complet
- Récupération en une seule requête
- Très lisible

---

##  3. Algorithmes de graphe

###  Shortest Path
Permet de trouver le chemin le plus court entre deux étudiants.

---

###  Centralité
Identifie les étudiants les plus connectés.

---

###  Louvain (communautés)
Permet de détecter :
- Groupes d’étudiants
- Cercles sociaux

---

##  4. Résultats communautés

Les communautés détectées correspondent généralement :
- Aux universités
- Aux filières
- Aux clubs

 Conclusion :
Les étudiants ayant les mêmes intérêts sont regroupés automatiquement.

---

##  5. Comparaison SQL vs Cypher

| Requête | SQL | Cypher |
|--------|-----|--------|
| Amis | JOIN | 1 hop |
| Amis d’amis | 2 JOINs | 2 hops |
| Chemin | complexe | shortestPath() |

 Conclusion :
Cypher est plus lisible et performant pour les graphes.

---

##  6. Conclusion

Neo4j est idéal pour les réseaux sociaux et systèmes relationnels complexes.

Ce TP nous a permis de :
- Modéliser un graphe de données
- Utiliser Cypher efficacement
- Implémenter des algorithmes avancés
- Comprendre les avantages des bases graphe

 Neo4j simplifie fortement les requêtes relationnelles complexes.
