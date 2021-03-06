StringGenerator
===============

Generate test data, unique ids, passwords, vouchers or other randomized
textual data very quickly using a template language. The template
language is superficially similar to regular expressions but instead of
defining how to match or capture strings, it defines how to generate
randomized strings. A very simple invocation to produce a random string
with word characters and digits of 10 characters length:

::

   >>> import strgen
   >>> strgen.StringGenerator("[\d\w]{10}").render()
   'sj5ic8vebF'

The purpose of this module is to save the Python developer from having
to write verbose code around the same pattern every time to generate
passwords, keys, tokens, test data, etc. of this sort:

::

     my_secret_key = ''.join(random.choice(string.ascii_uppercase + string.digits) for x in range(30))

that is:

1. Hard to read even at this simplistic level.

2. Hard to safely change quickly. Even modest additions to the
   requirements need unreasonably verbose solutions.

3. Doesn’t use safe encryption standards.

4. Doesn’t provide the implied minimal guarantees of character
   occurance.

5. Hard to track back to requirements (“must be between x and y in
   length and have characters from sets Q, R and S”).

The template uses short forms similar to those of regular expressions.
An example template for generating a strong password:

::

    [\w\p\d]{20}

will generate something like the following:

::

    P{:45Ec5$3)2!I68x`{6

Guarantee at least two “special” characters in a string:

::

    [\w\p]{10}&[\p]{2}

You can also generate useful test data, like fake emails with plenty of
variation:

::

    [\c]{10}.[\c]{5:10}@[\c]{3:12}.(com|net|org)

Testing
-------

For running the unit tests, you might want to try:

::

   pip install pytest
   pytest strgen/test.py --verbose

License
-------

Released under the BSD license.

Acknowledgements
----------------

Thanks to Robert LeBlanc who caught some important errors in escaping
special characters. Thanks to Andreas Motl for the progress counter.

Original Author: paul.wolf@yewleaf.com


.. toctree::
   :maxdepth: 2
   :caption: Contents:

   installation
   usage
   progress
   debugging
   rationale

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
