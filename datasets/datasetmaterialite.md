## Documents du jeux de données "Materialité"

Lié à plusieurs programmes de recherche :
  * [**Les collections Rothschild dans les institutions publiques françaises**](https://www.inha.fr/fr/recherche/le-departement-des-etudes-et-de-la-recherche/domaines-de-recherche/histoire-des-collections-histoire-des-institutions-artistiques-et-culturelles-economie-de-l-art/les-collections-rothschild-dans-les-institutions-publiques-francaises.html)
  * [**Répertoire des tableaux italiens dans les collections publiques françaises (RETIF)**](https://www.inha.fr/fr/recherche/le-departement-des-etudes-et-de-la-recherche/domaines-de-recherche/histoire-des-collections-histoire-des-institutions-artistiques-et-culturelles-economie-de-l-art/repertoire-des-tableaux-italiens-dans-les-collections-publiques-francaises-retif.html)
  * [**Le musée des Monuments français d'Alexandre Lenoir, histoire et collection**](https://www.inha.fr/fr/ressources/outils-documentaires/acces-global-et-organise-aux-ressources-en-histoire-de-l-art-agorha/le-musee-des-monuments-francais-d-alexandre-lenoir-histoire-et-collections.html?search-keywords=LENOIR)
### Composition du corpus téléchargé :

Ce fichier readme précise la structure des 3 fichiers présent dans le [répertoire suivant](datamaterialite/), à savoir :
1. allLenoir.csv : les objets de la base Lenoir
2. allRETIF.csv : les objets de la base RETIF
3. allRothschild.csv : les objets de la base Rothschild

Ce sont tous des extraits des bases disponibles sur https://agorha.inha.fr/ selon les critères suivants :
- des objets ayants une dimension largeur-hauteur
- des objets ayant une illustraton
- uniquement une valeur par type d'information pour simplifier le jeux de données. Au besoin, possibilité d'avoir le jeux de données dans son intégralité.

es métadonnées sont placées sous licence Creative Commons 4.0. Dans ce cadre, l’utilisateur est autorisé : à reproduire et à rediffuser ces métadonnées, sous réserve de la mention exacte de la source (permalien de la notice Agorha) ; à retraiter, à inclure ou à exploiter ces contenus et métadonnées, sous réserve de ne pas en dénaturer le sens ni l’exactitude et de ne pas induire en erreur des tiers quant au contenu ou à la source de ces informations ; pour le monde entier et sans limitation de durée ; à des fins commerciales ou non.


#### Détails des colonnes des fichiers 
artwork - TITRE	= titre/intitulé de l'object
artwork - HAUTEUR	= hauteur
artwork - UNIQUE_KEY = id de la notice documentaire de l'objet
artwork - URL	= url de la notice sur AGORHA
artwork - IMG_DIRECT_ACCESS	= url de la vignette de l'objet
artwork - DISPLAY_DENOMINATION	= type d'oeuvre
artwork - DISPLAY_LIEU_CONSERV	= lieux de conservation de l'oeuvre
artwork - DISPLAY_MATIERE	= matière de l'objet
artwork - DISPLAY_DATE_EXE_TXT	= date de l'objet
artwork - LARGEUR	= largeur 
artwork - DISPLAY_PERSONNE_AUTEUR	= auteur (attention, formulation, qui comprend le nom de l'auteur, ses dates et sa profession)
artwork - DISPLAY_TECHNIQUE	= technique de l'object
artwork - DISPLAY_ROLE_AUTEUR	= le rôle de l'auteur par rapport à l'oeuvre (de, d'après, etc.)
