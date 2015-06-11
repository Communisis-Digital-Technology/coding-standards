/* 
Title: Accessibility
Sort: 1
*/

## WCAG 2.0

Communisis Digital projects SHALL be developed to meet [WCAG 2.0][wcag20] **Level AA**
conformance.  WCAG has three levels of conformance (A, AA, and AAA), and Level
AA is a reasonable and achievable compromise for many sites, especially those
with rich and varied content.

WCAG 2.0's guidelines are broadly divided into four categories:

* Perceivable.
* Operable.
* Understandable.
* Robust.

We provide a brief summary of each section below.

[wcag20]: http://www.w3.org/TR/WCAG/

### Perceivable

Visual content generally requires a text-based alternative in order to achieve
conformance. Examples would include:

* Alternative text for images.
* Controls (buttons, input) having names.
* Video and audio having a description and, if possible, captions.

Colour and contrast SHOULD be used cautiously; colour should not be used as the
primary means to convey information, and there should be a reasonable contrast
between text or active elements (eg. buttons) and backgrounds or
incidental/decorative elements.

### Operable

The site SHOULD be able to be navigated and, in a broad sense, operated using a
keyboard. Likewise, navigation should be clear and obvious:

* Pages should have meaningful `TITLE`s.
* The purpose of a link should be evident from its text.
* Headings and labels are used where appropriate.
* The current element in focus should be visible, and the order of focus follows
  the order of the page's content.

### Understandable

This covers a broad range of issues, including:

* The site SHOULD indicate its language using the appropriate methods.

* Navigation SHOULD be presented in a consistent and predictable manner (eg.
  a series of navigation tabs will always render in the same order over
  multiple pages).

### Robust

The site MUST be valid HTML, and HTML controls (`INPUT`, `TEXTAREA`, etc.)
SHOULD be used appropriately; where custom controls are created, these SHOULD
have identifiable names (see WAI-ARIA below).

## WAI-ARIA

The [**W**eb **A**ccessibility **I**nitiative's **A**ccessible **R**ich
**I**nternet **A**pplications][aria] - commonly referred to as WAI-ARIA - is a
Candidate Recommendation (ie. draft specification) from the W3C, which describes
a variety of attribute-based extensions to HTML in order to increase
accessibility.

It presents a standardised means of adding semantic information to:

* The sorts of widgets and custom controls which typically mark the difference
  between a traditional web _site_ and a web _application_.

* Structural elements of a page.

* Navigational elements of a page.

WAI-ARIA uses _roles_ to describe these, which it calls, respectively:

* Widget Roles.

* Document Structure Roles.

* Landmark Roles.

These are discussed briefly below.

A second major feature of WAI-ARIA are _states and properties_; these are
intended to be used in combination with roles to convey to assistive
technologies changes following user interaction. The nature and usage of states
and properties are discussed below.

Lastly, WAI-ARIA also advocates the use of the `tabindex` attribute to assist
users who are, typically, using the TAB key to move through the page. This
attribute's value should be used to direct the focus of the elements along the
logical navigation flow of the page.

### Roles

[The WAI-ARIA roles taxonomy UML class diagram][aria-uml] presents a useful
overview of all the roles available.

Roles are implemented using the `role` attribute on an element. As an example, a
common feature of web sites is a sequence of "tabs" which can be used to show
and hide "panels". WAI-ARIA defines `tablist`, `tab`, and `tabpanel`, and
example markup would be as follows:

    <ul role="tablist">
        <li role="tab"><a href="#panel1">First tab</a></li>
        <li role="tab"><a href="#panel2">Second tab</a></li>
        <li role="tab"><a href="#panel3">Third tab</a></li>
    </ul>

    <div id="panel1" class="panel" role="tabpanel">
        <h3>Panel 1</h3> ...
    </div>

    <div id="panel2" class="panel" role="tabpanel">
        <h3>Panel 2</h3> ...
    </div>

    <div id="panel3" class="panel" role="tabpanel">
        <h3>Panel 3</h3> ...
    </div>


[aria-uml]: http://www.w3.org/TR/wai-aria/rdf_model

#### Widget

Widget roles are used to describe custom controls which are typically
dynamically added to a page using JavaScript. A few examples (there are many
more) from the WAI-ARIA specification include:

* `alertdialog`
* `progressbar`
* `sliders`
* `tooltip`

#### Document Structure

Document Structure roles are used to indicate the semantic structure of a page.
Examples include:

* `article`
* `heading`
* `img`
* `region`

#### Landmark

These roles are used to describe specific regions of a page which would
typically help a user navigate around it. Examples include:

* `banner`
* `navigation`
* `search`

### States and properties

States and properties are used to describe an element which is typically playing
a particular role.  They are implemented using an `aria-*` attribute; continuing
the tab example from above, we can extend it to use a property thus:

    <ul role="tablist">
        <li role="tab" id="tab1"><a href="#panel1">First tab</a></li>
    ...
    <div id="panel1" class="panel" role="tabpanel" aria-labelledby="tab1">
    ...

Quite simply, `panel1` is _labelled by_ `tab1`.

As a second example, perhaps we have a registration form with a customised DIV
representing a slider; as the user interacts with the slider, we might update
its `aria-valuenow` property using jQuery as follows:

```javascript
    $("form#register div[role=slider]").attr("aria-valuenow", newVal);
```

`aria-labelledby` and `aria-valuenow` are examples of properties. States are
implemented identically, using attributes; the distinction between a state and a
property is somewhat grey, but examples of states include those that are:

* Applicable to widgets:
    * `checked`
    * `disabled`
    * `selected`
* Broadly applicable:
    * `hidden`
    * `busy`

#### `aria-live`

This property deserves special mention. A "live region" is one which is flagged
as being subject to updates. There are three values for this attribute:

* **off** (the default): unless the region has focus, the user will not be
  "presented" (the manner of this presentation will differ depending on the
  assistive technology) with an update.

* **polite**: updates are "presented" at the next "graceful opportunity" (the
  end of a sentence, a pause in typing).

* **assertive**: the update is "presented" immediately.

### Impact assessment

Traditional web site builds from Communisis Digital, although not usually web
applications, it does feature elements of functionality which SHOULD be marked up
according to the WAI-ARIA guidelines. The following are RECOMMENDED:

* Roles can easily be added to applicable widgets and landmark elements.

* The `tabindex` attribute should be added where appropriate.

* Adding in WAI-ARIA states and properties to the relevant elements, both in
  mark-up and dynamically added and modified with JavaScript where necessary,
  should be considered a simple and effective way to increase the site's
  accessibility.

* The benefits of structural roles seem somewhat less obvious given their
  considerable overlap with HTML5's semantic elements, and it may be worth
  disregarding these.

[aria]: http://www.w3.org/TR/wai-aria/

## Miscellaneous

* Links SHOULD never open in a new window (`target="_blank"` in HTML or
  `window.open()` in JavaScript) - this breaks the back button and provides a
  frustrating experience for users; this is supported by
  [advice from the RNIB][rnib-nw] and [Webcredible][webcredible-nw], as well as
  articles from usability and accessibility experts [Jakob Nielsen][useit-nw]
  and [Mark Pilgrim][dive-nw].

* For a discussion of tables and how they should be used accessibly, see _HTML_.

[rnib-nw]:        http://www.rnib.org.uk/professionals/webaccessibility/designbuild/navigation/pages/new_windows.aspx
[webcredible-nw]: http://www.webcredible.co.uk/user-friendly-resources/web-usability/new-browser-windows.shtml
[useit-nw]:       http://www.useit.com/alertbox/990530.html
[dive-nw]:        http://diveintoaccessibility.info/day_16_not_opening_new_windows.html

### `alt` attributes

The HTML `alt` attribute is used to provide a text alternative for images.
Inline `image` tags MUST always have an `alt` attribute. The following examples
are allowed.

    <img src="image.png" alt="" />
    <img src="logo.png" alt="{{Client Name}}" />

If the image in question is used purely for visual effect or if the information
the image is conveying is present elsewhere within the same area of the page,
the `alt` attribute SHOULD be left empty.

    <img src="divider.png" alt="" />
    <img src="spacer.png" alt="" />

The `alt` attribute MUST NOT be omitted. The following example is not allowed.

    <img src="logo.png" />

Where text is used in an `alt` attribute, the text used MUST be meaningful,
relevant and helpful. The following examples show useful alternative text.

    <img src="logo.png" alt="{{Client Name}}" />
    <img src="icon-zoom.png" alt="View larger image" />

The following examples show `alt` text that is not useful.

    <img src="logo.png" alt="Logo" />
    <img src="icon-zoom.png" alt="Magnifying glass" />

CSS background images are ignored by screen readers and MUST be used for
decorative images only, and MUST NOT be used for images intended to convey
information to the user.

### Form labels

Form field elements (such as `input`, `textarea` and `select`) MUST be
associated with a `label` element. The `label` element MUST contain a `for`
attribute containing the `id` of the associated form field. However, if the
`label` element encloses the related form element, the `for` attribute may be
excluded.

If form fields are not associated with `label`s, screen reader users will not be
able to understand what information is necessary to complete each field in a
form.

The following are examples of _correct_ `label` usage.

**Text type:**

    <label for="first-name" />First name:</label>
    <input type="text" id="first-name" />


**Select:**

    <label for="country" />Country:</label>
    <select id="country">
        <option value="united kingdom">United Kingdom</option>
        ...
    </select>

**Checkbox with wrapped `label`:**

    <label>
        <input type="checkbox" /> Accept Terms and Conditions
    </label>


The following are examples of _incorrect_ `label` usage.

**no `label` used:**

    First name:
    <input type="text" id="last-name" />


**`label` does not match `id`:**

    <label for="first-name" />First name:</label>
    <input type="text" id="last-name" />


**`for` attribute is missing from `label`:**

    <label />First name:</label>
    <input type="text" id="last-name" />

