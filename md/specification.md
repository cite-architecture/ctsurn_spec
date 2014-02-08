# The Canonical Text Services URN specification, version @version@ #

**Content**:  This document defines version @version@ of the Canonical Text Services URN.

**Editors**:  Christopher Blackwell and Neel Smith, Center for Hellenic Studies Technical Working Group leads.

**Date**:  February, 2014.

**License**:  This specification is available under the terms of the Creative Commons Attribution-ShareAlike 4.0 International License, <http://creativecommons.org/licenses/by-sa/4.0/deed.en_US>.

## Background ##

 RFC2141 defines the goal of URNs as follows:

> Uniform Resource Names (URNs) are intended to serve as persistent, location-independent, resource identifiers.

The Canonical Text Services URN (CTS URN) scheme defined here closely follows the syntactic requirements of a URN, but extends its goal to provide a system of persistent, *technology-independent* identifiers for texts and passages of texts.   Specificaly, the semantics of the CTS URN scheme are recognized by implementations of the [Canonical Text Services](http://www.homermultitext.org/hmt-docs/specifications/cts/) protocol, but CTS URNs can be used in any system, digital or other, that can parse the syntax of CTS URN values according to the syntax and semantics of this specification. 

## Semantics of a CTS citation ##

There are three major components to a citation with CTS  URN version @version@:  a component identifying a naming authority, a component identifying a work hierarchy, and a component identifying a passage within the identified work.   

The naming authority component is a single identifer;  systems using CTS URNs must be able to resolve this value to a unique URI.

The work component is a hierarchy representing texts as they are cited by scholars.  Conceptually, the work hierarchy partially overlaps with the Functional Requirements for Bibliographic Records (FRBR), but since FRBR aims to model bibliographic entries as they are cataloged by librarians, there are also noteworthy differences.  The work component begins with an identifier for any group of texts that are conventionally cited together in the naming authority's tradition.  Examples could be based on concepts such as "author" (e.g., the works of Mark Twain),  "geographic origin" (e.g., papyri from Oxyrhynchus), or "theme" (e.g., Latin curse tablets).  This identifier *may* be  followed by an identifier for a specific notional work within that group, corresponding to the *work* level of FRBR.  This in turn *may* be followed with an identifier for a specific version of that work, either a translation or an edition, corresponding to the *expression* level of FRBR.  A version identifier *may* be followed by an identifier for a specific exemplar of the version, corresponding to the *item* level of FRBR.  (Note that there is no level of a CTS URN correponding to the FRBR *manifestation*.)

The passage component is a hierarchy of one or more levels expressing a logical citation scheme applying to all versions of a text.  A poem might be cited by the single unit of "poetic line."  A prose work might be cited by a hierarchy such as "book/chapter/section/subsection."  Passage references at any level of the text's citation hierarchy *may* identify either a single citable node or a range indicated by the first and last nodes of the range.

If the work component of the CTS URN is at the version or exemplar level, reference to a single citable node *may* be extended with indexed occurrences of a substring or a range of substrings; in a reference to a range of nodes, either or both of the first and last nodes *may* be extended in the same way.  Indexed substring references are permitted only with URNs at the version or example level because they are inherently language-specific. 

## Syntax of a CTS citation

All URNs begin with the string `urn:` followed by a protocol identifier (the "urn namespace identifier"), followed by a  colon (":", Unicode x003a).  The protocol identifier for the CTS URN is `cts`.  The rest of the CTS URN consists of a CTS namespace, a work component, and a passage component.  

The CTS namespace is separated from the work component by a colon, and the work component is separated from the passage component by a namespace.  A value for the CTS namespace and for the work component is required.  The value of the passage component *may* be a null string; in this case, the work component *must* still be separated from the null string by a colon.

The work component and the passage reference *may* have one than one part, separated by a full stop  (".", Unicode x002e).

The work component consists of one to four parts.  Each part is separated from a following part by a full stop.  A full stop *must not* be appended to the part value if there is no following part.  The value for the first part of the work component is mandatory, and *must* be a valid value for a textgroup in the URN's CTS namespace.  The second part of the work component is optional; its value *must* be a valid value for a notional work within the parent textgroup.  The third part of the work component is allowed if the URN also includes a value for a work, and *must* be a valid value for a version (edition or translation) in the parent notional work.  The fourth part of the work component is allowed if the URN also includes a value for a version, and *must* be a valid value for an exemplar in the parent version.

The passage component *may* be a null string.  It *may* have a non-null value only if the work component includes two or more parts.  The passage component *may* identify either a citable node of the text, or a range of citable nodes.  A

Periods separate second-level hierarchical components of the work identifier and passage reference. Within either of those components, any use of a period as a data value must be escaped. When a passage reference or subreference refers to a range value (defined below), a hyphen separates beginning and ending reference elements. Within those elements, any use of a hyphen as a data value must be escaped. 
The subreference *may* optionally be organized in a multipart structure described below

urn:cts:CTSNAMESPACE:WORK:PASSAGE@SUBREFERENCE

### Valid data characters ###

 The colon must not be used as a data value. 
(":", Unicode x003a).

-
[] but "[" | "]"   are excluded in URNS!
@ is reserved

 
ALSO allow Unicode not normally allowed in URNS? 



CTSNAMESPACE:WORK:PASSAGE


  The first element is a single 

urn name space (required: always cts)cts namespace (required: a value registered in the Center for Hellenic Studies registry of registries)work identifier (required: a value registered in the designated registry) passage reference (required, but possibly empty)subreference (optional)
 The general structure of a CTS URN is therefore 
 urn:cts:CTSNAMESPACE:WORK:PASSAGE:SUBREFERENCE? 
 Periods separate second-level hierarchical components of the work identifier and passage reference. Within either of those components, any use of a period as a data value must be escaped. When a passage reference or subreference refers to a range value (defined below), a hyphen separates beginning and ending reference elements. Within those elements, any use of a hyphen as a data value must be escaped. 
The subreference *may* optionally be organized in a multipart structure described below. 
CTS namespace
 The work citation must include a namespace prefix registered with the CHS namespace Registry. 
Work identifiers
 Work identifiers are formatted as dot-separated components representing at least one of 
 textgroup, work, edition | translation, exemplar 
 
Values must be registered with the registry identified by the CTS namespace component. 
 Example: The namespace Registry identifies the CHS Canon of ancient Greek literary texts with the namespace greekLit; the CHS Canon in turn identifies the textgroup "Homer" with the ID tlg0012 and the work Iliad with the ID tlg001. A URN reference to the Iliad would therefore be expressed as urn:cts:greekLit:tlg0012.tlg001 
Passage citations
Passage citations *may* refer either to individual passages or to ranges within a work. 
 A reference to an individual passage is formatted as dot-separated components representing one or more levels of the citation hierarchy defined in a CTS TextInventory for that work. 
 A reference to a range is formatted as two passage references separated by a hyphen. 
 Examples: Extending the previous example, a reference to line 10 of book 1 of the Iliad would be urn:cts:greekLit:tlg0012.tlg001:1.10. A reference to lines 10-20 of the same book would be: 
 urn:cts:greekLit:tlg0012.tlg001:1.10-1.20 
Subreferences
Subreferences identify spans within a single citation unit using indexed substrings. 
The subreference consists of a literal string, and an optional 0-origin index value, separated from the literal string by a colon. The default value of the index is 0, so if we extended the previous example to refer to a specific translation of the Iliad identified as mth-01, the following two URNs would be semantically equivalent: 
 urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1:Achilles:0 
 urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1:Achilles 
In both cases, the reference is to the first occurence of the string "Achilles" in line 1 of book 1. 
Just as pairs of passage references may be joined with a hyphen to identify a range, pairs of subreferences may be joined with a hyphen to identify a continuous span of text within a passage reference. 
Examples:
 urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1-10:Achilles-Atreus 
This identifies a span of text running from the first occurrence of the string "Achilles" to the first occurrence of the string "Atreus" in lines 1-10 of the specified translation of Iliad. 
 urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1-10:Achilles-the:1 
 This identifies a span of text running from the first occurrence of the string "Achilles" to the second occurrence of the string "the" in lines 1-10 of the specified translation of Iliad


 -----

## Semantics of a CTS URN

CTS URNs refer to a passage of text in terms of two hierarchies.The first hierarchy identifies a text in a model similar to the conceptual model of the
Functional Requirements for Bibliographic Records (FRBR). (For an introduction to FRBR,
see this [basic reading list][1].  Where the conceptual model of FRBR aims to represent bibliographic entries as they are cataloged by librarians, however, CTS URNs aim to model works as they are cited by scholars.
[1]: http://www.ifla.org/VII/s13/frbr/readings.htm














CTS URNs organize *works* in *text groups*.  Text groups have no direct parallel in FRBR, and
do not have a predefiend semantic range. Instead, they associate works, according to traditional
citation practice, in groups with various meanings.  The text group may reflect authorship (e.g., a work entitled
*Huckleberry Finn* might belong to a group named "Mark Twain"), or may represent some other kind of corpus (e.g., a work numbered 1 belonging to a group named "Federalist Papers"). Within a text group, a CTS URN's work  is a conceptual entity, like the FRBR work: it is an abstract idea of the content expressed in all versions of a work, in the original language or in translation. The work may optionally be identified with 
increasing specificity as *versions* (translation or edition), or *exemplars* (individual physical copies).
The CTS URN's version corresponds to the "expression" in the FRBR model, while exemplars correspond to "items" in FRBR parlance.

The second hierarchy in a CTS URN refers to a passage expressed in a logical citation scheme. While the nature of this hierarchy depends on the specific work referred to by a CTS URN, many texts will fall into one of a few common citation schemes.  Prose works might be cited by chapter and section, or book, chapter and section, for example, or poems might be cited by line, stanza and line, or book and line, for example.

Within the smallest citation unit (such as a paragraph or section for a prose work, or line of verse for a poem), CTS URNs can further specify a span of text with a *subreference*.  Subreferences identify indexed substrings, or a range between an indexed pair of substrings. Because subreferences are inherently language-specific, they are only valid when the work identifier is specified to the level of a version (edition or translation), or exemplar.

## Resolving CTS URNs

By "resolving CTS URNs," we mean specifically the symmetric problems of how we determine what work a CTS URN refers to, and how we determine what URN values to use to refer to a work.  (The further question of how to *retrieve* a passage of text referred to by a CTS URN is beyond the scope of the CTS URN's location-independent identifiers:  see instead the related topic of Canonical Text Services.)  

resolving internet domain names to numeric addresses, and vice versa, and it is unsurprising that CTS URNs use analogous mechanisms solve them.  Like the internet domain name system, CTS URNs must guarantee that the values used to identify a work are globally unique. Like DNS, CTS URNs achieve this by delegating responsibility for managing authoritative registries.  Like a top-level DNS server, CTS URNs depend ultimately on a top-level registry listing what further CTS registries are responsible for specific domains. This top-level registry is housed in the Scaife Digital Library, a durable digital repository.  (Further links to SDL will be added here when they are available.)


Just as a university or business can manage domain names within its own domain name space, an organization can manage a registry of canonical identifiers for texts within its domain. So the top-level registry assigns the identifier 
`greekLit` to a registry maintained at the Center for Hellenic Studies covering ancient Greek transmitted by manuscript copying.  Other registries could be added to cover specific collections of epigraphic or papyrological texts.

##Syntax of a CTS URN

URNs always begin with the string `urn:` followed by a protocol identifier.  We use the identifier `cts` for our protocol.  

Colons separate the top-level elements of a CTS URN:  any use of a semicolon as a data value must therefore be
escaped. The top-level elements are: 
  
- urn name space (required:  always `cts`)
- cts namespace (required:  a value registered with the Scaife Digital Library list of CTS namespaces)
- work identifier (required:  a value registered in the designated registry)
- passage reference (optional)
- subreference (optional)

The general structure of a CTS URN is therefore

`urn:cts:CTSNAMESPACE:WORK:PASSAGE:SUBREFERENCE?`


Periods separate second-level hierarchical components of the work identifier and passage reference.  Within either of those
components, any use of a period as a data value must be escaped. 

### CTS namespace

The work citation must include a namespace prefix registered with the CHS namespace Registry.

### Work identifiers

Work identifiers are formatted as dot-separated components representing at least one of

    textgroup, work, edition | translation, exemplar

Values must be registered with the registry identified by the CTS namespace component.

*Example*:  The namespace Registry identifies the
CHS registry of ancient Greek transmitted by manuscript copying with the namespace
`greekLit`;  the CHS registry in turn identifies the textgroup "Homer" with the ID `tlg0012` and the work *Iliad* with the ID `tlg001`. A URN reference to the *Iliad*  would therefore be expressed as `urn:cts:greekLit:tlg0012.tlg001`.


### Passage citations

Passage citations may refer either to individual passages or to ranges within a work.

A reference to an individual passage is formatted as dot-separated components representing one or more levels of the citation hierarchy defined in a CTS TextInventory for that work.

A reference to a range is formatted as two passage references separated by a hyphen.

CTS accommodates works with multiple citation schemes.  Because different parts of a work might have citation schemes with different depths to their citation  hierarchy, it is essential to allow ranges to include references to beginning and end points at different depths in different citation schemes.  To avoid ambiguity, each of the two passage references in a range expression must be given fully:  implicit context, as is commonly used in informal normal, is not permitted.  (E.g., while common informal usage allows expressions like "1.10-20" to mean "lines 10-20 of book 1," a CTS URN would require
an passage expression like "1.10-1.20".)

*Examples*: Extending the previous example, a reference to line 10 of book 1 of the *Iliad* would be
`urn:cts:greekLit:tlg0012.tlg001:1.10`.  A reference to lines 10-20 of the same book would be:

    urn:cts:greekLit:tlg0012.tlg001:1.10-1.20

### Subreferences

Subreferences identify spans within a single citation unit using indexed substrings.

h2. Overview

A subreference points to a string of characters within
a leaf-level citation node.  While CTS URN references are
abstract, and apply to any version of a text, subrefernces
expressed in terms of strings of characters are inherently tied
to a specific language.  They are only valid on URNs that include
work references at the version or exemplar level.


h2. Syntax

Syntactically, substrings are set off form the passage reference
they qualify by the pound sign "#" (recalling the use of the same
character in URL references to refer to loations within a URL).
A subreference may contain two parts:  a literal string,
and an index value.
If an index value is included, it is enclosed in square brackets "\[\]"
and follows any substring.  The index value must evalute to a positive integer.

h2. Semantics

At least one of the two parts of the subreference must be present.
If both a substring and an index, @n@, are included, the
reference points to the @n@th occurrence of the substring
in the cited node.
If a substring is given, but no index value, then it is taken to mean
the first occurrence of the substring in the cited node.
If an index is given, but no substring, it is taken to mean the
@n@th code point in the cited node.
Index values are 1-origin values.

h2. Examples

*\[1\]* The following two URNs are equivalent:

@urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1#Achilles\[1\]@

@urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1#Achilles@

In both cases, the reference is to the first occurence of the string "Achilles" in line 1 of book 1.

*\[2\]* A subreference spanning leaf citation nodes:

@urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1#Achilles-1.10#Atreus@

This identifies a span of text running from the first occurrence of
the string "Achilles" in book 1, line 1 of a version of
the _Iliad_, to the first occurrence of the string "Atreus"
in book 1, line 10 of the same translation.

*\[3\]* Indexed substrings

@urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1#Achilles-1.10#the\[2\]@

This identifies a span of text running from the first occurrence of
the string "Achilles" in book 1, line 1,
to the second occurrence of the string "the"
in book 1, line 10 of the specified translation of _Iliad_.  



*\[4\]* Indexed code points

@urn:cts:greekLit:tlg0012.tlg001.mth-01:1.1#\[4\]-1.1#\[6\]@

This URN refers to the fourth through sixth code points (inclusive)
of book 1, line 1 of the _Iliad_, in a specified version.
Note that the meaning of this will
depend both on the reading of the specific version, and the
digital character encoding of the specific version.
In particular, for non-ASCII characters in UTF-8,
it is worth emphasizing that character data values in a programming
language may not be equivalent to Unicode code points
in that text.




## Links

- Maven settings for using the release version of this specification and its schemas from a maven client: 
    - group: `org.homermultitext`
    - artifact: `ctsurn-spec`
    - version: `3.0`
-  Nexus repository to proxy this release:  <http://beta.hpcc.uh.edu/nexus/content/repositories/releases>
-  Known mirrors of this specification:
    - from the Homer Multitext project:  <http://www.homermultitext.org/hmt-docs/specifications/ctsurn>
    - from Furman University: <http://folio.furman.edu/projects/citedocs/ctsurn>
    - from the College of the Holy Cross:  <http://shot.holycross.edu/hmt-docs/specifications/ctsurn>
- RFC2141, "URN Syntax": <http://www.ietf.org/rfc/rfc2141.txt> 
- The Canonical Text Services protocol specification: <http://www.homermultitext.org/hmt-docs/specifications/cts> 
- Report of the IFLA Study Group on the Functional Requirements for Bibliographic Records (FRBR): <http://www.ifla.org/publications/functional-requirements-for-bibliographic-records>

## Acknowledgments ##

The authors would especially like to acknowledge contributions from Gabriel Weaver in developing the URN notation.
