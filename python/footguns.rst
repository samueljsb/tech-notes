Python footguns
===============

Some not-so-obvious problems that can come up and how to solve them.

ABCs and dataclasses
--------------------

inherited attributes
^^^^^^^^^^^^^^^^^^^^

Beware mixing ABCs and dataclasses: ``ABCMeta`` defines some attributes which
can be picked up by the dataclass machinery by mistake. e.g:

.. code:: python

   import abc
   from dataclasses import dataclass

   class Base(abc.ABC):
       ...

   @dataclass
   class Child(Base):
       register: str
       foo: int

This will fail to import with a ``TypeError``:

.. code:: console

   $ python -mb
   Traceback (most recent call last):
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/runpy.py", line 196, in _run_module_as_main
      return _run_code(code, main_globals, None,
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/runpy.py", line 86, in _run_code
      exec(code, run_globals)
   File "/private/tmp/tmpvenv-5542/b.py", line 8, in <module>
      class Child(Base):
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/dataclasses.py", line 1185, in dataclass
      return wrap(cls)
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/dataclasses.py", line 1176, in wrap
      return _process_class(cls, init, repr, eq, order, unsafe_hash,
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/dataclasses.py", line 1025, in _process_class
      _init_fn(all_init_fields,
   File "/usr/local/Cellar/python@3.10/3.10.8/Frameworks/Python.framework/Versions/3.10/lib/python3.10/dataclasses.py", line 546, in _init_fn
      raise TypeError(f'non-default argument {f.name!r} '
   TypeError: non-default argument 'foo' follows default argument

Solutions
"""""""""

1. re-order the attributes -- if ``register`` is after the other attributes,
   the dataclass machinery will not have a problem with it
2. use a diferent attribute name
3. use ``attrs``

abstract properties
^^^^^^^^^^^^^^^^^^^

Dataclasses canot be used to implement abstract properties:

.. code:: python

   import abc
   from dataclasses import dataclass


   class Base(abc.ABC):
       @property
       @abc.abstractmethod
       def foo(self) -> str: ...


   @dataclass(frozen=True)
   class C(Base):
       foo: str


   c = C(foo="hello")  # TypeError: Can't instantiate abstract class C with abstract method foo

Solutions
"""""""""

An ``attrs`` class will satisfy the ABC.
