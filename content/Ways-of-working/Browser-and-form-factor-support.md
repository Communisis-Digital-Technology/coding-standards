/* 
Title: Browser and device support
Sort: 1
*/


## Introduction

This document outlines default browser and form factor support for Communisis Digital.

All code produced for Communisis Digital MUST abide by the support charts detailed 
below.

Browser support requirements are expected to be updated on a quarterly basis.
See the _Introduction_ for more detail on the update cycle.

You MUST confirm that you have the most recent version of this document before
proceeding with development or testing.

## Notes on browser support

The modern browser landscape is quite complex and rapidly changing all the time.  In all our projects, Communisis Digital try to strike the right balance between delivering features efficiently by using modern technologies, whilst trying to ensure the maximum reach for the site through compatibility with legacy browsers, minor and edge case browsers and deprecated platforms.

Website code is interpreted at runtime by browser clients, and the various implementations of rendering engines in different browser clients interpret code differently.  It is the aim of all projects to implement features in such a way to provide a consistent experience across all browsers, however there will always be variation in the way browsers interpret and render code and content, and in the level of support for features of the code.  There is more information on this in our coding standards documentation and we refer to [http://www.caniuse.com/](http://www.caniuse.com/) for a guide to compatibility of specific features within web technology.  

Since there is a limit to what we can naturally support completely without branching code for specific platforms (to be avoided wherever possible), we take a graded approach to browser support with the following levels:

+ Grade A - Fully supported, both functionally and visually.  These are normally the major or latest versions of a browser in common circulation.  This information is taken from global and local market statistics as well as previous traffic reporting for incumbent sites where relevant.  We would expect these browsers to appear both functionally and visually as per all proposed designs, wireframes expected functionality.  There may be certain variations in the way that even Grade A browsers render some elements, particularly in the way rich fonts appear.  The aim is for consistency and robustness.

+ Grade B - As much functional support as possible, with some degradation of visual elements and performance.  Grade B browsers are expected to make all functions of the site (i.e. navigation, links, scripts, forms, interactions) available – the user should not be constricted from interacting with the site.  Where a function set is not supported, it should be entirely removed from display in Grade B browsers.  Visually, the site should not appear ‘broken’ but some degradation in the visual fidelity is to be expected (e.g. rounded corners appearing square, minor layout or spacing issues etc.).    Any degradation in visual or functional fidelity should be handled gracefully without impairment to the end users enjoyment of the site.

+ Grade C - No direct support for site function provided. We do not QA on Grade C browsers.  Sites may well work to a significant level on these platforms but we do not test on them and we do not, except if explicitly required, guarantee functional or visual compatibility on them.  This normally includes deprecated browser versions, niche/edge cases (i.e. games console browsers) or instances of a web rendering engine in non-browser applications.
A matrix is given below on current browser grading. If any exceptions are required, please inform Communisis Digital. If internal IT policies cannot support a grade A browser, please also flag this so we can identify in detail elements of the site build that likely to be degraded.

The cut-off for Core grade A support is 1% of total usage in any given quarter.
Any browser falling below this threshold should be considered B grade.

In Compatibility View, websites will be displayed as if you were viewing them in a previous version of Internet Explorer. Support of a particular version of IE does not extend to support for that version of the browser in "compatibility mode" or in "emulation" mode, but only in the standard mode for that browser. Versions 8, 9 & 10 of Internet Explorer offer compatibility mode, it was renamed "emulation" in version 11. 

### Desktop Browser Grade A

| Platform | Name | Version |
|----------|------|---------|
|OSX 10.9, OSX 10.10, Win7, Win8 | Chrome | Latest*|
|OSX 10.9, OSX 10.10, Win7, Win8 | Firefox | Latest*|
|OSX 10.10 | Safari | 8|
|OSX 10.9| Safari | 7|
|Win8 | IE | 11+|
|Win7 | IE | 10|
|Vista | IE | 9|

*Both Firefox and Chrome implement a rapid release cycle with background updating.  We therefore work to the current stable build.

### Desktop Browser Grade B

|Platform |  Name | Version |
|---------|-------|---------|
|Vista| IE | 8|

*Both Firefox and Chrome implement a rapid release cycle with background updating. Where possible, we also work to the previous browser version on the previous OS version. 

### Desktop Browser Grade C

|Platform |  Name | Version |
|---------|-------|---------|
|WinXP | IE | <8|
|OS X 10.9, OSX 10.10, WinXP, Vista, Win7, Win8 | Opera | All versions|

Alternate platforms not covered above (e.g. games consoles, linux, non-browser based implementations of a web rendering engine)


### Mobile Browser Grading

Communisis Digital only support grade A browsers on mobile. All others will not be included within test scope unless otherwise agreed. This also includes native application in-built webviews (i.e. Twitter clients).

|Platform |  Name | Version |
|---------|-------|---------|
|iOS8+| Mobile Safari| 7+|
|IOS8+ | Chrome | Current vers only|
|Android 4.3+ | Chrome* | Current vers only|

*please note, as of Jellybean, Chrome is the default browser on Android devices and we will test this as our target Android platform.  Android browser is not supported directly as a result, however since all versions of the browser from 4.0 (Ice Cream Sandwich) onward are built on the same version of Webkit, we don’t anticipate there being much variance in the rendering of pages.  We don’t, however, test thoroughly on ICS since the platform is in steep decline.  

### Mobile and tablet test devices

Communisis Digital test on the following devices:
+ iOS7, iOS8 (iPad Mini, iPad air, iPhone 5, iPhone 6) 
+ Android 4.3, 4.4 (Samsung Galaxy S5, Nexus 5, Samsung Galaxy tablet, Nexus 7)
Additional devices can be targeted on request. Devices outside this configuration may incur extra charges. 

The following devices are also avaliable for testing if requested by the client:
+ iOS5, iOS6 (iPad 1, iPad 2, iPad 3, iPhone 3, iPhone 4) 
+ Android 4.0.3, 4.0.4 (Samsung Galaxy tablet, Samsung Galaxy S2, Samsung Galaxy S3, Samsung Galaxy S4)

## Responsive design

The site will be built in a "mobile-first" manner - that is to say, it will
be a responsive site which will effectively render with differing layouts
(number of columns, font and image size, etc) at different resolutions on
different devices at different "breakpoints".

## Graceful degradation and progressive enhancement

Core grade A support MUST NOT be taken to mean that the user experience will be
exactly the same in all supported browsers.

This approach helps ensure that:

* Advanced features in modern browsers can be employed where available and
  appropriate. For example, HTML5 form input types such as `search`, `email` and
  `url` will enhance the user experience in modern, supported browsers (Chrome,
  Firefox, Safari, IE10+) but will not be supported in less capable supported
  browsers (IE8, IE9).

* Techniques employed to cater for non-critical visual-only effects in less
  capable Core grade browsers (eg. IE8) are not employed when they would
  adversely affect the performance of more capable, popular browsers. For
  example, using images to create rounded corners on containers involves
  additional HTTP overheads. Instead, rounded corners should be generated using
  the CSS3 `border-radius` property. In this example, users of modern browsers
  (Chrome, Firefox, Safari, IE9+) would see rounded corners as intended. Users
  of less capable browsers (IE8) would see the same element with square corners.

For more on graceful degradation and progressive enhancement, refer to
the _Development principles_ section of this document.

### Form factor support

Form factor and interaction requirements SHOULD be considered during development
and testing of Core grade browsers and SHOULD follow the principle of
progressive enhancement.

For example, if a Core grade A browser and OS combination supports or requires
Touch events (notably iPad Safari 5.x+), these SHOULD work as expected on that
browser and OS combination.

*Notes*

* iPad is accounted for under the Desktop and tablet support.
* The Android market is [exceptionally fragmented][android-fragmentation].
  Testing across a wide range of devices, operating systems and browser versions
  is impractical and costly. As such, we recommend that testing be limited to
  the two most popular Android devices; the Samsung GT-I9100 Galaxy S2 and the
  original HTC Desire. This selection should be reviewed regularly as part of
  the quarterly update.

[android-fragmentation]:               http://opensignalmaps.com/reports/fragmentation.php
