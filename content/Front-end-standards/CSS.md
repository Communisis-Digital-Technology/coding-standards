/* 
Title: CSS coding standards
Sort: 2
*/

## Introduction

CSS (**C**ascading **S**tyle**S**heets) is used to control the presentation of
web pages. CSS obeys the principle of "separation of concerns" - HTML is used to
mark up content and CSS is used to control its presentation.

CSS may be included inline using the `style` attribute, inside a `<style>` node,
or separately in an external linked stylesheet. On projects we will normally
usr the external linked stylesheet method. To control more dynamic
elements, we will also use JavaScript to modify their styling, using jQuery's
`addClass()` and `removeClass()` methods, and also `css()` where applicable.

## Specifics

### Formatting

The policies outlined in _File formats and encodings_ MUST be applied to CSS for
all projects for Communisis Digital.

CSS SHALL be written in the more verbose multi-line format; prefer this:

    element {
        prop1 : val1;
        prop2 : val2;
        prop3 : val3;
    }


Rather than this:

    element { prop1 : val1; prop2 : val2; prop3 : val3; }

The latter is harder to read and harder to edit, and also less appropriate for
version control.

Property/value key pairs SHOULD be separated by a space, a colon, and another
space (this is uncommon in CSS, but aids readability and mirrors common
conventions in other languages for creating objects and hashes).

Where there is only one property/value pair for a selector, _the semicolon MUST
still be used_. Even though the semicolon, as per CSS's grammar, is optional in
this case, include it anyway - if a second property/value pair is added a later
date, there is the no requirement to check whether a semicolon needs to be added
on the previous line since there will always be one there. (These problems can
be very hard to spot later - often the CSS rendering engine will silently ignore
one or both properties.) As an example, do this:

    body {
        background : red;
    }

Rather than this:

    body {
        background : red
    }

### Property order

Having a standardised convention for ordering CSS properties has no performance
benefits, but it does make projects easier for developers to work on and
maintain. We recommend ordering properties around their type of functionality
(rather than alphabetically, by length, or any other more abstruse method). We
therefore SHALL use the following order:

1. Display and flow.
2. Positioning.
3. Dimensions (width before height).
4. Margins, padding, borders.
5. Typography.
6. Colours and backgrounds.
7. Miscellaneous.
8. CSS3 (prefixed) properties. *

(* See _CSS3 and vendor prefixes_ for a full discussion on this point.)

A (contrived) example follows:

    .panel {
    /* display and flow */
        display : block;
        position : relative;
        float : left;
        z-index : 10;

    /* dimensions */
        width : 500px;
        height : 200px;

    /* margins, padding, borders */
        margin : 10px 20px;
        padding : 1em;
        border : 1px solid red;

    /* typography */
        font-size : 1.5em;
        font-weight : bold;

    /* colours and backgrounds */
        color : red;
        background-image : ... ;
        background-color : blue;
        background-position : 10px 20px;
        background-repeat : no-repeat;

    /* miscellaneous */
        opacity : 0.8;
        cursor : pointer;

    /* CSS3 property with vendor-prefixes last */
        -webkit-border-radius : 12px;
        -moz-border-radius : 12px;
        -ms-border-radius : 12px;
        -o-border-radius : 12px;
        border-radius : 12px;
    }

(Comments have been added here only for clarity. In real code, there would be no
comments and the property types would stand by themselves.)

### Naming conventions

Please see below under _SMACSS_.

### Spritesheets

Spritesheets (sometimes referred to as "CSS Sprites" or simply "sprites") are
separate images combined into one image file, with individual image elements
aligned appropriately in a grid. The general reason for this methodology is to
reduce the number of distinct HTTP requests (and also to decrease the download
size, in many cases).

Spritesheets SHOULD be used for:

* Sets of grouped icons (eg. social media sharing icons).

* Buttons where there are multiple states (eg. default, over, and active).

They MUST be avoided when a repeating background is required or where they will
lead to increased complexity; on the latter point,
[a sprite sheet like Amazon's][amazon-sprite] will almost certainly massively
increase development and maintenance time.

The original, layered version of each spritesheet MUST be kept in the folder
defined for non-web assets in the project repository. Each spritesheet MUST
be described in the associated project documentation. The description MUST
define:

* The filename of the spritesheet.
* The logic behind the grouping of each spritesheet (eg. "Additional product
  information icons").
* Whether the sprite should be used horizontally or vertically.
* The order of the states used for each image (eg. "off, over, active").

[amazon-sprite]: http://g-ecx.images-amazon.com/images/G/01/gno/images/orangeBlue/navPackedSprites-US-15._V202471683_.png

### Units

For fonts, we SHALL use `em`. This is a relative, scalable unit and well-suited
for pages which may be viewed in varying contexts.

In-page modules SHOULD, where possible, be fluid and not have fixed widths.
Their _container elements_, however, will have fixed widths. By "container
element", we broadly mean an element which contains no content directly by
itself, but instead "wraps around" other content; examples would include the
container around the entire page, the header or footer portions of the page, or
the structure which contains the principal navigation. In the SMACSS model (see
below), these would generally each be controlled by a _Layout_ rule.

In general, this approach will help cater for a
responsive design, should one be implemented in a future release.

## SMACSS

[SMACSS][smacss] (**S**calable and **M**odular **A**rchitecture for CSS) is a
methodology which is intended to help developers working on larger projects. We
SHOULD loosely follow the principles defined in the core SMACSS chapters (ie.
3-9).

Key concepts:

* Division of rules into five categories:

    * **Base**

        Defaults for a site - eg. `html` and `body` having no padding or margin.

    * **Layout**

        Styles which divide the page into sections (putting modules into place).

    * **Module**

        Reusable components of the page (sidebars, footers, product listings,
        etc.).

    * **State**

        Styles which can be applied to a module and describe its state, eg.
        open, closed, hidden, expanded.

    * **Theme**

        Styles which may be used to apply a theme to module (optional).

* Naming conventions:

    * For layouts, use `l-` as a prefix.

    * For states, use `is-` as a prefix, eg. `is-hidden`

* Specificity and selectors:

    * Avoid making unnecessary assumptions and being too specific with
      ID and element selectors - using classes can often provide a more
      generic solution.

* "Sub-classing" - supposing you have a generic element with a class of `panel`,
  you may wish to use this element in different contexts (for instance in a the
  main content area and also in a sidebar); in these contexts it may have
  slightly different properties, eg. its width.  To avoid specificity
  complexities, SMACSS proposes "sub-classing" the `panel` class by creating a
  second class with the particulars of the context applied to it:

        .panel {
            width : 100px;
        }
            .panel.panel-sidebar {
                width : 80px;
            }

The convention is to give the element the same name followed by a hyphen and
then the context; in the markup, we would then have:

        <div id="sidebar">
            <div class="panel panel-sidebar">

[smacss]: http://smacss.com/

## CSS3 and vendor prefixes

[CSS3] is not, in its entirety, a formal recommendation from the W3C yet, but
browser vendors have, nonetheless, begun implementing some of its functionality.
To indicate that this functionality is experimental or has not been formalised,
browser vendors have taken to prefixing the properties with certain strings;
these are known as "vendor prefixes".

The vendor prefixes in current and common use are:

* `-webkit-`: Chrome, Safari, most mobile browsers.
* `-moz-`: Firefox and browsers using the Gecko engine.
* `-ms-`: recent versions of Internet Explorer.
* `-o-`: Opera.

An example of handling these vendor prefixes follows:

    .element {
        -webkit-transition: all 4s ease;
        -moz-transition: all 4s ease;
        -ms-transition: all 4s ease;
        -o-transition: all 4s ease;
        transition: all 4s ease;
    }

The unprefixed version SHALL be placed last as per this article:
<http://css-tricks.com/ordering-css3-properties/>

[CSS3]: http://www.w3.org/TR/#tr_CSS

## Browser feature detection

As with JavaScript, we SHOULD be targeting features rather than browsers.
Modernizr's "feature" classes, which it adds to the `html` node, will be used
for feature detection.

Where it is absolutely necessary, we MAY use
[HTML5 Boilerplate's IE HTML tags][bp-ie-tags] to provide CSS workarounds
for particular Internet Explorer issues.

[bp-ie-tags]: http://html5boilerplate.com/docs/The-markup/#ie-html-tag-classes

## Media types

Styles relating to distinct media types (chiefly `print` as opposed to the
default `screen`) MUST be kept in the same stylesheet.
["5 years later: print CSS still sucks"][print-css-sucks] explains why. Where
necessary, minimal print-based styles can be invoked using `@media` queries:

    body {
        background : green;
    }


    @media print {
        body {
            background : white;
        }
    }


[print-css-sucks]: http://www.phpied.com/5-years-later-print-css-still-sucks/

## Build process

CSS MUST be stripped of comments and unnecessary whitespace during the build
process - it MUST be minified to its most succinct and optimal form. During
development, CSS MUST be appropriately indented and commented.

All non-CDN CSS files MUST be concatenated into a single 'master' CSS file. See
_Build process_ for more information.
