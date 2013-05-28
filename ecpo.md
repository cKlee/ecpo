# Introduction

The **Enumeration and Chronology of Periodicals Ontology (ECPO)** defines the common bibliographic terms for the description of enumeration and chronology of periodicals.

Institutions like libraries normally describing their holdings of periodicals like journals, annuals, newspapers etc. on a more abstract level than on a single unit level like they do it with books.

Holding descriptions of periodicals are more on the level of ranges of units. Periodical units are commonly called "issues" mostly grouped into "volumes". Ranges of periodical units are described by beginning and ending groups.

Newspapers descriptions might be a little bit more complex than other periodicals because they might have multiple subissues (e.g. one in the morning, another in the evening).  

A document using this ontology shall give answers to the questions:

  -  What units of a periodical are held by an agent?
  -  What units of a periodical are not held by an agent?
  -  Is the chronology of a holding of a periodical closed or open?
 
A Question a document using this ontology might not answer:

  -  Does an agent hold a specific unit of a periodical?

## Status of this document

This HTML document and RDF serializations of the Enumeration and Chronology of Periodicals Ontology ([**`ecpo.ttl`**](ecpo.ttl) in RDF/Turtle and [**`ecpo.owl`**](ecpo.owl) in RDF/XML) are generated automatically from a source file written in Pandoc Markdown syntax. Sources and updates are available at <http://github.com/cklee/ecpo>. The current version of this document was last modified at GIT_REVISION_DATE with revision GIT_REVISION_HASH.

The current version of this ontology is a preliminary draft for open
discussion. [Feedback](https://github.com/cklee/ecpo/issues) is welcome!

**Revision history**

GIT_CHANGES

## Terminology

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in RFC 2119.

## Namespaces and ontology

The URI namespace of this ontology is <http://purl.org/ontology/ecpo#>. The
namespace prefix `ecpo` is recommeded. The URI of this ontology as a whole
is <http://purl.org/ontology/ecpo>.

	@prefix ecpo: <http://purl.org/ontology/ecpo#> .
	@base        <http://purl.org/ontology/ecpo> .

The following namspace prefixes are used to refer to [related ontologies]:

	@prefix owl:   <http://www.w3.org/2002/07/owl#> .
	@prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
	@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
	@prefix vann:  <http://purl.org/vocab/vann/> .
	@prefix dcterms: <http://purl.org/dc/terms/> .
	@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

The Enumeration and Chronology of Periodicals Ontology (ECPO) is defined in RDF/Turtle as following:

	<> a owl:Ontology ;
		rdfs:label "Enumeration and Chronology of Periodicals Ontology"@en ;
		rdfs:label "ECPO" ;
		vann:preferredNamespacePrefix "ecpo" .

# Overview

The following diagram illustrates the classes and properties defined in this ontology.

``` {.ditaa}
	
	+--------------------+   hasChronology    +-------------------------+   hasSubChronology
	| any document class +------------------->|        Chronology       +------------------+
	+---+------------+---+                    | +---------------------+ |                  |
	    |            |		                  | |                     | |<-----------------+
	hasChronology    |                        | |  RunningChronology  | |
		|            |                        | |                     | |
		v            |                        | +---------------------+ |-------+
	+-----------+    |                        | +---------------------+ |       |
	|  Running  |    |    hasChronologyGap    | |                     | |       |
	|  Closed   |    +------------------------->|  ClosedChronology   | |       |
	+-----------+                             | |                     | |       |
	                                          | +----------+----------+ |       |
											  +------------|------------+       |
											               |                    |
														hasEnd              hasBegin
														   |                    |
												  hasEndVolumeNumbering   hasBeginVolumeNumbering
												  hasEndVolumeExtension   hasBeginVolumeExtension
												  hasEndIssueNumbering    hasBeginIssueNumbering
												  hasEndIssueExtension    hasBeginIssueExtension
												  hasEndTemporal          hasBeginTemporal
												  hasEndDayCount          hasBeginDayCount
												  hasEndMonthCount        hasBeginMonthCount
												  hasEndComment           hasBeginComment
												           |                    |
														   +----------+---------+
														              |
																	  v
																   Literal
```

A document might have a [Chronology] which is related to closed chronolgies and/or running chronologies via the property [hasSubChronology] or is either a [ClosedChronology] or a [RunningChronology].
  
While the property [hasChronology] states that the described units of the document are held by someone, the property [hasChronologyGap] states that the described units of the document are not held by someone.

In order to simply state that a Chronology is running or closed, one could easily relate a document with the individuals [Running] or [Closed] via the property [hasChronology], because they are instances of [RunningChronology] or [ClosedChronology].

While instances of the class [RunningChronology] must not make use [hasEnd] or the subproperties of [hasEnd], instances of [ClosedChronology] must make use of [hasEnd] or one or more subproperties of [hasEnd]. All Instances of [RunningChronology] or [ClosedChronology] must make use of [hasBegin] or one or more subproperties of [hasBegin].

# Classes

## Chronology

[Chronology]: #chronology

A [Chronology] is the description of enumeration and chronology of a periodical. Use [RunningChronology] or [ClosedChronology] to describe either running or closed Chronlogies.

	ecpo:Chronology a owl:Class ;
		rdfs:label "Chronological designation"@en ;
		rdfs:label "Bestandsverlauf"@de ;
		rdfs:comment "A Chronology is the description of enumeration and chronology of a periodical."@en ;
		rdfs:isDefinedBy <> .

## RunningChronology
		
[RunningChronology]: #runningchronology

A [RunningChronology] is a [Chronology] which must not have a property describing an ending group.

	ecpo:RunningChronology a owl:Class ;
		rdfs:label "running chronology"@en ;
		rdfs:label "Bestandsverlauf laufend"@de ;
		rdfs:comment "A Chronology without an ending group."@en ;
		owl:disjointWith ecpo:ClosedChronology ;
		rdfs:subClassOf ecpo:Chronology ;
		rdfs:subClassOf [ 
			a owl:Restriction ;
			owl:maxCardinality "0"^^xsd:nonNegativeInteger ;
			owl:onProperty ecpo:hasEnd
		] ;		
		rdfs:subClassOf [ 
			a owl:Restriction ;
			owl:minCardinality "1"^^xsd:nonNegativeInteger ;
			owl:onProperty ecpo:hasBegin
		] ;
		rdfs:isDefinedBy <> .
		
## ClosedChronology
		
[ClosedChronology]: #closedchronology

A [ClosedChronology] is a [Chronology] which must make usage of minimum one property describing an ending group.

	ecpo:ClosedChronology a owl:Class ;
		rdfs:label "closed chronology"@en ;
		rdfs:label "Bestandsverlauf abgeschlossen"@de ;
		rdfs:comment "A Chronology having an ending group."@en ;
		owl:disjointWith ecpo:RunningChronology ;
		rdfs:subClassOf ecpo:Chronology ;
		rdfs:subClassOf [
			a owl:Restriction ;
			owl:minCardinality "1"^^xsd:nonNegativeInteger ;
			owl:onProperty ecpo:hasEnd
		] ;		
		rdfs:subClassOf [
			a owl:Restriction ;
			owl:minCardinality "1"^^xsd:nonNegativeInteger ;
			owl:onProperty ecpo:hasBegin
		] ;
		rdfs:isDefinedBy <> .

# Properties

## hasChronology

[hasChronology]: #hasChronology

Relation between a document and a [Chronology]. Having this property means that the described periodical units by the [Chronology] are held by someone. To relate a [Chronology] and a [Chronology] use [hasSubChronology] instead.

	ecpo:hasChronology a owl:ObjectProperty ;
		rdfs:label "has chronology"@en ;
		rdfs:label "hat Bestandsverlauf"@de ;
		rdfs:range ecpo:Chronology ;
		rdfs:comment "Relation between a document and a Chronology"@en ;
		rdfs:isDefinedBy <> .

## hasChronologyGap

[hasChronologyGap]: #haschronologygap

Relation between a document and a [ClosedChronology], indicating the [ClosedChronology] is a gap. Having this property means that the described periodical units by the [ClosedChronology] are not held by someone. To relate a [Chronology] and a [Chronology] use [hasSubChronology] instead.

	ecpo:hasChronologyGap a owl:ObjectProperty ;
		rdfs:label "has chronology gap"@en ;
		rdfs:label "hat Bestandsverlauflücke"@de ;
		rdfs:range ecpo:ClosedChronology ;
		rdfs:comment "Relation between a document and a Chronology, indicating the Chronology is a gap"@en ;
		rdfs:isDefinedBy <> .
		
## hasSubChronology

[hasSubChronology]: #hassubchronology

Relation between a [Chronology] and a [Chronology]. Meaning the object is part of the subject.

	ecpo:hasSubChronology a owl:TransitiveProperty ;
		rdfs:label "has subchronology"@en ;
		rdfs:label "hat untergeordneten Bestandsverlauf"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range ecpo:Chronology ;
		rdfs:comment "Relation between a Chronology and a Chronology"@en ;
		rdfs:subPropertyOf dcterms:hasPart ;
		rdfs:isDefinedBy <> .

## hasBegin

[hasBegin]: #hasbegin

Super-property to all properties of the beginning group

	ecpo:hasBegin a owl:DatatypeProperty ;
		rdfs:label "has begin"@en ;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "Super-property to all properties of the beginning group"@en ;
		rdfs:isDefinedBy <> .

## hasBeginVolumeNumbering

[hasBeginVolumeNumbering]: #hasbeginvolumenumbering

The numbering of the beginning volume

	ecpo:hasBeginVolumeNumbering a owl:DatatypeProperty ;
		rdfs:label "has begin volume numbering"@en ;
		rdfs:label "hat beginnende Bandzählung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "The numbering of the beginning volume"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasBeginVolumeExtension

[hasBeginVolumeExtension]: #hasbeginvolumeextension

A textual descrimination of the beginning volume

	ecpo:hasBeginVolumeExtension a owl:DatatypeProperty ;
		rdfs:label "has begin volume extension"@en ;
		rdfs:label "has beginnende Bandbezeichnung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the beginning volume"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasBeginIssueNumbering

[hasBeginIssueNumbering]: #hasbeginissuevumbering

The numbering of the beginning issue

	ecpo:hasBeginIssueNumbering a owl:DatatypeProperty ;
		rdfs:label "has begin issue numbering"@en ;
		rdfs:label "hat beginnende Ausgabenzählung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "The numbering of the beginning issue"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .
		
## hasBeginIssueExtension

[hasBeginIssueExtension]: #hasbeginissueextension

A textual descrimination of the beginning issue

	ecpo:hasBeginIssueExtension a owl:DatatypeProperty ;
		rdfs:label "has begin issue extension"@en ;
		rdfs:label "hat beginnende Ausgabenbezeichnung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the beginning issue"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .
		
## hasBeginTemporal

[hasBeginTemporal]: #hasbegintemporal

A temporal information, like a year

	ecpo:hasBeginTemporal a owl:DatatypeProperty ;
		rdfs:label "has begin temporal"@en ;
		rdfs:label "hat beginnende Zeit"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A temporal information, like a year"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasBeginDayCount

[hasBeginDayCount]: #hasbegindaycount

The day count of the beginning group

	ecpo:hasBeginDayCount a owl:DatatypeProperty ;
		rdfs:label "has begin day count"@en ;
		rdfs:label "hat beginnende Tageszählung"@de ;
		rdfs:range rdfs:Literal;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The day count of the beginning group"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasBeginMonthCount

[hasBeginMonthCount]: #hasbeginmonthcount

The month count of the beginning group

	ecpo:hasBeginMonthCount a owl:DatatypeProperty ;
		rdfs:label "has begin month count"@en ;
		rdfs:label "hat beginnende Montaszählung"@de ;
		rdfs:range rdfs:Literal;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The month count of the beginning group"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasBeginComment

[hasBeginComment]: #hasbegincomment

A comment to the beginning group

	ecpo:hasBeginComment a owl:DatatypeProperty ;
		rdfs:label "has begin comment"@en ;
		rdfs:label "hat Kommentar zum Beginn"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A comment to the beginning group"@en ;
		rdfs:subPropertyOf ecpo:hasBegin ;
		rdfs:isDefinedBy <> .

## hasEnd

[hasEnd]: #hasend

Super-property to all properties of the ending group

	ecpo:hasEnd a owl:DatatypeProperty ;
		rdfs:label "has end"@en ;
		rdfs:domain ecpo:ClosedChronology ;
		rdfs:comment "Super-property to all properties of the ending group"@en ;
		rdfs:isDefinedBy <> .

## hasEndVolumeNumbering

[hasEndVolumeNumbering]: #hasendvolumenumbering

The numbering of the ending volume

	ecpo:hasEndVolumeNumbering a owl:DatatypeProperty ;
		rdfs:label "has end volume numbering"@en ;
		rdfs:label "hat endende Bandzählung"@de ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The numbering of the ending volume"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndVolumeExtension

[hasEndVolumeExtension]: #hasendvolumeextension

A textual descrimination of the endning volume

	ecpo:hasEndVolumeExtension a owl:DatatypeProperty ;
		rdfs:label "has end volume extension"@en ;
		rdfs:label "hat endende Bandbenennung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the endning volume"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndIssueNumbering

[hasEndIssueNumbering]: #hasendissuenumbering

The numbering of the ending issue

	ecpo:hasEndIssueNumbering a owl:DatatypeProperty ;
		rdfs:label "has end issue numbering"@en ;
		rdfs:label "hat endende Ausgabenzählung"@de ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The numbering of the ending issue"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndIssueExtension

[hasEndIssueExtension]: #hasendissueextension

A textual descrimination of the endig issue

	ecpo:hasEndIssueExtension a owl:DatatypeProperty ;
		rdfs:label "has end issue extension"@en ;
		rdfs:label "hat endende Ausgabenbenennung"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the ending issue"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndTemporal

[hasEndTemporal]: #hasendtemporal

A temporal information, like a year
	
	ecpo:hasEndTemporal a owl:DatatypeProperty ;
		rdfs:label "has end temporal"@en ;
		rdfs:label "has endende Zeit"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A temporal information, like a year"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndDayCount
	
[hasEndDayCount]: #hasenddaycount

The day count of the ending group

	ecpo:hasEndDayCount a owl:DatatypeProperty ;
		rdfs:label "has end day count"@en ;
		rdfs:label "hat endende Tageszählung"@de ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The day count of the ending group"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndMonthCount

[hasEndMonthCount]: #hasendmonthcount

The month count of the ending group

	ecpo:hasEndMonthCount a owl:DatatypeProperty ;
		rdfs:label "has end month count"@en ;
		rdfs:label "hat endende Montaszählung"@de ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Chronology ;
		rdfs:comment "The month count of the ending group"@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .

## hasEndComment

[hasEndComment]: #hasendcomment

A comment to the ending group

	ecpo:hasEndComment a owl:DatatypeProperty ;
		rdfs:label "has end comment"@en ;
		rdfs:label "hat Kommentar zum Ende"@de ;
		rdfs:domain ecpo:Chronology ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A comment to the ending group."@en ;
		rdfs:subPropertyOf ecpo:hasEnd ;
		rdfs:isDefinedBy <> .
		
# Individuals

## Running

[Running]: #running

Instance of [RunningChronology]. Use this individual to simply state that a document has a running [Chronology].

	ecpo:Running a owl:NamedIndividual ;
		rdf:type ecpo:RunningChronology ;
		rdfs:label "running"@en ;
		rdfs:label "laufend"@de ;
		owl:differentFrom ecpo:Closed ;
		rdfs:comment "A running Chronology."@en ;
		ecpo:hasBegin "true"^^xsd:boolean ;
		rdfs:isDefinedBy <> .

## Closed

[Closed]: #closed

Instance of [ClosedChronology]. Use this individual to simply state that a document has a closed [Chronology].

	ecpo:Closed a owl:NamedIndividual ;
		rdf:type ecpo:ClosedChronology ;
		rdfs:label "closed"@en ;
		rdfs:label "abgeschlossen"@de ;
		owl:differentFrom ecpo:Running ;
		rdfs:comment "A closed Chronology."@en ;
		ecpo:hasBegin "true"^^xsd:boolean ;
		ecpo:hasEnd "true"^^xsd:boolean ;
		rdfs:isDefinedBy <> .

# References

## Normative References

* **[RFC 2119]** S. Bradner: *Key words for use in RFCs to Indicate Requirement Levels*. 
March 1997 <http://tools.ietf.org/html/rfc2119>.

* **[RFC 2396]** T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*.
August 1998 <http://tools.ietf.org/html/rfc2396>.
