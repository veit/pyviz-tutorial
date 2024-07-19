Quick Start
===========

.. image:: https://img.shields.io/github/contributors/veit/pyviz-tutorial.svg
   :alt: Contributors
   :target: https://github.com/veit/pyviz-tutorial/graphs/contributors
.. image:: https://img.shields.io/github/license/veit/pyviz-tutorial.svg
   :alt: License
   :target: https://github.com/veit/pyviz-tutorial/blob/main/LICENSE
.. image:: https://results.pre-commit.ci/badge/github/veit/pyviz-tutorial/main.svg
   :alt: pre-commit.ci status
   :target: https://results.pre-commit.ci/latest/github/veit/pyviz-tutorial/main
.. image:: https://readthedocs.org/projects/pyviz-tutorial/badge/?version=latest
   :alt: Docs
   :target: https://pyviz-tutorial.readthedocs.io/de/latest/
.. image:: https://img.shields.io/badge/dynamic/json?label=Mastodon&query=totalItems&url=https%3A%2F%2Fmastodon.social%2F@PyViz%2Ffollowers.json&logo=mastodon
   :alt: Mastodon
   :target: https://mastodon.social/@PyViz

Installation
------------

#. Download and unpack:

   .. code-block:: console

    $ curl -O https://codeload.github.com/veit/pyviz-tutorial/zip/refs/heads/main
    $ unzip main
    Archive:  main
    …
       creating: pyviz-tutorial-main/
    …

#. Install Pandoc:

   * for Ubuntu and Debian:

     .. code-block:: console

        $ sudo apt install pandoc

   * for macOS:

     .. code-block:: console

        $ brew install pandoc

#. Install Python packages:

   .. code-block:: console

    $ cd pyviz-tutorial
    $ python3 -m venv .
    $ bin/python -m pip install  --upgrade pip setuptools
    $ bin/python -m pip install -r requirements.txt

#. Create HTML documentation:

   .. code-block:: console

    $ bin/sphinx-build -b html docs/ docs/_build/

#. Create PDF:

   You will need additional packages to create PDFs.

   For Debian/Ubuntu you can get these with:

   .. code-block:: console

    $ apt-get install texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended latexmk

   or for macOS with::

   .. code-block:: console

    $ brew cask install mactex
    …
    🍺  mactex was successfully installed!
    $ curl --remote-name https://www.tug.org/fonts/getnonfreefonts/install-getnonfreefonts
    $ sudo texlua install-getnonfreefonts
    …
    mktexlsr: Updating /usr/local/texlive/2020/texmf-dist/ls-R...
    mktexlsr: Done.

   You can then generate a PDF with:

   .. code-block:: console

    $ cd docs/
    $ make latexpdf
    …
    The LaTeX files are in _build/latex.
    Run 'make' in that directory to run these through (pdf)latex
    …

   You will then find the PDF in ``docs/_build/latex/pyviz-tutorial.pdf``.

Follow us
---------

* `GitHub <https://github.com/veit/pyviz-tutorial>`_
* `Mastodon <https://mastodon.social/@PyViz>`_
* `Mastodon <https://mastodon.social/@PyViz>`_

Pull-Requests
-------------

Wenn ihr Vorschläge für Verbesserungen und Ergänzungen habt, empfehle ich euch,
einen `Fork <https://github.com/veit/pyviz-tutorial/fork>`_ meines
`GitHub-Repository <https://github.com/veit/pyviz-tutorial/>`_ zu erstellen
und darin eure Änderungen vorzunehmen. Gerne dürft ihr auch einen *Pull Request*
stellen. Sofern die darin enthaltenen Änderungen klein und atomar sind, schaue
ich mir eure Vorschläge gerne an.
