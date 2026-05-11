#  TP3 Cassandra — SmartGrid DZ

##  Contexte

Ce projet consiste à gérer des données IoT massives provenant de capteurs électriques.

Objectif :
- Ingestion rapide (10 000 mesures/min)
- Requêtes temps réel
- Gestion efficace des séries temporelles

---

##  1. Modélisation Cassandra

###  Principe clé
 "Model your queries, not your data"

---

###  Table mesures_par_capteur

✔ Partition Key : (capteur_id, date)  
✔ Clustering : timestamp DESC  

 Avantages :
- Évite hot partitions
- Accès rapide par capteur

---

###  Table alertes_par_wilaya

 Partition : wilaya + date  

 Permet :
- Requêtes rapides sur alertes quotidiennes

---

###  Table agregats_horaires

 Pré-calcul des données  

 Avantage :
- Dashboard rapide sans agrégation coûteuse

---

##  2. Risque de Hot Partition

Un mauvais choix de partition key peut :
- Concentrer trop de données sur un nœud
- Dégrader les performances

 Solution :
- Ajouter date dans la partition
- Distribuer les données

---

##  3. Pourquoi éviter ALLOW FILTERING

ALLOW FILTERING :
- Scanne toute la table
- Très lent
- Non scalable

 Solution :
- Créer une table adaptée à la requête

---

##  4. Stratégies de Compaction

###  TWCS (TimeWindowCompactionStrategy)
 Idéal pour séries temporelles  
 Supprime efficacement données expirées  

---

###  STCS (SizeTiered)
 Bon pour données générales  

---

###  LCS (Leveled)
 Lecture rapide  
 Écriture plus coûteuse  

---

##  5. Performance ingestion

Résultat :
- Insertion batch → amélioration significative
- Débit élevé (plusieurs milliers de mesures/sec)

---

##  6. TTL (Time To Live)

Utilisé pour :
- Supprimer automatiquement les données anciennes

| Donnée | TTL |
|--------|-----|
| Mesures | 90 jours |
| Alertes | 1 an |
| Agrégats | 5 ans |

---

##  7. Conclusion

Cassandra est parfaitement adapté aux systèmes IoT massifs.

Ce TP nous a permis de :
- Comprendre la modélisation orientée requêtes
- Optimiser l’ingestion de données
- Gérer efficacement les séries temporelles
- Utiliser les stratégies de compaction
   Cassandra permet une scalabilité horizontale idéale pour les systèmes temps réel.
