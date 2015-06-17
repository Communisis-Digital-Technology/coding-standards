/* 
Title: JS coding standards
Sort: 3
*/

## General concepts

### Introduction

This document defines policies for usage and authoring of JavaScript for
Communisis Digital projects.

It is important to note that JavaScript should be used to _enhance the user's
experience_ by adding engaging and interactive functionality. It is acceptable
to use JavaScript to create an interactive widget (for example, a carousel or
a lightbox), but it is not acceptable to use JavaScript where non-dynamic
or "plain" HTML and CSS would in normal circumstances suffice - that is to say,
JavaScript MUST be used only where it is strictly necessary. Examples of
unnecessary JavaScript:

* Using JavaScript where a normal anchor link (`A`) would suffice.
* Using JavaScript to submit a form, where the form's `action` would suffice.
* Using JavaScript to replace images on mouse rollover/rollout, where CSS can
  achieve the same effect.

## Libraries

### Standard libraries

The following libraries SHOULD be used:

1. *jQuery*

    [jQuery][jQuery] is the *de facto* standard library for working with
    JavaScript. Its key features are: a consistent API which works across all
    current browsers; the [Sizzle selector engine][Sizzle], offering
    CSS-style selectors for DOM elements; simplified AJAX functionality;
    and basic support for animations.

2. *Modernizr*

    [Modernizr][Modernizr] offers a comprehensive API for detecting and working
    with HTML5 and CSS3 technologies.

    It includes the popular [HTML5Shiv][h5shiv] - a small JavaScript library
    enabling the use of new HTML5 markup elements (including the semantic
    elements such as `HEADER`, `NAV`, `FOOTER`, etc.) in browsers with no
    support for them.

    In terms of feature detection, Modernizr can test for browser support for
    everything from CSS transformations to WebGL support.  In addition to using
    JavaScript to access the `Modernizr` object with boolean properties
    describing the feature support, Modernizr also adds classes to the `HTML`
    element so that support for differing feature sets can be handled in CSS;
    eg. `html.cssAnimations { /* ... */ }`

    Modernizr provides a tool for creating custom builds which detect as many or
    as few features as required.

3. *mustache.js*

    Mustache is a popular templating system which has been ported to most of
    today's popular programming languages, including JavaScript. See
    [JavaScript Templating](#javascript-templating) below for a full discussion
    of [Mustache][mustache].

4. *Underscore*

    [Underscore][_] is a utility library which provides a large number of useful
    functions for JavaScript development.


[jQuery]:       http://jquery.com/
[Sizzle]:       http://sizzlejs.com/
[Modernizr]:    http://modernizr.com/
[h5shiv]:       http://code.google.com/p/html5shiv/
[bb]:           http://backbonejs.org/
[_]:            http://underscorejs.org/
[mustache]:     http://mustache.github.com/

### Third-party plugins/modules

Third-party plugins and modules, especially for jQuery, SHOULD be avoided where feasible.
Instead, developers SHOULD build suitable custom functionality according to our
JavaScript and web development standards. In many cases, functionality such as a
lightbox or carousel can be achieved with relatively minimal effort; for more
complex modules, a 100% custom approach is inherently more desirable.

Removing any dependency on third-party plugins and modules has a number of
advantages including:

* Tighter control over coding standards verifiability of code being deployed.

* No support issues if plugins stop being updated and fail to work with updated
  libraries (eg. jQuery).

* Complete customisation of JavaScript being developed deployed to ensure that
  it is wholly relevant to the project.

However pragmatism should be used - if a project's requirements match the functionality
offered by a third party project, and it gives a suitable API for customisation, it can
offer significant advantages over a dogmatic [Not Invented Here][nih] approach.

Open source projects can be forked if necessary and if improvements can be made to
an existing codebase, pull requests to the main repository can ensure that Communisis Digital take
an active part in the open source community, to the advancement of all.

[nih]: https://www.wikiwand.com/en/Not_invented_here

### Upgrade policy

Consideration should be given to how and when to upgrade third-party libraries
in use, especially jQuery (see below). Broadly speaking, when upgrading a
library, it is important to conduct a thorough review of the code against the
library's changelog to see whether any of the changes mentioned overlap with
code currently deployed.

If there is overlap and the changes are significant, then the benefits of the
upgraded library SHOULD be weighed up against the time to re-work critical
functionality. If the time and cost of using the upgraded version outweighs the
benefits it brings, it is worth waiting until a subsequent upgrade which offers
genuine benefits.

[Semantic versioning][semver] principles mean that libraries which use this standard can
usually be safely upgraded in patch or minor update version ticks.

[semver]: http://semver.org/

## Coding standards (style guide)

These standards provide a guide to writing JavaScript that can be read,
understood, and maintained within a team environment.

### General conventions

#### Whitespace and semicolons

In common with the file formats and encodings conventions, indent with two spaces.
Tabs MUST NOT be used. Lines SHOULD be kept to a reasonable length;
< 100 characters is preferable. An editorConfig file should be included in a project
to define the acceptable formatting rule for other developers.

While ending a statement with a semicolon in JavaScript is in some cases
optional, the rules around this (generally called "Automatic Semicolon
Insertion", or ASI) are surprisingly complicated. For this reason, semicolons
MUST be used in all traditional places to terminate lines.

#### Naming

Variables and functions SHOULD have concise but meaningful names. When referring
to a jQuery wrapped object (for example, a collection returned from a query
selector), it is a common and very useful practice to prefix the variable name
with the jQuery `$` sigil.

Use `camelCase` for:

* variables:

        var searchButton,
            $listItem; // $ used to indicate a jQuery object, eg. [<li>]

* functions:

        function openPage() { ... }
        function closeNavigation() { ... }

Use `UpperCamelCase` for:

* constructors and prototypes:

        var ButtonView = function() {
            ...
        };

        var searchButton = new ButtonView;

        var Carousel = function() {
            ...
        };

Use `CAPITALS_WITH_UNDERSCORES` for:

* constants:

        var SECONDS_IN_A_MINUTE = 60,
            SEARCH_SERVICE = "/search.jsp?";

JavaScript's `const` keyword MUST NOT be used - this has limited browser
support.

#### Variables

A good practice is to use the `var` keyword sparingly and to indent multiple
declarations. For example:

    var foo,
        bar = "baz",
        i = 0;

Indenting the variable declarations without repeating the keyword saves typing
and looks "cleaner".  Declare all variables together at the beginning of their
scope.

#### Braces and brackets

The following style of indentation SHOULD be used for functions (this is
referred to as the [One True Brace Style][1tbs] and is a variant of that used by
Kernighan and Ritchie):

    function func(arg1, arg2) {
        ... // body
    }

Brackets SHOULD be used as follows (notably with whitespace after the `if` but
not between the brackets and the terms of the condition itself):

    if (a === b) {
        ... // logic
    }

Where it aids clarity and readability, additional whitespace SHOULD be used:

    if ( (a > b) || (this.day < 5) ) {
        ... // logic
    }

[1tbs]: http://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS

#### Flow of control

When using JavaScript's looping structures, it is always fastest to use this
pattern:

    var i = 0,
        len = array.length;

    for (; i < len; i++) {
        ... // repeat
    }

This obviates the need to calculate the length of the array for each iteration
of the loop (or to allocate memory for `i` more than once).

Favour an early return in a function where possible. This promotes readability
and comprehensibility of code. The following code demonstrates an early return
based on a falsy argument:

    function foo(arg) {
        var result;

        if (!arg) {
            return false; // early return
        }

        ... // more logic


        return result;
    }


#### Miscellaneous

* Create an array like this:

        var arr = [];

* Create an object like this:

        var obj = {};

### Commenting code

Short inline comments should generally follow a line:


    var len = $(".carousel > .item").length; // number of carousel items


### More advanced specifics

#### Function binding

In JavaScript, the scope of `this` varies according to the context in which the
function is called.  A particularly obvious example would be within the scope of
an event-listener; consider the following:

    var obj = {
        init : function() {
            var click = function() {
                this.testFunc(); // undefined
            };

            // jQuery event listener
            $elem.on("click", click);
        },

        testFunc : function() {
            ...
        }
    }

A call to `testFunc()` would fail here because `this` would be scoped to the
click event listener rather than `obj`. We can resolve this by *binding* the
click event listener to the `obj` scope; with Underscore, this is as simple as:

            var click = _.bind(function() {
                this.testFunc();
            }, this);

(Modern browsers which have implemented ECMAScript 5 will have a native
implementation of function binding with `Function.bind()`, which is what
Underscore will default to if it is available.)

Underscore's `bind()` and `bindAll()` SHOULD be used rather than littering your
code with:

    var _this = this;


in order to keep a reference to the scope.

### Prototypal inheritance

Where necessary, we will favour the prototypal style of inheritance in
JavaScript. For example:

    var PredictiveSearch = (function() {

        function PredictiveSearch() {
            ...
        }

        var proto = PredictiveSearch.prototype;

        proto.render = function() {
            ...
        };

        proto.destroy = function() {
            ...
        };

        return PredictiveSearch;
    })();

    module.exports = PredictiveSearch;

    // usage:

    var PredictiveSearch = require("./search"),
        search = new PredictiveSearch();

    search.doSomething();


## Modular JavaScript with Browserify

[Browserify][browserify] will be used on projects to organise JavaScript
into separate modules which can be loaded with `require` statements, in the
style of Node.js, but in the browser.

[browserify]: https://github.com/substack/node-browserify

## JavaScript templates with Mustache.js

Where front-end templates are required, the standard choice should be 
[Mustache.js][mustache-js].

Mustache templates are "logic-less" - that is to say, they contain no specific
logic relating to routing (eg. there is no if/else construct) and limited
control of flow beyond looping over a collection. This helps promote a good
separation of concerns between views and logic.

[mustache-js]: https://github.com/janl/mustache.js

## AJAX

AJAX will be used on normal builds for two purposes:

1. User experience.
2. To improve performance of the web journey by reducing load on the
   underlying infrastructure.

Examples of AJAX usage would include:

1. Adding a piece of content to a user's collection.
2. Adding notes to a piece of content.
3. Incrementing an up-vote for a piece of content.

In general, the use of AJAX will mean that we are not diverting the user to a
different flow.

Where there is a natural page change then we SHOULD NOT be using AJAX to reload
the page; rather, we should be relying on a direct server call. For example,
the login process - this should result in a full page call back to the server
and then a page reload rather than using AJAX.

As each design is received it should be annotated in conjunction with the
development/UX teams to indicate which components or flows would be suitable
for AJAX.

### Invocation

The correct HTTP verb should be used for the AJAX call.

#### `GET`

`GET` means that we are simply requesting information from the server and once
the request has occurred, there will be no lasting data change on the server;
showing the next set of products would be an example of such an idempotent
operation.

#### `POST`

`POST` is used to indicate that there is a change to the data on the server.
An example of such an operation would be adding a product to the shopping
trolley.

#### Exceptions

There are fringe cases where the volume of data that needs to go to the server
in a GET request will exceed the URL length limits imposed by our
infrastructure; in these cases a POST request is acceptable.

### Message content

Messaging between components of the application MUST be in the form of a JSON
string in a format specified in a [JSON Schema Definition (JSD)][jsd]. This will
allow the calling application to maintain responsibility for the correct
presentation of the information.

Calls within an application SHOULD be in the form a JSD-specified JSON string,
however in situations where performance means that it is more optimal to serve
HTML back to the browser, this MAY be acceptable.

Calls to externally hosted applications need to be handled on a case by case
basis in liaison with the supplier. The preferable method SHOULD be for a JSON
string to be supplied so that we maintain ownership of the look and feel of the
resulting page updates.

[jsd]: http://json-schema.org/

### Implementation

All AJAX calls MUST specify both a timeout condition and an error condition.
Notification of these conditions back to the user should be as defined during
the UX design phase.
