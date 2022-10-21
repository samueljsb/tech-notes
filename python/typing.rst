Python typing
=============

Python is progressively typed: you don't *have* to type everything but it can
be useful.

Protocols
---------

Protocols are used for *structural subtyping*, which is a thing Python allows
because it is dynamically typed.

resources
^^^^^^^^^
- `PEP 544`_ explains a lot. This has a lot
   of discussion and links to further reading, so it's a good place to go for a
   deep dive into this stuff.
- anthony explains: `structural subtyping in python with Protocol`_

.. _PEP 544: https://peps.python.org/pep-0544/
.. _structural subtyping in python with Protocol: https://www.youtube.com/watch?v=QjFChmQHJxk

Name mangling
-------------

This usually applies to class attributes (or methods), but can be used for
argument names, too. This is documented in the `mypy docs
<https://mypy.readthedocs.io/en/stable/protocols.html?highlight=double%20underscore#callback-protocols>`_

   Argument names in __call__ methods must be identical, unless a double
   underscore prefix is used.

Attribute mangling is documented in the `Python docs for classes`_. (Be careful
here: "private" doesn't mean the same thing in Python that it does in other
languages. There's a video from Anthony Sottile explaining that `double
underscored names are NOT "more private"`_.)

.. _Python docs for classes: https://docs.python.org/3/tutorial/classes.html#private-variables
.. _double underscored names are NOT "more private": https://www.youtube.com/watch?v=IVqLW1NWtPc
