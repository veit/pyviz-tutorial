yt
==

`yt <https://yt-project.org/>`_ analyses and visualises volume data.

Installation
------------

.. code-block:: console

    $ pipenv install yt

.. note::
   If you have not yet installed pipenv, you can find instructions for this at
   :doc:`python4datascience:productive/envs/pipenv/install`.

You can then check the installation with:

.. code-block:: console

    $ yt -h
    usage: yt [-h] [--config CONFIG] [--paste] [--paste-detailed] [--detailed]
    …

Example
-------

.. code-block:: pycon

    >>> import yt
    >>> ds = yt.load("IsolatedGalaxy/galaxy0030/galaxy0030")
    yt : [INFO     ] 2019-06-05 13:10:39,581 Parameters: current_time              = 0.0060000200028298
    yt : [INFO     ] 2019-06-05 13:10:39,583 Parameters: domain_dimensions         = [32 32 32]
    yt : [INFO     ] 2019-06-05 13:10:39,585 Parameters: domain_left_edge          = [0. 0. 0.]
    yt : [INFO     ] 2019-06-05 13:10:39,586 Parameters: domain_right_edge         = [1. 1. 1.]
    yt : [INFO     ] 2019-06-05 13:10:39,588 Parameters: cosmological_simulation   = 0.0
    >>> ds.r[0.45:0.55, :, :].sum("cell_mass").in_units("Mjup")
    Parsing Hierarchy : 100%|██████████| 173/173 [00:00<00:00, 3427.19it/s]
    yt : [INFO     ] 2019-06-05 13:10:39,676 Gathering a field list (this may take a moment.)
    9985379895930.627 Mjup

.. note::
   An experimental hardware-accelerated interactive volume renderer was
   introduced in version 3.3 of yt. In order to use `Interactive Data
   Visualization (IDV)
   <https://yt-project.org/doc/visualizing/interactive_data_visualization.html>`_,
   `PyOpenGL <https://pypi.org/project/PyOpenGL/>`_ and `cyglfw3
   <https://pypi.org/project/cyglfw3/>`_ with their respective dependencies must
   also be installed.

.. seealso::
   - `Quickstart <https://yt-project.org/doc/quickstart/index.html>`_
   - `Cookbook <https://yt-project.org/doc/cookbook/index.html>`_
   - `Docs <https://yt-project.org/doc/>`_
   - `Extensions <https://yt-project.org/extensions.html>`_
