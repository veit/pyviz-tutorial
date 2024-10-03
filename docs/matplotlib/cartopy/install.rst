Cartopy installation
====================

.. tab:: Spack

   With :doc:`python4datascience:productive/envs/spack/index` you can deploy
   Cartopy in your kernel, for example with:

   .. code-block:: console

       $ spack env activate python-311
       $ spack install py-cartopy~epsg~ows~plotting

   This installs Cartopy with the support of:

   * `epsg <https://epsg.io>`_
   * `Open Geospatial Consortium (OGC) <https://www.ogc.org>`_
   * Plot functionality

   The following packages are also installed:

   * `gdal <https://gdal.org/en/latest/>`_
   * :doc:`/matplotlib/index`
   * `OWSLib <https://geopython.github.io/OWSLib/>`_
   * `Pillow <https://pillow.readthedocs.io/en/stable/>`_
   * `pyepsg <https://pyepsg.readthedocs.io/en/latest/>`_
   * `PyShp <https://github.com/GeospatialPython/pyshp>`_
   * `shapely <https://shapely.readthedocs.io/en/stable/>`_
   * `six <https://six.readthedocs.io>`_

.. tab:: Linux

   Alternatively, Cartopy can also be installed with Linux package managers, for
   example for Debian≥9 (Stretch) with:

   .. code-block:: console

       $ sudo apt install proj-bin
       $ sudo apt install libproj-dev
       $ sudo apt install libgeos-dev

.. tab:: macOS

   .. code-block:: console

       $ brew install proj
       $ brew install geos

Cartopy can then be installed for your kernel, for example with:

.. code-block:: console

    $ export PIP_NO_BINARY=:shapely:
    $ pipenv install cython numpy cartopy

For the Cartopy :doc:`examples`, you will also need the following two Python
packages:

.. code-block:: console

    $ pipenv install matplotlib scipy

Optional requirements
---------------------

* `rtree <https://github.com/Toblerity/rtree>`_ for `libspatialindex
  <https://github.com/libspatialindex/libspatialindex>`_
* `psycopg2 <https://pypi.org/project/psycopg2/>`_ for `PostGIS
  <https://postgis.net/>`_
* `geopy <https://github.com/geopy/geopy>`_

Plotting requirements
---------------------

* :doc:`/matplotlib/index`
* `descartes <https://pypi.org/project/descartes/>`_
* `mapclassify <https://pysal.org/mapclassify/>`_

Verify
------

Finally, you can check the installation with:

.. code-block:: pycon

    >>> import cartopy
