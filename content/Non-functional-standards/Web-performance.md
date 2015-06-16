/* 
Title: Web performance
Sort: 5
*/

## Introduction

Web performance can be broadly categorised into three areas:

* *Application performance*: how well the application builds and serves pages
  and how it responds to heavy usage.
* *Network performance*: concerned with the route between the application and
  the client.
* *Client performance*: how quickly the browser is able to render the page.

As far as application performance, this document will not go into great detail.
At the very least, follow Ruby and Rails best practices should be followed to
ensure a high level of application performance. We will implement application
monitoring software though we have not confirmed which software package we
will use.

## Importance

> Speed matters online. Study after study has shown that even 100 millisecond
> delays in load times negatively impact user experience and conversions.

Web performance is critical for most projects. Web pages should render as
quickly as possible in the browser. For context:

> * The average Internet connection speed around the world was 2.3 Mbps by the
>   end of 2011. That’s down about 14% from the previous quarter.
> * If a page load takes more than two seconds, 40% are likely to abandon that
>   site.
> * The average impact of a one-second delay means a 7% reduction in
>   conversions. For the $100,000 per day ecommerce site, a one-second delay
>   means $2.5 million in lost revenues in a year.
> * Sales at Amazon increase by 1% for every 100 milliseconds it shaves off
>   download times.
> * When Shopzilla decreased load time by 4 sec, they saw a 25% increase in page
>   views, and conversion rates went up 7-12%.

Source and attribution: <http://www.lukew.com/ff/entry.asp?1553>

## Measuring performance

The traditional measurement of page performance is page weight ie. the combined
filesize of all HTML, CSS, JavaScript, images and other assets required to
render an individual page.

While reducing the amount of data sent to the user can improve
performance, these measurements are somewhat simplistic as they:

* Do not offer significant performance gains unless the existing assets in
  the site are unusually large.
* Can make it difficult to improve page weight without removing content and
  features from a page, which can adversely affect the user experience.
* Do not take into account more significant performance-related factors such as
  asynchronous script loading.

For this reason, the Non-Functional Requirements SHALL be supplemented with
Google's Page Speed measurement.

From the introduction to Google's
[Web Performance Best Practices][web-performance-best-practices]:

> Page Speed evaluates performance from the client point of view, typically
> measured as the page load time. This is the lapsed time between the moment a
> user requests a new page and the moment the page is fully rendered by the
> browser. The best practices cover many of the steps involved in page load time
> including resolving DNS names, setting up TCP connections, transmitting HTTP
> requests, downloading resources, fetching resources from cache, parsing and
> executing scripts, and rendering objects on the page.

> Essentially Page Speed evaluates how well your pages either eliminate these
> steps altogether, parallelize them, and shorten the time they take to
> complete.

[web-performance-best-practices]:       https://developers.google.com/speed/docs/best-practices/rules_intro

### Why use Page Speed?

* *Reasonable approach*: Optimising the performance of existing elements is
  considered to be the most beneficial approach, rather than mandating removal
  of elements. The latter approach can lead to a sub-optimal experience for
  users as features and content are sacrificed for performance.
* *Simplicity*: Page Speed uses a number of tests to score a page from 1 to 100.
  A single number per page makes tracking performance and reporting
  straightforward.
* *Tools*: Page Speed tools are available for a variety of contexts. These
  include browser extensions for [Chrome][page-speed-chrome] and
  [Firefox][page-speed-firefox], hosted services and APIs.
* *Consistency*: Results from Page Speed are consistent regardless of the
  particular tool used to derive the score.
* *Industry standard*: Many useful third-party web performance tools provide
  Page Speed scoring, including [WebPagetest][webpagetest] and
  [HTTP Archive][http-archive]. These tools allow straightforward comparisons
  with competing websites.

**Every page on Communisis Digital builds SHOULD have a Page Speed score of at least 90.**

[page-speed-chrome]:                    https://developers.google.com/speed/docs/insights/using_chrome
[page-speed-firefox]:                   https://developers.google.com/speed/docs/insights/using_firefox
[webpagetest]:                          http://www.webpagetest.org/
[http-archive]:                         http://httparchive.org/

## Approach

Web performance rules can be broadly categorised into two types:

1. HTML and HAML template development rules.
2. Server configuration rules.

The first set of rules SHOULD be used when developing templates. The second set
of rules MAY be implemented when developing templates where practical, as
this allows more accurate testing. However, they should not be considered
mandatory and templates SHOULD NOT be tested against the second set.

Production and test environments MUST conform to both sets of rules.

Each rule in the following section is summarised to avoid duplication. Please
refer to the linked documentation for a full description. Explanatory comments
have been added where necessary. A small number of rules that are not official
Page Speed rules have been included below. These SHOULD be validated manually
during testing.

## HTML and HAML template development rules

These best practices MUST be applied to both HTML and HAML template development.

### *[Avoid bad requests][rule-avoid-bad-requests]*

> Removing "broken links", or requests that result in 404/410 errors, avoids
> wasteful requests.

### *[Avoid CSS @import][rule-avoid-css-import]*

> Using CSS `@import` in an external stylesheet can add additional delays during
> the loading of a web page.

### *[Avoid CSS expressions][rule-avoid-css-expressions]*

> CSS expressions degrade rendering performance; replacing them with
> alternatives will improve browser rendering for IE users.

### *[Avoid document.write][rule-avoid-document-write]*

> Using `document.write()` to fetch external resources, especially early in the
> document, can significantly increase the time it takes to display a web page.

### *[Combine images using CSS sprites][rule-sprite-images]*

> Combining images into as few files as possible using CSS sprites reduces the
> number of round-trips and delays in downloading other resources, reduces
> request overhead, and can reduce the total number of bytes downloaded by a web
> page.

### *[Defer loading of JavaScript][rule-defer-loading-js]*

> Deferring loading of JavaScript functions that are not called at startup
> reduces the initial download size, allowing other resources to be downloaded
> in parallel, and speeding up execution and rendering time.

Please also refer to
[Modular JavaScript and script-loading](#modular-javascript-and-script-loading)
in the [JavaScript](#javascript) section of this document.

### *[Defer parsing of JavaScript][rule-defer-parsing-js]*

> In order to load a page, the browser must parse the contents of all `<script>`
> tags, which adds additional time to the page load. By minimizing the amount of
> JavaScript needed to render the page, and deferring parsing of unneeded
> JavaScript until it needs to be executed, you can reduce the initial load time
> of your page.

Please also refer to
[Modular JavaScript and script-loading](#modular-javascript-and-script-loading)
in the [JavaScript](#javascript) section of this document.

### *[Optimize images][rule-compress-images]*

> Properly formatting and compressing images can save many bytes of data.

Third-party sources (e.g. product images) should deliver compressed images.

Image compression MAY be undertaken as a step in the build process and/or as a
pre-commit hook. However, a number of manual, GUI-based tools are available when
this is not feasible, including:

* [PngOptimizer][tool-pngoptimizer] for Windows
* [ImageOptim][tool-imageoptim] for Mac OS X

[tool-pngoptimizer]:                    http://psydk.org/PngOptimizer.php
[tool-imageoptim]:                      http://imageoptim.com/

### *[Optimize the order of styles and scripts][rule-put-styles-before-scripts]*

> Correctly ordering external stylesheets and external and inline scripts
> enables better parallelization of downloads and speeds up browser rendering
> time.

### *[Parallelize downloads across hostnames][rule-parallelize-downloads]*

> Serving resources from two different hostnames increases parallelization of
> downloads.

HTML and JavaScript SHOULD be served by the application on the primary domain,
but the following assets SHOULD be served from different hostnames:

* Static assets (e.g. CSS and structural images)
* Media assets (e.g. product imagery, CMS imagery and video)

Note that this need not necessarily be a subdomain of the main domain. Many
websites now register a separate, autonomous domain for serving static assets.
For example, `youtube.com` uses `ytimg.com`. This allows for a greater degree of
control over caching. For a more detailed explanation, see
[Why move your Javascript files to a different main domain?][asset-domain].

[asset-domain]:                         http://stackoverflow.com/a/160538

### *[Prefer asynchronous resources][rule-prefer-async-resources]*

> Fetching resources asynchronously prevents those resources from blocking the
> page load.

### *[Put CSS in the document head][rule-put-css-in-head]*

> Moving inline style blocks and `<link>` elements from the document body to the
> document head improves rendering performance.

### *[Remove unused CSS][rule-remove-unused-css]*

> Removing or deferring style rules that are not used by a document avoid
> downloads unnecessary bytes and allow the browser to start rendering sooner.

This rule conflicts with the requirement to serve a single CSS file. It should
be taken to mean that any style rules that are not used anywhere in the site
should be removed from the stylesheet. Note that if styles are commented out,
they should be removed as part of the build process.

### *[Serve resources from a consistent URL][rule-duplicate-resources]*

> It's important to serve a resource from a unique URL, to eliminate duplicate
> download bytes and additional RTTs.

### *[Serve scaled images][rule-scale-images]*

> Properly sizing images can save many bytes of data.

### *[Specify image dimensions][rule-specify-image-dimensions]*

> Specifying a width and height for all images allows for faster rendering by
> eliminating the need for unnecessary reflows and repaints.

### *[Use efficient CSS selectors][rule-use-efficient-css-selectors]*

> Avoiding inefficient key selectors that match large numbers of elements can
> speed up page rendering.

### *[Avoid the use of `media="print"`][rule-avoid-media-print]*

> In the best case scenario it will only block onload. In the worst case it will
> block initial paint, onload and DOMContentLoaded.

Instead, all print rules MUST be included inline in normal screen stylesheet.

```css
    @media print {
        body {font: fit-to-print;}
        .sidebar, .menu {display: none;}
    }
```

The normal screen stylesheet MUST not use a media attribute on the link element.

```html
    <link rel="stylesheet" href="css/main.css" />
```

Note that this is not a formal Page Speed rule and as such is not covered by
Page Speed tests.

<!-- template rules -->

[rule-avoid-bad-requests]:              https://developers.google.com/speed/docs/best-practices/rtt#AvoidBadRequests
[rule-avoid-css-import]:                https://developers.google.com/speed/docs/best-practices/rtt#AvoidCssImport
[rule-avoid-css-expressions]:           https://developers.google.com/speed/docs/best-practices/rendering#AvoidCSSExpressions
[rule-avoid-document-write]:            https://developers.google.com/speed/docs/best-practices/rtt#AvoidDocumentWrite
[rule-sprite-images]:                   https://developers.google.com/speed/docs/best-practices/rtt#SpriteImages
[rule-defer-loading-js]:                https://developers.google.com/speed/docs/best-practices/payload#DeferLoadingJS
[rule-defer-parsing-js]:                https://developers.google.com/speed/docs/best-practices/mobile#DeferParsingJS
[rule-compress-images]:                 https://developers.google.com/speed/docs/best-practices/payload#CompressImages
[rule-put-styles-before-scripts]:       https://developers.google.com/speed/docs/best-practices/rtt#PutStylesBeforeScripts
[rule-parallelize-downloads]:           https://developers.google.com/speed/docs/best-practices/rtt#ParallelizeDownloads
[rule-prefer-async-resources]:          https://developers.google.com/speed/docs/best-practices/rtt#PreferAsyncResources
[rule-put-css-in-head]:                 https://developers.google.com/speed/docs/best-practices/rendering#PutCSSInHead
[rule-remove-unused-css]:               https://developers.google.com/speed/docs/best-practices/payload#RemoveUnusedCSS
[rule-duplicate-resources]:             https://developers.google.com/speed/docs/best-practices/payload#duplicate_resources
[rule-scale-images]:                    https://developers.google.com/speed/docs/best-practices/payload#ScaleImages
[rule-specify-image-dimensions]:        https://developers.google.com/speed/docs/best-practices/rendering#SpecifyImageDimensions
[rule-use-efficient-css-selectors]:     https://developers.google.com/speed/docs/best-practices/rendering#UseEfficientCSSSelectors
[rule-avoid-media-print]:               http://www.phpied.com/5-years-later-print-css-still-sucks/

### Server configuration rules

These best practices concern production environments.

They MUST be used in production and test environments.

Where possible, they SHOULD be configured on test environments used to preview
HTML templates.

### *[Combine external CSS][rule-combine-external-css]*

> Combining external stylesheets into as few files as possible cuts down on RTTs
> and delays in downloading other resources.

NB: This MUST be done as part of the build process.

### *[Combine external JavaScript][rule-combine-external-js]*

> Combining external scripts into as few files as possible cuts down on RTTs and
> delays in downloading other resources.

NB: This MUST be done as part of the build process.

### *[Enable compression][rule-gzip-compression]*

> Compressing resources with gzip or deflate can reduce the number of bytes sent
> over the network.

All files of formats that do not already include some form of compression SHOULD
be compressed with gzip, notably:

* HTML
* CSS
* JavaScript
* JSON
* Plaintext
* XML (including XML Sitemaps, RSS and Atom feeds)
* TTF and OTF (but not WOFF) fonts

NB: The detailed recommendation for this rule states an ordering for CSS key-
value pairs.

> Specify CSS key-value pairs in the same order where possible, i.e. alphabetize
> them.

This point conflicts with the ordering specified in the _CSS_ section of this
document and SHOULD be ignored.

### *[Leverage browser caching][rule-leverage-browser-caching]*

> Setting an expiry date or a maximum age in the HTTP headers for static
> resources instructs the browser to load previously downloaded resources from
> local disk rather than over the network.

Note that caching must be carefully managed to ensure that users always receive
the most recent version of files; this is known as 'revving filenames'.

The filename itself SHOULD be changed between versions; using a querystring to
rev filenames can cause performance issues with proxy servers and caches. See
[Revving Filenames: don’t use querystring][revving-querystring] for more on
this.

See also the
[_Parallelize downloads across hostnames_][rule-parallelize-downloads] rule.

[revving-querystring]:                  http://www.stevesouders.com/blog/2008/08/23/revving-filenames-dont-use-querystring/

### *[Leverage proxy caching][rule-leverage-proxy-caching]*

> Enabling public caching in the HTTP headers for static resources allows the
> browser to download resources from a nearby proxy server rather than from a
> remote origin server.

### *[Make landing page redirects cacheable][rule-cache-landing-page-redirects]*

> Many pages, especially mobile pages, redirect users to a different URL, for
> instance from `www.example.com` to `m.example.com`. Making this redirect
> cacheable by the user's browser can speed up page load times for repeat
> visitors to a site.

### *[ Minify CSS][rule-minify-css]*

> Compacting CSS code can save many bytes of data and speed up downloading,
> parsing, and execution time.

NB: This MUST be done as part of the build process.

### *[ Minify HTML][rule-minify-html]*

> Compacting HTML code, including any inline JavaScript and CSS contained in it,
> can save many bytes of data and speed up downloading, parsing, and execution
> time.

NB: This MUST be done as part of the build process.

### *[Minify JS][rule-minify-js]*

> Compacting JavaScript code can save many bytes of data and speed up
> downloading, parsing, and execution time.

NB: This MUST be done as part of the build process.

### *[Minimize request size][rule-minimize-request-size]*

> Keeping cookies and request headers as small as possible ensures that an HTTP
> request can fit into a single packet.

### *[Minimize DNS lookups][rule-minimize-dns-lookups]*

> Reducing the number of unique hostnames from which resources are served cuts
> down on the number of DNS resolutions that the browser has to make, and
> therefore, RTT delays.

This rule contains a recommendation that early-loaded JavaScript files be served
from the same hostname as the main document.

### *[Minimize redirects][rule-avoid-redirects]*

> Minimizing HTTP redirects from one URL to another cuts out additional RTTs and
> wait time for users.

### *[Serve static content from a cookieless domain][rule-serve-from-cookieless-domain]*

> Serving static resources from a cookieless domain reduces the total size of
> requests made for a page.

### *[Specify a character set][rule-specify-charset-early]*

> Specifying a character set in the HTTP response headers of your HTML documents
> allows the browser to begin parsing HTML and executing scripts immediately.

[rule-combine-external-css]:            https://developers.google.com/speed/docs/best-practices/rtt#CombineExternalCSS
[rule-combine-external-js]:             https://developers.google.com/speed/docs/best-practices/rtt#CombineExternalJS
[rule-gzip-compression]:                https://developers.google.com/speed/docs/best-practices/payload#GzipCompression
[rule-leverage-browser-caching]:        https://developers.google.com/speed/docs/best-practices/caching#LeverageBrowserCaching
[rule-leverage-proxy-caching]:          https://developers.google.com/speed/docs/best-practices/caching#LeverageProxyCaching
[rule-cache-landing-page-redirects]:    https://developers.google.com/speed/docs/best-practices/mobile#CacheLandingPageRedirects
[rule-minify-css]:                      https://developers.google.com/speed/docs/best-practices/payload#MinifyCSS
[rule-minify-html]:                     https://developers.google.com/speed/docs/best-practices/payload#MinifyHTML
[rule-minify-js]:                       https://developers.google.com/speed/docs/best-practices/payload#MinifyJS
[rule-minimize-request-size]:           https://developers.google.com/speed/docs/best-practices/request#MinimizeRequestSize
[rule-minimize-dns-lookups]:            https://developers.google.com/speed/docs/best-practices/rtt#MinimizeDNSLookups
[rule-avoid-redirects]:                 https://developers.google.com/speed/docs/best-practices/rtt#AvoidRedirects
[rule-serve-from-cookieless-domain]:    https://developers.google.com/speed/docs/best-practices/request#ServeFromCookielessDomain
[rule-specify-charset-early]:           https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly
