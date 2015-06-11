/* 
Title: File formats and encoding
Sort: 2
*/

## Image files

Always choose the appropriate image format. The following guidelines MUST be
applied to all image usage.

* Use JPEGs for all photographic images.
    * JPEGs larger than 10KB should be saved as [Progressive JPEGs][prog-jpg].
* Use PNGs for non-photographic (vector/line-art) images.
* Use GIFs for images which contain animation.
* Do not use any other image formats.
    * In particular, do not use BMPs or TIFFs. These formats generate large
      files that are unsuitable for the web.

[prog-jpg]: http://notes.jayrobinson.org/post/19777516761/quick-note-on-why-you-should-always-use-progressive

## Documentation

Any documentation that requires the use of a separate file (ie. not in-line
documentation) SHOULD be written using the [Markdown][markdown-syntax] syntax
and be saved with a `.md` extension.

The Markdown version of these standards SHOULD be used as a style reference.

[markdown-syntax]: http://daringfireball.net/projects/markdown/

## Text files

Text-based documents (including HTML, CSS, JavaScript, Markdown and plaintext)
MUST meet the following criteria:

* Use UNIX-style line-endings (i.e. LF, not CRLF).
* Strip trailing whitespace from line endings.
* A newline character must be used at the end of each file.

These criteria help ensure consistency and allow proper use of version control
tools.

You SHOULD configure your editor or IDE to enforce these settings.

### Indentation

HTML documents MAY use 2 spaces for indentation.

All other text-based documents (CSS, JavaScript, Ruby, etc.) MUST use 4 spaces
for indentation.

## File naming

### HTML

These conventions MUST be adhered to:

* Use only lowercase characters.
* Use only underscores to separate words e.g. `category_page.html` (please see
  the associated note in *Project-specific requirements* for an explanation).
* Ensure that the correct spelling is used.

### JavaScript

During development, there will be separate JavaScript files for separate
modules; these SHOULD be organised into packages as per their type and function.
All filenames MUST be lowercase, with words separated by hyphens. Examples:

    views/mega-nav.js
    models/nav.js

When deployed in production, the separate JavaScript files representing core
functionality MUST be concatenated and minified into one master file.  We
anticipate this MAY have a name such as `bundle.js`.

Libraries will be stored inside a `libs` directory and will have filenames which
denote their name and version number. During development, we will not use
minified versions of libraries. Examples:

    libs/jquery-1.7.1.js
    libs/backbone-0.9.2.js

### All other files

This includes images, CSS, SWFs and Markdown documentation; these conventions
MUST be adhered to:

* Use only lowercase characters.
* Use only underscores to separate words eg. `main_logo.png`
* Ensure that the correct spelling is used.

## Folder structure

The folder structure SHOULD be specified in the `README.md` at the root of each
project (or similar). Ensure all files accord to the defined file structure.

## Links

### Protocol-relative URLs

[Protocol-relative URLs][protocol-relative-urls] MUST be used when linking to
assets on other domains from HTML and CSS documents. Note that in the follow
examples, `http` or `https` have not been used:

    <img src="//static.domain.com/images/static/file.png" />

    .module { background: url("//static.domain.com/images/static/file.png"); }

Using this approach keeps all asset requests within the same protocol, avoiding
the need to duplicate assets for both secure and non-secure protocols and avoids
the triggering of mixed security zone warnings in Internet Explorer.

[protocol-relative-urls]:   http://paulirish.com/2010/the-protocol-relative-url/
