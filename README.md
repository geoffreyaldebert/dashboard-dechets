# Dashboard Dechets - Données SINOE

Le dashboard est disponible ici : https://dashboard-dechets.netlify.app/

## Données

Les données du dashboard ne se concentre que sur l'année 2017.

Les données utilisées pour construire ce dashboard sont les suivantes : 
- SINOE - Tonnage DMA par type de déchets et département - téléchargeable [ici](https://www.data.gouv.fr/fr/datasets/sinoe-r-tonnage-dma-par-type-de-dechet-et-departement/)
- SINOE - Performance de collecte OMA par type de déchet et par département - téléchargeable [ici](https://www.data.gouv.fr/fr/datasets/sinoe-r-performance-de-collecte-oma-par-type-de-dechet-et-par-departement/)
- SINOE - Tonnage déchèteries par type de déchet et département, téléchargeable [ici](https://www.data.gouv.fr/fr/datasets/sinoe-r-tonnage-decheteries-par-type-de-dechet-et-departement/)

Pour compléter les données, il a également été utilisé les données de population légales de 2009 à 2017 de l'INSEE :
- Année 2017, téléchargeable [ici](https://www.insee.fr/fr/statistiques/4265511)
- Les données ont été mis en forme et stockées dans le répertoire [notebooks/insee](https://github.com/geoffreyaldebert/dashboard-dechets/tree/master/notebooks/insee) de ce repo git

## Traitement

L'ensemble des traitements tient en un seul notebook python disponible sur ce repo git ici : [notebooks/sinoe-notebook.ipynb](https://github.com/geoffreyaldebert/dashboard-dechets/blob/master/notebooks/sinoe-notebook.ipynb)

### Etapes 

- Agrégation des trois fichiers sources (OMA, DMA et Déchets) en un seul tableau
- Sous-sélection du tableau sur les données 2017
- Elimination de certains types de déchets qui semblent redondants entre les trois sources de données : 
    - Données DMA '07A - Ordures ménageres résiduelles' (en effet les données OMA '08A - Ordures ménagères résiduelles' semblent être les mêmes) 
    - Données DMA '07B - Déblais et gravats' (en effet les données Déchets '02E - Déblais et gravats' semblent être les mêmes)
    - Données DMA '07C - Encombrants' (en effet les données Déchets '02D - Encombrants' semblent être les mêmes)
    - Données Déchets de type '02C - Déchets verts' (ces données semblent comprises dans les données DMA '07F - Dechets Verts et biodéchets')
- Ajout des données de populations légales INSEE au tableau
- Calcul d'un ratio TONNAGE/POPULATION*100 pour connaître le nombre de kg moyen par habitant pour chaque type de déchets
- génération de fichiers json : 
    - un fichier maille national
    - un fichier maille régional
    - un fichier maille départemental
- développement de l'application web qui se base sur les fichiers json
