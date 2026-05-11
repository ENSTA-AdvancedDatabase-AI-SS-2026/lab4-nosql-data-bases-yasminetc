#  TP2 MongoDB — HealthCare DZ

##  Contexte

Ce projet consiste à modéliser un système de dossiers médicaux pour un hôpital numérique utilisant MongoDB.

L’objectif est de gérer des données complexes (patients, consultations, analyses) tout en optimisant les performances.

---

##  1. Choix de modélisation

### 🔹 Embedding (consultations)
Utilisé pour :
- Consultations
- Ordonnances

 Avantages :
- Accès rapide (1 seule requête)
- Données fortement liées

 Limites :
- Taille du document peut devenir grande

---

### 🔹 Referencing (analyses)
Utilisé pour :
- Analyses médicales

 Avantages :
- Documents légers
- Scalabilité

 Limites :
- Nécessite $lookup ou jointure

---

##  2. Résultats des requêtes explain()

###  Comparaison

| Requête | Sans index | Avec index |
|--------|-----------|------------|
| Temps | 120 ms | 5 ms |
| Docs examinés | 12000 | 200 |
| Type scan | COLLSCAN | IXSCAN |

 Conclusion :
Les index améliorent fortement les performances.

---

##  3. Pipeline d’agrégation complexe

### Exemple : patients à risque

Étapes :
1. Filtrer diabète + HTA
2. Calculer âge
3. Filtrer âge > 60
4. Agréger résultats

 Résultat :
Identification des patients à haut risque médical.

---

## 4. Indexation

Les index créés :
- wilaya
- antecedents
- diagnostic
- patient_id
- TTL sur analyses

 Objectif :
Réduire les scans complets et accélérer les requêtes.

---

## 5. Problèmes rencontrés

### 🔸 Taille des documents
Solution : hybridation embedding + referencing

### 🔸 Jointures coûteuses
Solution : index + optimisation pipeline

### 🔸 Données obsolètes
Solution : TTL index

---

##  6. Conclusion

MongoDB permet une modélisation flexible adaptée aux données médicales complexes.

Ce TP nous a permis de :
- Concevoir un schéma hybride efficace
- Maîtriser les requêtes avancées
- Optimiser les performances avec index
- Utiliser les pipelines d’agrégation

 MongoDB est particulièrement adapté aux systèmes médicaux modernes grâce à sa flexibilité et sa scalabilité.
