
> Uniform Resource Names (URNs) are intended to serve as persistent, location-independent, resource identifiers.

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


