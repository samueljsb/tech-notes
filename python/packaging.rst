Python packaging
================

Guidance for packaging and distributing Python packages.

Distribution
------------

Before starting, make sure ``main`` is checked out and up to date.

Update the version in ``setup.cfg`` and anywhere else, then commit those
changes::

   git commit -am v0.0.0
   git tag v0.0.0
   git push origin HEAD --tags

Build the package and publish on PYPI::

   rm -rf build/ dist/
   python setup.py sdist bdist_wheel
   twine upload dist/*
