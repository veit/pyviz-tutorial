Graphviz
========

``Graph-`` and ``Digraph`` objects have a ``_repr_svg_()`` method so that they
can be rendered and displayed directly in a Jupyter notebook.

Installation
------------

.. tab:: Spack

   With :doc:`python4datascience:productive/envs/spack/index` you can provide
   Graphviz in your kernel:

   .. code:: console

      $ spack env activate python-311
      $ spack env status
      ==> In environment python-311
      $ spack install py-graphviz
      …
      ==> Successfully installed py-graphviz
      …
      ==> Updating view at /srv/jupyter/spack/var/spack/environments/python-311/.spack-env/view

.. tab:: Debian/Ubuntu

   First, Graphviz is installed with:

   .. code:: console

      $ sudo apt install graphviz

   You can then install the corresponding Python package in your kernel:

   .. code:: console

      $ pipenv install graphviz

.. tab:: macOS

   First, Graphviz is installed with `Homebrew <https://brew.sh/>`_:

   .. code:: console

      $ brew install graphviz

   You can then install the corresponding Python package in your kernel:

   .. code:: console

      $ pipenv install graphviz

.. toctree::
    :titlesonly:
    :maxdepth: 0
    :hidden:

    examples.ipynb
    libs-tools
