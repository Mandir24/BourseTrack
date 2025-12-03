# 📈 BourseTrack : Suivi et Analyse des Données Financières et Actualités du Marché

Ce projet a été développé dans le cadre de la **SAÉ 3.VCOD.01 : Collecte automatisée de données web** et vise à créer une plateforme simple pour suivre les performances financières des grandes entreprises sur les **100 derniers jours ouvrés**.

BourseTrack automatise l'extraction, le traitement et le reporting des données financières, en enrichissant l'analyse avec la contextualisation des actualités pertinentes.

***

## ✨ Fonctionnalités Clés
* **Collecte de Données** : Récupération des données boursières et des 10 dernières actualités par entreprise via des APIs externes.
* **Pipeline de Données Robuste** : Utilisation d'un processus structuré de sauvegarde **CSV** et d'intégration **SQLite** pour gérer les limitations de requêtes API.
* **Calcul d'Indicateurs** : Détermination des performances via des requêtes SQL pour obtenir la Volatilité, le Rendement, la Tendance Globale, etc.
* **Génération de Rapport** : Production d'une page **HTML dynamique** présentant les résultats sous forme de tableaux et de graphiques.
* **Filtrage Intelligent des Actualités** : Affichage des actualités uniquement pour les entreprises présentant une **tendance globale significative** ($\ge 0.15$ ou $\le -0.15$).

***

## 🛠️ Stack Technique & Architecture
Le projet repose sur l'approche **orientée objet en Python** et suit une méthodologie rigoureuse pour l'acquisition et la persistance des données.

### APIs Utilisées
| Type de Donnée | API | Rôle |
| :--- | :--- | :--- |
| **Données Financières** | **Alpha Vantage** | Obtention des prix (ouverture, clôture, haut, bas) et du volume des actions. |
| **Actualités** | **News API** | Collecte des actualités pertinentes pour le marché financier. |

### Pipeline de Traitement
1.  **Extraction** : Le script utilise la classe `GestionnaireAPI` pour interroger les services.
2.  **Sauvegarde CSV (Caching)** : Pour respecter les limites de requêtes, les données sont stockées localement dans des fichiers CSV distincts (e.g., `TSLA_financial.csv` et `TSLA_news.csv`).
3.  **Nettoyage et Stockage** : Les données sont traitées puis insérées dans une base de données **SQLite**, structurée selon un **Modèle Relationnel de Données (MLD)** (tables `ENTREPRISE`, `FINANCIER`, et `ACTUALITE`).
4.  **Analyse** : Les indicateurs finaux sont calculés à l'aide de requêtes SQL exécutées par la classe `GestionnaireBDD`.

***

## 📊 Indicateurs Analysés
Le rapport final synthétise les performances sur les 100 jours ouvrés autour des indicateurs suivants:

| Indicateur | Objectif |
| :--- | :--- |
| **Tendance Globale** | Différence (Prix Clôture Moyen - Prix Ouverture Moyen). Indique une pression d'achat ou de vente. |
| **Volatilité Moyenne** | Moyenne des écarts (Plus Haut - Plus Bas), indiquant le niveau de risque ou d'instabilité. |
| **Volume Moyen** | Reflète l'intérêt des investisseurs pour l'action et sa liquidité. |
| **Rendement Moyen Journalier** | Moyenne des variations journalières en pourcentage, utilisée pour la comparaison relative. |

### Visualisation
* **Graphique Circulaire (Pie Chart)** : Représente la répartition du **Volume total des échanges** par entreprise, généré à l'aide de Matplotlib et Seaborn. 
* **Tableau HTML Stylisé** : Les tendances positives et négatives sont mises en évidence par des couleurs CSS.

***
