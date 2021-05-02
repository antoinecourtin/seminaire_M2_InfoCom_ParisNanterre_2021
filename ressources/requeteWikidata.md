## Exemples de requêtes wikidata avec des commentaires


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
