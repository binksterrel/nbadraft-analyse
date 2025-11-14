# Compte Rendu de Projet : Analyse de la Performance des Joueurs NBA

**Auteur:** Terrel NUENTSA
**Date:** 14 novembre 2025
**Outils:** Tableau 

---

## 1. Objectif du Projet

L'objectif de cette analyse était de déterminer si le rang de draft d'un joueur NBA est un prédicteur fiable de sa performance en carrière, mesurée par le total de points marqués (`career_PTS`).

Le projet a couvert l'intégralité du cycle de vie de l'analyse de données : la définition d'un outil de travail (Tableau), le nettoyage de données brutes, l'exploration (EDA), la modélisation statistique et l'interprétation finale.

---

## 2. Dataset

* **Source :** `players.csv`
* **Contenu :** Données biographiques et statistiques de 4 685 joueurs NBA.
* **Période (brute) :** 1968 - 2018 (pour les années de draft).

---

## 3. Méthodologie d'Analyse

Le projet a suivi une méthodologie rigoureuse en plusieurs étapes, directement dans Tableau Public.

### 3.1. Nettoyage et Préparation des Données (Data Cleaning)

Cette étape a été cruciale car les données brutes n'étaient pas exploitables. Plusieurs transformations ont été effectuées à l'aide de **Champs Calculés** :

* **Taille (`height`) :** Conversion du format texte ("6-10") en une valeur numérique en centimètres (`Taille (cm)`) en utilisant les fonctions `SPLIT` et `INT`.
* **Poids (`weight`) :** Conversion du format texte ("240lb") en valeur numérique (`Poids (Num)`) en utilisant la fonction `REPLACE`.
* **Rang de Draft (`draft_pick`) :** Extraction du numéro de draft (ex: "25" à partir de "25th overall") en utilisant la fonction `REGEXP_EXTRACT` (Expressions Régulières).
* **Dates (`birthDate`, `draft_year`) :** Conversion des champs de texte en formats "Date" et "Nombre (entier)" pour permettre les calculs.
* **Données manquantes :** Nettoyage des statistiques (ex: `career_FG3%`) qui contenaient des `"-"`. Une logique `IF-THEN-ELSE` a été utilisée pour les convertir en `NULL` et transformer la colonne en type `FLOAT` (nombre décimal).
* **Création de variable :** Création de la variable `Âge au Draft` via la formule `[draft_year] - YEAR([birthDate])` pour une analyse contextuelle.

### 3.2. Analyse Exploratoire (EDA)

Pour valider la qualité des données nettoyées, un **histogramme** de la `Taille (cm)` a été créé. Celui-ci a révélé une distribution normale (une "courbe en cloche"), confirmant l'absence d'anomalies ou d'outliers majeurs dans les données de taille.

### 3.3. Analyse Principale (Modélisation)

Pour répondre à l'objectif, la relation entre le rang de draft et la performance a été modélisée :

1.  **Création d'un Nuage de Points :** La relation entre le `Draft Pick (Num)` (Axe X) et les `career_PTS` (Axe Y) a été visualisée.
2.  **Désagrégation :** L'option "Agréger les mesures" a été désactivée pour que chaque point représente un joueur individuel, et non la somme de tous.
3.  **Ajout d'une Ligne de Tendance (Régression Linéaire) :** Une ligne de tendance a été appliquée pour modéliser mathématiquement la relation.

---

## 4. Résultats et Découverte Majeure

L'analyse a révélé une découverte cruciale qui n'était pas apparente au premier abord.

* **Analyse Initiale (1968-2018) :** L'analyse sur *l'ensemble* des données montrait une relation **statistiquement significative** (`P-valeur < 0.0001`) mais **extrêmement faible** (`R-carré = 0.009`). Le rang de draft n'expliquait que **0.9%** de la performance.

* **Hypothèse et Affinement :** L'hypothèse a été émise que les données d'avant 1985 "polluaient" le modèle. Un **filtre** a été appliqué pour n'analyser que les joueurs draftés **entre 1985 et 2018** (l'ère moderne).

* **Résultat Final (1985-2018) :**
    * **P-valeur :** `< 0.0001` (La relation est toujours statistiquement réelle).
    * **R-carré :** `0.22` (La relation est **24 fois plus forte**).

---

## 5. Conclusion

La conclusion de cette analyse est que le rang de draft est un **prédicteur de performance modérément fort dans la NBA moderne**.

En filtrant les données pour se concentrer sur l'ère 1985-2018, nous avons démontré que le rang de draft **explique 22%** de la variation des points marqués en carrière.

Cette analyse prouve l'importance de ne pas se fier à une première analyse globale et de savoir **segmenter et filtrer les données** pour découvrir des tendances contextuelles plus profondes et plus précises.
