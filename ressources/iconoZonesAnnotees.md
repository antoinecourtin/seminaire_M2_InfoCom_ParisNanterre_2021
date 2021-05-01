## Outils et exemples pour le projet "Iconographie et zones annotées"

### Ressources 

* La catégorie Art dans Wikimedia commons : https://commons.wikimedia.org/wiki/Category:Art
* Le projet WikiProject sum of all paintings : https://www.wikidata.org/wiki/Wikidata:WikiProject_sum_of_all_paintings
* Wikidata en 10 min : l'essentiel à lire : https://www.wikidata.org/wiki/Wikidata:Introduction/fr + https://www.wikidata.org/wiki/Help:About_data/fr

### Outils à tester/utiliser 

* Wikidata Image Positions : https://wd-image-positions.toolforge.org/ + [documentation](https://www.wikidata.org/wiki/User:Lucas_Werkmeister/Wikidata_Image_Positions)
* IIIF Image Cropper : http://zone47.com/crotos/lab/cropper/?l=fr

### Exemples d'utilisation

* Afficher dans Mirador, les zones annotées d'une image sur wikimedia commons
````
https://mirador.toolforge.org/?manifest=https://tools.wmflabs.org/wd-image-positions/iiif/Q21013224/P18/manifest.json
````
* VIsualiser toutes les zones annotées représentant un dragon : http://zone47.com/crotos/lab/cropper/p180iiif.php?q=Q7559&l=fr


### Exemple de requêtes (à compléter)
````sparql
SELECT distinct ?item ?itemLabel ?coord (GROUP_CONCAT(distinct ?creatorLabel; separator=" - ") as ?crea)
(GROUP_CONCAT(distinct STR(?collLabel); separator=" - ") as ?collection)
(SAMPLE(year(?d))as ?date)(SAMPLE(?image) as ?img)
((wikibase:decodeUri(substr(str(?img),52))) AS ?imgsansurl)
(CONCAT("http://tools.wmflabs.org/zoomviewer/proxy.php?iiif=",STR(?imgsansurl),"/",STR(?coord),"/full/0/default.jpg") as ?toto)
WHERE{
 ?item wdt:P180/wdt:P279* wd:Q7307 .
  ?item p:P180 ?DeclarationDepeint.
 ?DeclarationDepeint ps:P180/wdt:P279* wd:Q7307.
 ?DeclarationDepeint pq:P2677 ?coord.
 ?item wdt:P18 ?image.
 OPTIONAL{?item wdt:P571 ?d_crea.}
 OPTIONAL{?item wdt:P577 ?d_publi.}
 BIND(COALESCE(?d_crea, ?d_publi) AS ?d)
 OPTIONAL{?item wdt:P170 ?creator.}
 OPTIONAL{?item wdt:P195 ?coll.}
 SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],fr,en".
  ?item rdfs:label ?itemLabel.
  ?creator rdfs:label ?creatorLabel.
  ?coll rdfs:label ?collLabel.
 }
}
GROUP BY ?item ?itemLabel ?coord 
ORDER BY ?date

````
![Image of Yaktocat](http://tools.wmflabs.org/zoomviewer/proxy.php?iiif=Amarillis Crowning Mirtillo.jpg/pct:43.6,25.9,17.5,14.8/full/0/default.jpg


