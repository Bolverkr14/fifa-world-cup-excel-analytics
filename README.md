# FIFA World Cup Analytics

## Excel Business Intelligence Project

Ce projet analyse les données historiques de la Coupe du monde de football de 1930 à 2026 avec Microsoft Excel.

L’objectif est de démontrer une démarche complète d’analyse de données, depuis le contrôle des données brutes jusqu’à la conception d’un tableau de bord interactif et d’un modèle indicatif de comparaison entre deux équipes.

![image of the dashboard overview](https://github.com/Bolverkr14/fifa-world-cup-excel-analytics/blob/main/images/dashboard-overview.png)

## Contexte

Les données historiques de la Coupe du monde permettent d’étudier l’évolution de la compétition, les performances des équipes nationales et les tendances liées aux buts, aux victoires et aux parcours en phase finale.

Ce projet a été conçu comme un cas pratique de Business Intelligence destiné à répondre à plusieurs questions :

- Quelles équipes ont obtenu les meilleures performances historiques ?
- Quelles équipes présentent les meilleurs profils offensifs et défensifs ?
- Comment le nombre de buts par match a-t-il évolué ?
- Quelles équipes ont remporté le plus de titres ?
- Quelles nations participent le plus régulièrement à la compétition ?
- Comment comparer deux équipes à partir de leurs performances historiques ?
- Quelle issue est suggérée par leurs statistiques et leur forme récente ?

## Objectifs du projet

Le projet vise à mettre en pratique les différentes étapes d’un workflow d’analyse de données :

1. comprendre la structure des données sources ;
2. identifier les problèmes de qualité ;
3. nettoyer et standardiser les données ;
4. construire des indicateurs de performance ;
5. analyser les résultats historiques ;
6. créer un dashboard interactif ;
7. documenter les calculs et les limites ;
8. proposer un modèle indicatif de probabilité de match.

## Données utilisées

Le projet s’appuie sur plusieurs jeux de données consacrés à la Coupe du monde :

- résultats des matchs de 1930 à 2026 ;
- séances de tirs au but ;
- sélections nationales de 2026 ;
- résumés statistiques des équipes de 2026.

Les principales variables utilisées sont :

- année de l’édition ;
- date du match ;
- phase de la compétition ;
- équipe à domicile ;
- équipe à l’extérieur ;
- buts marqués ;
- conditions de victoire ;
- pays ;

## Méthodologie

Le projet suit la chaîne de traitement suivante :

`Données brutes → Contrôle qualité → Nettoyage → Calculs → KPI → Synthèse → Dashboard`

### 1. Contrôle des données

Les contrôles réalisés portent notamment sur :

- les doublons ;
- les valeurs manquantes ;
- les noms de pays ;
- les caractères spéciaux ;
- les formats numériques ;
- les phases de la compétition ;
- la cohérence des scores ;
- les vainqueurs ;
- le nombre de matchs par édition.

### 2. Nettoyage

Les principales transformations incluent :

- suppression des doublons identifiés ;
- correction des erreurs d’encodage ;
- standardisation des noms de pays et d’équipes ;
- harmonisation des phases de compétition ;
- conversion des données numériques ;
- création de colonnes de contrôle ;
- préparation des données destinées aux analyses.

Exemples de normalisation :

- `USA` devient `United States` ;
- `Republic of Korea` devient `South Korea` ;
- `Cape Verde` devient `Cabo Verde` ;
- `DR Congo` devient `Democratic Republic of the Congo` ;
- `West Germany` devient `FR Germany`.

### 3. Construction des KPI

Les principaux indicateurs comprennent :

- nombre d’éditions ;
- nombre de matchs ;
- nombre d’équipes participantes ;
- nombre total de buts ;
- moyenne et médiane des buts par match ;
- victoires, matchs nuls et défaites ;
- taux de victoire ;
- buts marqués et encaissés ;
- différence de buts ;
- participations ;
- meilleure phase atteinte ;
- titres remportés ;
- scores offensif, défensif et global.

## Structure du classeur

Le fichier Excel est organisé en plusieurs feuilles :

| Feuille | Description |
|---|---|
| `README` | Présentation du projet et de ses objectifs |
| `DATA_DICTIONNAIRE` | Documentation des tables et des champs |
| `KPI_DICTIONNAIRE` | Définition des indicateurs et règles de calcul |
| `DATA_BRUT` | Données sources conservées sans transformation |
| `DATA_QUALITE` | Contrôles, anomalies et tables de correspondance |
| `DATA_CLEANED` | Données nettoyées et normalisées |
| `CALCULES` | Calculs intermédiaires et indicateurs par équipe |
| `RESUME` | Synthèse historique par édition |
| `DASHBOARD` | Visualisations, filtres et comparaison d’équipes |

## Dashboard

Le dashboard fournit plusieurs niveaux d’analyse :

### Vue d’ensemble

- nombre d’éditions ;
- nombre de matchs ;
- nombre de buts ;
- moyenne de buts par match ;
- nombre d’équipes participantes.

### Évolution de la compétition

- évolution du nombre de matchs ;
- évolution du nombre de buts ;
- moyenne de buts par édition ;
- évolution du nombre d’équipes.

### Performances historiques

- équipes les plus titrées ;
- taux de victoire ;
- parcours dans la compétition ;
- performances offensives et défensives.

### Fin des matchs

- matchs nuls ;
- prolongations ;
- tirs au but ;
- but en or.

### Classements

- meilleures équipes offensives ;
- meilleures équipes défensives ;
- score global de performance.

## Comparaison VERSUS

Le bloc `VERSUS` permet de sélectionner deux équipes et de comparer :

- leur meilleure phase atteinte ;
- leur nombre de participations ;
- leurs victoires, matchs nuls et défaites ;
- leurs buts marqués et encaissés ;
- leurs moyennes par match ;
- leur différence de buts ;
- leurs scores offensif, défensif et global ;
- leur forme lors des derniers matchs.

![image of the versus](https://github.com/Bolverkr14/fifa-world-cup-excel-analytics/blob/main/images/versus-model.png)

## Modèle indicatif de probabilité

Le modèle estime le nombre de buts attendus pour les deux équipes à partir de leurs performances historiques.

Le calcul repose notamment sur :

- les buts marqués par match ;
- les buts encaissés par match ;
- la force offensive ;
- la solidité défensive ;
- le volume de matchs disponible ;
- la forme récente ;
- un coefficient de fiabilité ;
- une distribution de Poisson.

Le modèle fournit :

- les buts attendus de chaque équipe ;
- la probabilité de victoire de l’équipe A ;
- la probabilité d’un match nul ;
- la probabilité de victoire de l’équipe B ;
- le score exact le plus probable ;
- un indice de confiance.

> Les probabilités produites sont uniquement indicatives. Ce modèle n’est pas un modèle professionnel de paris sportifs et ne garantit aucun résultat futur.

## Principaux enseignements

Le projet permet notamment de constater que :

- les performances historiques varient fortement selon les équipes et les périodes ;
- le nombre de matchs disponibles influence la fiabilité des comparaisons ;
- la moyenne et la médiane ne décrivent pas la performance de la même manière ;
- les scores offensifs et défensifs doivent être interprétés avec le volume de données ;
- le score exact le plus probable n’est pas nécessairement identique à l’issue globale la plus probable.

## Compétences mises en pratique

### Excel

- formules dynamiques ;
- tableaux structurés ;
- listes déroulantes ;
- tableaux croisés dynamiques ;
- graphiques croisés dynamiques ;
- mise en forme conditionnelle ;
- dashboard interactif.

### Fonctions utilisées

- `RECHERCHEX` ;
- `FILTRE` ;
- `UNIQUE` ;
- `TRIER` ;
- `LET` ;
- `SOMME.SI.ENS` ;
- `NB.SI.ENS` ;
- `SOMMEPROD` ;
- `INDEX` ;
- `EQUIV` ;
- fonctions statistiques ;
- loi de Poisson.

### Analyse de données

- exploration des données ;
- nettoyage ;
- contrôle qualité ;
- analyse descriptive ;
- création de KPI ;
- normalisation des indicateurs ;
- visualisation ;
- documentation ;
- communication de résultats.

## Limites

Les principales limites du projet sont :

- le nombre de matchs varie fortement entre les équipes ;
- certaines nations ont changé de nom ou de périmètre historique ;
- les statistiques historiques ne garantissent pas les performances futures ;
- le modèle ne prend pas en compte les blessures, les convocations ou les tactiques ;
- la localisation du match n’est pas intégrée ;
- la force des adversaires rencontrés n’est pas encore pondérée ;
- la loi de Poisson repose sur des hypothèses simplificatrices ;
- les données 2026 peuvent correspondre à des scénarios ou projections.

## Améliorations futures

Les prochaines étapes envisagées sont :

- reproduire la préparation des données avec Power Query ;
- interroger les données avec SQL ;
- reconstruire le dashboard dans Power BI ;
- créer des mesures DAX ;
- séparer les résultats historiques des scénarios 2026 ;
- ajuster les statistiques selon la force des adversaires ;
- intégrer l’avantage du terrain ;
- tester la qualité prédictive du modèle sur des matchs historiques ;
- explorer Microsoft Fabric.

## Fichiers du dépôt

- `workbook/FIFA_WORLD_CUP_ANALYTICS.xlsx` : classeur Excel principal ;
- `images/` : captures du dashboard ;
- `([documentation/data-dictionary.md](https://github.com/Bolverkr14/fifa-world-cup-excel-analytics/blob/main/documentation/data-dictionary.md)` : dictionnaire des données ;
- `documentation/kpi-dictionary.md` : dictionnaire des KPI ;
- `documentation/methodology.md` : méthode de traitement et limites.

## Ouvrir le projet

1. Télécharger le fichier Excel depuis le dossier `workbook`.
2. Ouvrir le fichier avec une version récente de Microsoft Excel.
3. Activer le contenu si Excel le demande.
4. Utiliser les listes déroulantes présentes dans le dashboard.
5. Sélectionner deux équipes dans la section `VERSUS`.

Une version récente de Microsoft Excel est recommandée, car le projet utilise des fonctions dynamiques telles que `FILTRE`, `UNIQUE`, `TRIER`, `LET` et `RECHERCHEX`.

## Auteur

**Yann Lecompte**

Projet réalisé dans le cadre de ma transition vers le métier de Data Analyst junior.

Mon parcours d’apprentissage :

`Excel → SQL → Power BI → Microsoft Fabric`
