Python packaging
================

Guidance for packaging and distributing Python packages.

Distribution
------------

Before starting, make sure ``main`` is checked out and up to date.

Update the version in ``setup.cfg`` and anywhere else, then commit those
changes::

   VERSION=0.0.0
   git commit -am "v$VERSION"
   git tag "v$VERSION"
   git push origin HEAD --tags

Build the package and publish on PYPI::

   rm -rf build/ dist/
   python setup.py sdist bdist_wheel
   twine upload dist/*
