Python Tooling
==============

Tools for working with Python and how to use them.

pdb
---

The standard python debugger.

pdb++
^^^^^

"A drop-in replacement for pdb" with extra features.

https://pypi.org/project/pdbpp/

Install with::

   pip install pdbpp

configuration
"""""""""""""

I like the 'sticky' feature that puts the current context above the input line,
so I know where I am. I enable it with a config file in my home directory:

.. code:: python

   import pdb


   class Config(pdb.DefaultConfig):
        # Enable pdb++'s sticky feature by default.
        sticky_by_default = True
