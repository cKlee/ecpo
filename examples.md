In the following examples a hypothetical copy of a document ```$item``` describes a holding of a periodical held by someone.

## Statement for a current chronology

[excurrent]: #excurrent

    $item ecpo:hasChronology ecpo:Current .

This statement just says that an item has a [current chronology](#currentchronology) without giving futher information which units are held.

## Statement for a closed chronology

[exclosed]: #exclosed

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

[exhaspart]: #exhaspart

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
    
The property [hasItemizedVolumeExtension] is described as "A textual descrimination of the volume". In this example it is used to transport the correction statement for the wron volume numbering. The expression with the property [dct:description](#dctdescription) is optional.

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

[exdc]: #exdc

The term [dct:description](#dctdescription) is recommended to give a description of the chronology. The term [dc:coverage](#dccoverage) is recommended to transport the given description if there is one. The term [dct:accrualPeriodicity] is recommended to give information about the frequency with which items are added to the collection. The term [dct:extend](#dcextend) is recommended to give information about the number of units in the chronology.

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
    
In this example the number of issues per series varies, which is expressed through the term [dct:description](#dctdescription) in the main chronology.

Each sub-chronology has another [dct:description](#dctdescription) which give more detailed information on the parts in textual form.

The sub-chronologies also contain the term [dct:accrualPeriodicity](#dctaccrualPeriodicity) which gives a hint about how many numbers a sub-chronologies consits of and also the term [dct:extent](#dctextent) which gives the exact number of units in the sub-chronologies. Both terms must have a resource as range. 

The term [dc:coverage](#dccoverage) holds the whole source description in once, for what ever reason.
