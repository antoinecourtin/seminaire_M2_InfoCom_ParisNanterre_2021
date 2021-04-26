## Documents du jeux de données "Proveance"

> Lié au programme de recherche [**Répertoire des ventes d'antiques au XIXe**](https://www.inha.fr/fr/recherche/le-departement-des-etudes-et-de-la-recherche/domaines-de-recherche/histoire-de-l-art-antique-et-de-l-archeologie/repertoire-des-ventes-d-antiques.html)

### Composition du coprus téléchargé :

Ce fichier readme précise la structure des 3 fichiers présent dans le [répertoire suivant](datasetProvenance/), à savoir :
1. INHA_objets.csv : contient tous les objets
2. INHA_ventes.csv : contient pour chaque objets, toutes les ventes qui lui sont associées
3. INHA_acteurs.csv : contient une description a minima des acteurs en lien avec le fichier INHA_ventes.csv

Ces métadonnées sont placées sous licence Creative Commons 4.0. Dans ce cadre, l’utilisateur est autorisé : à reproduire et à rediffuser ces métadonnées, sous réserve de la mention exacte de la source (permalien de la notice Agorha) ; à retraiter, à inclure ou à exploiter ces contenus et métadonnées, sous réserve de ne pas en dénaturer le sens ni l’exactitude et de ne pas induire en erreur des tiers quant au contenu ou à la source de ces informations ; pour le monde entier et sans limitation de durée ; à des fins commerciales ou non.

Les données sont issues du dépouillement exhaustive de deux ventes : vente Magnoncour de 1839 + vente Caninno de 1837

#### Détails du fichier INHA_objets.csv

Nom_colonne | Description | Exemple
------------ | ------------- | -----
id_objet | identifiant unique de l'objet dans la base AGORHA | 136343
classement_objet | 1 ou 2. Si 1, on retrouve l'objet dans l'onglet "Découvrir une histoire"  | 1
description | texte de l'objet dans "Découvrir une histoire" | Cette amphore, destinée à l'origine [...]
texte_creation | texte de l'objet pour la 1er étape du parcours | Découvrez l’histoire de cette a [...]
texte_decouverte | texte de l'objet pour la 2ème étape du parcours |  Après sa découverte, le vase se retrouve dan
texte_ventes | texte de l'objet pour la 3ème étape du parcours | Les catalogues des ventes
texte_conservation | texte de l'objet pour la 4ème étape du parcours | Le vase est conservé au Musée
auteur_objet | nom de l'auteur (attribution) | Exékias
nom_objet | Intitulé (titre forgé) de l'objet | Amphore attique à figures noires et son couvercle
type_objet | Type de l'objet | vase plastique
categorie_picto | correspondance pour l'affichage du picto (simplification de type_objet | vase
matiere_filtre | matière de l'objet, utilisé dans les filtres pour l'exploration des objets | terre cuite
dim_cm | dimension de l'objet en chaine de caractère, affiché dans la cartel de l'objet | 44,50 cm (diamètre : 30,5 cm)
echelle_cm | dimension utilisée pour générer l'échelle | 44,5
lieu_creation_nom | Nom du lieu de création de l'objet | attique
lieu_creatio_pays | Pays du lieu de création de l'objet | Grèce
lieu_creation_lat | lattitude du lieu de création de l'objet (info récupérée sur Pelagios, notamment pour identifier un point si'il s'agit d'une région) | 38.0519988333
lieu_creation_long | longitude du lieu de création de l'objet (info récupérée sur Pelagios, notamment pour identifier un point si'il s'agit d'une région)  | 23.8189911
lieu_creation_type | Type du lieu création de l'objet (région, ville, pays, etc.) | région
date_creation_string | date de création de l'objet, forme affichée dans la cartel de l'objet | 1er quart du 5e siècle avant J.C.
date_creation_debut | valeur numérique de la date de création inférieure de l'objet utile pour générer la timeline | 475
date_creation_fin | valeur numérique de la date de création supérieure de l'objet utile pour générer la timeline | 500
lieu_decouverte_nom | Nom du lieu de découverte de l'objet | Vulci
lieu_decouverte_lat | Lattitude du lieu de découverte de l'objet ((info récupérée sur Pelagios, notamment pour identifier un point si'il s'agit d'une région) | 42.4192224
lieu_decouverte_long | Longitude du lieu de découverte de l'objet ((info récupérée sur Pelagios, notamment pour identifier un point si'il s'agit d'une région) | 11.6286618333
lieu_decouverte_pays | Pays du lieu de découverte de l'objet | italie
lieu_decouverte_certitude | 2 valeurs possible (certain/incertain) | incertaine
lieu_decouverte_type | Type du lieu de découverte de l'objet (région, ville, pays, etc.) | ville
date_decouverte_string | date de création de l'objet, forme affichée dans la cartel de l'objet | 12 janvier 1838
date_decouverte_fin | valeur numérique de la date de découverte de l'objet utile pour générer la timeline | 1838
date_decouverte_debut | valeur numérique de la date de découverte de l'objet utile pour générer la timeline | 1838
conservation_nom | Nom de l'institution qui conserve aujourd'hui l'objet | Musée Antoine Vivenel
conservation_id | identifiant unique de l'organisme. Vide pour le moment |  -
conservation_date_entree | date d'entrée de l'objet dans la collection du musée qui conserve l'objet | 1852
conservation_ville | ville du l'institution qui conserve aujourd'hui l'objet | Compiègne
conservation_pays | Pays du l'institution qui conserve aujourd'hui l'objet | France
lieu_conservation_lat | Lattiude du l'institution qui conserve aujourd'hui l'objet | 49.417635
lieu_conservation_long | Longitude du l'institution qui conserve aujourd'hui l'objet | 2.821754
conservation_type |  Type de l'institution qui conserve aujourd'hui l'objet  | bätiment
URL_objet_AGORGA | URL pérenne pour accéder à la notice complète de l'objet dans AGORHA | http://www.purl.org/inha/agorha/003/140451


#### Détails du fichier INHA_ventes.csv

Nom_colonne | Description | Exemple
------------ | ------------- | -----
id_objet | identifiant unique de l'objet dans la base AGORHA. Cette colonne sert de clé primaire pour associer l'objet à toutes ces ventes| 136343
vente_nom | Intitulé de la vente générale | Vente Magnoncour 1839
type_vente  | Deux valeurs possibles: vente ou vente de lot  | vente de lot
id_appvente | Concaténation de l'id_objet et de vente_nom | 136343 - Vente Magnoncour 1839
id_vente | identifiant de la vente | 6876
vente_date | Date de la vente. S'il s'agit d'une vente générale, les dates sont sous forme d'intervalle. S'il s'agit d'une vente de lot, la date précise le jour exacte sous la forme jj mois aaaa | 10 mai 1836
vente_ville | Ville du lieu de vente | Paris
vente_pays | Pays du lieu de vente | France
vente_adresse_1 | Adresse du lieu de vente | Domicile de Durand 20, boulevard Poissonnière
vente_long | longitude du lieu de vente | 2.345466
vente_lat | lattitude du lieu de vente  | 48.871698
vente_vendeur | Nom du vendeur de l'objet lors de la vente. Information uniquement présente s'il s'agit d'une vente de lot  | Durand, Edme Antoine
uk_acteur_vente_vendeur | identifiant unique de l'acteur, utile pour lier l'information avec le fichier INHA_acteurs.csv | 142387
vente_acheteur | Nom de l'acheteur de l'objet lors de la vente. Information uniquement présente s'il s'agit d'une vente de lot  |  Durand-Duclos, Laurent
uk_acteur_vente_acheteur | identifiant unique de l'acteur, utile pour lier l'information avec le fichier INHA_acteurs.csv | 144353
ventes_prix_francs | Indication de prix de la transaction. Information uniquement s'il s'agit d'une vente de lot | 8,50 francs
url_vente | URL pérenne pour accéder à la notice complète de la vente. Il s'agit à chaque fois de la vente générale même s'il s'agit d'une vente de lot  | http://www.purl.org/inha/agorha/004/6218

#### Détails du fichier INHA_acteurs.csv

Nom_colonne | Description | Exemple
------------ | ------------- | ------
acteur_nom	| nom de l'acteur. Il contient entre parenthèse les dates de naissance et de décès si nous possédons l'info | Magnoncour, Flavien de (1800 - 1875)
uk_acteur		| identifiant unique pour chaque acteur | 144353
acteur_nature		| type d'entité. 3 valeurs possibles : personnes, collectivité, famille | personne
acteur_star		| 2 valeurs possibles : 1 ou 2. Valeur utilisée pour générer les filtres des top10 des acteurs  | 1
acteur_url	| URL de la notice détaillée de l'acteur dans AGORHA | 	http://www.purl.org/inha/agorha/002/142829
