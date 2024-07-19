plotnine installation
=====================

In most cases the following installation should be sufficient:

.. code:: console

    $ pipenv install plotnine

For use together with `scikit-learn <https://scikit-learn.org/>`_ and
`scikit-misc <https://github.com/has2k1/scikit-misc>`_, extras can be installed
with

.. code:: console

    $ pipenv install "plotnine[all]"

.. tab:: Jupyter-Notebooks

   .. code:: console

      $ jupyter nbextension enable --py widgetsnbextension

.. tab:: JupyterLab

   .. code:: console

      $ jupyter labextension install @jupyter-widgets/jupyterlab-manager
