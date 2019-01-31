# rdf

<subject> HAS <predicate> <object>
Triple patterns in queries often have more than one variable 多个查询变量

Without the OPTIONAL keyword, a SPARQL processor will only return data for a graph pattern if it can match every single triple pattern in that graph pattern.

A namespace prefix can simply be a colon. This is popular for name- spaces that are used often in a particular document because the reduced clutter makes it easier for human eyes to read.

After declaring that the prefix v: refers to the namespace http://www.w3.org/2006/vcard/, an RDF dataset could say that Berners-Lee has a v:title of “Director”, but it could also say that he has a <http://www.w3.org/2006/vcard/title> of “Director”, using the entire namespace URI instead of the prefix.

URI 是 universally unique， 没有数据库表的概念

When evaluating a triplestore, along with typical database manager issues such as size, speed, platform availability, and cost, there are several SPARQL-related issues to consider:
• Does it support real SPARQL, or some “SPARQL-like” query and update language that the triplestore’s developers made up themselves?
• How easy is it to give the triplestore a SPARQL query and to then get the result back, both interactively and programatically?
• Can the triplestore serve as a SPARQL endpoint?
• Does the triplestore support the latest SPARQL standard?

_:名字 是空白节点，用于逻辑分组，例如_:address 有predicate x:name, x:postcode 等等

## Ontology
an ontology is a formal, explicit specification of a shared conceptual- ization

Reusing and Creating Vocabularies: RDF Schema and OWL
RDF Vocabulary Description Lan- guage: RDF Schema
describe these vocabularies with RDF, so this metadata is just as accessible to your SPARQL queries as the data itself.

ab:playsInstrument
  rdf:type rdf:Property ;
  rdfs:comment "Identifies the instrument that someone plays" ; 
  rdfs:label "plays instrument" ;
  rdfs:domain ab:Musician ;
  rdfs:range ab:MusicalInstrument .
The rdfs:domain property means that if I use this ab:playsInstrument property in a triple, then the subject of the triple is an ab:Musician. The rdfs:range property means that the object of such a triple is an ab:MusicalInstrument.


Once I’ve added the new triple shown at the end of ex045.ttl, an RDFS-aware SPARQL processor knows that Richard Mutt (or, more precisely, resource ab:i0432) is now a member of the class ab:Musician, because ab:playsInstrument has a domain of ab:Musician. Because ab:playsInstrument has a range of ab:MusicalInstrument, ab:vacuumCleaner is now a member of the ab:MusicalInstrument class, even if it never was before.

This ability of RDF resources to become members of classes based on their data values has made RDF technology popular in areas such as medical research and intelligence agencies. Researchers can accumulate data with little apparent structure and then see what structure turns out to be there—that is, which resources turn out to be members of which classes, and what their relationships are.

Ontologies are formal definitions of vocabularies that allow you to define complex structures as well as new relationships between your vocabulary terms and between members of the classes that you define

The Update specification is the key difference between SPARQL 1.0 and 1.1 be- cause it takes SPARQL from just being a query language to something that can add data to a dataset and replace and delete it as well. Chapter 6 covers the key features of this specification.


PREFIX d: <http://dbpedia.org/ontology/>
SELECT ?artistName ?albumName WHERE
{
  ?album d:producer :Timbaland . 
  ?album d:musicalArtist ?artist . 
  ?album rdfs:label ?albumName . 
  ?artist rdfs:label ?artistName .
}
uri返回的不一定是readable的，使用rdfs:label返回label更好

REFIX d: <http://dbpedia.org/ontology/>
SELECT ?artistName ?albumName WHERE
{
  ?album d:producer :Timbaland . 
  ?album d:musicalArtist ?artist . 
  ?album rdfs:label ?albumName . 
  ?artist rdfs:label ?artistName . 
  FILTER ( lang(?artistName) = "en" ) 
  FILTER ( lang(?albumName) = "en" )
}

A given resource doesn’t always have to be either a subject or a predicate or an object; it can play two or three of these roles in different triples. Putting the same variable in different positions in your query’s triple patterns,


PREFIX ab: <http://learningsparql.com/ns/addressbook#>
SELECT ?first ?last ?workTel ?nick WHERE
{
?s ab:firstName ?first ; ab:lastName ?last .
OPTIONAL { ?s ab:workTel ?workTel . } OPTIONAL { ?s ab:nick ?nick . }
}
默认必选，可选需要指定"OPTIONAL"，注意OPTIONAL里面的本身也是一整个graph pattern
The order of OPTIONAL graph patterns matters.

There are some edge cases where FILTER NOT EXISTS and MINUS may return different results. See the SPARQL 1.1 Query Recommenda- tion’s “Relationship and difference between NOT EXISTS and MINUS” section for details.

关联查询技巧：use of the same variable in the object position of one triple pattern and the subject position of another

RDF triple的object虽然可以用string，但是用URI扩展性更好，可以通过URI获得更多客户端需要的信息，例如：rdfs:label

^ operator at the beginning of the c:cites prop- erty tells the query processor that we want the inverse of this property


使用 property path
PREFIX : <http://learningsparql.com/ns/papers#> PREFIX c: <http://learningsparql.com/ns/citations#>
SELECT ?s WHERE
{
?s c:cites/^c:cites :paperF .
FILTER(?s != :paperF) }

there’s no reason to ask for the values of any variables standing in for blank nodes
blank node的名字都是临时的，有可能返回的和数据里面的不一样。但是blank node引用的数据是固定的。只要不在select的时候直接返回blank nodes的值就行。


SELECT DISTINCT ?p WHERE
{ ?s ?p ?o . }

A set of stored triples has no order

When using LIMIT and OFFSET together, don’t expect much consis- tency in the results if you don’t use ORDER BY with them.

FROM NAMED doesn’t contribute triples to the query unless you actually use the named graph.

VALUES offers an extra layer of result filtering that can give you more control over your final search results with very little extra code in your quer

The HAVING keyword does for aggregate values what FILTER does for individual values

easy data aggregation is one of RDF’s greatest benefits. Combining data, finding patterns, and then storing new data about what was found is popular in many of the fields that use this technology, such as pharmaceutical and intelligence research.
