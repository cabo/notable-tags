---
v: 3

title: >
  Notable CBOR Tags
abbrev: Notable CBOR Tags
docname: draft-bormann-cbor-notable-tags-latest
# date: 2025-02-12

keyword: Internet-Draft
cat: info
submissiontype: IETF

author:
  - name: Carsten Bormann
    org: Universität Bremen TZI
    street: Postfach 330440
    city: Bremen
    code: D-28359
    country: Germany
    phone: +49-421-218-63921
    email: cabo@tzi.org
contributor:
  - name: Peter Occil
    email: poccil14 at gmail dot com
    contribution: |
      Peter Occil registered tags 30, 264, 265, 268–270
      ({{advanced-arithmetic}}), 38, 257, 266 and 267
      ({{domain-specific}}), and contributed much of the text about
      these tags in this document.
  - name: Duncan Coutts
    email: duncan@well-typed.com
  - name: Michael Peyton Jones
    email: me@michaelpj.com

  - name: Jane Doe
    org: To do
    contribution: |
      Further contributors will be listed here as text is added.

      Please stay tuned.

normative:
  STD63:
    -: utf8
#    =: RFC3629
  STD94:
    -: cbor
#    =: RFC8949
  IANA.cbor-tags: tags
  IANA.cose: cose-reg
  IANA.named-information: ni
  RFC8610: cddl
#    ann: foo
  STD96: cose # includes RFC9052 and RFC9338
  RFC9053: cose-alg
  RFC9054: cose-hash
  RFC9360: certhash

informative:
  RFC8152:
  BCP47:
  W3C-STRINGS-BIDI:
    target: https://www.w3.org/International/articles/strings-and-bidi/
    title: Strings and bidi
    date: 2017-07-31
  W3C-BIDI-USE-CASES:
    target:   https://www.w3.org/International/articles/lang-bidi-use-cases/
    title: Use cases for bidi and language metadata on the Web
    date: 2021-05-06
  W3C-UBA-BASICS:
    target: https://www.w3.org/International/articles/inline-bidi-markup/uba-basics
    title: Unicode Bidirectional Algorithm basics
    date: 2016-08-09
  W3C-SIMPLE-RUBY:
    target: https://www.w3.org/TR/simple-ruby/
    title: W3C Rules for Simple Placement of Japanese Ruby
    date: 2020-06-09
    rc: W3C First Public Working Draft
  HTML:
    target: https://html.spec.whatwg.org
    title: HTML — Living Standard
    author:
    - org: WHATWG
    date: false

  RFC2045: mime
  RFC4122: uuid
  RFC9562: uuid-new
  RFC7049: orig
  RFC8742: seq
  RFC7493: ijson
  RFC8259: json
  I-D.ietf-cbor-time-tag: time-tag
  RFC9485: iregexp
  RFC9290: probdet
  RFC6991: yang-types
  RFC9254: yang-cbor
  RFC9542: mac
  RFC9164: ip
  I-D.bormann-cbor-numbers: numbers
  I-D.bormann-cbor-yang-standin: standin
  C:
    target: https://www.iso.org/standard/74528.html
    title: Information technology — Programming languages — C
    author:
    - org: International Organization for Standardization
    date: 2018-06
    seriesinfo:
      ISO/IEC: 9899:2018
  Cplusplus20:
    target: https://isocpp.org/files/papers/N4860.pdf
    title: Programming languages — C++
    author:
    - org: International Organization for Standardization
    date: 2020-03
    rc:
      ISO/IEC JTC1 SC22 WG21 N4860
  IEEE754:
    target: https://ieeexplore.ieee.org/document/8766229
    title: IEEE Standard for Floating-Point Arithmetic
    author:
    - org: IEEE
    date: false
    seriesinfo:
      IEEE Std: 754-2019
      DOI: 10.1109/IEEESTD.2019.8766229

--- abstract

The Concise Binary Object Representation (CBOR, RFC 8949) is a data
format whose design goals include the possibility of extremely small
code size, fairly small message size, and extensibility without the
need for version negotiation.

In CBOR, one point of extensibility is the definition of CBOR tags.
RFC 8949's original edition, RFC 7049, defined a basic set of 16 tags as well
as a registry that can be used to contribute additional tag
definitions {{-tags}}.
Since RFC 7049 was published, at the time of writing some 190
definitions of tags and ranges of tags have been added to that
registry.

<!-- TAG_REPORT_SQUASH_RANGES=1 tag-report.rb minus the 16 -->

The present document provides a roadmap to a large subset of these tag
definitions.  Where applicable, it points to an IETF standards or
standard development document
that specifies the tag.  Where no such document exists, the intention
is to collect specification information from the sources of the
registrations.  After some more development, the present document is
intended to be useful as a reference document for the IANA
registrations of the CBOR tags the definitions of which have been
collected.

--- note_Note_to_Readers

This is an individual submission to the CBOR working group of the
IETF, <https://datatracker.ietf.org/wg/cbor/about/>.
Discussion currently takes places on the github repository
<https://github.com/cabo/notable-tags>.
If the CBOR WG believes this is a useful document, discussion is
likely to move to the CBOR WG mailing list and a github repository at
the CBOR WG github organization, <https://github.com/cbor-wg>.

The current version is true work in progress; some of the sections
haven't been filled in yet, and in particular, permission has not been
obtained from all authors of registered tag definitions to copy over their text.


--- middle

Introduction        {#intro}
============

(TO DO, expand on text from abstract here; move references here and
neuter them in the abstract as per {{Section 4.3 of ?RFC7322}}.)

The selection of the tags presented here is somewhat arbitrary;
considerations such as how wide the scope and area of application of a
tag definition is combine with an assessment how "ready to use" the
tag definition is (i.e., is the tag specification in a state where it
can be used).

This document can only be a snapshot of a subset of the current registrations.
The most up to date set of registrations is always available in the
registry "{{cbor-tags (CBOR Tags)<IANA.cbor-tags}}" {{IANA.cbor-tags}}.

Terminology         {#terms}
------------

The definitions of {{-cbor}} apply.
Specifically: The term "byte" is used in its now customary sense as a synonym for
"octet"; "byte strings" are CBOR data items carrying a sequence of
zero or more (binary) bytes, while "text strings" are CBOR data items carrying a
sequence of zero or more Unicode scalar values (code points that can
be part of a string of Unicode characters), encoded in UTF-8 {{-utf8}}.
Where bit arithmetic is explained, this document uses the notation
familiar from the programming language C ({{C}}, including C++14's `0bnnn`
binary literals {{Cplusplus20}}), except that superscript notation
(example for two to the power of 64: 2<sup>64</sup>) denotes exponentiation; in
the plain text version of this document, superscript notation is
rendered in paragraph text by C-incompatible surrogate notation as
seen in this example.
Ranges expressed using `..` are inclusive of the limits given.
<!-- , and in display math by a crude plain text representation. -->
Type names such as "int", "bigint" or "decfrac" are taken from
{{Section D of -cddl}}, the Concise Data Definition Language (CDDL).

[^cpa]

[^cpa]: RFC-Editor: This document uses the CPA (code point allocation)
      convention described in [I-D.bormann-cbor-draft-numbers].  For
      each usage of the term "CPA", please remove the prefix "CPA"
      from the indicated value and replace the residue with the value
      assigned by IANA; perform an analogous substitution for all other
      occurrences of the prefix "CPA" in the document.  Finally,
      please remove this note.


# RFC 7049 (original CBOR specification)

{{-orig}} defines a number of tags that are listed here for
convenience only.

| Tag number | Tag content  | Short Description                         | Section of RFC 7049 |
|          0 | UTF-8 string | Standard date/time string                 |               2.4.1 |
|          1 | multiple     | Epoch-based date/time                     |               2.4.1 |
|          2 | byte string  | Positive bignum                           |               2.4.2 |
|          3 | byte string  | Negative bignum                           |               2.4.2 |
|          4 | array        | Decimal fraction                          |               2.4.3 |
|          5 | array        | Bigfloat                                  |               2.4.3 |
|         21 | multiple     | Expected conversion to base64url encoding |             2.4.4.2 |
|         22 | multiple     | Expected conversion to base64 encoding    |             2.4.4.2 |
|         23 | multiple     | Expected conversion to base16 encoding    |             2.4.4.2 |
|         24 | byte string  | Encoded CBOR data item                    |             2.4.4.1 |
|         32 | UTF-8 string | URI                                       |             2.4.4.3 |
|         33 | UTF-8 string | base64url                                 |             2.4.4.3 |
|         34 | UTF-8 string | base64                                    |             2.4.4.3 |
|         35 | UTF-8 string | Regular expression                        |             2.4.4.3 |
|         36 | UTF-8 string | MIME message                              |             2.4.4.3 |
|      55799 | multiple     | Self-describe CBOR                        |               2.4.5 |
{: #origtags title="Tag numbers defined in RFC 7049"}

## Tags Related to Those Defined in RFC 7049 {#related-tags}

Separately registered tags that are directly related to the tags
predefined in RFC 7049 include:

* Tag 63, registered by this document ({{iana}}), is a parallel to tag 24, with
  the single difference that its byte string tag content carries a
  CBOR Sequence {{-seq}} instead of a single CBOR data item.

* {: #expected-tags} Tag CPA108, requested to be registered by this document ({{iana}}), is
  a parallel to tag 23, with the single difference that the
  hexadecimal form uses lowercase instead of uppercase letters. [^cpa]

  <!-- {:aside} -->
  <!-- This should be an aside, but xml2rfc's grammar doesn't allow -->
  <!-- that as of 3.27.0. -->
  > >
    Note that tag 23 has a serialization that is one byte shorter than
    tag CPA108, so if all else is equal, tag 23 (and thus upper case
    hex) would be chosen as it is slightly more efficient than tag CPA108.
    However, designers of CBOR protocols that use one of these tags
    often have reason to prefer lowercase hex in the application they
    are trying to be compatible with, in which case CPA108 provides a
    solution that is only one byte more expensive.

* Tag 257, registered by Peter Occil with a specification in
  <http://peteroupc.github.io/CBOR/binarymime.html>, is a parallel to
  tag 36, except that the tag content is a byte string, which
  therefore can also carry binary MIME messages as per {{-mime}}.

* Tag 21065, having been registered by this document ({{iana}}), is a parallel to tag 35, with
  the difference that its text string tag content carries an
  I-Regexp regular expression {{-iregexp}} instead of a regexp of a
  more unspecified flavor.
  Companion tag 21066, having been registered by Joe Hildebrand with a
  specification in
  <https://github.com/hildjj/cbor-specs/blob/main/regexp.md>, is the
  equivalent for JavaScript (ECMA262), but besides the regular
  expression itself also can include the regular expression flags
  as a separate item.

## Tags from RFC 7049 not listed in RFC 8949 {#tag35}

{{Appendix G.3 of RFC8949@-cbor}}
states:

{:quote}
>
   Tag 35 is not defined by this document; the registration based on the
   definition in RFC 7049 remains in place.

The reason for this exclusion is that the definition of Tag 35 in
{{Section 2.4.4.3 of -orig}}, leaves too much open to ensure interoperability:

{:quote}
>
  Tag 35 is for regular expressions in Perl Compatible Regular
  Expressions (PCRE) / JavaScript syntax \[ECMA262].

Not only are two partially incompatible specifications given for the
semantics, JavaScript regular expressions have also developed
significantly within the decade since JavaScript 5.1 (which was
referenced as "ECMA262" by {{-orig}}),
making it less reliable to assume that a producing application will
manage to stay within that 2011 subset.

Nonetheless, the registration is in place, so it is available for
applications that simply want to mark a text string as being a regular
expression roughly of the PCRE/Javascript flavor families.
See also Tag 21065 and 21066 above.

# Security

A number of CBOR tags are defined in security specifications that make
use of CBOR.

## COSE

CBOR Object Signing and Encryption (COSE) is defined in a number of RFCs.
{{RFC8152}} was the initial specification, set up the registries, and
populated them with an initial set of assignments.
A revision split this specification into the data
structure definitions ({{RFC9052}}), an Internet Standard {{STD96}}, and a
separate document defining the representation for the algorithms
employed {{RFC9053}}, which is expected to be updated more frequently
than the COSE format itself.
{{RFC9054}} added a separate set of algorithms for cryptographic hash
functions (Hash functions have been a component of some {{RFC9053}} combined
algorithms but weren't originally assigned separate codepoints themselves).
A revised COSE counter signature structure was defined in {{RFC9338}}, another part
of {{STD96}}; this also defines a tag for these.

| Tag number | Tag content           | Short Description                               |
|         16 | COSE_Encrypt0         | COSE Single Recipient Encrypted Data Object     |
|         17 | COSE_Mac0             | COSE Mac w/o Recipients Object                  |
|         18 | COSE_Sign1            | COSE Single Signer Data Object                  |
|         19 | COSE_Countersignature | COSE standalone V2 countersignature ({{RFC9338}}) |
|         96 | COSE_Encrypt          | COSE Encrypted Data Object                      |
|         97 | COSE_Mac              | COSE MACed Data Object                          |
|         98 | COSE_Sign             | COSE Signed Data Object                         |
{: #cosetags title="Tag numbers defined in RFC9052, COSE, and RFC 9338"}

### Tags for Bare Hash Values {#hashtags}

{{RFC9054}} does not define CBOR tags for cryptographic Hash values; it rightly notes
that Hash values are often used in structures that are
application-specific and should be defined with those applications.

However, there are many cases where just a bare hash value is
required, and for these cases common tags are useful.
In one use case, these tags occur in a data structure that is
specified to indicate elision by using one of these tags as an
alternative to some other data structure.
To enable agility, tags need to indicate the hash function used,
preferably using the COSE algorithms registry as populated by
{{RFC9054}}.

{:aside}
>
(Note that there is another registry, "{{hash-alg (Named Information
Hash Algorithm Registry)<IANA.named-information}}"
{{IANA.named-information}}, that also defines numbers for some hash algorithms.
We are not using this registry here, as more recent entries seem to
have stopped assigning numbers.
If desired, tags that employ this registry could be added later.)

The codepoint range available for the COSE algorithms registry is
large, but the most likely range to be used for standard Hash
functions is "Integer values between -256 and 255", which have the
registry policy "Standards Action With Expert Review" ({{Section 16.4
of RFC8152}}, Registry "{{algorithms (COSE Algorithms)<IANA.cose}}" {{IANA.cose}}).

To this end, the present document registers a range of 512 tags from
18300 to 18811 (inclusive), paralleling the algorithm identifier
range of `-256 .. 255` (inclusive).
The tag number for COSE algorithm number N is then defined to be
`18556+N`, except for `N = 0` (see below).
The tag value is a CBOR byte string, with the exception `N = 0`.

For example, in {{IANA.cose}} SHA-256 has the COSE algorithm identifier
`-16`.
This is in the range `-256 .. 255` (inclusive range).
Therefore, tag 18540 (`= 18556 + (-16)`) is the tag for a byte string
containing a SHA-256 hash.

As a special case, there is one exception: Tag 18556 (`= 18556 + 0`)
stands for the combination of a an explicit numeric COSE algorithm
identifier with a hash value in an array, analogous to the use of
`COSE_CertHash` in {{RFC9360}}:

~~~ cddl
Standard_COSE_Hash<alg, value> =
    #6.<hashmiddle .plus (alg .within directhash)>(value)
General_COSE_Hash<alg, value> = #6.<hashmiddle>([
    hashAlg: alg .within (int .ne directhash  / tstr),
    hashValue: value .within bstr ])
hashmiddle = 18556
directhash = (-256 .. -1) / (1 .. 255)
~~~
{: #hashcddl title="Generic CDDL for Tags for Bare Hash Values"}

An example for the SHA-256 hash of "hello world" in CBOR diagnostic
notation:

~~~ cbor-diag
18540(
 h'b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9')
~~~

The same in CBOR pretty printed hex:

~~~ cbor-pretty
d9 486c                                 # tag(18540)
   58 20                                # bytes(32)
      b94d27b9934d3e08a52e52d7da7dabfac484efe37a5380ee9088f7ace2efcde9
~~~
{: post="fold"}

As none has been registered, no real example can be given for a hash
algorithm with an identifier not in the standard range, but if
`-4711` were such an identifier, a hash with an explicit algorithm
number could look like:

~~~ cbor-diag
18556([-4711, h'1234123412341234123412341234123412341234'])
~~~

Note that not all tags assigned in this section do parallel an
algorithm that is a cryptographic hash algorithm.
Where this is not the case, there currently is no defined semantics
for this tag, but the tags are assigned anyway.
The semantics of tags that parallel algorithm assignments other than
for cryptographic hash functions could be defined by a future version
of this specification.

Note also that the cryptographic hashes in the content of the tag are
not protected; any further protection (confidentiality, integrity)
needs to be provided in the surrounding data structure, storage
system, or communication channel.

## RFC 8392 (CWT)

{{!RFC8392}} defines the CBOR Web Token (CWT), making use of COSE to
define a CBOR variant of the JOSE Web Token (JWT), {{?RFC7519}}, a
standardized security token that has found use in the area of web
applications, but is not technically limited to those.

| Tag number | Tag content          | Short Description    |
|         61 | CBOR Web Token (CWT) | CBOR Web Token (CWT) |
{: #cwttags title="Tag number defined for RFC 8392 CBOR Web Token (CWT)"}

# CBOR-based Representation Formats

Representation formats can be built on top of CBOR.

## YANG-CBOR

YANG {{?RFC7950}} is a data modeling language originally designed in
the context of the Network Configuration Protocol (NETCONF)
{{?RFC6241}}, now widely used for modeling management and
configuration information.  {{?RFC7950}} defines an XML-based
representation format, and {{?RFC7951}} defines a JSON-based
{{-json}} representation format for YANG.

YANG-CBOR {{-yang-cbor}} is a representation format for
YANG data in CBOR.

| Tag number | Tag content                              | Short Description                 | Section of YANG-CBOR |
|         43 | byte string                              | YANG bits datatype                |                  6.7 |
|         44 | unsigned integer                         | YANG enumeration datatype         |                  6.6 |
|         45 | unsigned integer or text string          | YANG identityref datatype         |                 6.10 |
|         46 | unsigned integer or text string or array | YANG instance-identifier datatype |                 6.13 |
|         47 | unsigned integer                         | YANG Schema Item iDentifier (sid) |                  3.2 |
{: #yangtags title="Tag numbers defined for YANG-CBOR"}

{{-standin}} proposes to employ additional tags to enable the use of
efficient binary encodings for certain frequently used YANG data types
{{-yang-types}}.

# Protocols

Protocols may want to allocate CBOR tag numbers to identify specific
protocol elements.

## DOTS

DDoS Open Threat Signaling (DOTS) defines tag number 271 for the DOTS
signal channel object in {{!RFC9132}}.

## RAINS

As an example for how experimental protocols can make use of CBOR tag
definitions, the RAINS (Another Internet Naming Service) Protocol
Specification defines tag number 15309736 for a RAINS Message
{{?I-D.trammell-rains-protocol}}.
(The seemingly random tag number was chosen so that, when represented
as an encoded CBOR tag
argument, it contains the Unicode character <u format="lit-num">雨</u>
in UTF-8, which represents rain in a number of languages.)


# Datatypes

## Advanced arithmetic

General information about the representation of numbers in CBOR can be
found in {{STD94}} as well as {{-numbers}}.

A number of tags have been registered for arithmetic representations
beyond those built into CBOR and defined by tags in {{-orig}}.
These are all documented under `http://peteroupc.github.io/CBOR/`; the
last pathname component for the URL is given in the column "Reference"
of {{arithtags}}.

| Tag number | Tag content | Short Description                         | Reference     |
|         30 | array       | Rational number                           | rational.html |
|        264 | array       | Decimal fraction with arbitrary  exponent | bigfrac.html  |
|        265 | array       | Bigfloat with arbitrary exponent          | bigfrac.html  |
|        268 | array       | Extended decimal fraction                 | extended.html |
|        269 | array       | Extended bigfloat                         | extended.html |
|        270 | array       | Extended rational number                  | extended.html |
{: #arithtags title="Tags for advanced arithmetic"}

CBOR's basic generic data model ({{Section 2 of RFC8949@-cbor}}) has a number
system with limited-range integers (major types 0 and 1:
-2<sup>64</sup>..2<sup>64</sup>-1) and floating point numbers that
cover binary16, binary32, and binary64 (including non-finites) from
{{IEEE754}}.
With the tags defined with {{-orig}}, the extended generic data model
({{Section 2.1 of RFC8949@-cbor}}) adds unlimited-range integers (tag numbers 2
and 3, "bigint" in CDDL) as well as floating point values using the bases
2 (tag number 5, "bigfloat") and 10 (tag number 4, "decfrac").

This pre-defined number system has a number of limitations that are
addressed in three of the tags discussed here:

* Tag number 30 allows the representation of rational numbers as a
  ratio of two integers: a numerator (usually written as the top part
  of a fraction), and a denominator (the bottom part), where both
  integers can be limited-range basic and unlimited-range integers.
  The mathematical value of a rational number is the numerator divided
  by the denominator.
  This tag can express all numbers that the extended generic data
  model of {{-orig}} can express, except for non-finites {{IEEE754}}; it
  also can express rational numbers that cannot be expressed with
  denominators that are a power of 2 or a power of 10.

  For example, the rational number 1/3 is encoded:

  ~~~cbor-pretty
    d8 1e      ---- Tag 30
       82      ---- Array length 2
          01   ---- 1
          03   ---- 3
  ~~~

  Many programming languages have built-in support for rational
  numbers or support for them is included in their standard libraries;
  tag number 30 is a way for these platforms to interchange these
  rational numbers in CBOR.

* Tag numbers 4 and 5 are limited in the range of the (base 10 or base
  2) exponents by the limited-range integers in the basic generic data
  model.  Tag numbers 264 and 265 are exactly equivalent to 4 and 5,
  respectively, but also allow unlimited-range integers as exponents.
  While applications for floating point numbers with exponents outside
  the CBOR basic integer range are limited, tags 264 and 265 allow
  unlimited roundtripping with other formats that allow very large or
  very small exponents, such as those JSON {{-json}} can provide if the
  limitations of I-JSON {{-ijson}} do not apply.

The tag numbers 268..270 extend these tags further by providing a way
to express non-finites within a tag with this number.  This does not
increase the expressiveness of the data model (the non-finites can
already be expressed using major type 7 floating point numbers), but
does allow both finite and non-finite values to carry the same tag.
In most applications, a choice that includes some of the three tags
30, 264, 265 for finite values and major type 7 floating point values
for non-finites (as well as possibly other parts of the CBOR number
system) will be the preferred solution.

This document suggests using the CDDL typenames defined in
{{arith-tags-cddl}} for the three most useful tag numbers in this section.

~~~ cddl
rational = #6.30([numerator: integer, denominator: integer .ne 0])
rational_of<N,D> = #6.30([numerator: N, denominator: D])
; the value 1/3 can be notated as rational_of<1, 3>

extended_decfrac = #6.264([e10: integer, m: integer])
extended_bigfloat = #6.265([e2: integer, m: integer])
~~~
{: #arith-tags-cddl title="CDDL for extended arithmetic tags"}

## Variants of undefined

`https://github.com/svaarala/cbor-specs/blob/master/cbor-absent-tag.rst`
defines tag 31 to be applied to the CBOR value Undefined (0xf7),
slightly modifying its semantics to stand for an absent value in a
CBOR Array.

(TO DO: Obtain permission to copy the definitions here.)

## Typed and Homogeneous Arrays

{{!RFC8746}} defines tags for various kinds of arrays.  A summary is
reproduced in {{arraytags}}.

| Tag  | Data Item            | Semantics                                      |
| 64   | byte string          | uint8 Typed Array                              |
| 65   | byte string          | uint16, big endian, Typed Array                |
| 66   | byte string          | uint32, big endian, Typed Array                |
| 67   | byte string          | uint64, big endian, Typed Array                |
| 68   | byte string          | uint8 Typed Array, clamped arithmetic          |
| 69   | byte string          | uint16, little endian, Typed Array             |
| 70   | byte string          | uint32, little endian, Typed Array             |
| 71   | byte string          | uint64, little endian, Typed Array             |
| 72   | byte string          | sint8 Typed Array                              |
| 73   | byte string          | sint16, big endian, Typed Array                |
| 74   | byte string          | sint32, big endian, Typed Array                |
| 75   | byte string          | sint64, big endian, Typed Array                |
| 76   | byte string          | (reserved)                                     |
| 77   | byte string          | sint16, little endian, Typed Array             |
| 78   | byte string          | sint32, little endian, Typed Array             |
| 79   | byte string          | sint64, little endian, Typed Array             |
| 80   | byte string          | IEEE 754 binary16, big endian, Typed Array     |
| 81   | byte string          | IEEE 754 binary32, big endian, Typed Array     |
| 82   | byte string          | IEEE 754 binary64, big endian, Typed Array     |
| 83   | byte string          | IEEE 754 binary128, big endian, Typed Array    |
| 84   | byte string          | IEEE 754 binary16, little endian, Typed Array  |
| 85   | byte string          | IEEE 754 binary32, little endian, Typed Array  |
| 86   | byte string          | IEEE 754 binary64, little endian, Typed Array  |
| 87   | byte string          | IEEE 754 binary128, little endian, Typed Array |
| 40   | array of two arrays* | Multi-dimensional Array, row-major order       |
| 1040 | array of two arrays* | Multi-dimensional Array, column-major order    |
| 41   | array                | Homogeneous Array                              |
{: #arraytags title="Tag numbers defined for Arrays"}
<!--  cols='r l l' -->

# Domain-Specific

(TO DO: Obtain permission to copy the definitions here; explain how
tags 52 and 54 essentially obsolete 260/261.)

| Tag number | Tag content          | Short Description                                               | Reference                                                              | Author         |
|         37 | byte string          | Binary UUID ({{Section 4.1.2 of RFC4122}})                        | https://github.com/lucas-clemente/cbor-specs/blob/master/uuid.md       | Lucas Clemente |
|         48 | byte string          | IEEE MAC Address                                                | {{-mac}}                                                                 |                |
|         52 | byte string or array | IPv4, \[prefixlen,IPv4], \[IPv4,prefixpart]                     | {{-ip}}                                                                  |                |
|         54 | byte string or array | IPv6, \[prefixlen,IPv6], \[IPv6,prefixpart]                     | {{-ip}}                                                                  |                |
|        257 | byte string          | Binary MIME message                                             | http://peteroupc.github.io/CBOR/binarymime.html                        | Peter Occil    |
|        260 | byte string          | Network Address (IPv4 or IPv6 or MAC Address)                   | http://www.employees.org/~ravir/cbor-network.txt                       | Ravi Raju      |
|        261 | map                  | Network Address Prefix (IPv4 or IPv6 Address + Mask Length)     | https://github.com/toravir/CBOR-Tag-Specs/blob/master/networkPrefix.md | Ravi Raju      |
|        263 | byte string          | Hexadecimal string                                              | https://github.com/toravir/CBOR-Tag-Specs/blob/master/hexString.md     | Ravi Raju      |
|        266 | text string          | Internationalized resource identifier (IRI)                     | https://peteroupc.github.io/CBOR/iri.html                              | Peter Occil    |
|        267 | text string          | Internationalized resource identifier reference (IRI reference) | https://peteroupc.github.io/CBOR/iri.html                              | Peter Occil    |
|       1048 | byte string          | IEEE OUI/CID                                                    | {{-mac}}                                                                 |                |
{: #tab-domain-specific title="Select Domain-Specific Tags"}

Notes:

* In the registration for Tag 37, the reference for UUID points to
{{RFC4122}}, which has been obsoleted by {{-uuid-new}}.
The new RFC has a somewhat different internal structure; the
definition of the layout of a binary UUID is now distributed over
{{Section 5 of -uuid-new}}.

* Tags 48, 52, and 54 are recommended for new designs that need to
  represent MAC addresses, IP addresses, and IP address prefixes; they
  essentially replace tags 260 and 261, which continue to be available
  for their existing applications.

* Tag 263 describes a different kind of Hexadecimal string
(sequence of hex digit pairs, same layout as tag 23) from the
hex-string defined by the YANG data type `hex-string` (sequence of hex
digit pairs separated by colons, {{Section 3 of -yang-types}}).

## Human-readable Text

| Tag | Data Item | Semantics              | Reference                |
|  38 | array     | Language-tagged string | {{Appendix A of -probdet}} |
{: #tab-text title="Select Tags for Human-readable Text"}

Tag 38 was originally registered by Peter Occil in
<http://peteroupc.github.io/CBOR/langtags.html>; it has since been
adopted and extended in {{Appendix A of -probdet}}, where a detailed
definition of the tag and a few simple examples for its use are
provided.

The problem that this tag was designed to solve is that text strings
often need additional information to be properly presented to a human.
While Unicode (and the UTF-8 form of Unicode used in CBOR) define the
characters, additional information about the human language in use
and the writing direction appropriate for the text given are often
required.

The need to provide language information with text has been well-known
for a while and led to a common form for this information, the
language tag, defined in {{BCP47}}.

Less well-known is the need to provide separate directionality
information as well.
The need for this information is demonstrated in {{W3C-STRINGS-BIDI}},
which points out that it is "actually a bad idea to rely on language
information to apply direction" and points out further reference
information on this.
{{W3C-BIDI-USE-CASES}} shows more examples for language tags and
directionality, while {{W3C-UBA-BASICS}} provides an introduction to the
way browsers, where "the order of characters in memory (logical) is
not the same as the order in which they are displayed (visual)",
"produce the correct order at the time of display" (Unicode
Bidirectional Algorithm).

Tag 38 meets the requirements of its specific application in
{{-probdet}}, which could be summarized as: Supplying the necessary
information to present isolated, linear, comparatively small pieces of
human-readable text.
It neither addresses more complex requirements of specific languages
such as {{W3C-SIMPLE-RUBY}}, nor does it address requirements for more
complex structure in texts such as emphasis, lists, or tables.
These more complex requirements are typically met by specific media
types such as HTML {{HTML}}.

## Extended Time Formats

Additional tag definitions have been provided for date and time values.

|  Tag | Data Item   | Semantics                          | Reference     |
|  100 | integer     | date in number of days since epoch | {{?RFC8943}}  |
| 1004 | text string | RFC 3339 full-date string          | {{?RFC8943}}  |
| 1001 | map         | extended time                      | {{-time-tag}} |
| 1002 | map         | duration                           | {{-time-tag}} |
| 1003 | map         | period                             | {{-time-tag}} |
{: #timetags cols='r l l' title="Tag numbers for date and time"}

Note that tags 100 and 1004 are for calendar dates that are not
anchored to a specific time zone; they are meant to specify calendar
dates as perceived by humans, e.g. for use in personal identification
documents.
Converting such a calendar date into a specific point in time needs the
addition of a time-of-day (for which a CBOR tag is outstanding) and
timezone information (also outstanding).  Alternatively, a calendar
date plus timezone information can be converted into a time period
(range of time values given by the starting and the ending time); note
that these time periods are not always exactly 24 h (86400 s) long.

{{?RFC8943}} does not suggest CDDL {{-cddl}} type names for the two tags.
We suggest copying the definitions in {{time-tags-cddl}} into
application-specific CDDL as needed.

~~~ cddl
caldate = #6.100(int); calendar date as # of days from 1970-01-01
tcaldate = #6.1004(tstr); calendar date as RFC 3339 full-date string
~~~
{: #time-tags-cddl title="CDDL for calendar date tags (RFC8943)"}

Tag 1001 extends tag 1 by additional information (such as picosecond
resolution) and allows the use of Decimal and Bigfloat numbers for the
time.

# Platform-oriented

## Perl

(These are actually not as Perl-specific as the title of this section
suggests.  See also the penultimate paragraph of {{Section 3.4 of RFC8949@-cbor}}.)

These are all documented under `http://cbor.schmorp.de/`; the
last pathname component is given in {{perltags}}.

(TO DO: Obtain permission to copy the definitions here.)


|   Tag | Data Item        | Semantics                                                                       | Reference      |
|   256 | multiple         | mark value as having string references                                          | stringref      |
|    25 | unsigned integer | reference the nth previously seen string                                        | stringref      |
|    26 | array            | Serialized Perl object with classname and constructor arguments                 | perl-object    |
|    27 | array            | Serialized language-independent object with type name and constructor arguments | generic-object |
|    28 | multiple         | mark value as (potentially) shared                                              | value-sharing  |
|    29 | unsigned integer | reference nth marked value                                                      | value-sharing  |
| 22098 | multiple         | hint that indicates an additional level of indirection                          | indirection    |
{: #perltags cols='r l l' title="Tag numbers that aid the Perl platform"}


## JSON

(TO DO: Obtain permission to copy the definitions here.)


Tag number 262 has been registered to identify byte strings that carry embedded
JSON text (`https://github.com/toravir/CBOR-Tag-Specs/blob/master/embeddedJSON.md`).

Tag number 275 can be used to identify maps that contain keys that are
all of type Text String, as they would occur in JSON
(`https://github.com/ecorm/cbor-tag-text-key-map`).

## Weird text encodings

(TO DO: Obtain permission to copy the definitions here.)

Some variants of UTF-8 are in use in specific areas of application.
Tags have been registered to be able to carry around strings
identified as to which of these
variants is used, in case they are not also valid UTF-8 and can therefore not
be represented as a CBOR text string
(`https://github.com/svaarala/cbor-specs/blob/master/cbor-nonutf8-string-tags.rst`).

| Tag Number | Data Item   | Semantics               |
|        272 | byte string | Non-UTF-8 CESU-8 string |
|        273 | byte string | Non-UTF-8 WTF-8 string  |
|        274 | byte string | Non-UTF-8 MUTF-8 string |
{: #weirdtags cols='r l l' title="Tag numbers for UTF-8 variants"}

# Application-specific

(TO DO: Obtain permission to copy the definitions here.)

| Tag number | Tag content | Short Description                                                          | Reference                                                                                         | Author            |
|         39 | multiple    | Identifier                                                                 | <https://github.com/lucas-clemente/cbor-specs/blob/master/id.md>                                  | Lucas Clemente    |
|         42 | byte string | IPLD content identifier                                                    | <https://github.com/ipld/cid-cbor/>                                                               | Volker Mische     |
|        103 | array       | Geographic Coordinates                                                     | <https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag103-Geographic-Coordinates.md>         | Danilo Vidovic    |
|        104 | multiple    | Geographic Coordinate Reference System  WKT or EPSG number                 | {{?I-D.clarke-cbor-crs}}                                                                           |                   |
|        120 | multiple    | Internet of Things Data Point                                              | <https://github.com/allthingstalk/cbor/blob/master/CBOR-Tag120-Internet-of-Things-Data-Points.md> | Danilo Vidovic    |
|        258 | array       | Mathematical finite set                                                    | <https://github.com/input-output-hk/cbor-sets-spec/blob/master/CBOR_SETS.md>                      | Alfredo Di Napoli |
|        259 | map         | Map datatype with key-value operations (e.g. `.get()`/`.set()`/`.delete()`)   | <https://github.com/shanewholloway/js-cbor-codec/blob/master/docs/CBOR-259-spec--explicit-maps.md> | Shane Holloway    |
{: #tab-apptags cols='r l l' title="Application-specific Tags"}

## Enumerated Alternative Data Items

(Original Text for this section was contributed by Duncan Coutts and
Michael Peyton Jones; all errors are the author's.)

A set of CBOR tag numbers has been allocated ({{iana}}) for
encoding data composed of enumerated alternatives:

|       Tags | Data Item          | Meaning                                 |
|   121..127 | any                | alternatives 0..6, 1+1 encoding         |
| 1280..1400 | any                | alternatives 7..127, 1+2 encoding       |
|        101 | array \[uint, any] | alternatives as given by the uint + 128 |
{: #tab-tag-enum cols='r l l' title="Tags for Enumerated Alternative Data Items"}

The tags defined in this section are for encoding data that can be
in one of a number of different enumerated forms.

For example data representing the result of some action might be either
a failure with some failure detail, or a success with some result. In
this example there are two cases, the failure case and the success case,
and we can enumerate them as 0 and 1.

In general the number of alternatives, and what data is expected in each
alternative case is entirely application dependent.

The tags defined in this specification allow the encoding of any number
of alternatives, but provide compact encoding for the common cases of
low numbers of alternatives:

-   Alternatives 0..6 can be encoded in 2 bytes;

-   Alternatives 7..127 can be encoded in 3 bytes;

-   Alternatives 128+ can be encoded in 3-12 bytes.

There are no special considerations for deterministic encoding
{{Section 4.2 of RFC8949@-cbor}}: The case numbers covered by each tag do not
overlap; particularly, tag 101 encoding starts where the more compact
special encodings for 0..6 and 7..127 end.

For cases 0..6 and 7..127, the tag value indicates the value of the alternative.
For cases 128+, a single tag number is used with an enclosed two-element array that contains the case number and the value of the alternative.

### Semantics

The value consists of a case number and a case body. The case number is
an unsigned integer that indicates which case out of the set of
alternatives is used. The case body is any CBOR data value.

In a setting where the application uses a schema (formally or
informally), then there will be an appropriate sub-schema for each case
in the set of alternatives. The representation of the case body should
comply with the schema corresponding to the case number used.

To continue the example above about representing failure or success,
suppose that the failure detail consists of an integer code and a
string, and suppose that the successful result is a byte string. A
failure value will use case 0 and the case body will be a CBOR list
containing an integer and a text string. Alternatively, a success value
will use case 1 and the body will be a single CBOR byte string.

Decoders that enforce a schema must check the case number is within the
range of cases allowed, and that the case body follows the schema for
the supplied case number. Generic decoders should allow any case number
and any CBOR data value for the case body.

### Rationale

CBOR has direct support for *combinations* of multiple values but not
for *alternatives* of multiple values. Combinations are expressed in
CBOR using lists or maps.

Most programming languages have a notion of data consisting of
combinations of data values, often called records, structs or objects. Many
programming languages also have a notion of data consisting of multiple
alternative data values. For example C has unions, and other languages
have "tagged" unions (where it is always clear which alternative is in
use).

Crucially for this set of tags, the set of alternatives must be closed
and ordered. This allows encoding using an unsigned number to distinguish
each case.

Note that this does *not* correspond to the notion in some programming
languages of classes and subclasses since in that context the set of
alternatives is open and unordered. Alternatives of this kind are
well-supported by tag 27 "Serialized language-independent object with
type name and constructor arguments".

In functional programming languages, the primary way of forming new data
types is to enumerate a set of alternatives (each of which may be a
record). Such forms of data are also supported in hybrid functional
languages or languages with functional features.

Thus, in some applications, it is very common to have data making use of
alternatives, and it is worth finding a compact encoding, at least for
the common cases. Just as most records are small, most alternatives are
also small.

In this specification we reserve 7 values in the 2-byte part of the
available tag encoding space for alternatives 0..6 which are by far the
most common. We reserve a range of 121 values in the 3-bytes tag
encoding space. To cover the general case we use an encoding using a
pair consisting of an unsigned integer and the case body, the first 24
of which also result in a 3-byte encoding.

### Examples

To elaborate on the example from the introduction, we have a "result"
that is a failure or success, where:

-   the failure detail consists of an integer code and a string;
-   the successful result is a byte string.

This corresponds to the following schema, in CDDL notation:

~~~ cddl
result = #6.121([int, text])
       / #6.122(bytes)
~~~

Example values:

~~~ cbor-diag
121([3, "the printer is on fire"])
~~~
~~~ cbor-diag
122(h'ff00')
~~~

As a second example, here is one based on a data type defined within the
Haskell programming language, representing a simple expression tree.

~~~ haskell
-- A data type representing simple arithmetic expressions

data Expr = Lit Int -- integer literal
| Add Expr Expr -- addition
| Sub Expr Expr -- subtraction
| Neg Expr -- unary negation
| Mul Expr Expr -- multiplication
| Div Expr Expr -- integer division
~~~

In CDDL notation, and using the tags in this specification, such data
could be encoded using this schema:

~~~ cddl
; A data type representing simple arithmetic expressions

expr = #6.121(int)          ; integer literal
     / #6.122([expr, expr]) ; addition
     / #6.123([expr, expr]) ; subtraction
     / #6.124(expr)         ; unary negation
     / #6.125([expr, expr]) ; multiplication
     / #6.126([expr, expr]) ; integer division
~~~

# Implementation aids

## Invalid Tag

The present document registers tag numbers 65535, 4294967295, and
18446744073709551615 (16-bit 0xffff, 32-bit 0xffffffff, and 64-bit
0xffffffffffffffff) as Invalid Tags, tags that are always invalid,
independent of the tag content provided.  The purpose of these tag
number registrations is to enable the tag numbers to be reserved for
internal use by implementations to note the absence of a tag on a data
item where a tag could also be expected with that data item as tag
content.

The Invalid Tags are not intended to ever occur in interchanged CBOR
data items.  Generic CBOR decoder implementations are encouraged to
raise an error if an Invalid Tag occurs in a CBOR data item even if
there is no validity checking implemented otherwise.

## Programming Aid for Simple Values {#invalid-simple}

In a similar way, the present document also requests to register tag
number CPA21334 as a fourth Invalid Tag.
This tag is set aside specifically for use by CBOR implementations
that have no natural way to represent Simple Values ({{Section 3.3 of
RFC8949@-cbor}}) beyond false, true, or null in their programming
interface.
For instance, such implementations can represent simple(123) as
CPA21334(123) in the programming interface.

[^cpa]

IANA Considerations {#iana}
============

In the registry "{{cbor-tags (CBOR Tags)<IANA.cbor-tags}}" {{IANA.cbor-tags}},
IANA has allocated the first to third tag in {{tab-tag-values}} from the
FCFS space, with the present document as the specification reference.
IANA also has allocated the tags in the next five rows from the Specification
Required space, with the present document as the specification reference.
Finally, IANA is requested to register the tags in the last two rows
(marked with CPA) from the Specification Required space, with the
present document as the specification reference.

|                        Tag | Data Item    | Semantics                                                         | Reference                                                   |           |
|                      65535 | (none valid) | always invalid                                                    | draft-bormann-cbor-notable-tags, {{invalid-tag}}              |           |
|                 4294967295 | (none valid) | always invalid                                                    | draft-bormann-cbor-notable-tags, {{invalid-tag}}              |           |
|       18446744073709551615 | (none valid) | always invalid                                                    | draft-bormann-cbor-notable-tags, {{invalid-tag}}              |           |
|                         63 | byte string  | Encoded CBOR Sequence {{-seq}}                                      | draft-bormann-cbor-notable-tags, {{related-tags}}             |           |
|                      21065 | text string  | I-Regexp                                                          | draft-bormann-cbor-notable-tags, {{related-tags}}; {{-iregexp}} |           |
| 18300 to 18555 (inclusive) | byte string  | Bare Hash value (COSE algorithm -256 to -1)                       | draft-bormann-cbor-notable-tags, {{hashtags}}                 |           |
|                      18556 | array        | \[COSE algorithm identifier, Bare Hash value]                     | draft-bormann-cbor-notable-tags, {{hashtags}}                 |           |
| 18557 to 18811 (inclusive) | byte string  | Bare Hash value (COSE algorithm 1 to 255)                         | draft-bormann-cbor-notable-tags, {{hashtags}}                 |           |
|                     CPA108 | byte string  | Expected conversion to base16 encoding (lowercase)                | draft-bormann-cbor-notable-tags, {{expected-tags}}            |           |
|                   CPA21334 | uint         | (always invalid in interchange)<br>programming aid for simple values | draft-bormann-cbor-notable-tags, {{invalid-simple}}           | <!--  --> |
{: #tab-tag-values cols='r l l' title="Values for Tags"}

In addition, IANA has allocated the tags from
{{tab-tag-enum}}, with a reference to the present document.

Security Considerations
============

The security considerations of {{-cbor}} apply; the tags discussed here
may also have specific security considerations that are mentioned in
their specific sections above.

--- back

{::include-all notable-tags-lists.md}

Acknowledgements
================
{: numbered="no"}

(Many, TBD)

<!--  LocalWords:  CBOR extensibility IANA uint sint IEEE endian
 -->
<!--  LocalWords:  signedness endianness
 -->
