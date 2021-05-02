# Liste de ressources utiles à tous les projets

### Tutoriels / auto-formation
* Tutoriel pour comprendre Markdown et l'utiliser : [https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md](https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md)

### Petits outils pratiques en ligne 
* générer des tables (html, markdown, etc.) : https://www.tablesgenerator.com/markdown_tables
* [Beautifytools](https://beautifytools.com/) : des petits outils web permettant de faire des petites conversions de fichiers, etc.
* Datawrangling et sanity check
  * [openrefine](https://openrefine.org/)
  * [Breve](http://hdlab.stanford.edu/breve/)
  * [WTF CSV](https://databasic.io/en/wtfcsv/)
  * [Transformy](http://www.transformy.io/#/) : petit outil en ligne pour modifier le format d'un jeu de données
  * [codebeautify](https://codebeautify.org/)
  * 
### Jekyll

>  ce générateur de site statique fonctionne sur la base d’un référentiel de templates qui contient une série de fichiers texte structurés et statiques (markdowns) de différents formats. Ils déterminent non seulement la mise en page mais aussi le contenu de chaque projet Web.

* Jekyll sur Github
  * [exemple de repo tout simple utilisant GithubesPages avec Jeckyl](https://github.com/antoinecourtin/demogithubpages)
* Jekyll sur Gitlab
  * [tutoriel](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html)
  
### Quelques outils en ligne pour visualiser un corpus

* https://macarte.ign.fr/
* https://umap.openstreetmap.fr/fr/
* https://app.flourish.studio/
* https://app.rawgraphs.io/
* https://www.datawrapper.de/
* http://voyant.tools.huma-num.fr/

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

### Quelques exemples de requêtes commentées

* requête SPARQL pour afficher les céramiques grecques antiques du musée Saint-Raymond ayant un id d'objet dans AGORHA 

```sparql
select DISTINCT ?objet ?objetLabel ?img ?idAgorha
where {
	?objet wdt:P31/wdt:P279* wd:Q738680. #que de la céramique grecque antique
?objet wdt:P195 wd:Q1376. #conservé au Musée Saint-Raymond
      ?objet wdt:P2344 ?idAgorha. #et un identifiant AGORHA
  OPTIONAL { #en option 
    ?objet wdt:P18 ?img.   #avec une image


  }
  SERVICE wikibase:label { #pour récuéprer les labels
bd:serviceParam wikibase:language "fr,en"}
}
```

* requête SPARQL pour afficher lar architectes américains 

```sparql
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
select distinct ?personneLabel 
where {
?personne wdt:P31 wd:Q5 . #pour chercher des personnes humaines
?personne wdt:P106 wd:Q42973 . #qui occupe la fonction d'architecte
?personne wdt:P27 wd:Q30 . #qui sont américains
SERVICE wikibase:label { 
bd:serviceParam wikibase:language "fr,en"}
}
```
* afficher sous forme de timeline les oeuvres du projet Europeana280

```sparql
#defaultView:Timeline
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
SELECT ?itemLabel ?image ?creatorLabel ?datecreation ?placebirthLabel where {
      ?item wdt:P31/wdt:P279* wd:Q838948 .  # œuvre d’art et ss-classe 
  ?item wdt:P608 wd:Q20980830. # du projet Europeana 280
  
 OPTIONAL  {
   ?item wdt:P571 ?datecreation. # date de création, utile pour l'affichage timeline
   ?item wdt:P170 ?creator. # créateur 
   ?item wdt:P18 ?image. #pour l'image
   ?creator wdt:P19 ?placebirth. # lieu de naissance 
   ?placebirth wdt:P625 ?geoloc . #coordonnées géo, utile pr l'affichage carto
  
           }
  SERVICE wikibase:label {
       bd:serviceParam wikibase:language "fr,es,en" .
    }
       
}
```

* Lister uniquement l'id de éléments des oeuvres de Klimt
````sparql
SELECT *
WHERE
{
  ?item wdt:P31 wd:Q3305213 .
  ?item wdt:P170 wd:Q34661 .
}
````
* Afficher sous forme de grille d'images toutes les oeuvres attribuées au Caravage
````sparql
#defaultView:ImageGrid
SELECT DISTINCT ?item ?itemLabel (YEAR(?date) AS ?year) ?dimensions ?locationLabel ?countryLabel ?image WHERE {
  { ?item wdt:P170 wd:Q42207 . } UNION { ?item wdt:P1773 wd:Q42207 }
  OPTIONAL { ?item p:P276 ?statement . ?statement ps:P276 ?location . FILTER NOT EXISTS { ?statement pq:P582 ?x } OPTIONAL { ?location wdt:P17 ?country } }
  OPTIONAL { ?item wdt:P18 ?image }
  OPTIONAL { ?item wdt:P2048 ?length }
  OPTIONAL { ?item wdt:P2049 ?width }
  OPTIONAL { ?item wdt:P571 ?date }
  BIND (CONCAT(STR(?length),"×",STR(?width)) AS ?dimensions)
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en" . }
} ORDER BY ?itemLabel
````
* Les groupes de personnages de l’univers Marvel sous forme de graphe de relation

````sparql
#defaultView:Graph
SELECT ?char ?charLabel ?group ?groupLabel ("7FFF00" as ?rgb)
WHERE {
	?group wdt:P31 wd:Q14514600 ;  # group of fictional characters
          wdt:P1080 wd:Q931597.  # from Marvel universe
 ?char wdt:P463 ?group # member of group
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en".}
}
````

* Afficher sous forme de liste toutes les céramiques grecques du Metropolitan Museum pour lesquelles la base AGORHA possède des informations de provenance.

````sparql
	select DISTINCT ?item ?itemLabel ?img ?idAgorha
	where {
		?item wdt:P31/wdt:P279* wd:Q738680 . # pottery of ancient Greece
		?item wdt:P18 ?img.    
	    ?item wdt:P276 wd:Q160236.
	  ?item wdt:P2344 ?idAgorha.

	  SERVICE wikibase:label {
	bd:serviceParam wikibase:language "fr,en"}
	}
````

* Afficher sous la forme d'une timeline, les propriétaires des céramiques grecques du MET

````sparql
	#defaultView:Timeline
	select DISTINCT ?item ?itemLabel ?eventLabel ?img ?proprietairesLabel ?datedebut ?datefin
	where {
		?item wdt:P31/wdt:P279* wd:Q738680 . # pottery of ancient Greece
		?item wdt:P18 ?img.    
	    ?item wdt:P276 wd:Q160236.
	    ?item p:P127 ?declaration_proprietaires.
	    ?declaration_proprietaires ps:P127 ?proprietaires.
	    OPTIONAL
		{?declaration_proprietaires pq:P580 ?datedebut.
		FILTER(!(STRSTARTS(?datedebut, 't')))}
	    OPTIONAL
		{?declaration_proprietaires pq:P582 ?datefin.
		FILTER(!(STRSTARTS(?datefin, 't')))}

	  SERVICE wikibase:label {
	bd:serviceParam wikibase:language "fr,en"}
	}
````
* Afficher sous forme de carte toutes les sculptures publiques dans Paris

````sparql
#defaultView:Map
SELECT DISTINCT ?item  ?Titre ?createur (year(?date) as ?AnneeCreation) ?image ?coord
WHERE {
   ?item wdt:P31/wdt:P279* wd:Q860861.                    # sculpture
   ?item wdt:P136 wd:Q557141 .                            # genre : art public
   {?item wdt:P131 wd:Q90.}                               # ... située dans Paris
   UNION
   {?item wdt:P131 ?arr.                                  # ... ou dans un arrondissement de Paris  
   ?arr wdt:P131 wd:Q90. }
   ?item rdfs:label ?Titre filter (lang(?Titre) = "fr").  # Titre

   OPTIONAL {?item wdt:P170 ?Qcreateur.                   # créateur/créatrice (option)
   ?Qcreateur rdfs:label ?createur filter (lang(?createur) = "fr") .}
   OPTIONAL {?item wdt:P571 ?date.}                       # date de création (option)
   OPTIONAL {?item wdt:P18  ?image.}                      # image (option)
   OPTIONAL {?item wdt:P625 ?coord.}                      # coordonnées géographiques (option)
}
````

* Qui fête son anniversaire aujourd'hui
````sparql
#Qui fête son anniversaire aujourd'hui ?
#Whose birthday is today?
SELECT ?entityLabel (YEAR(?date) as ?year)
WHERE
{
    BIND(MONTH(NOW()) AS ?nowMonth)
    BIND(DAY(NOW()) AS ?nowDay)

    ?entity wdt:P569 ?date .
    FILTER (MONTH(?date) = ?nowMonth && DAY(?date) = ?nowDay)
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "en" .
    }
}
LIMIT 10
````
* Classement général des causes de décès sous forme de BubbleChart

````sparql
#Classement général des causes de décès
#defaultView:BubbleChart
#TEMPLATE={"template":"Overall causes of death ranking of ?thing ","variables":{"?thing": {"query":"SELECT ?id  (COUNT(?id) AS ?count) WHERE {  ?sub wdt:P509 ?y.  ?sub wdt:P31 ?id. } GROUP BY ?id "} } }
SELECT ?cid ?cause (COUNT(*) AS ?count) WHERE {
  BIND(wd:Q5 AS ?thing)
  ?pid wdt:P31 ?thing;
      wdt:P509 ?cid.
SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". ?cid rdfs:label ?cause}
}
GROUP BY ?cid ?cause
ORDER BY DESC(?count) ?cause
````
* Nombre de films par an et par genre sous forme d'un scatterplot avec animation

````sparql
#Nombre de films par an et par genre
#defaultView:ScatterChart
SELECT   ?year  (COUNT(?_genre) AS ?count ) (SAMPLE(?_genreLabel) AS ?label )  (?year as ?year_shown) WHERE {
  ?item wdt:P31 wd:Q11424.
  ?item wdt:P577 ?_publication_date.
  ?item wdt:P136 ?_genre.
  ?_genre rdfs:label ?_genreLabel.
  BIND(str(YEAR(?_publication_date)) AS ?year)
  FILTER((LANG(?_genreLabel)) = "en")

 FILTER (?_publication_date >= "2000-00-00T00:00:00Z"^^xsd:dateTime)
}
GROUP BY ?_genreLabel ?year
HAVING (?count > 30)
````


* Évolution du nombre d'œuvres par "Genre" entre 1500-1600.
````sparql
#defaultView:BarChart
SELECT   ?year  (COUNT(?_genre) AS ?count ) (SAMPLE(?_genreLabel) AS ?label )  (?year as ?year_shown) WHERE {
  ?item wdt:P31 wd:Q3305213.
  ?item wdt:P170 ?creator.
  ?item wdt:P571 ?_creation_date.
  ?item wdt:P136 ?_genre.
  ?_genre rdfs:label ?_genreLabel.
  BIND(str(YEAR(?_creation_date)) AS ?year)
  FILTER((LANG(?_genreLabel)) = "fr")

 FILTER (?_creation_date >= "1500-00-00T00:00:00Z"^^xsd:dateTime)
 FILTER (?_creation_date <= "1600-00-00T00:00:00Z"^^xsd:dateTime)
}
GROUP BY ?_genreLabel ?year
HAVING (?count > 1)
````



* Afficher sur une carte, les villes en France dont le nom se termine par "ac"

````sparql
#Communes françaises dont le nom fini par ac
#added before 2016-10

#defaultView:Map
SELECT ?item ?itemLabel ?coord
WHERE
{
	?item	wdt:P31/wdt:P279* wd:Q484170;
				wdt:P17 wd:Q142;
				rdfs:label ?itemLabel;
				wdt:P625 ?coord;
	FILTER (lang(?itemLabel) = "fr").
	FILTER regex (?itemLabel, "ac$").
	FILTER not exists { ?item wdt:P131 wd:Q33788 } # excluding Koumac, New Caledonia...
}
````
:wink: Pour les linguistes : Œuvres d’Art dont le titre est une allitération

````sparql

#added before 2016-10
SELECT DISTINCT ?work ?title
WHERE
{
  ?work wdt:P31/wdt:P279* wd:Q838948;
        wdt:P1476 ?title.
  FILTER(REGEX(STR(?title), "^(\\p{L})\\w+(?:\\W+\\1\\w+){2,}$", "i")).
}
ORDER BY STR(?title)
````

### Palladio 

Pour tester Palladio
  * pour accéder à l'application : http://hdlab.stanford.edu/palladio-app/#/upload
  * Palladio et cartes anciennes
      * exemple d'URL Tiles https://mapwarper.net/maps/tile/47146/{z}/{x}/{y}.png
      * [tutoriel pour geomapper une carte ancienne numérisée et l'utiliser dans palladio](https://medium.com/@seeksanusername/exploiter-des-cartes-anciennes-num%C3%A9ris%C3%A9es-99d4ffc7788a)
  * jeux de tests :
     * télécharger le paquet json : [data_RETIF_HdF_2017_all_Palladio.json](https://github.com/antoinecourtin/DEFI_2019/raw/master/data_exemple/data_RETIF_HdF_2017_all_Palladio%20(1).json)
     * télécharger un fichier csv : [Export_EnvoisdeRome_oeuvres_20190325.csv](https://github.com/antoinecourtin/DEFI_2019/raw/master/data_exemple/Export_EnvoisdeRome_oeuvres_20190325.csv)
