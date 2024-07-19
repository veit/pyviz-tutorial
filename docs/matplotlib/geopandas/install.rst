GeoPandas installation
======================

With :doc:`python4datascience:productive/envs/spack/index` you can install
GeoPandas in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install py-geopandas

Alternatively, you can also install GeoPandas with other package managers, for
example with :doc:`python4datascience:productive/envs/pipenv/index`:

.. code-block:: console

    $ pipenv install fiona matplotlib descartes geopandas

.. note::
   If you have not yet installed pipenv, you can find instructions on how to do
   this in :doc:`Pipenv installation
   <python4datascience:productive/envs/pipenv/install>`.

You can then check the installation with:

.. code-block:: pycon

    >>> import geopandas as gpd
