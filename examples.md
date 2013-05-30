# Examples for Enumeration and Chronology of Periodicals Ontology (ECPO)

In the following examples a hypothetical document ```:Holding``` describes a holding of a periodical held by someone.

## Statement for a running chronology

	:Holding ecpo:hasChronology ecpo:Running .
	
This statement just says that a document has a running chronology without giving futher information which units are held.

## Statement for a closed chronology

    :Holding ecpo:hasChronology ecpo:Closed .
	
This statement just says that a document has a closed chronology without giving futher information which units are held.

## Description of a running Chronology

Given description: v.26,issue 1-

    :Holding ecpo:hasChronology [
		a ecpo:RunningChronology ;
		ecpo:hasBeginVolumeCapation "v." ;
	    ecpo:hasBeginVolumeNumbering "26" ;
		ecpo:hasBeginIssueCapation "issue" ;
		ecpo:hasBeginIssueNumbering "1" 
	] .
		
## Description of a closed Chronology

Given description: v.26,issue 1-v.31, issue 6

    :Holding ecpo:hasChronology [
	    a ecpo:ClosedChronology ;
		ecpo:hasBeginVolumeCapation "v." ;
	    ecpo:hasBeginVolumeNumbering "26" ;
		ecpo:hasBeginIssueCapation "issue" ;
		ecpo:hasBeginIssueNumbering "1" ;
		ecpo:hasEndVolumeCapation "v." ;
	    ecpo:hasEndVolumeNumbering "31" ;
		ecpo:hasEndIssueCapation "issue" ;
		ecpo:hasEndIssueNumbering "6" 
	] .

## Description of a closed Chronology with temporal information

Given description: (2001:Jan.-2006:June)=no.320-no.385

    :Holding ecpo:hasChronology [
	    a ecpo:ClosedChronology ;
		ecpo:hasBeginTemporal "2001" ;
		ecpo:hasBeginMonth "Jan." ;
		ecpo:hasBeginIssueCapation "no." ;
		ecpo:hasBeginIssueNumbering "320" ;
		ecpo:hasEndTemporal "2006" ;
		ecpo:hasEndMonth "June" ;
		ecpo:hasEndIssueCapation "no." ;
		ecpo:hasEndIssueNumbering "385" 
	] .

## Description of a running chronology with subchronologies

Given description: v.5:no.1(1975:spring)-v.7:no.4(1977:autumn),v.8:no.2(1978:winter)-

    :Holding ecpo:hasChronology [
		a ecpo:RunningChronology ;
		dcterms:hasPart [
		    a ecpo:ClosedChronology ;
		    ecpo:hasBeginVolumeCapation "v." ;
	        ecpo:hasBeginVolumeNumbering "5" ;
		    ecpo:hasBeginIssueCapation "no." ;
		    ecpo:hasBeginIssueNumbering "1" ;
		    ecpo:hasBeginTemporal "1975" ;
		    ecpo:hasBeginTemporalExtension "spring" ;
		    ecpo:hasEndVolumeCapation "v." ;
	        ecpo:hasEndVolumeNumbering "7" ;
		    ecpo:hasEndIssueCapation "no." ;
		    ecpo:hasEndIssueNumbering "4" ;
		    ecpo:hasEndTemporal "1977" ;
		    ecpo:hasEndTemporalExtension "autumn" 		   
		] ;
		dcterms:hasPart [
		    a ecpo:ClosedChronology ;
		    ecpo:hasBeginVolumeCapation "v." ;
	        ecpo:hasBeginVolumeNumbering "8" ;
		    ecpo:hasBeginIssueCapation "no." ;
		    ecpo:hasBeginIssueNumbering "2" ;
		    ecpo:hasBeginTemporal "1978" ;
		    ecpo:hasBeginTemporalExtension "winter"	   
		] .
		
In this example the main chronology is made as an instance of ```RunningChronology``` for the sake of expressivity. It also had been made as an instance of ```Chronology```. But this way it is easier to tell if the whole chronology is running or not.
		
## Description of a chronology in an itemized way and comments

Given description: v.1 v.2 v.2[i.e. 3] v.6
In this example Volume 3 was incorrectly numbered by the publisher.

    :Holding ecpo:hasChronology [
	    a ecpo:Chronology ;
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "1"
		] ;		
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "2"
		] ;		
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "2" ;
			ecpo:hasItemizedVolumeExtension "[i.e. 3]" ;
			ecpo:hasItemizedComment "Volume 3 was incorrectly numbered by the publisher"@en
		] ;
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "6"
		]
	] .
	
The property ```hasItemizedVolumeExtension``` is described as "A textual descrimination of the volume". In this example it is used to transport the correction statement for the wron volume numbering. The expression with the property ```hasItemizedComment``` is optional.

## Description of a gap in the chronology

As in the example above the volumes v.4 and v.5 are missing. There are two possibilities to express this.

### Itemized way

    :Holding ecpo:hasChronologyGap [
		a ecpo:Chronology ;
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "4"
		] ;		
		dcterms:hasPart [
			a ecpo:Chronology ;
			ecpo:hasItemizedVolumeCaption "v." ;
			ecpo:hasItemizedVolumeNumbering "5"
		]
	] .
	
### Range

    :Holding ecpo:hasChronologyGap [
		a ecpo:Chronology ;
		ecpo:hasBeginVolumeCapation "v." ;
	    ecpo:hasBeginVolumeNumbering "4" ;
		ecpo:hasEndVolumeCapation "v." ;
	    ecpo:hasEndVolumeNumbering "5"	
	] .
	
## Usage of dcterms:description and dc:coverage

The term ```dcterms:description``` is recommended to give a description of the hole chronology. The term ```dc:coverage``` is recommended to transport the given description if there is one.

Given description: ser.1:no.1-ser.1:no.4,ser.2:no.1-ser.2:no.6

    :Holding ecpo:hasChronology [
		a ecpo:RunningChronology ;
		dcterms:hasPart [
		    a ecpo:ClosedChronology ;
		    ecpo:hasBeginVolumeCapation "ser." ;
	        ecpo:hasBeginVolumeNumbering "1" ;
		    ecpo:hasBeginIssueCapation "no." ;
		    ecpo:hasBeginIssueNumbering "1" ;
		    ecpo:hasEndVolumeCapation "ser." ;
	        ecpo:hasEndVolumeNumbering "1" ;
		    ecpo:hasEndIssueCapation "no." ;
		    ecpo:hasEndIssueNumbering "4" ;	
            dcterms:description "4 numbers"@en		
		] ;
		dcterms:hasPart [
		    a ecpo:ClosedChronology ;
		    ecpo:hasBeginVolumeCapation "ser." ;
	        ecpo:hasBeginVolumeNumbering "2" ;
		    ecpo:hasBeginIssueCapation "no." ;
		    ecpo:hasBeginIssueNumbering "1" ;
		    ecpo:hasEndVolumeCapation "ser." ;
	        ecpo:hasEndVolumeNumbering "2" ;
		    ecpo:hasEndIssueCapation "no." ;
		    ecpo:hasEndIssueNumbering "6" ;	
			dcterms:description "6 numbers"@en
		] ;
		dcterms:description "the numbers per series varies"@en ;
		dc:coverage "ser.1:no.1-ser.1:no.4,ser.2:no.1-ser.2:no.6" 
	] .
	
In this example the number of issues per series varies, which is expressed through the term ```dcterms:description``` in the main chronology. Each subchronology has another ```dcterms:description``` which specifies the exact number of the series.

The term ```dc:coverage``` holds the whole source description in once, for what ever reason.