pandas installation
===================

With :doc:`python4datascience:productive/envs/spack/index` you can provide pandas
in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install py-pandas

Alternatively, you can also install pandas with other package managers, for
example with :doc:`Pipenv <python4datascience:productive/envs/pipenv/index>`.

.. note::
   If you have not yet installed pipenv, you can find instructions on how to do
   this in `Pipenv installation
   <python4datascience:productive/envs/pipenv/install>`.

.. code-block:: console

    $ pipenv install pandas

You can then check the installation with:

.. code-block:: pycon

    >>> import pandas as pd
