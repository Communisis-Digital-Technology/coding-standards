/* 
Title: HTML coding standards
Sort: 1
*/

## Introduction

HTML (**H**yper**T**ext **M**arkup **L**anguage) is the principal language used
to mark-up web pages. It defines a standard set of _elements_ which describe the
page's content; elements are written as _tags_ surrounded by angle brackets -
`<` and `>`. As an example, a level one header would be written:

    <h1>Header</h1>

The tag is opened with `<h1>`, there is then content, and then the tag is closed
with `</h1>`.

A web browser would be encouraged to render this as a large, bold piece of text
on a line by itself.

There can also be empty-element tags, which do not "wrap around" content:

    <img src="/images/logo.png" alt="{{Client}} logo" />

A graphical browser would render this as an image.

HTML is intended to be used purely for content; control over its appearance is
handled by CSS. HTML's basic abilities can be augmented with JavaScript.

## HTML5

All Projects SHALL be developed to the [HTML5 specification][html5].
While this specification is a draft or "living" specification, it has now seen
broad industry adoption and is the new _de facto_ standard.

[html5]: http://whatwg.org/html

### DOCTYPE

HTML5 has a much simplified DOCTYPE, as follows:

    <!DOCTYPE html>

(This is actually case-insensitive.)

## DOM Depth

Pages SHOULD be developed to make use of the smallest number of DOM elements
possible. The number of DOM elements in a document SHOULD be less than 1000.

## Polyglot Markup

We SHALL be using [Polyglot Markup] - that is to say, markup which conforms to
the HTML5 specification but is also well-formed XML.

A few specific examples of differences between HTML5 and XML:

* HTML5 does not, in its regular form, mandate that so-called empty-element tags
  be closed with a trailing slash (`/`); for example, the following are both
  perfectly valid in HTML5:

        <meta charset="utf-8">
        <link rel="stylesheet" media="screen" href="css/master.css">


* To be well-formed XML, however, they would need a trailing slash:

        <meta charset="utf-8" />
        <link rel="stylesheet" media="screen" href="css/master.css" />


* The same applies to the closing of tags like `<p>`.

* Attributes:

    * In HTML5, attributes need not be enclosed in quotes if they do not contain
      spaces.

    * To be well-formed XML, attributes must be enclosed in quotes.

* Tag case-sensitivity:

    * In HTML5, tags are not case-sensitive.

    * In XML, tags must be lowercase.

As can be seen, the differences between the two are relatively minimal and there
is very little time impact in using the more strict Polyglot Markup.

A few benefits of Polyglot Markup:

* XML well-formedness is a good standard to aim towards: it is consistent, easy
  to understand, and logical.

* Any XML parsing tools which may be used in conjunction with the site (either
  producing content for it or analysis from it) will be more easily coaxed into
  working with it if the site is valid XML.

* Most developers have been writing XHTML (ie. valid HTML) for the last decade
  so will be familiar with the strictness of Polyglot Markup.

[Polyglot Markup]: http://dev.w3.org/html5/html-xhtml-author-guide/html-xhtml-authoring-guide.html

## HTML5 semantic elements

We SHALL be using a subset of HTML5's new semantic elements for marking up
projects, specifically (descriptions from [HTML5 Doctor][h5doctor]):

* `header`:

    > Represents the "header" of a document or section of a document. The
    > `header` element is typically used to group a set of `h1`–`h6` elements to
    > mark up a page's title with its subtitle or tagline. `header` elements
    > may, however, contain more than just the section's headings and
    > subheadings — e.g., version history information or publication date.

* `nav`:

    > Represents navigation for a document. The `nav` element is a section
    > containing links to other documents or to parts within the current
    > document.

    > Not all groups of links on a page need to be in a `nav` element — only
    > groups of primary navigation links. In particular, it is common for
    > footers to have a list of links to various key parts of a site, but the
    > footer element is more appropriate in such cases.

* `article`:

    > Represents a section of a page that consists of a composition that forms
    > an independent part of a document, page, or site. This could be a forum
    > post, a magazine or newspaper article, a Web log entry, a user-submitted
    > comment, or any other independent item of content.

* `footer`:

    > Represents the "footer" of a document or section of a document. The
    > `footer` element typically contains metadata about its enclosing section,
    > such as who wrote it, links to related documents, copyright data, etc.
    > Contact information for the section given in a footer should be marked up
    > using the address element.

Other semantic elements MAY be used as appropriate.

[h5doctor]: http://html5doctor.com/element-index/

### [Modernizr]

Modernizr SHALL be used as a "shim" to enable support for HTML5 semantic
elements in older browsers.

In Internet Explorer prior to version 9, unrecognised elements - such as HTML5
elements - could not have styling applied to them; curiously, the solution is
simply to use JavaScript to iterate through each of these nodes and re-add them
to the DOM, at which point Internet Explorer will now recognise them as valid,
stylable nodes.

[Modernizr]: http://modernizr.com/

### Use of "polyfills"

A polyfill is a fix (typically implemented in JavaScript) to "plug" a gap in
browser support for a particular HTML5 feature. For example, the HTML5 `range`
input is typically rendered as a "slider" control in browsers which understand
it; for those that do not, a polyfill might implement the same functionality
using JavaScript (and images) to create a draggable thumb on a track. The
polyfill would dynamically replace the `input` (which, in non-aware browsers,
would appear like a normal `text` input) with the custom slider control, and
thus the experience for the user would be relatively seamless.

Where possible, we MAY prefer to avoid using polyfills and would rather opt for
features of HTML5 that have strong native support and/or an absence of support
for them does not result in a negative or disrupted experience for the user.
Where this isn't possible, exceptions MAY be reviewed on a per-case basis.

(Modernizr's shim for HTML5 semantic elements in general is an exception to
this.)

## Forms

Forms SHALL be marked up accessibly and will take advantage of the new
attributes afforded by HTML5.

### Accessibility

* Each field SHALL have a descriptive label. The `for` attribute of the label
  MUST match the `id` attribute of the `input` element. (In most browsers, this
  means that clicking/tapping the label will automatically select/focus the
  `input`.)

* Radio buttons and checkboxes SHOULD be wrapped inside a `fieldset` element and
  have a `legend`.

* Required fields and error messages:

    * Indicate required fields using an asterisk (also see below on HTML5
      validation attributes).

    * Error messages SHOULD, if possible, be placed next to the field which has
      caused the error (if constraints of the design or space available make
      this difficult, error messages should be at the top of the relevant
      section of the form and the erroneous elements should be highlighted).

    * Red is a fairly standard colour for both "required asterisks" and error
      messages (but, as per [WCAG 2.0 section 1.4.1], do not rely simply on the
      colour to indicate that there is an error - there needs to be descriptive
      text too).

[WCAG 2.0 section 1.4.1]: http://www.w3.org/TR/WCAG/#visual-audio-contrast-without-color

### HTML5 attributes

The HTML5 specification offers some improvements for form handling. It is worth
noting that browser support for these new features is, in some cases, limited,
and rendering methods, where the specification is liberal, may differ between
browsers.

Mobile browsers typically have native controls for certain types of input (eg.
date pickers, or text input biased towards certain types of content - regular
text versus numbers or email addresses) and using the new HTML5 attributes will,
in most cases, invoke these on selection.

It is RECOMMENDED that we use the following, which have reasonable browser
support and a lack of thereof would not be destructive:

* Required fields - these can be indicated using the `required` attribute.

* Placeholder text (initial text in an `input` which generally is shown before
  the user inserts their own content) - this can be supplied using the
  `placeholder` attribute.

* `input` types:

    * `type="email"`

        On mobile touchscreen devices, this may cause the onscreen keyboard to
        display the @ symbol in its primary state rather than hidden in a
        "symbols" secondary, or tertiary, menu.

    * `type="tel"`

        On mobile touchscreen devices, this may cause the onscreen keyboard to
        display a numeric keypad rather than the default keyboard.

    * `type="date"`

        On mobile touchscreen devices, this may cause the native date picker
        control to appear.

    * `type="search"`

        This may provide a subtle change to the `input`'s appearance to
        differentiate it from a regular text `input`.

Quirksmode has support tables for both [mobile][qm-forms-mobile] and
[desktop][qm-forms-desktop] for these (and other) elements.

[qm-forms-mobile]: http://www.quirksmode.org/html5/inputs_mobile.html
[qm-forms-desktop]: http://www.quirksmode.org/html5/inputs_desktop.html

## Tables

Tables MUST be used for tabular data only; they MUST NOT be used for any form of
markup relating to presentation. We define data as being tabular where there are
rows (tuples) which would naturally be presented sequentially, and where there
may be columns with particular headings. Content taken directly from a
spreadsheet or a database would typically be considered tabular data.

Valid examples of tabular data:

* Conversion charts for weights, liquids, length.
* Nutritional information for recipes.
* Delivery pricing options

Examples where tables MUST NOT be used:

* To position text in two columns - use CSS and floated `DIV` elements.
* To create a horizontal tabbed navigation menu - use CSS and a styled `UL`.
* To position an image between two pieces of text - use CSS and any of various
standard techniques.

Where tables are used, we SHALL make good,
accessible use of:

* `thead` and `tfoot` - wrapping around the header and footer (if needed)
elements of the table.

* `tbody` - wrapping around the rows forming the body of the table.

* `th` - to indicate column or row header cells in the table.

* `caption` - to provide a title for the table.

* The `summary` attribute - to describe the content of the table.

We recommend this [article on accessible data tables][accessible-tables] as a
thorough study on this topic.

[accessible-tables]: http://www.usability.com.au/resources/tables.cfm

## Microformats / Microdata

For an in-depth discussion on this topic, see _Search Engine Optimisation_.
