Bokeh
=====

`Bokeh <https://docs.bokeh.org/en/latest/>`_ is an interactive visualisation
library for modern web browsers. Its goal is to provide versatile graphics and
extend this capability to very large and streaming datasets through
high-performance interactivity. Bokeh is useful for quickly and easily creating
interactive charts, dashboards and data applications.

To provide both simple and powerful and flexible features required for
extensible customisation, Bokeh provides two interfaces:

:ref:`bokeh.models <bokeh:bokeh.models>`
    Low-level interface that offers application developers the greatest possible
    flexibility
:ref:`bokeh.plotting <bokeh:bokeh.models_plots>`
    High-level interface for the creation of visual glyphs

.. seealso::
   * :doc:`Home <bokeh:index>`
   * :ref:`User Guide <bokeh:userguide>`
   * :doc:`Gallery <bokeh:docs/gallery>`
   * :doc:`Reference Guide <bokeh:docs/reference>`
   * `Source code <https://github.com/bokeh/bokeh>`_
   * Examples

     * `github.com/bokeh/bokeh/tree/main/examples
       <https://github.com/bokeh/bokeh/tree/main/examples>`_
     * `cdn.pydata.org/bokeh/examples/examples-x.y.z.zip
       <https://cdn.pydata.org/bokeh/examples/examples-1.0.4.zip>`_

Installation
------------

With :doc:`python4datascience:productive/envs/spack/index` you can deploy
Bokeh in your kernel, for example with:

.. code-block:: console

    $ spack env activate python-311
    $ spack install   py-bokeh

Alternatively, you can also install Bokeh with other package managers, for
example

.. code-block:: console

    $ pipenv install bokeh

Optional extensions
~~~~~~~~~~~~~~~~~~~

There are extensions for Bokeh for the following functions:

`NodeJS <https://nodejs.org/en/>`_
    Necessary to extend Bokeh or to define ``CustomJS`` implementations in
    CoffeeScript or TypeScript
`pandas <https://pandas.pydata.org/>`_
    Necessary for the Hexbin function. Some applications are simplified by using
    pandas, for example pandas DataFrames are automatically converted to Bokeh
    data sources by Glyph functions
`Psutil <https://psutil.readthedocs.io/en/latest/>`_
    Required to enable detailed memory logging in the Bokeh server
`NetworkX <https://networkx.org>`_
    With ``from_networkx``, the bokeh diagram renderer can be applied directly
    to NetworkX data
`Selenium <https://www.selenium.dev/>`_, `PhantomJS <https://phantomjs.org/>`_
    Necessary for exporting plots to PNG and SVG images

Examples
--------

When installing with ``pip``, the examples are not installed. However, you can
clone the Git repository and look at the examples/ directory to see the
``examples``.

Most of these examples use sample data, which must also be provided separately.
To download these files, simply enter the following:

    $ pipenv run bokeh sampledata

.. toctree::
    :titlesonly:
    :maxdepth: 0
    :hidden:

    styling-theming.ipynb
    data-sources-transformations.ipynb
    annotations.ipynb
    interactions.ipynb
    graph.ipynb
    geographic-plots.ipynb
    bokeh-server.ipynb
    directory-format-apps.ipynb
    embedding-export/notebook.ipynb
    embedding-export/export-html.ipynb
    embedding-export/static-images.ipynb
    embedding-export/flask
    extend.ipynb
    integration/index
