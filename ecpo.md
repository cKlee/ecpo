# Introduction

The **Enumeration and Chronology of Periodicals Ontology (ECPO)** defines the common bibliographic terms for the description of enumeration and chronology of periodicals.

Institutions like libraries normally describing their holdings of periodicals like journals, annuals, newspapers etc. on a more abstract level than on a single unit level like they do it with books.

Holding descriptions of periodicals are more on the level of ranges of units. Periodical units are commonly called "issues" mostly grouped into "volumes". Ranges of periodical units are described by beginning and ending groups.

Newspapers descriptions might be a little bit more complex than other periodicals because they might have multiple subissues (e.g. one in the morning, another in the evening).  

A document using this ontology shall give answers to the questions:

  -  What units of a periodical are held by an agent?
  -  What units of a periodical are not held by an agent?
  
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

## Notes

In favour of brevity the comprehensive German term "Bestandsverlauf" is used instead of an English description.

## Namespaces and ontology

The URI namespace of this ontology is <http://purl.org/ontology/ecpo#>. The
namespace prefix `ecpo` is recommeded. The URI of this ontology as a whole
is <http://purl.org/ontology/ecpo>.

	@prefix ecpo: <http://purl.org/ontology/ecpo#> .
	@base        <http://purl.org/ontology/ecpo> .

The following namspace prefixes are used to refer to [related ontologies]:

	@prefix owl:   <http://www.w3.org/2002/07/owl#> .
	@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
	@prefix vann:  <http://purl.org/vocab/vann/> .
	@prefix dcterms: <http://purl.org/dc/terms/> .

The Enumeration and Chronology of Periodicals Ontology (ECPO) is defined in RDF/Turtle as following:

	<> a owl:Ontology ;
		rdfs:label "Enumeration and Chronology of Periodicals Ontology" ;
		rdfs:label "ECPO" ;
		vann:preferredNamespacePrefix "ecpo" .


# Classes

## Bestandsverlauf

[Bestandsverlauf]: #bestandsverlauf

A Bestandsverlauf is the description of enumeration and chronology of a periodical.

	ecpo:Bestandsverlauf a owl:Class ;
		rdfs:label "Bestandsverlauf" ;
		rdfs:isDefinedBy <> .

# Properties

## hasBestandsverlauf

[hasBestandsverlauf]: #hasBestandsverlauf

This property relates a holding description to a [Bestandsverlauf]. Having this property means that the described periodical units by the [Bestandsverlauf] are held by someone. To relate a [Bestandsverlauf] and a [Bestandsverlauf] use [hasSubBestandsverlauf] instead.

	ecpo:hasBestandsverlauf a owl:ObjectProperty ;
		rdfs:label "hasBestandsverlauf" ;
		rdfs:range ecpo:Bestandsverlauf ;
		rdfs:isDefinedBy <> .

## hasBestandsverlaufGap

[hasBestandsverlaufGap]: #hasBestandsverlaufGap

This property relates a holding description to a [Bestandsverlauf]. Having this property means that the described periodical units by the [Bestandsverlauf] are not held by someone. To relate a [Bestandsverlauf] and a [Bestandsverlauf] use [hasSubBestandsverlauf] instead.

	ecpo:hasBestandsverlaufGap a owl:ObjectProperty ;
		rdfs:label "hasBestandsverlaufGap" ;
		rdfs:range ecpo:Bestandsverlauf ;
		rdfs:isDefinedBy <> .
		
## hasSubBestandsverlauf

[hasSubBestandsverlauf]: #hasSubBestandsverlauf

This property relates a [Bestandsverlauf] to a [Bestandsverlauf]. Meaning the object is a subpart to the subject.

	ecpo:hasSubBestandsverlauf a owl:ObjectProperty ;
		rdfs:label "hasSubBestandsverlauf" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range ecpo:Bestandsverlauf ;
		rdfs:subPropertyOf dcterms:hasPart ;
		rdfs:isDefinedBy <> .

## hasBeginVolumeNumbering

[hasBeginVolumeNumbering]: #hasBeginVolumeNumbering

The numbering of the beginning volume

	ecpo:hasBeginVolumeNumbering a owl:DatatypeProperty ;
		rdfs:label "hasBeginVolumeNumbering" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "The numbering of the beginning volume"@en ;
		rdfs:isDefinedBy <> .

## hasBeginVolumeExtension

[hasBeginVolumeExtension]: #hasBeginVolumeExtension

A textual descrimination of the beginning volume

	ecpo:hasBeginVolumeExtension a owl:DatatypeProperty ;
		rdfs:label "hasBeginVolumeExtension" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the beginning volume"@en ;
		rdfs:isDefinedBy <> .

## hasBeginIssueNumbering

[hasBeginIssueNumbering]: #hasBeginIssueNumbering

The numbering of the beginning issue

	ecpo:hasBeginIssueNumbering a owl:DatatypeProperty ;
		rdfs:label "hasBeginIssueNumbering" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "The numbering of the beginning issue"@en ;
		rdfs:isDefinedBy <> .
		
## hasBeginIssueExtension

[hasBeginIssueExtension]: #hasBeginIssueExtension

A textual descrimination of the beginning issue

	ecpo:hasBeginIssueExtension a owl:DatatypeProperty ;
		rdfs:label "hasBeginIssueExtension" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the beginning issue"@en ;
		rdfs:isDefinedBy <> .
		
## hasBeginTemporal

[hasBeginTemporal]: #hasBeginTemporal

A temporal information, like a year

	ecpo:hasBeginTemporal a owl:DatatypeProperty ;
		rdfs:label "hasBeginTemporal" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A temporal information, like a year"@en ;
		rdfs:isDefinedBy <> .

## hasBeginDayCount

[hasBeginDayCount]: #hasBeginDayCount

The day count of the beginning group

	ecpo:hasBeginDayCount a owl:DatatypeProperty ;
		rdfs:label "hasBeginDayCount" ;
		rdfs:range rdfs:Literal;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The day count of the beginning group"@en ;
		rdfs:isDefinedBy <> .

## hasBeginMonthCount

[hasBeginMonthCount]: #hasBeginMonthCount

The month count of the beginning group

	ecpo:hasBeginMonthCount a owl:DatatypeProperty ;
		rdfs:label "hasBeginMonthCount" ;
		rdfs:range rdfs:Literal;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The month count of the beginning group"@en ;
		rdfs:isDefinedBy <> .

## hasBeginComment

[hasBeginComment]: #hasBeginComment

A comment to the beginning group

	ecpo:hasBeginComment a owl:DatatypeProperty ;
		rdfs:label "hasBeginComment" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A comment to the beginning group"@en ;
		rdfs:isDefinedBy <> .

## hasEndVolumeNumbering

[hasEndVolumeNumbering]: #hasEndVolumeNumbering

The numbering of the ending volume

	ecpo:hasEndVolumeNumbering a owl:DatatypeProperty ;
		rdfs:label "hasEndVolumeNumbering" ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The numbering of the ending volume"@en ;
		rdfs:isDefinedBy <> .

## hasEndVolumeExtension

[hasEndVolumeExtension]: #hasEndVolumeExtension

A textual descrimination of the endning volume

	ecpo:hasEndVolumeExtension a owl:DatatypeProperty ;
		rdfs:label "hasEndVolumeExtension" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the endning volume"@en ;
		rdfs:isDefinedBy <> .

## hasEndIssueNumbering

[hasEndIssueNumbering]: #hasEndIssueNumbering

The numbering of the ending issue

	ecpo:hasEndIssueNumbering a owl:DatatypeProperty ;
		rdfs:label "hasEndIssueNumbering" ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The numbering of the ending issue"@en ;
		rdfs:isDefinedBy <> .

## hasEndIssueExtension

[hasEndIssueExtension]: #hasEndIssueExtension

A textual descrimination of the endig issue

	ecpo:hasEndIssueExtension a owl:DatatypeProperty ;
		rdfs:label "hasEndIssueExtension" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A textual descrimination of the ending issue"@en ;
		rdfs:isDefinedBy <> .

## hasEndTemporal

[hasEndTemporal]: #hasEndTemporal

A temporal information, like a year
	
	ecpo:hasEndTemporal a owl:DatatypeProperty ;
		rdfs:label "hasEndTemporal" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A temporal information, like a year"@en ;
		rdfs:isDefinedBy <> .

## hasEndDayCount
	
[hasEndDayCount]: #hasEndDayCount

The day count of the ending group

	ecpo:hasEndDayCount a owl:DatatypeProperty ;
		rdfs:label "hasEndDayCount" ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The day count of the ending group"@en ;
		rdfs:isDefinedBy <> .

## hasEndMonthCount

[hasEndMonthCount]: #hasEndMonthCount

The month count of the ending group

	ecpo:hasEndMonthCount a owl:DatatypeProperty ;
		rdfs:label "hasEndMonthCount" ;
		rdfs:range rdfs:Literal ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:comment "The month count of the ending group"@en ;
		rdfs:isDefinedBy <> .

## hasEndComment

[hasEndComment]: #hasEndComment

A comment to the ending group

	ecpo:hasEndComment a owl:DatatypeProperty ;
		rdfs:label "hasEndComment" ;
		rdfs:domain ecpo:Bestandsverlauf ;
		rdfs:range rdfs:Literal ;
		rdfs:comment "A comment to the ending group."@en ;
		rdfs:isDefinedBy <> .

# References

## Normative References

* **[RFC 2119]** S. Bradner: *Key words for use in RFCs to Indicate Requirement Levels*. 
March 1997 <http://tools.ietf.org/html/rfc2119>.

* **[RFC 2396]** T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*.
August 1998 <http://tools.ietf.org/html/rfc2396>.

