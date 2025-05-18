Visualising data
================

This tutorial provides an overview of the various Python libraries that you can
use for data visualisation. It was developed from the cusy training courses on
`data visualisation with Python
<https://cusy.io/en/our-training-courses/python-training-for-analysts-scientists-and-engineers>`_.

It is currently very difficult to get an :doc:`overview` of the libraries for
data visualisation. In the following, we try to simplify the search for the
right library by taking a closer look at some aspects:

* :ref:`technologies`
* :ref:`core-libs`
* :ref:`pandas-plot-api`
* :ref:`further-high-level-apis`
* :ref:`big-data`
* :ref:`chart-types` (statistical representations, regular and irregular grids,
  :abbr:`etc. (et cetera)`)

We then give a practical introduction to the most common Python libraries.

However, we will not cover  :doc:`design principles
<cusy-design:viz/diagram-anatomy/index>`,  :doc:`the structure of a diagram
<cusy-design:viz/diagram-anatomy/index>`, :doc:`data storytelling
<cusy-design:viz/data-storytelling>` or :doc:`the selection of the appropriate
diagram type <cusy-design:viz/types/index>`. However, we would like to refer you
to the :doc:`cusy-design:index`.

In addition, the PyViz tutorial is part of a series of tutorials on data
analysis and visualisation:

* `Python Basics <https://python-basics-tutorial.readthedocs.io/en/latest/>`_
* :doc:`jupyter-tutorial:index`
* :doc:`python4datascience:index`

All tutorials serve as seminar documents for our harmonised training courses:

+---------------+--------------------------------------------------------------+
| Duration      | Topic                                                        |
+===============+==============================================================+
| 3 days        | `Introduction to Python`_                                    |
+---------------+--------------------------------------------------------------+
| 2 days        | `Advanced Python`_                                           |
+---------------+--------------------------------------------------------------+
| 2 days        | `Design patterns in Python`_                                 |
+---------------+--------------------------------------------------------------+
| 2 days        | `Efficient testing with Python`_                             |
+---------------+--------------------------------------------------------------+
| 1 day         | `Software documentation with Sphinx`_                        |
+---------------+--------------------------------------------------------------+
| 2 days        | `Technical writing`_                                         |
+---------------+--------------------------------------------------------------+
| 3 days        | `Jupyter notebooks for efficient data science workflows`_    |
+---------------+--------------------------------------------------------------+
| 2 days        | `Numerical calculations with NumPy`_                         |
+---------------+--------------------------------------------------------------+
| 2 days        | `Analysing data with pandas`_                                |
+---------------+--------------------------------------------------------------+
| 3 days        | `Read, write and provide data with Python`_                  |
+---------------+--------------------------------------------------------------+
| 2 days        | `Cleanse and validate data with Python`_                     |
+---------------+--------------------------------------------------------------+
| 5 days        | `Visualising data with Python`_                              |
+---------------+--------------------------------------------------------------+
| 1 days        | `Designing data visualisations`_                             |
+---------------+--------------------------------------------------------------+
| 2 days        | `Create dashboards`_                                         |
+---------------+--------------------------------------------------------------+
| 3 days        | `Versioned and reproducible storage of code and data`_       |
+---------------+--------------------------------------------------------------+
| Subscription  | `News from Python for data science`_                         |
| of 2 hours    |                                                              |
| per quarter   |                                                              |
+---------------+--------------------------------------------------------------+

.. _`Introduction to Python`:
   https://cusy.io/en/our-training-courses/introduction-to-python
.. _`Advanced Python`:
   https://cusy.io/en/our-training-courses/advanced-python
.. _`Design patterns in Python`:
   https://cusy.io/en/our-training-courses/design-patterns-in-python
.. _`Efficient testing with Python`:
   https://cusy.io/en/our-training-courses/efficient-testing-with-python
.. _`Software documentation with Sphinx`:
   https://cusy.io/en/our-training-courses/software-documentation-with-sphinx
.. _`Technical writing`:
   https://cusy.io/en/our-training-courses/technical-writing
.. _`Jupyter notebooks for efficient data science workflows`:
   https://cusy.io/en/our-training-courses/jupyter-notebooks-for-efficient-data-science-workflows
.. _`Numerical calculations with NumPy`:
   https://cusy.io/en/our-training-courses/numerical-calculations-with-numpy
.. _`Analysing data with pandas`:
   https://cusy.io/en/our-training-courses/analysing-data-with-pandas
.. _`Read, write and provide data with Python`:
   https://cusy.io/en/our-training-courses/read-write-and-provide-data-with-python
.. _`Cleanse and validate data with Python`:
   https://cusy.io/en/our-training-courses/cleanse-and-validate-data-with-python
.. _`Visualising data with Python`:
   https://cusy.io/en/our-training-courses/visualising-data-with-python
.. _`Designing data visualisations`:
   https://cusy.io/en/our-training-courses/designing-data-visualisations
.. _`Create dashboards`:
   https://cusy.io/en/our-training-courses/create-dashboards
.. _`Versioned and reproducible storage of code and data`:
   https://cusy.io/en/our-training-courses/versioned-and-reproducible-storage-of-code-and-data
.. _`News from Python for data science`:

.. seealso::

   * `Data Visualisation Guide
     <https://data.europa.eu/apps/data-visualisation-guide/>`_
   * `Graphical Perception: Theory, Experimentation, and Application to the
     Development of Graphical Methods
     <https://www.math.pku.edu.cn/teachers/xirb/Courses/biostatistics/Biostatistics2016/GraphicalPerception_Jasa1984.pdf>`_
   * `Financial Times Chart Doctor: Visual vocabluary
     <https://github.com/Financial-Times/chart-doctor/tree/main/visual-vocabulary>`_
   * `The Data Visualisation Catalogue <https://datavizcatalogue.com/>`_
   * `Cartography Guide <https://www.axismaps.com/guide/map-projections>`_
   * `Xenographics <https://xeno.graphics/>`_

.. toctree::
    :titlesonly:
    :maxdepth: 0
    :hidden:

    first-steps
    overview
    matplotlib/index
    vega/index
    bokeh/index
    opengl/index
    d3js/index
    js/index
    protomaps/index
