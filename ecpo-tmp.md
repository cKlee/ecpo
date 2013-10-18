% Enumeration and Chronology of Periodicals Ontology (ECPO)
% Carsten Klee (ZDB)
% 2013-07-30 11:24:26 +0200

# Introduction

The **Enumeration and Chronology of Periodicals Ontology (ECPO)** defines the common bibliographic terms for the description of enumeration and chronology of periodicals.

Institutions like libraries normally describing their holdings of periodically issued media like journals, serials, annuals, newspapers etc. on a more abstract level than on a single unit level like they do it with books.

Holding descriptions of periodicals are more on the level of ranges of units. Ranges of periodical units are described by beginning and ending groups. Periodical units are commonly called "issues" mostly grouped into "volumes" but in both cases the caption and hierarchy depth may vary. There are more complex structures than this, like for instance Newspapers descriptions might have multiple subissues (e.g. one in the morning, another in the evening). This ontology is trying to cope this, but not all complex structures might be expressed.

It it also possible that the enumeration and chronology of periodicals is described in a itemized way. Itemized means that the enumeration and chronology of a periodical is described by a listing of each part of the unit held [see ANSI/NISO Z39.71-2006](http://www.niso.org/apps/group_public/project/details.php?project_id=38 "ANSI/NISO Z39.71-2006") not using ranges.

A document using this ontology shall give answers to the questions:

  -  What units of a periodical are held by an agent?
  -  What units of a periodical are not held by an agent?
  -  Is the chronology of a holding of a periodical closed or open?
 
A Question a document using this ontology might not answer:

  -  Does an agent hold a specific unit of a periodical?

## Status of this document

This HTML document and RDF serializations of the Enumeration and Chronology of Periodicals Ontology [**`ecpo.ttl`**](ecpo.ttl) in RDF/Turtle and [**`ecpo.owl`**](ecpo.owl) in RDF/XML) are generated automatically from a source file written in Pandoc Markdown syntax. Sources and updates are available at <http://github.com/cklee/ecpo>. The current version of this document was last modified at 2013-07-30 11:24:26 +0200 with revision [a214d21](https://github.com/cKlee/ecpo/commit/a214d21a9b7b2bf5224ad7aa45f87385c1f03a5a).

The current version of this ontology is a preliminary draft for open discussion. [Feedback](https://github.com/cklee/ecpo/issues) is welcome!

**Revision history**


* [`2013-07-30 11:24:26 +0200`](ecpo-a214d21.html): [with dublin core annotation properties](https://github.com/cKlee/ecpo/commit/a214d21a9b7b2bf5224ad7aa45f87385c1f03a5a)


## Terminology

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## Namespaces and ontology

The URI namespace of this ontology is <http://purl.org/ontology/ecpo#>. The
namespace prefix `ecpo` is recommended. The URI of this ontology as a whole
is <http://purl.org/ontology/ecpo>.

    @prefix ecpo: <http://purl.org/ontology/ecpo#> .
    @base        <http://purl.org/ontology/ecpo> .

The following namespace prefixes are used to refer to [related ontologies]:

    @prefix owl:   <http://www.w3.org/2002/07/owl#> .
    @prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix vann:  <http://purl.org/vocab/vann/> .
    @prefix dc: <http://purl.org/dc/elements/1.1/> .
    @prefix dct: <http://purl.org/dc/terms/> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .

The Enumeration and Chronology of Periodicals Ontology (ECPO) is defined in RDF/Turtle as following:

    <> a owl:Ontology ;
        rdfs:label "Enumeration and Chronology of Periodicals Ontology"@en ;
        rdfs:label "ECPO" ;
        vann:preferredNamespacePrefix "ecpo" ;
        vann:preferredNamespaceUri "http://purl.org/ontology/ecpo#" ;
        dc:title "Enumeration and Chronology of Periodicals Ontology"@en ;
        dc:description "Defines the common bibliographic terms for the description of enumeration and chronology of periodicals"@en .

# Overview

The following diagram illustrates the classes and properties defined in this ontology.

``` {.ditaa}
    
    +--------------------+   hasChronology    +-------------------------+  dct:hasPart
    | every item class   +------------------->|        Chronology       +------------------+
    +---+----------------+  hasChronologyGap  | +---------------------+ |                  |
        |                                     | |                     | |<-----------------+
    hasChronology                             | |  CurrentChronology  | |
        |                                     | |                     | |
        v                     +---------------+ +---------------------+ +---------------+----------------------+
    +-----------+             |               | +---------------------+ |               |                      |
    |  Current  |             |               | |                     | |               |                      |
    |  Closed   |             |               | |  ClosedChronology   | |               |                      |
    +-----------+             |               | |                     | |               |                      |
                              |               | +----------+----------+ |               |                      |
                              |               +------------|------------+               |                      |
                              |                            |                            |                      |
                           hasBegin                      hasEnd                      hasItemized         dct:description
                              |                            |                            |                dc:coverage
                    hasBeginVolumeCaption         hasEndVolumeCaption        hasItemizedVolumeCaption    dct:accrualPeriodicity
                    hasBeginVolumeNumbering       hasEndVolumeNumbering      hasItemizedVolumeNumbering  dct:extend
                    hasBeginVolumeExtension       hasEndVolumeExtension      hasItemizedVolumeExtension        |
                    hasBeginIssueCaption          hasEndIssueCaption         hasItemizedIssueCaption           |
                    hasBeginIssueNumbering        hasEndIssueNumbering       hasItemizedIssueNumbering         |
                    hasBeginIssueExtension        hasEndIssueExtension       hasItemizedIssueExtension         |
                    hasBeginTemporal              hasEndTemporal             hasItemizedTemporal               |
                    hasBeginTemporalExtension     hasEndTemporalExtension    hasItemizedTemporalExtension      |
                              |                            |                            |                      |
                              |                            |                            |                      |
                              v                            v                            v                      v
```

An Agent always holds a copy of a document called item. An item might have a [Chronology] which is related to other [Chronologies](#chronology) via the property [dct:hasPart]. While current [Chronologies](#chronology) should be instances of [CurrentChronology], closed [Chronologies](#chronology) should be instances of [ClosedChronology].

While the property [hasChronology] states that the described units of the item are held by someone, the property [hasChronologyGap] states that the described units of the item are not held by someone.

In order to simply state that a Chronology is current or closed, one could easily relate an item with the individuals [Current] or [Closed] via the property [hasChronology], because they are instances of [CurrentChronology] or [ClosedChronology].

[Chronologies](#chronology) as long as they describe ranges consist of either a beginning and an ending group or just of one beginning group. Beginning and ending groups are defined through the existence of the property [hasBegin] or one or more of its subproperties (for a beginning group) or the property [hasEnd] or one or more of its subproperties (for an ending group). 

While instances of the class [CurrentChronology] must not make use [hasEnd] or the subproperties of [hasEnd], instances of [ClosedChronology] must make use of [hasEnd] or one or more subproperties of [hasEnd]. All Instances of [CurrentChronology] or [ClosedChronology] must make use of [hasBegin] or one or more subproperties of [hasBegin].

In cases of a itemized [Chronologies](#chronology) which are neither current nor closed nor having a beginning or ending group, one should make use of the property [hasItemized] or one of its subproperties. To list multiple single items within a [Chronology] one must make use of the property [dct:hasPart], because one [Chronology] must only describe one item in a itemized way.

# Classes

## Chronology

[Chronology]: #chronology

A [Chronology] is the description of enumeration and chronology of a periodical. Use [CurrentChronology] or [ClosedChronology] to describe either current or closed [Chronlogies](#chronology).

Instances of [Chronology] must at least participate in a relation with one of the properties [hasBegin] or [hasItemized].

See [General class axioms] for further rules.


    ecpo:Chronology a owl:Class ;
        rdfs:label "enumeration and chronology"@en ;
        rdfs:label "Bestandsverlauf"@de ;
        rdfs:comment "A Chronology is the description of enumeration and chronology of a periodical."@en ;
        rdfs:subClassOf [
            a owl:Class ;
            owl:unionOf (
                [ a owl:Restriction ;
                    owl:onProperty ecpo:hasBegin ;
                    owl:someValuesFrom owl:Thing
                ] [ a owl:Restriction ;
                    owl:onProperty ecpo:hasItemized ;
                    owl:someValuesFrom owl:Thing
                ]
            )
        ] .

## CurrentChronology
        
[CurrentChronology]: #currentchronology

A [CurrentChronology] is a [Chronology] which must not have a property describing an ending group.
Instances of [CurrentChronology] must not make use [hasEnd] or one of its subproperties.
Instances of [CurrentChronology] must at least participate in a relation with the property [hasBegin] or one of its subproperties. 

    ecpo:CurrentChronology a owl:Class ;
        rdfs:label "current chronology"@en ;
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
        ] .


        
## ClosedChronology
        
[ClosedChronology]: #closedchronology

A [ClosedChronology] is a [Chronology] which must make usage of minimum one property describing an ending group.
Instances of [ClosedChronology] must at least participate in a relation with both properties [hasBegin] or one of its subproperties and [hasEnd] or one of its subproperties.

    ecpo:ClosedChronology a owl:Class ;
        rdfs:label "closed chronology"@en ;
        rdfs:label "Bestandsverlauf abgeschlossen"@de ;
        rdfs:comment "A Chronology having an ending group."@en ;
        owl:disjointWith ecpo:CurrentChronology ;
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
         ] .

# Object properties

## hasChronology

[hasChronology]: #hasChronology

Relation between an item and a [Chronology]. Having this property means that the described periodical units by the [Chronology] are held by someone. To relate a [Chronology] and a [Chronology] use [dct:hasPart] instead.

    ecpo:hasChronology a owl:ObjectProperty ;
        rdfs:label "has chronology"@en ;
        rdfs:label "hat Bestandsverlauf"@de ;
        rdfs:range ecpo:Chronology ;
        rdfs:comment "Relation between an item and a Chronology"@en .

## hasChronologyGap

[hasChronologyGap]: #haschronologygap

Relation between an item and a [Chronology], indicating the [Chronology] is a gap. Having this property means that the described periodical units through the [Chronology] are not held by someone. To relate a [Chronology] and a [Chronology] use [dct:hasPart] instead.

    ecpo:hasChronologyGap a owl:ObjectProperty ;
        rdfs:label "has chronology gap"@en ;
        rdfs:label "hat Bestandsverlauflücke"@de ;
        rdfs:range ecpo:Chronology ;
        rdfs:comment "Relation between an item and a Chronology, indicating the Chronology is a gap"@en .

# Datatype properties

## hasBegin

[hasBegin]: #hasbegin

Super-property to all properties of the beginning group

    ecpo:hasBegin a owl:DatatypeProperty ;
        rdfs:label "has begin"@en ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "Super-property to all properties of the beginning group"@en .

## hasBeginVolumeCaption

[hasBeginVolumeCaption]: #hasbeginvolumecaption

The caption of the beginning volume, like 'Vol.', 'Bd.', 'Tome'

    ecpo:hasBeginVolumeCaption a owl:DatatypeProperty ;
        rdfs:label "has begin volume caption"@en ;
        rdfs:label "hat beginnende Bandbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the beginning volume"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .
        
## hasBeginVolumeNumbering

[hasBeginVolumeNumbering]: #hasbeginvolumenumbering

The numbering of the beginning volume

    ecpo:hasBeginVolumeNumbering a owl:DatatypeProperty ;
        rdfs:label "has begin volume numbering"@en ;
        rdfs:label "hat beginnende Bandzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the beginning volume"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .

## hasBeginVolumeExtension

[hasBeginVolumeExtension]: #hasbeginvolumeextension

A textual descrimination of the beginning volume

    ecpo:hasBeginVolumeExtension a owl:DatatypeProperty ;
        rdfs:label "has begin volume extension"@en ;
        rdfs:label "has beginnende Bandergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the beginning volume"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .

## hasBeginIssueCaption

[hasBeginIssueCaption]: #hasbeginissuecaption

The caption of the beginning issue, like 'Issue', 'No.', 'Ausg.'

    ecpo:hasBeginIssueCaption a owl:DatatypeProperty ;
        rdfs:label "has begin issue caption"@en ;
        rdfs:label "hat beginnende Ausgabenbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the beginning issue"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .
        
## hasBeginIssueNumbering

[hasBeginIssueNumbering]: #hasbeginissueumbering

The numbering of the beginning issue

    ecpo:hasBeginIssueNumbering a owl:DatatypeProperty ;
        rdfs:label "has begin issue numbering"@en ;
        rdfs:label "hat beginnende Ausgabenzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the beginning issue"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .
        
## hasBeginIssueExtension

[hasBeginIssueExtension]: #hasbeginissueextension

A textual descrimination of the beginning issue

    ecpo:hasBeginIssueExtension a owl:DatatypeProperty ;
        rdfs:label "has begin issue extension"@en ;
        rdfs:label "hat beginnende Ausgabenergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the beginning issue"@en ;
        rdfs:subPropertyOf ecpo:hasBegin .
        
## hasBeginTemporal

[hasBeginTemporal]: #hasbegintemporal

A temporal information for the beginning group, like a year, a season, a month or a day

    ecpo:hasBeginTemporal a owl:DatatypeProperty ;
        rdfs:label "has begin temporal"@en ;
        rdfs:label "hat beginnende Zeit"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A temporal information for the beginning group, like a year, a season, a month or a day"@en ;
        rdfs:subPropertyOf ecpo:hasBegin ;
        rdfs:subPropertyOf dct:temporal .
        
## hasBeginTemporalExtension

[hasBeginTemporalExtension]: #hasbegintemporalextension

Refines the value of the property [hasBeginTemporal]

    ecpo:hasBeginTemporalExtension a owl:DatatypeProperty ;
        rdfs:label "has begin temporal extension"@en ;
        rdfs:label "hat beginnende Zeit Ergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "Refines the value of the property hasBeginTemporal"@en ;
        rdfs:subPropertyOf ecpo:hasBegin ;
        rdfs:subPropertyOf dct:temporal .

## hasEnd

[hasEnd]: #hasend

Super-property to all properties of the ending group

    ecpo:hasEnd a owl:DatatypeProperty ;
        rdfs:label "has end"@en ;
        rdfs:domain ecpo:ClosedChronology ;
        rdfs:comment "Super-property to all properties of the ending group"@en .

## hasEndVolumeCaption

[hasEndVolumeCaption]: #hasendvolumecaption

The caption of the ending volume, like 'Vol.', 'Bd.', 'Tome'

    ecpo:hasEndVolumeCaption a owl:DatatypeProperty ;
        rdfs:label "has end volume caption"@en ;
        rdfs:label "hat endende Bandbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the ending volume"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .
        
## hasEndVolumeNumbering

[hasEndVolumeNumbering]: #hasendvolumenumbering

The numbering of the ending volume

    ecpo:hasEndVolumeNumbering a owl:DatatypeProperty ;
        rdfs:label "has end volume numbering"@en ;
        rdfs:label "hat endende Bandzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the ending volume"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .

## hasEndVolumeExtension

[hasEndVolumeExtension]: #hasendvolumeextension

A textual descrimination of the endning volume

    ecpo:hasEndVolumeExtension a owl:DatatypeProperty ;
        rdfs:label "has end volume extension"@en ;
        rdfs:label "hat endende Bandergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the endning volume"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .

## hasEndIssueCaption

[hasEndIssueCaption]: #hasendissuecaption

The caption of the ending issue, like 'Issue', 'No.', 'Ausg.'

    ecpo:hasEndIssueCaption a owl:DatatypeProperty ;
        rdfs:label "has end issue caption"@en ;
        rdfs:label "hat endende Ausgabenbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the ending issue"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .

## hasEndIssueNumbering

[hasEndIssueNumbering]: #hasendissuenumbering

The numbering of the ending issue

    ecpo:hasEndIssueNumbering a owl:DatatypeProperty ;
        rdfs:label "has end issue numbering"@en ;
        rdfs:label "hat endende Ausgabenzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the ending issue"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .

## hasEndIssueExtension

[hasEndIssueExtension]: #hasendissueextension

A textual descrimination of the endig issue

    ecpo:hasEndIssueExtension a owl:DatatypeProperty ;
        rdfs:label "has end issue extension"@en ;
        rdfs:label "hat endende Ausgabenergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the ending issue"@en ;
        rdfs:subPropertyOf ecpo:hasEnd .

## hasEndTemporal

[hasEndTemporal]: #hasendtemporal

A temporal information for the ending group, like a year, a season, a month or a day
    
    ecpo:hasEndTemporal a owl:DatatypeProperty ;
        rdfs:label "has end temporal"@en ;
        rdfs:label "has endende Zeit"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A temporal information for the ending group, like a year, a season, a month or a day"@en ;
        rdfs:subPropertyOf ecpo:hasEnd ;
        rdfs:subPropertyOf dct:temporal .
        
## hasEndTemporalExtension

[hasEndTemporalExtension]: #hasendtemporalextension

Refines the value of the property [hasEndTemporal]

    ecpo:hasEndTemporalExtension a owl:DatatypeProperty ;
        rdfs:label "has end temporal extension"@en ;
        rdfs:label "hat endende Zeit Ergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "Refines the value of the property hasEndTemporal"@en ;
        rdfs:subPropertyOf ecpo:hasEnd ;
        rdfs:subPropertyOf dct:temporal .
        
## hasItemized

[hasItemized]: #hasitemized

Super-property to all properties of a itemized [Chronology]

    ecpo:hasItemized a owl:DatatypeProperty ;
        rdfs:label "has itemized"@en ;
        rdfs:label "hat einzelne"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "Super-property to all properties of a itemized Chronology"@en .
        
## hasItemizedVolumeCaption

[hasItemizedVolumeCaption]: #hasitemizedvolumecaption

The caption of the volume

    ecpo:hasItemizedVolumeCaption a owl:DatatypeProperty ;
        rdfs:label "has itemized volume caption"@en ;
        rdfs:label "hat einzelne Bandbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the volume"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .
        
## hasItemizedVolumeNumbering

[hasItemizedVolumeNumbering]: #hasitemizedvolumenumbering

The numbering of the volume

    ecpo:hasItemizedVolumeNumbering a owl:DatatypeProperty ;
        rdfs:label "has itemized volume numbering"@en ;
        rdfs:label "hat einzelne Bandzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the volume"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .

## hasItemizedVolumeExtension

[hasItemizedVolumeExtension]: #hasitemizedvolumeextension

A textual descrimination of the volume

    ecpo:hasItemizedVolumeExtension a owl:DatatypeProperty ;
        rdfs:label "has itemized volume extension"@en ;
        rdfs:label "hat einzelne Bandergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the volume"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .

## hasItemizedIssueCaption

[hasItemizedIssueCaption]: #hasitemizedissuecaption

The caption of the issue

    ecpo:hasItemizedIssueCaption a owl:DatatypeProperty ;
        rdfs:label "has itemized issue caption"@en ;
        rdfs:label "hat einzelne Ausgabenbeschriftung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The caption of the issue"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .
        
## hasItemizedIssueNumbering

[hasItemizedIssueNumbering]: #hasitemizedissuenumbering

The numbering of the issue

    ecpo:hasItemizedIssueNumbering a owl:DatatypeProperty ;
        rdfs:label "has itemized issue numbering"@en ;
        rdfs:label "hat einzelne Ausgabenzählung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "The numbering of the issue"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .

## hasItemizedIssueExtension

[hasItemizedIssueExtension]: #hasitemizedissueextension

A textual descrimination of the issue

    ecpo:hasItemizedIssueExtension a owl:DatatypeProperty ;
        rdfs:label "has itemized issue extension"@en ;
        rdfs:label "hat einzelne Ausgabenergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A textual descrimination of the issue"@en ;
        rdfs:subPropertyOf ecpo:hasItemized .

## hasItemizedTemporal

[hasItemizedTemporal]: #hasitemizedtemporal

A temporal information, like a year, a season, a month or a day
    
    ecpo:hasItemizedTemporal a owl:DatatypeProperty ;
        rdfs:label "has itemized temporal"@en ;
        rdfs:label "has einzelne Zeit"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "A temporal information, like a year, a season, a month or a day"@en ;
        rdfs:subPropertyOf ecpo:hasItemized ;
        rdfs:subPropertyOf dct:temporal .
        
## hasItemizedTemporalExtension

[hasItemizedTemporalExtension]: #hasitemizedtemporalextension

Refines the value of the property [hasItemizedTemporal]

    ecpo:hasItemizedTemporalExtension a owl:DatatypeProperty ;
        rdfs:label "has temporal extension"@en ;
        rdfs:label "hat Zeit Ergänzung"@de ;
        rdfs:domain ecpo:Chronology ;
        rdfs:comment "Refines the value of the property hasItemizedTemporal"@en ;
        rdfs:subPropertyOf ecpo:hasItemized ;
        rdfs:subPropertyOf dct:temporal .

# Annotation Properties

## dc:coverage

[dc:coverage]: #coverage

Used to transport the whole source description of a chronology. See [examples](#ex_dc) for usage.

    dc:coverage a owl:AnnotationProperty ;
        skos:scopeNote "Used to transport the whole source description of a chronology."@en ;
        rdfs:definedBy <http://purl.org/dc/elements/1.1/> .

## dct:accrualPeriodicity

[dct:accrualPeriodicity]: #accrualperiodicity

Used to give information about the frequency with which items are added to the collection. See [examples](#ex_dc) for usage.

    dct:accrualPeriodicity a owl:AnnotationProperty ;
        skos:scopeNote "Used to give information about the frequency with which items are added to the collection."@en ;
        rdfs:definedBy <http://purl.org/dc/elements/1.1/> .

## dct:description

[dct:description]: #description

Used to transport the whole source description of a chronology. See [examples](#ex_dc) for usage.

    dct:description a owl:AnnotationProperty ;
        skos:scopeNote "Used to transport the whole source description of a chronology."@en ;
        rdfs:definedBy <http://purl.org/dc/elements/1.1/> .

## dct:extend

[dct:extend]: #extend

Used to give information about the number of units in the chronology. See [examples](#ex_dc) for usage.

    dct:extend a owl:AnnotationProperty ;
        skos:scopeNote "Used to give information about the number of units in the chronology."@en ;
        rdfs:definedBy <http://purl.org/dc/elements/1.1/> .

## dct:hasPart

[dct:hasPart]: #haspart

Used to relate a [Chronology] to a [sub chronology](#chronology). See [examples](#ex_haspart) for usage.

    dct:hasPart a owl:AnnotationProperty ;
        skos:scopeNote "Used to relate a chronology to a sub chronology."@en ;
        rdfs:definedBy <http://purl.org/dc/elements/1.1/> .


# Individuals

## Current

[Current]: #current

Instance of [CurrentChronology]. Use this individual to simply state that an item has a current [Chronology]. See [examples](#ex_current) for usage.

    ecpo:Current a owl:NamedIndividual ;
        rdf:type ecpo:CurrentChronology ;
        rdfs:label "current"@en ;
        rdfs:label "laufend"@de ;
        owl:differentFrom ecpo:Closed ;
        rdfs:comment "A current Chronology."@en ;
        ecpo:hasBegin "true"^^xsd:boolean .

## Closed

[Closed]: #closed

Instance of [ClosedChronology]. Use this individual to simply state that an item has a closed [Chronology]. See [examples](#ex_closed) for usage.

    ecpo:Closed a owl:NamedIndividual ;
        rdf:type ecpo:ClosedChronology ;
        rdfs:label "closed"@en ;
        rdfs:label "abgeschlossen"@de ;
        owl:differentFrom ecpo:Current ;
        rdfs:comment "A closed Chronology."@en ;
        ecpo:hasBegin "true"^^xsd:boolean ;
        ecpo:hasEnd "true"^^xsd:boolean .

# General class axioms

[General class axioms]: #generalclassaxioms

The individuals [Closed] and [Current] are different from each other.

    [ 
        rdf:type owl:AllDifferent ;
        owl:distinctMembers (
            <http://purl.org/ontology/ecpo#Closed>
            <http://purl.org/ontology/ecpo#Current>
        )
    ] .

Instances of [Chronology] which participate in relations with [hasBegin] and [hasEnd] may not participate in relations with [hasItemized] and vice versa.

    [
        rdf:type owl:Class ;
        owl:disjointWith [
            rdf:type owl:Class ;
            owl:intersectionOf ( 
                ecpo:Chronology [ 
                    rdf:type owl:Restriction ;
                    owl:onProperty ecpo:hasItemized ;
                    owl:someValuesFrom owl:Thing
                ]
            )
        ] ;
        owl:intersectionOf ( 
            ecpo:Chronology [
                rdf:type owl:Class ;
                owl:unionOf ( 
                    [ 
                        rdf:type owl:Restriction ;
                        owl:onProperty ecpo:hasBegin ;
                        owl:someValuesFrom owl:Thing
                    ] [ 
                        rdf:type owl:Restriction ;
                        owl:onProperty ecpo:hasEnd ;
                        owl:someValuesFrom owl:Thing
                    ]
                )
            ]
        )
    ] .

Instances of [Chronology] which participates in a relation with [hasEnd] must also participate in a relation with [hasBegin].

    [
        rdf:type owl:Class ;
        rdfs:subClassOf [
            rdf:type owl:Restriction ;
            owl:onProperty ecpo:hasBegin ;
            owl:someValuesFrom owl:Thing
            ] ;
        owl:intersectionOf ( 
            ecpo:Chronology [
                rdf:type owl:Restriction ;
                owl:onProperty ecpo:hasEnd ;
                owl:someValuesFrom owl:Thing
            ]
        )
    ] .

# Related ontologies

[related ontologies]: #relatedontologies

ECPO recommends the use of [dct:description], [dct:accrualPeriodicity], [dct:extent] and [dc:coverage] for some extended chronology description.

# Extending ECPO

It is not the intension of ECPO to restrict the ontology extension through other ontologies on purpose. If you have suggestions to make this ontology more useable, please give me [Feedback](https://github.com/cklee/ecpo/issues).

# Examples

[Examples]: #exaples

In the following examples a hypothetical copy of a document ```$item``` describes a holding of a periodical held by someone.

## Statement for a current chronology

[ex_current]: #ex_current

    $item ecpo:hasChronology ecpo:Current .

This statement just says that an item has a [current chronology](#currentchronology) without giving futher information which units are held.

## Statement for a closed chronology

[ex_closed]: #ex_closed

    $item ecpo:hasChronology ecpo:Closed .

This statement just says that an item has a [closed chronology](#closedchronology) without giving futher information which units are held.

## Description of a current Chronology

Given description: v.26,issue 1-

    $item ecpo:hasChronology [
        a ecpo:CurrentChronology ;
        ecpo:hasBeginVolumeCaption "v." ;
        ecpo:hasBeginVolumeNumbering "26" ;
        ecpo:hasBeginIssueCaption "issue" ;
        ecpo:hasBeginIssueNumbering "1" 
    ] .
        
## Description of a closed Chronology

Given description: v.26,issue 1-v.31, issue 6

    $item ecpo:hasChronology [
        a ecpo:ClosedChronology ;
        ecpo:hasBeginVolumeCaption "v." ;
        ecpo:hasBeginVolumeNumbering "26" ;
        ecpo:hasBeginIssueCaption "issue" ;
        ecpo:hasBeginIssueNumbering "1" ;
        ecpo:hasEndVolumeCaption "v." ;
        ecpo:hasEndVolumeNumbering "31" ;
        ecpo:hasEndIssueCaption "issue" ;
        ecpo:hasEndIssueNumbering "6" 
    ] .

## Description of a closed Chronology with temporal information

Given description: (2001:Jan.1-2006:June 30)=no.320-no.385

    $item ecpo:hasChronology [
        a ecpo:ClosedChronology ;
        ecpo:hasBeginTemporal "2001" ;
        ecpo:hasBeginTemporalExtension "Jan.1" ;
        ecpo:hasBeginIssueCaption "no." ;
        ecpo:hasBeginIssueNumbering "320" ;
        ecpo:hasEndTemporal "2006" ;
        ecpo:hasEndTemporalExtension "June 30" ;
        ecpo:hasEndIssueCaption "no." ;
        ecpo:hasEndIssueNumbering "385" 
    ] .

## Description of a current chronology with subchronologies

[ex_haspart]: #ex_haspart

Given description: v.5:no.1(1975:spring)-v.7:no.4(1977:autumn),v.8:no.2(1978:winter)-

    $item ecpo:hasChronology [
        a ecpo:CurrentChronology ;
        dct:hasPart [
            a ecpo:ClosedChronology ;
            ecpo:hasBeginVolumeCaption "v." ;
            ecpo:hasBeginVolumeNumbering "5" ;
            ecpo:hasBeginIssueCaption "no." ;
            ecpo:hasBeginIssueNumbering "1" ;
            ecpo:hasBeginTemporal "1975" ;
            ecpo:hasBeginTemporalExtension "spring" ;
            ecpo:hasEndVolumeCaption "v." ;
            ecpo:hasEndVolumeNumbering "7" ;
            ecpo:hasEndIssueCaption "no." ;
            ecpo:hasEndIssueNumbering "4" ;
            ecpo:hasEndTemporal "1977" ;
            ecpo:hasEndTemporalExtension "autumn"
        ] ;
        dct:hasPart [
            a ecpo:ClosedChronology ;
            ecpo:hasBeginVolumeCaption "v." ;
            ecpo:hasBeginVolumeNumbering "8" ;
            ecpo:hasBeginIssueCaption "no." ;
            ecpo:hasBeginIssueNumbering "2" ;
            ecpo:hasBeginTemporal "1978" ;
            ecpo:hasBeginTemporalExtension "winter"
        ] .
        
In this example the main chronology is made as an instance of [CurrentChronology] for the sake of expressivity. It also had been made as an instance of [Chronology]. But this way it is easier to tell if the whole chronology is current or not.
        
## Description of a chronology in an itemized way and comments

Given description: v.1 v.2 v.2[i.e. 3] v.6

In this example Volume 3 was incorrectly numbered by the publisher.

    $item ecpo:hasChronology [
        a ecpo:Chronology ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "1"
        ] ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "2"
        ] ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "2" ;
            ecpo:hasItemizedVolumeExtension "[i.e. 3]" ;
            dct:description "Volume 3 was incorrectly numbered by the publisher"@en
        ] ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "6"
        ]
    ] .
    
The property [hasItemizedVolumeExtension] is described as "A textual descrimination of the volume". In this example it is used to transport the correction statement for the wron volume numbering. The expression with the property [dct:description] is optional.

## Description of a gap in the chronology

As in the example above the volumes v.4 and v.5 are missing. There are two possibilities to express this.

### Itemized way

    $item ecpo:hasChronologyGap [
        a ecpo:Chronology ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "4"
        ] ;
        dct:hasPart [
            a ecpo:Chronology ;
            ecpo:hasItemizedVolumeCaption "v." ;
            ecpo:hasItemizedVolumeNumbering "5"
        ]
    ] .
    
### Range

    $item ecpo:hasChronologyGap [
        a ecpo:Chronology ;
        ecpo:hasBeginVolumeCaption "v." ;
        ecpo:hasBeginVolumeNumbering "4" ;
        ecpo:hasEndVolumeCaption "v." ;
        ecpo:hasEndVolumeNumbering "5"
    ] .
    
## Usage of dct:description, dct:accrualPeriodicity, dct:extend and dc:coverage

[ex_dc]: #ex_dc

The term [dct:description] is recommended to give a description of the chronology. The term [dc:coverage] is recommended to transport the given description if there is one. The term [dct:accrualPeriodicity] is recommended to give information about the frequency with which items are added to the collection. The term [dct:extend] is recommended to give information about the number of units in the chronology.

Given description: ser.1:no.1-ser.1:no.4,ser.2:no.1-ser.2:no.6

    $item ecpo:hasChronology [
        a ecpo:CurrentChronology ;
        dct:hasPart [
            a ecpo:ClosedChronology ;
            ecpo:hasBeginVolumeCaption "ser." ;
            ecpo:hasBeginVolumeNumbering "1" ;
            ecpo:hasBeginIssueCaption "no." ;
            ecpo:hasBeginIssueNumbering "1" ;
            ecpo:hasEndVolumeCaption "ser." ;
            ecpo:hasEndVolumeNumbering "1" ;
            ecpo:hasEndIssueCaption "no." ;
            ecpo:hasEndIssueNumbering "4" ;	
            dct:description "double number issue 2/3"@en ;
            dct:accrualPeriodicity [ rdfs:label "4 numbers per series"@en ] ;
            dct:extent [ rdf:value "3" ] .
        ] ;
        dct:hasPart [
            a ecpo:ClosedChronology ;
            ecpo:hasBeginVolumeCaption "ser." ;
            ecpo:hasBeginVolumeNumbering "2" ;
            ecpo:hasBeginIssueCaption "no." ;
            ecpo:hasBeginIssueNumbering "1" ;
            ecpo:hasEndVolumeCaption "ser." ;
            ecpo:hasEndVolumeNumbering "2" ;
            ecpo:hasEndIssueCaption "no." ;
            ecpo:hasEndIssueNumbering "6" ;
            dct:description "triple number issue 2-4"@en ;
            dct:accrualPeriodicity [ rdfs:label "6 numbers per series"@en ] ;
            dct:extent [ rdf:value "4" ] .
        ] ;
        dct:description "the numbers per series varies"@en ;
        dc:coverage "ser.1:no.1-ser.1:no.4,ser.2:no.1-ser.2:no.6" 
    ] .
    
In this example the number of issues per series varies, which is expressed through the term [dct:description] in the main chronology.

Each subchronology has another [dct:description] which give more detailed information on the parts in textual form.

The subchronologies also contain the term [dct:accrualPeriodicity] which gives a hint about how many numbers a subchronologies consits of and also the term [dct:extent] which gives the exact number of units in the subchronologies. Both terms must have a resource as range. 

The term [dc:coverage] holds the whole source description in once, for what ever reason.

# References

## Normative References

* **[RFC 2119]** S. Bradner: *Key words for use in RFCs to Indicate Requirement Levels*. March 1997 <http://tools.ietf.org/html/rfc2119>.

* **[RFC 2396]** T. Berners-Lee et al.: *Uniform Resource Identifiers (URI): Generic Syntax*. August 1998 <http://tools.ietf.org/html/rfc2396>.