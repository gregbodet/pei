![GeoCompiegnois](img/Logo_web-GeoCompiegnois.png)

# Documentation technique de l'application PEI

* Statut
  - [x] à rédiger
  - [ ] relecture
  - [ ] finaliser
  - [ ] révision
  
* Historique des versions

|Date | Auteur | Description
|:---|:---|:---|
|29/03/2018|Florent VANHOUTTE|version initiale|

## Data

### Champs calculés

-- etiquette

    CASE WHEN {type_pei}=NR THEN NULL ELSEE {type_pei} END

-- texte brut

-- disponible_false

    http://geo.compiegnois.fr/documents/metiers/deci/cc_nonconforme.png

-- type image

-- disponible_true

    http://geo.compiegnois.fr/documents/metiers/deci/cc_conforme.png

-- type image

-- disponible_img

    CASE WHEN {disponible} = 't' THEN {disponible_true} 
    WHEN {disponible} = 'f' THEN {disponible_false} END


-- style

-- V2 : par disponibilité

    CASE
    -- pei statut non renseigné
    WHEN {statut}='00' THEN 'Snr'
    -- pei statut privé
    WHEN {statut}='02' AND {etat_pei} IN ('00','01',02') THEN 'aaa'
    -- pei statut privé
    WHEN {statut}='02' AND {etat_pei}='03' THEN 'bbb'
    -- pei statut public et état projet ou non renseigné
    WHEN {statut}='01' AND {etat_pei} IN ('00','01') THEN 'ccc'
    -- pei statut public supprimé
    WHEN {statut}='01' AND {etat_pei}='03' THEN 'ddd'
    -- pei statut public existant et dispo non renseignée
    WHEN {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'eee'
    -- pei statut public existant et conforme
    WHEN {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'fff'
    -- pei statut public existant et non conforme
    WHEN {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'ggg' 
    END

-- V1 : détaillée par type_pei

    CASE
    -- PEI statut privé
    WHEN {type_pei}='PI' AND {statut}='02' THEN 'PI-blanc'
    WHEN {type_pei}='BI' AND {statut}='02' THEN 'BI-blanc'
    WHEN {type_pei}='CI' AND {statut}='02' THEN 'CI-blanc'
    WHEN {type_pei}='PA' AND {statut}='02' THEN 'PA-blanc'
    WHEN {type_pei}='NR' AND {statut}='02' THEN 'NR-blanc'
    -- PEI statut non renseigné
    WHEN {type_pei}='PI' AND {statut}='00' THEN 'PI-gris'
    WHEN {type_pei}='BI' AND {statut}='00' THEN 'BI-gris'
    WHEN {type_pei}='CI' AND {statut}='00' THEN 'CI-gris'
    WHEN {type_pei}='PA' AND {statut}='00' THEN 'PA-gris'
    WHEN {type_pei}='NR' AND {statut}='00' THEN 'NR-gris'
    -- PEI statut public projet ou supprimé
    WHEN {type_pei}='PI' AND {statut}='01' AND {etat_pei} IN ('00','01','03') THEN 'PI-gris'
    WHEN {type_pei}='BI' AND {statut}='01' AND {etat_pei} IN ('00','01','03') THEN 'BI-gris'
    WHEN {type_pei}='CI' AND {statut}='01' AND {etat_pei} IN ('00','01','03') THEN 'CI-gris'
    WHEN {type_pei}='PA' AND {statut}='01' AND {etat_pei} IN ('00','01','03') THEN 'PA-gris'
    WHEN {type_pei}='NR' AND {statut}='01' AND {etat_pei} IN ('00','01','03') THEN 'NR-gris'
    -- PEI statut public existant et conforme
    WHEN {type_pei}='PI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'PI-vert'
    WHEN {type_pei}='BI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'BI-vert'
    WHEN {type_pei}='CI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'CI-vert'
    WHEN {type_pei}='PA' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'PA-vert'
    WHEN {type_pei}='NR' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='t' THEN 'NR-vert'
    -- PEI statut public existant et non conforme
    WHEN {type_pei}='PI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'PI-rouge'
    WHEN {type_pei}='BI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'BI-rouge'
    WHEN {type_pei}='CI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'CI-rouge'
    WHEN {type_pei}='PA' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'PA-rouge'
    WHEN {type_pei}='NR' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='f' THEN 'NR-rouge'
    -- PEI statut public existant et conformité non renseignée
    WHEN {type_pei}='PI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'PI-gris'
    WHEN {type_pei}='BI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'BI-gris'
    WHEN {type_pei}='CI' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'CI-gris'
    WHEN {type_pei}='PA' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'PA-gris'
    WHEN {type_pei}='NR' AND {statut}='01' AND {etat_pei}='02' AND {disponible}='0' THEN 'NR-gris'
    END


## Fonctionnel

## Cartothèque

## Application
