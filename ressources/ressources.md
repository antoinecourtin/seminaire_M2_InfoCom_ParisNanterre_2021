# Liste de ressources utiles à tous les projets

### D'autres jeux de données en histoire de l'art
* Le site des collections des musées de la Ville de Paris : https://www.parismuseescollections.paris.fr/fr (export CSV à partir des résultats)
* Liste de musées présents sur github avec libre téléchargement de jeux de données : https://github.com/Ambrosiani/museums-on-github

### Markdown/github/jekyll
* Tutoriel pour comprendre Markdown et l'utiliser : [https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md](https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md)
* [Récupérer un jeu de données et le mettre à jour grâce à git et Github](https://github.com/Humanistica/ArtDesignDH/blob/master/tutoriels/tutoriel_recuperer_un_jeu_de_donnees_grace_a_git.md)
* Jekyyl = générateur de site statique fonctionne sur la base d’un référentiel de templates qui contient une série de fichiers texte structurés et statiques (markdowns) de différents formats. Ils déterminent non seulement la mise en page mais aussi le contenu de chaque projet Web.
* Jekyll sur Github
  * [exemple de repo tout simple utilisant GithubesPages avec Jeckyl](https://github.com/antoinecourtin/demogithubpages)
* Jekyll sur Gitlab
  * [tutoriel](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html)
  

### Petits outils pratiques en ligne 
* générer des tables (html, markdown, etc.) : https://www.tablesgenerator.com/markdown_tables
* [Beautifytools](https://beautifytools.com/) : des petits outils web permettant de faire des petites conversions de fichiers, etc.
* Datawrangling et sanity check
  * [openrefine](https://openrefine.org/)
  * [Breve](http://hdlab.stanford.edu/breve/)
  * [WTF CSV](https://databasic.io/en/wtfcsv/)
  * [Transformy](http://www.transformy.io/#/) : petit outil en ligne pour modifier le format d'un jeu de données
  * [codebeautify](https://codebeautify.org/)


### Quelques outils en ligne pour visualiser un corpus

* https://macarte.ign.fr/ : création de carte
* https://umap.openstreetmap.fr/fr/ : création de carte
* https://app.flourish.studio/ : création de visualisations
* https://app.rawgraphs.io/ : création de visualisations
* https://www.datawrapper.de/ : création de visualisations
* http://voyant.tools.huma-num.fr/ : environnement en ligne de lecture et d’analyse de textes numériques.

### OpenRefine

* Télécharger le fichier de la démonstration : https://filesender.renater.fr/?s=download&token=6220e034-30d1-44b4-99d8-8b7e8215b372 (export de la base de collection du Powerhouse Museum de Sydney pour les catégorie models)

#### Adresses de téléchargement d'OpenRefine et de plugin
* http://openrefine.org/download.html
* https://github.com/fadmaa/grefine-rdf-extension/releases 
* http://refine.codefork.com/reconcile/viaf
* https://www.bits.vib.be/index.php/software-overview/openrefine
* https://github.com/RubenVerborgh/Refine-NER-Extension
* https://github.com/sparkica/refine-stats

#### Wikidata et OpenRefine
* Adresse pour paramétrer l'outil de réalignement avec wikidata dans OpenRefine
https://tools.wmflabs.org/openrefine-wikidata/fr/api
* APrès un alignement, pouvoir créer dans une colonne dédié l'id ou le name : cell.recon.match.id / cell.recon.match.name

#### Quelques exemples de "formule" utiles dans OpenRefine
* rajouter une valeur fixe à une table : "valeur que tu veux ajouter" + cells['nom_delacolone'].value`
* exemple pour faire un rechercher/remplacer : `value.replace("MotRecherché","MotLeRemplaçant")`
* effectuer plusieurs modifications en un seul passage : `value.replace("~", "").replace(",","")`
* `value.replace("\"", "")`. Le caractère \ est un caractère d'échappement, il permet d'indiquer à OpenRefine qu'il doit utiliser le guillemet comme caractère à remplacer et non pas comme élément de la fonction value.replace.
* Enlever tout sauf les chiffres" : `replace(value,/[[a-z],[A-Z],(é|è|à|ù),\,\;\:\.\?\/\!\=\+\"\'\-\(\)\[\]]/,"")`
* Extraction d'une date de type aaaa : `value.match(/.*(\d{4}).*/)[0]`
* Supprimer les contenus semblables dans une même cellule : `value.split(", ").uniques().join(", ")`
* comparer les valeurs  de 2 colonnes :
  * via "Add column" > `if(cells["a"].value == cells["b"].value, "Yes", "No")`
  * via une construction de facet dans Facet > Custom text facet avec l'expression `value == cells["b"].value`
* géocodage avec adresse.data.gouv.fr > https://goo.gl/P3sqsB
* Calculer des longueurs de chaînes : `value.length()`
* Récupérer les info des parenthèses dans une chaine de charactère : `value.match(/.*(\(.*\)).*/)[0]`
* Compter les mots d'une chaîne : `value.split(/\b/).length()`
* Supprimer les espaces superflus d'une chaîne : `value.trim()`
* Transformer des caractères spéciaux HTML (ex: &eacute;) : Edit cells > Common transform > Unescape HTML entities
* extration des parenthèse : `value.match(/.*(\(.*\)).*/)[0]`
* extraction d'une date de type "12 janvier 1987" : `value.match(/.*(\d{2} [a-z]* \d{4}).*/)[0]`
* appeler une API via la fonction Fetching URL: `"http://maps.google.com/maps/api/geocode/json?sensor=false&address=" + escape(value, "url")"`
* Extraitre une info dans un json (lattitude) issue d'une requête à une API : `value.parseJson().results[0].geometry.location.lat`
* Extraire l'id (ou le nom du Q) de wikidata après le réalignement: `cell.recon.match.id / cell.recon.match.name`
* Template pour croiser 2 jeux de données = `cell.cross("My Address Book", "friend")[0].cells["address"].value`
=> cell.cross("nomduprojet", "nomColonneeCléIntermédiaire")[0].cells["nomColonneArécupérer"].value
* si plusieurs valeurs à récupérer dans un cell.cross, utiliser la formule suivante `forEach(cross(cell,"inha_ventes","id_objet"),v,v.cells["vente_ville"].value).join(' ; ')`
* pour exporter en geojson : https://gist.github.com/psychemedia/53e30d3d151fea23af68
* pour appeler une API tel que geonames : http://api.geonames.org/search?name=paris&country=FR&maxRows=3&username=formationbulac1

##### Liens vers ressources indispensables en français pour OpenRefine appliqués aux GLAMs
> * Mathieu Saby, Tutoriel OpenRefine 3.4 : nettoyer, préparer et transformer des données - 06/11/2020](https://msaby.gitlab.io/tutoriel-openrefine/index.html)

* Les supports de cours de Mathieu Saby sur Slideshare
https://fr.slideshare.net/27point7/nettoyer-et-prparer-des-donnes-avec-openrefine
* Le support de Maïwenn Bourdic, régulièrement mis à jour
https://patrimoine-et-numerique.fr/tutoriels/52-36-openrefine-excel-aux-hormones-pour-nettoyage-de-donnees

##### Liens vers quelques tuto complémentaire intégrant OpenRefine
* TUTO : “Reconcilier” une liste de nom d’architectes avec Wikidata en utilisant OpenRefine : https://medium.com/@seeksanusername/reconcilier-une-liste-darchitecte-avec-wikidata-en-utilisant-openrefine-16819fbb2903
* TUTO : Exploiter/visualiser/explorer un corpus issue de l’OAI-PMH grâce au duo OpenRefine/Palladio
https://medium.com/@seeksanusername/exploiter-visualiser-explorer-un-corpus-issue-de-loai-pmh-gr%C3%A2ce-au-couple-openrefine-palladio-1241323cf626
* Exploiter des cartes anciennes numérisées - Trucs et astuces (avec du Mapwarper, Palladio, umaps)
https://medium.com/@seeksanusername/exploiter-des-cartes-anciennes-num%C3%A9ris%C3%A9es-99d4ffc7788a

### Flourish

* https://help.flourish.studio/category/10-flourish-basics
* [11 vidéos](https://www.youtube.com/playlist?list=PLI0e4-ERAU-M-I9FuNxirXWdhYkR0_G_x), chacune d'environ 8min, pour l'utilisation avancée de Flourish 

### Wikidata

* wikidata : https://www.wikidata.org/wiki/Wikidata:Main_Page
* SPARQLendpoint : https://query.wikidata.org/
* Mix'n'Match : https://tools.wmflabs.org/mix-n-match/#/
* reasonator : https://tools.wmflabs.org/reasonator/
* exemple d'item wikidata avec des sources identifiées : 
	* https://www.wikidata.org/wiki/Q42173809
	* https://www.wikidata.org/wiki/Q3393987
* 1 exemple de requête pour Lister l'id, le titre et l'image de éléments des oeuvres de Klimt
````sparql
SELECT DISTINCT ?item ?itemLabel ?img
WHERE
{
  ?item wdt:P31 wd:Q3305213 .
  ?item wdt:P170 wd:Q34661 .
  OPTIONAL {
    ?item wdt:P18 ?img
    }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
````
* D'autres [exemples de requêtes commentées](/requeteWikidata.md) pour wikidata


### Palladio 

Pour tester Palladio
  * pour accéder à l'application : http://hdlab.stanford.edu/palladio-app/#/upload
  * Palladio et cartes anciennes
      * exemple d'URL Tiles https://mapwarper.net/maps/tile/47146/{z}/{x}/{y}.png
      * [tutoriel pour geomapper une carte ancienne numérisée et l'utiliser dans palladio](https://medium.com/@seeksanusername/exploiter-des-cartes-anciennes-num%C3%A9ris%C3%A9es-99d4ffc7788a)
  * jeux de tests :
     * télécharger le paquet json : [data_RETIF_HdF_2017_all_Palladio.json](https://github.com/antoinecourtin/DEFI_2019/raw/master/data_exemple/data_RETIF_HdF_2017_all_Palladio%20(1).json)
     * télécharger un fichier csv : [Export_EnvoisdeRome_oeuvres_20190325.csv](https://github.com/antoinecourtin/DEFI_2019/raw/master/data_exemple/Export_EnvoisdeRome_oeuvres_20190325.csv)

### Catalogues de visualisation de données
* www.datavizcatalogue.com
* http://www.visualcomplexity.com/vc
* http://ft-interactive.github.io/visual-vocabulary/
* https://datavizproject.com/
* http://chartmaker.visualisingdata.com/
* https://www.anychart.com/chartopedia/usage-type/
* https://journocode.com/data-journalism-tools/
