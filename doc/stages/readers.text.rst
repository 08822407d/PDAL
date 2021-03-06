.. _readers.text:

readers.text
============

The **text reader** reads data from ASCII text files.  Each point is
represented in the file as a single line.  Each line is expected to be divided
into a number of fields by a separator.  Each field represents a value for
a point's dimension.  Each value needs to be `formatted`_ properly for
C++ language double-precision values.

The text reader expects a header line to 1) indicate the separator character
for the fields and 2) name the point dimension for each field.  Any
single non-alphanumeric character can be used as a separator.  The header line
separator can be overridden by the `separator`_ option.  Each line in the
file must contain the same number of fields as indicated by
dimension names in the header.  Spaces are generally ignored in the input
unless used as a separator.  When a space character is used as a separator,
any number of consecutive spaces are treated as single space and
leading/trailing spaces are ignored.

Blank lines are ignored after the header line is read.

.. embed::

.. streamable::

Example Input File
------------------

This input file contains X, Y and Z value for 10 points.

::

    X,Y,Z
    289814.15,4320978.61,170.76
    289814.64,4320978.84,170.76
    289815.12,4320979.06,170.75
    289815.60,4320979.28,170.74
    289816.08,4320979.50,170.68
    289816.56,4320979.71,170.66
    289817.03,4320979.92,170.63
    289817.53,4320980.16,170.62
    289818.01,4320980.38,170.61
    289818.50,4320980.59,170.58

Example Pipeline
----------------

.. code-block:: json

  [
      {
          "type":"readers.text",
          "filename":"inputfile.txt"
      },
      {
          "type":"writers.text",
          "filename":"outputfile.txt"
      }
  ]


Options
-------

filename
  text file to read [Required]

.. include:: reader_opts.rst

header
  String to use as the file header.  All lines in the file as assumed to be
  records containing point data unless skipped with the `skip`_ option.
  [Default: None]

_`separator`
  Separator character to override that found in header line. [Default: None]

_`skip`
  Number of lines to ignore at the beginning of the file. [Default: 0]

.. _formatted: http://en.cppreference.com/w/cpp/string/basic_string/stof
