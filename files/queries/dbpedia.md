1 - Prime Minister of Countries:

	PREFIX dbo: <http://dbpedia.org/ontology/>
	PREFIX dbr: <http://dbpedia.org/resource/>
	PREFIX yago: <http://dbpedia.org/class/yago/>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	
	SELECT *
	FROM <http://dbpedia.org>
	WHERE {
		?person dbo:termPeriod ?timePeriod . 
		?timePeriod dbo:office ?office . 
		?timePeriod dbo:activeYearsStartDate ?from . 
		?timePeriod dbo:activeYearsEndDate ?to .
		FILTER (regex(?office, "^Prime Minister of.*"))
	}
	
2 - Births of persons:
	
	PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

	SELECT ?person ?place ?date  
	WHERE {   
	    ?person dbpedia-owl:birthPlace ?place .   
	    ?place rdf:type dbpedia-owl:City  .   
	    ?person dbpedia-owl:birthDate ?date .  
	}   

3 - Actors starring in a movie:
	
	PREFIX dbo: <http://dbpedia.org/ontology/>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

	SELECT DISTINCT ?film ?actor ?date 
	WHERE {   
	    ?film dbo:starring ?actor .   
	    ?film rdf:type dbo:Film .  
	    ?film dbo:releaseDate ?date .
	}   

4 - Deaths of persons:
		
	PREFIX dbpedia-owl: <http://dbpedia.org/ontology/> 
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

	SELECT ?person ?place ?date
	FROM <http://dbpedia.org>
	WHERE {  
	    ?person dbpedia-owl:deathPlace ?place .  
	    ?place rdf:type dbpedia-owl:City  .  
	    ?person dbpedia-owl:deathDate ?date . 
	} 
	
5 - NBA team associations of basketball players:
	
	PREFIX dbo: <http://dbpedia.org/ontology/>
	PREFIX dbr: <http://dbpedia.org/resource/>
	PREFIX yago: <http://dbpedia.org/class/yago/>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

	SELECT ?player ?timePeriod ?team ?from ?to
	FROM <http://dbpedia.org> 
	WHERE {
	     ?player dbo:league dbr:National_Basketball_Association .
	     ?player dbo:termPeriod ?timePeriod .
	     ?timePeriod dbo:team ?team .
	     ?timePeriod dbo:activeYearsStartYear ?from . 
	     ?timePeriod dbo:activeYearsEndYear ?to .
	     ?team rdf:type yago:WikicatNationalBasketballAssociationTeams .
	     FILTER( xsd:gYear(?from) > "2000"^^xsd:gYear )
	}
		