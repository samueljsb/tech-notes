Python basics
=============

General advice and explanations about Python.

Position-only and keyword-only arguments
----------------------------------------

We use the keyword-only syntax a lot in Kraken. We have a convention to make
use cases keyword-only, although I personally prefer to make the first argument
positional if it's obvious what it should be, e.g::

   issue_billing_document(billing_document=billing_document, ...)

looks a bit silly to me.

resources
^^^^^^^^^

- anthony explains: `all python argument / parameter types`_
- `PEP 570`_ introduced positional-only arguments.

.. _all python argument / parameter types: https://www.youtube.com/watch?v=aKCfCmSggPg&t=641s
.. _PEP 570: https://peps.python.org/pep-0570/
