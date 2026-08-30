pandas installation
===================

With :doc:`python4datascience:productive/envs/spack/index` you can provide pandas
in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install py-pandas

Alternatively, you can also install pandas with other package managers, for
example with :doc:`uv <python4datascience:productive/envs/uv/index>`.

.. note::
   If you have not yet installed uv, you can find instructions on how to do this
   in `uv installation <python-basics:uv>`.

.. code-block:: console

    $ uv add pandas

You can then check the installation with:

.. code-block:: pycon

    >>> import pandas as pd
