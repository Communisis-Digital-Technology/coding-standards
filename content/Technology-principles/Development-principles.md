/* 
Title: Development Principles
Sort: 1
*/

This section outlines a number of broad principles which underpin all
development work for Communisis Digital's clients.  Everything discussed is
realistic, achievable, and generally considered good practice.

## Progressive enhancement and graceful degradation

All aspects of the site MUST remain usable in a "lowest common denominator"
scenario.

Do not create an experience which relies on specific features being available in
order to be usable and navigable.  Examples for CSS and JavaScript follow:

* Using CSS3's `border-radius` to match the design is good: there is no impact
  on the site's usability if a browser does not support it.

* Using CSS3's `rgba()` syntax by itself to create a transparent background will
  not degrade gracefully in browsers that do not support it; the following
  solution should be used:

        // solid background colour declared first
        background : #000000;

        // then, for browsers with support, a transparent background
        background : rgba(0, 0, 0, 0.9);

* Do not use CSS to hide a section of the page and then JavaScript to show it:

        // CSS:
        div#navigation { display : none; }
        ...
        // JavaScript:
        $("#navigation").fadeIn(500);

* Instead, use Modernizr to detect whether the user has JavaScript:

        html.js div#navigation { display : none }

* Modernizr allows us to _test for features rather than browsers_ - that is to
  say, it is better to test whether a browser supports, for example, CSS
  animations, than to test whether the browser is not Internet Explorer (user
  agent strings can easily be faked).

Features not addressed in the examples above should be researched at
<http://caniuse.com/> and compared against the _Browser and form factor support_
detailed elsewhere in this document.

## Don't be needlessly clever

Advanced, cryptic, or complex language features SHOULD NOT be used unless there
is a specific and obvious benefit. If there is a benefit, document both what the
code does and why it is being used. _Saving typing is not a benefit._

As an example, the following two pieces of code are equivalent:

    var arr = ["a", "b", "c"];

    !!~arr.indexOf("a") && doSomething();

And:

    var arr = ["a", "b", "c"];

    if (arr.indexOf("a") >= 0) {
        doSomething();
    }

The latter, however, requires no in-depth understanding of the nuances of
JavaScript's syntax.

## Be consistent

Consistency means developers in a team can easily work on different sections of
a project without worrying about differing naming or coding conventions;
likewise, it reduces the chances of finding any "nasty surprises".

Where there is a defined convention in this document, this convention SHOULD be
followed.  If an exception to the convention is necessary, document why.

## Re-use, DRY, the single responsibility principle

[DRY (**D**on't **R**epeat **Y**ourself)][dry] and the [single responsibility
principle][srp] encourage abstracting common functionality into re-usable
modules or components. Broadly, where multiple elements share common properties,
create an abstract element which encompasses the shared functionality and can be
extended by other elements which require specific functionality.

An example:

    var AbstractButton = View.extend({
        // generic event handlers
        events : {
            "click" : "click",
            "mouseover" : "over",
            "mouseout" : "out"
        },
        click : function() { ... },
        over : function() { ... },
        out : function() { ... }
    });

    var SubmitButton = AbstractButton.extend({
        initialize : function() {
            // specific code here
        },

        click : function() {
            // specific code here
        }
    });

Having an `AbstractButton` to re-use when you wish to create a `SubmitButton`
represents the main advantages of DRY/SRP, which are:

* Saving time.
* Reducing repeated code.
* Reducing likelihood of errors in code.
* Potential reduction of testing.

[dry]: http://en.wikipedia.org/wiki/Don't_repeat_yourself
[srp]: http://csswizardry.com/2012/04/the-single-responsibility-principle-applied-to-css/

## Leave optimisation to the build process

For JavaScript and CSS, be liberal with whitespace, and use meaningful variable
names - minification is part of the build process and it will strip out and
refactor anything that is unnecessary, whilst also concatenating files.

## Documentation

Inline comments MUST be stripped during the build process, while external
documentation MUST be automatically generated as discussed in the JavaScript
standards section. This documentation structure MUST be kept out of the web
root.
