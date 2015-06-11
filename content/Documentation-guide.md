/* 
Title: Guide to this documentation
Sort:  2
*/

This document specifies code standards for Communisis Digital.

These standards are designed to promote best practice and MUST be followed by
all teams developing code.  If a particular project requires deviation from these standards, then this repository should be branched, and a project specific standards document set, and subsequently referred to.

If any point in these standards is deemed unrealistic in the long-term, an
exception MUST be raised with the relevant parties and - if accepted - noted
in the _Project-specific requirements_ section at the end of this document.

## Update cycle

This document is expected to be updated on a quarterly basis. All sections
should be reviewed, with particular emphasis on the following:

* Document control: version number and comments.
* Browser and form factor support: statistics and support charts.
* JavaScript: library versions and upgrade policy.
* Web performance: new Page Speed rules
* Project-specific requirements: addition or removal of exceptions

You MUST confirm that you have the most recent version of this document before
proceeding with development or testing.

## Language

Throughout this document, we will use several specific keywords in the manner of
[RFC 2119][rfc2119] to indicate the strength of the requirements. These words
will be capitalised and are as follows (definitions from RFC 2119):

1. *MUST*

    > This word, or the terms "REQUIRED" or "SHALL", mean that the definition is
    > an absolute requirement of the specification.

2. *MUST NOT*

    > This phrase, or the phrase "SHALL NOT", mean that the definition is an
    > absolute prohibition of the specification.

3. *SHOULD*

    > This word, or the adjective "RECOMMENDED", mean that there may exist valid
    > reasons in particular circumstances to ignore a particular item, but the
    > full implications must be understood and carefully weighed before choosing
    > a different course.

4. *SHOULD NOT*

    > This phrase, or the phrase "NOT RECOMMENDED" mean that there may exist
    > valid reasons in particular circumstances when the particular behavior is
    > acceptable or even useful, but the full implications should be understood
    > and the case carefully weighed before implementing any behavior described
    > with this label.

5. *MAY*

    > This word, or the adjective "OPTIONAL", mean that an item is truly
    > optional.  One vendor may choose to include the item because a particular
    > marketplace requires it or because the vendor feels that it enhances the
    > product while another vendor may omit the same item. An implementation
    > which does not include a particular option MUST be prepared to
    > interoperate with another implementation which does include the option,
    > though perhaps with reduced functionality. In the same vein an
    > implementation which does include a particular option MUST be prepared to
    > interoperate with another implementation which does not include the option
    > (except, of course, for the feature the option provides.)

NB. "MUST" and "SHALL" are regarded as synonymous.

[rfc2119]: http://rfc.bas.me.uk/rfc2119.txt

## Reach

These standards MUST be adhered to by all parties producing code, regardless of whether the code is intended to be a part
of the DOM or included via IFRAME.
