---
layout: post
---

Typography Test Page
====================

Hypothesis knows that it's looking at the same PDF because it looks at the
PDF's fingerprint. Computing the fingerprint of a PDF turns out to be a simple
algorithm, implemented by PDF.js, based on top of standard identifiers that
PDFs contain.

## Normal Paragraphs

The ID entry is an array of two byte strings.
The first byte string in the array is a "permanent identifier" that's
"based on the contents of the file at the time it was originally created" and
"shall not change when the file is incrementally updated".
This is the identifier that we're interested in.

The second byte string is a secondary identifier that should also be based on
the contents of the file, and should initially have the same value as the first
identifier, but that should be re-computed based on the new file contents each
time the file is updated. It enables you to identify a different version of the
same file. Hypothesis doesn't use this second identifier.

Section 14.4 of ISO 32000-1 goes on to say that file identifiers "should be
computed by means of a message digest algorithm such as MD5" using the current
time, the file's pathname, the size of the file in bytes, and the contents of
the file.  There's of course no guarantee that every program that creates PDFs
computes the IDs in this way.

## Inline Formatting

**bold** _italic_ [A link](http://example.com) `some code` <q>a quote</q>.
A keyboard shorcut: <kbd><kbd>Ctrl</kbd> + <kbd>c</kbd></kbd>.
A `<samp>`: <samp>Sampled Text</samp>.

Code inside a link: [the `foobar` function](/).

## Headings

# Level 1 Heading
## Level 2 Heading
### Level 3 Heading
#### Level 4 Heading
##### Level 5 Heading
###### Level 6 Heading

Using `<code>` within a heading

## How To Use The `MagicMock` Class
### How To Use The `MagicMock` Class

## Code Blocks

A single-line code block:

```sh
$ unison music -auto=false -batch=false
```

A multiline code block:

```python
#!/usr/bin/env python2
"""
Print out the fingerprint of the given PDF file.

Exit with non-zero status code if fingerprinting the file fails.

Installation:

1. Create a new Python virtual environment

2. Install PDFMiner from git (because the version on PyPI is out of date and
   missing AES v2 decryption support):

   pip install git+https://github.com/euske/pdfminer.git

Usage:

    ./fingerprint.py /path/to/file.pdf

"""
import hashlib
import sys

import pdfminer.pdfparser
import pdfminer.pdfdocument


def hexify(byte_string):
    ba = bytearray(byte_string)

    def byte_to_hex(b):
        hex_string = hex(b)

        if hex_string.startswith('0x'):
            hex_string = hex_string[2:]

        if len(hex_string) == 1:
            hex_string = '0' + hex_string

        return hex_string

    return ''.join([byte_to_hex(b) for b in ba])


def hash_of_first_kilobyte(path):
    f = open(path, 'rb')
    h = hashlib.md5()
    h.update(f.read(1024))
    return h.hexdigest()


def file_id_from(path):
    """
    Return the PDF file identifier from the given file as a hex string.

    Returns None if the document doesn't contain a file identifier.

    """
    parser = pdfminer.pdfparser.PDFParser(open(path, 'rb'))
    document = pdfminer.pdfdocument.PDFDocument(parser)

    for xref in document.xrefs:
        if xref.trailer:
            trailer = xref.trailer

            try:
                id_array = trailer["ID"]
            except KeyError:
                continue

            # Resolve indirect object references.
            try:
                id_array = id_array.resolve()
            except AttributeError:
                pass

            try:
                file_id = id_array[0]
            except TypeError:
                continue

            return hexify(file_id)


def fingerprint(path):
    return file_id_from(path) or hash_of_first_kilobyte(path)


if __name__ == '__main__':
    print fingerprint(sys.argv[1])
```

A wide code block should have a horizontal scrollbar:

```python
def test_validate_url_returns_an_http_url_unmodified():
    assert validate_url('http://github.com/jimsmith') == 'http://github.com/jimsmith'

def test_validate_url_adds_http_prefix_to_urls_that_lack_it():
    assert validate_url('github.com/jimsmith') == 'http://github.com/jimsmith'
```

Using `<strong>` (or `<b>`) within a `<pre><code>`:

<pre><code>
@pytest.mark.parametrize('document_uris,expected_web_uri', [
    # Given a single http or https URL it just uses it.
    <strong>([('http://example.com',  'self-claim')],    'http://example.com')</strong>,
    ([('https://example.com', 'self-claim')],    'https://example.com'),
</code></pre>

## Lists

A short unordered list:

* One
* Two
* Three

A short ordered list:

1. One
2. Two
3. Three

A longer list:

* Extract the file identifier from the PDF’s trailer, if it has one

* If the ID can’t be extracted (because the PDF doesn’t contain a trailer,
  the trailer doesn’t contain a valid ID array, etc) then use an MD5 digest
  of the first 1024 bytes of the file instead.

  Blah blah blah.

* Either way, convert the bytes of the ID or digest to a hex string and that’s
  your fingerprint

Nested lists:

1. One
   1. One point one
2. Two
   1. Two point one
   1. Two point two
3. Three

## A Horizontal Rule

A horizontal rule:

* * *

## Quotes

An inline quote: <q>this is the quote</q>.

A blockquote:

> Nothing great is created suddenly, any more than a bunch of grapes or a fig.
> If you tell me that you desire a fig. I answer you that there must be time.
> Let it first blossom, then bear fruit, then ripen.
> <cite>– Epictetus</cite>

## Figures

This is a figure with a caption:

<figure>
<img src="/images/datapackager-dashboard.png" alt="Screenshot of my Data Packager dashboard">
<figcaption>My Data Packager dashboard</figcaption>
</figure>

This is some text following the figure.

## Full Bleed

{% capture code %}
Link checker service                                            Client site
deadoralive                                                     ckanext-deadoralive
                - Give me up to 50 resources to check ------->
                <-------------------- [<id_1>, <id_2>, ... ] -  (Gets resource IDs from db)

                - What's the URL for resource <id_1>? ------->
                <---- The URL for resource <id_1> is <url_1> -  (Gets URL from db)
(Checks <url_1>) - Resource <id_1>'s URL is broken ----------->  (Saves result)

                - What's the URL for resource <id_2>? ------->
                <---- The URL for resource <id_2> is <url_2> -  (Gets URL from db)
(Checks <url_2>) - Resource <id_2>'s URL is working --------->  (Saves result)

                ...
{% endcapture %}

This is the post footer:

