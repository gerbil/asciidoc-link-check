(Based on [markdown-link-check](https://github.com/tcort/markdown-link-check) module)

<a href="https://asciinema.org/a/TsMPXxqz92aJIeYhUQTsxbpjn?autoplay=1"><img src="https://raw.githubusercontent.com/gaurav-nelson/asciidoc-link-check/master/scr-rec.gif"/></a>

Local Installation
==================

To install the command line tool, run:

``` bash
npm install -g asciidoc-link-check
```

Usage
-----

(Optional) Use the `-p` or `--progress` switch to view progress.

### Check links for a local file

``` bash
asciidoc-link-check README.adoc --progress
```

### Check links for an online file

``` bash
asciidoc-link-check https://github.com/gaurav-nelson/asciidoc-link-check/blob/master/README.adoc
```

### Check links from standard input

``` bash
cat <filename>.adoc | asciidoc-link-check -p
```

### Check links in all asciidoc files in a directory

Check recursively in the current directory:

``` bash
find . -name \*.adoc -exec asciidoc-link-check -p {} \;
```

Check recursively in the other directories:

``` bash
find <directory> -name \*.adoc -exec asciidoc-link-check -p {} \;
```

Using in your node project
--------------------------

To add the module to your project, run:

``` bash
npm install --save asciidoc-link-check
```

Docker Run
==================
1. Clone the repository:

        git clone https://github.com/gaurav-nelson/asciidoc-link-check.git

2. Open the repository directory:

        cd asciidoc-link-check

3. Build a Docker image:

        docker build --tag asciidoc-link-check .

4. Pipe any asciidoc file `test.adoc` to `docker run`:

        docker run --rm -i asciidoc-link-check < test.adoc

API
===

Use the following function:

``` javascript
asciidocLinkCheck(asciidoc, callback)
```

Accepts a string containing `asciidoc` formatted text and a `callback`, extracts all links and checks if they are alive or dead. Then calls the `callback` with `(err, results)`.

Examples
========

JavaScript
----------

``` javascript
'use strict';

var asciidocLinkCheck = require('asciidoc-link-check');

asciidocLinkCheck('xref:https://www.google.com[Google]', function (err, results) {
    if (err) {
        console.error('Error', err);
        return;
    }
    results.forEach(function (result) {
        console.log('%s is %s', result.link, result.status);
    });
});
```
