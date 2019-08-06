Character encoding
******************

In most circumstances, pikepdf performs appropriate encodings and
decodings on its own, or returns :class:`pikepdf.String` if it is not clear
whether to present data as a string or binary data.

``str(pikepdf.String)`` is performed by inspecting the binary data. If the
binary data begins with a UTF-16 byte order mark, then the data is
interpreted as UTF-16 and returned as a Python ``str``. Otherwise, the data
is returned as a Python ``str``, if the binary data will be interpreted as
PDFDocEncoding and decoded to ``str``. Again, in most cases this is correct
behavior and will operate transparently.

Some functions are available in circumstances where it is necessary to force
a particular conversion.

PDFDocEncoding
==============

The PDF specification defines PDFDocEncoding, a character encoding used only
in PDFs. It is quite similar to ASCII but not equivalent.

When pikepdf is imported, it automatically registers ``"pdfdoc"`` as a codec
with the standard library, so that it may be used in string and byte
conversions.

.. code-block:: python

    "•".encode('pdfdoc') == b'\x81'

Other codecs
============

Two other codecs are commonly used in PDFs, but they are already part of the
standard library.

**WinAnsiEncoding** is identical Windows Code Page 1252, and may be converted
using the ``"cp1251"`` codec.

**MacRomanEncoding** may be converted using the ``"macroman"`` codec.