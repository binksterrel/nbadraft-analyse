# Analyse NBA : Le Rang de Draft Prédit-il le Succès ?

Ce dépôt contient l'analyse complète d'un jeu de données de joueurs NBA (`players.csv`).

L'objectif était de déterminer la corrélation entre le rang de draft et la performance en carrière. L'analyse a révélé que cette corrélation est **24 fois plus forte dans l'ère moderne (R² = 22%)** que sur l'historique complet (R² = 0.9%).

**Compétences démontrées :** `Tableau Public`, `Analyse de Données`, `Nettoyage de Données (Data Cleaning)`, `EDA (Exploratory Data Analysis)`, `Data Visualization`, `Analyse de Régression`, `REGEX`

---

## 🎯 Problématique

L'objectif initial de ce projet était de répondre à une question simple : **"Est-ce que les joueurs draftés haut (ex: choix 1, 2, 3) ont de meilleures carrières (en points) que les joueurs draftés plus bas ?"**

Dans un jeu de données logique, on s'attendrait à une corrélation négative forte (un choix n°1 devrait avoir plus de points qu'un choix n°30). Ce projet audite cette hypothèse.

---

## 🕵️ Méthodologie et Découvertes Clés

Mon analyse s'est déroulée en trois étapes critiques, menées entièrement dans Tableau Public.

### 1. Nettoyage de Données Complexes (Data Cleaning)
Les données brutes étaient inutilisables. Une étape de préparation intensive a été nécessaire pour parser et convertir les données textuelles en mesures numériques exploitables via les **Champs Calculés** de Tableau :

* **Taille (`height`) :** Conversion du format texte (ex: "6-10") en une valeur numérique en centimètres (via les fonctions `SPLIT` et `INT`).
* **Poids (`weight`) :** Conversion du format texte (ex: "240lb") en valeur numérique (via la fonction `REPLACE`).
* **Rang de Draft (`draft_pick`) :** Extraction du numéro de draft (ex: "25" depuis "25th overall") en utilisant la fonction `REGEXP_EXTRACT` (Expressions Régulières).
* **Données manquantes :** Nettoyage des colonnes statistiques (ex: `career_FG3%`) qui contenaient des `"-"` non numériques (via une logique `IF-THEN-ELSE`).

### 2. Analyse Initiale (Corrélation Faible - 1968-2018)
Une première analyse de régression linéaire sur l'ensemble du jeu de données a révélé un paradoxe :

* **P-valeur :** `< 0.0001` (La relation est **statistiquement significative** et n'est pas due au hasard).
* **R-carré :** `0.009` (La relation est **extrêmement faible**).

Cette première passe concluait que le rang de draft n'expliquait que **0.9%** des performances en carrière.

### 3. Découverte par Affinement (Ère Moderne - 1985-2018)
L'hypothèse a été émise que les données anciennes (pré-1985, une ère très différente de la NBA) faussaient le modèle.

En appliquant un **filtre** pour n'étudier que l'"ère moderne" (1985-2018), la véritable corrélation a été découverte :

* **P-valeur :** `< 0.0001` (Toujours significative).
* **R-carré :** `0.22` (La relation est **24 fois plus forte**).

---

## 🏁 Conclusion

Ce projet n'est pas une simple analyse de corrélation, mais une démonstration de l'importance de **l'affinage et de la segmentation**.

J'ai prouvé que le rang de draft **EST** un prédicteur de performance modérément fort, mais **uniquement si l'on se concentre sur l'ère moderne**, où il explique **22%** de la variation des points en carrière.

Ce projet démontre ma capacité à ne pas m'arrêter à un premier résultat, à remettre en question les données et à utiliser les outils d'analyse pour trouver la véritable histoire cachée.

---

## 🚀 Comment l'exécuter

Ce projet est un dashboard interactif conçu pour être visualisé en ligne.

**Fichiers dans ce dépôt :**
* `players.csv` : Le jeu de données brutes utilisé pour l'analyse.
* `README.md` : Cette documentation.

**Visualisation :**
Le dashboard final, qui inclut l'histogramme des tailles et le nuage de points filtré, est publié sur Tableau Public.

### [➡️ Voir le Dashboard Interactif en Ligne]([COLLEZ VOTRE LIEN TABLEAU PUBLIC ICI])
