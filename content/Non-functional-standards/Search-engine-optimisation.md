/* 
Title: Search Engine Optimisation
Sort: 3
*/

We offer some basic guidelines and suggestions around optimisation of
site content to increase its prominence, visibility, and
usefulness in search engine results pages. Our suggestions are mainly focused
on Google, which has considerably the [highest market share][market-share].

[market-share]: http://en.wikipedia.org/wiki/Web_search_engine#Market_share

## Page title

Pages SHOULD make effective use of the `TITLE` element; where possible, the
`TITLE` of the page SHOULD reflect both the page that is currently being viewed
_and_ the category or section under which it falls, if applicable. The page
title is what is shown first in search engine results.

The name of the page (product name, for example) SHOULD be given priority in the
page and be followed by category or section title (where users have multiple
tabs open, the name of the tab is truncated from right to left, thus having the
category at the start should ensure that it is always visible).

Examples:

* Homepage:

       Site title

* Category selected:

        Catagory - Site title

* Sub-category within category:

        Sub Cat - Catagory - Site title

* Final sub-sub-category:

        Sub-sub Cat - Sub Cat  - Catagory - Site title

We would not advise going deeper than two sub-categories in the page title (even
though this may be possible on the site itself) - Google limits page titles in
search results to approximately 70 characters, and any in-page
breadcrumb navigation should be sufficient to indicate to the user where they
currently are.

The `META` `title` tag is superfluous and SHOULD NOT be used.

## Use of `META` tags

The site SHOULD use a small but useful subset of `META` tags.

This MAY include site specific meta tags with appropriate namespacing (e.g. Facebook Opengraph OG: tags)

### `description`

This SHOULD be used to provide a succinct summary of the _current page_ - that
is to say, each page should have a description which matches its particular
content.

The description is shown beneath the title in search engine results; they are
typically truncated at around 160 characters, so this SHOULD be the upper limit
on the length of the description.

### `keywords`

A minimal set of relevant keywords MAY be used on each page. If possible, the
keywords used should be tailored to fit the content of each page. Repetition of
keywords (and keywords with common misspellings) should be avoided: Google at
least, will downrank pages due to "keyword stuffing".

### Dublin Core

There is very little evidence that search engines respect this attempt at
standardisation of `META` tags, so this MUST NOT be used.

## Google Rich Snippets and microdata

Google has functionality for displaying a small amount of additional information
underneath search results, which it calls "[rich snippets][rich-snippets]". A
small amount of extra markup, in a specific format, must be added to the page in
order for Google to render it as a rich snippet.

Google supports rich snippets for a variety of different types of content; we
RECOMMEND focusing on [Products][snippets-products] and
[Recipes][snippets-recipes], and also using [Organizations][snippets-orgs] to
provide rich contact information for the site.

Google supports three formats of markup: Microdata, Microformats, and RDFa. Of
these, it recommends Microdata, which is a [draft specification][microdata] and
part of the HTML5 standardisation process. Although Microformats and RDFa are
older and more established, our two main points of concern are:

* Simplicity of implementation.
* Support from Google.

Since Google supports all three formats, simplicity is the more important
factor. We can summarise implementation for each format as follows:

* _Microdata_ - custom properties on regular HTML elements:

        <span itemprop="address" itemscope itemtype="http://data-vocabulary.org/Address">
            ...


* _Microformats_ - keywords used with the standard `class` attribute:

        <div class="vcard">
            ...
            <span class="fn"> ...
            <span class="adr"> ...


* _RDFa_ - XHTML namespacing and custom properties:

        <div xmlns:v="http://rdf.data-vocabulary.org/#" typeof="v:Person">


Because Microformats uses the `class` attribute, this may cause conflicts with
other `class`es in use and may lead to extra markup. RDFa seems to have an extra
layer of complexity for little gain, and requires the use of XHTML.

For these reasons, we RECOMMEND using Microdata.

[rich-snippets]:        http://support.google.com/webmasters/bin/answer.py?hl=en&answer=99170
[snippets-products]:    http://support.google.com/webmasters/bin/answer.py?hl=en&answer=146750
[snippets-recipes]:     http://support.google.com/webmasters/bin/answer.py?hl=en&answer=173379
[snippets-orgs]:        http://support.google.com/webmasters/bin/answer.py?hl=en&answer=146861
[microdata]:            http://dev.w3.org/html5/md/

## Sitemap

We RECOMMEND producing a sitemap; this will increase the site's
crawlability and may also boost the site's accessibility. The sitemap SHOULD,
broadly, cover the main categories of products and services that the site
provides, and should present this information hierarchically (mirroring the
navigation menus).

It MUST be kept current and updated (ie. it should be generated automatically).

We do not see any utility in having a product listing page.

### Google Sitemap

We RECOMMEND producing a sitemap based on the Web Sitemap protocol and
submitting this to Google. They have a [good support article][sitemap] about
this process.

[sitemap]: http://support.google.com/webmasters/bin/answer.py?hl=en&answer=183668

### Redirects

Redirects MUST be "path-to-path" rather than "path-to-root" (eg.
`http://domain.com/foo/bar` should redirect to
`http://www.domain.com/foo/bar` rather than to `http://www.domain.com/`).

Redirects MUST have a status code of `301 Moved Permanently`. Do not use 302
('Found' or 'Moved Temporarily'), the HTML `META refresh` tag, or JavaScript
redirects (ie. using client-side scripting to change the `window.location`
with `document.write` or a function called on `window.onload`).

### Policy for usage of `rel="canonical"`

Canonical links MUST be specified on all pages which are reachable via multiple
URLs. The canonical URL should be that of the cleanest path to the data.

### Friendly URL construction

Page URLs SHOULD be friendly and human-readable. This can help users know what
content to expect from a page and aids search engine indexing.
