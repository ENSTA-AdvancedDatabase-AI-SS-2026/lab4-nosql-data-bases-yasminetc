#  TP5 — Benchmark NoSQL

##  Contexte

Ce projet vise à comparer les performances de 4 bases NoSQL :
- Redis
- MongoDB
- Cassandra
- Neo4j

Objectif :
 Choisir la meilleure base selon le besoin métier

---

##  1. Benchmark Écriture

| Base       | Débit (ops/sec) | P50 | P95 | P99 |
|------------|----------------|-----|-----|-----|
| Redis      | Très élevé     | Très faible | Faible | Moyen |
| MongoDB    | Élevé          | Faible | Moyen | Moyen |
| Cassandra  | Très élevé     | Faible | Faible | Faible |
| Neo4j      | Moyen          | Moyen | Élevé | Élevé |

###  Analyse
- Redis et Cassandra dominent en écriture
- Neo4j plus lent (coût des relations)

---

##  2. Benchmark Lecture

###  Point Lookup
- Redis → ultra rapide
- Cassandra → rapide
- MongoDB → bon
- Neo4j → moyen

---

###  Range Query
- Cassandra → excellent
- MongoDB → bon
- Redis → limité
- Neo4j → peu adapté

---

###  Requêtes complexes
- Neo4j → excellent
- MongoDB → bon
- Cassandra → limité
- Redis → très limité

---

##  3. Test de charge concurrente

| Base       | Résistance charge |
|------------|------------------|
| Redis      | Très bonne       |
| Cassandra  | Excellente       |
| MongoDB    | Bonne            |
| Neo4j      | Moyenne          |

###  Observations
- Cassandra scale horizontalement très bien
- Redis dépend de la RAM
- Neo4j limité sur gros volumes

---

##  4. Goulots d’étranglement

- Redis → mémoire limitée
- MongoDB → index mal optimisés
- Cassandra → mauvais partition key
- Neo4j → traversals très profonds

---

##  5. Tableau de décision

| Critère            | Redis        | MongoDB     | Cassandra     | Neo4j        |
|--------------------|-------------|-------------|---------------|--------------|
| Débit écriture     | Très élevé  | Élevé       | Très élevé    | Moyen        |
| Débit lecture      | Très élevé  | Élevé       | Élevé         | Moyen        |
| Requêtes complexes | Faible      | Élevé       | Limité        | Très élevé   |
| Scalabilité        | Bonne       | Bonne       | Excellente    | Moyenne      |
| Use case           | Cache       | Documents   | IoT / Logs    | Graphe       |
---

##  6. Recommandation finale

###  Redis
 Idéal pour cache, sessions, temps réel

###  MongoDB
 Idéal pour applications web (flexibilité)

###  Cassandra
 Idéal pour IoT, logs, big data

###  Neo4j
 Idéal pour réseaux sociaux, recommandations

---

##  7. Conclusion

Chaque base NoSQL est optimisée pour un type de workload spécifique.

 Il n’existe pas de base universelle.

Le choix dépend :
- du type de données
- du volume
- des requêtes

