Matplotlib installation
=======================

With :doc:`python4datascience:productive/envs/spack/index` you can provide
Matplotlib in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install py-matplotlib

Alternatively, you can also install Matplotlib with other package managers, for
example with :doc:`Pipenv <python4datascience:productive/envs/pipenv/index>`:

.. code-block:: console

    $ pipenv install matplotlib

You can then check the installation with:

.. code-block:: pycon

    >>> import matplotlib.pyplot as plt

.. note::
   If you get the error ``TclError: no display name and no $DISPLAY environment
   variable``, you probably need to use the iPython backend for Matplotlib with

   .. code-block:: ipython

      import matplotlib.pyplot as plt

      # iPython backend for matplotlib
      %matplotlib inline

   If you import Matplotlib in a Python file, you must insert the following
   instead:

   .. code-block:: python

      import matplotlib.pyplot as plt


      # iPython backend for matplotlib
      get_ipython().run_line_magic("matplotlib", "inline")
