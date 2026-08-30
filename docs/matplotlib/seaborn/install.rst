seaborn installation
====================

With :doc:`python4datascience:productive/envs/spack/index` you can install seaborn in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install py-seaborn

Alternatively, you can also install seaborn with other package managers, for
example with :doc:`uv <python4datascience:productive/envs/uv/index>`.

.. note::
   If you have not yet installed uv, you can find instructions on how to do this
   in :ref:`uv installation <python-basics:uv>`.

.. code-block:: console

    $ uv add seaborn

You can check the installation with

.. code-block:: pycon

    >>> import seaborn as sns
