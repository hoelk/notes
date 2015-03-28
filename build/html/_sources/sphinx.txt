.. Sphinx Notes documentation master file, created by
   sphinx-quickstart on Tue Oct 28 19:52:57 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Sphinx
######

Contents:

.. toctree::
   :maxdepth: 2

This file documents my struggle with python, django and the sphinx document
format, which is `explained here <http://sphinx-doc.org/rest.html#paragraphs>`_

.. note::
    use ``make html`` in project dir to compile the html file

**Header styles for Documentation**::

    # with overline, for parts
    * with overline, for chapters
    =, for sections
    -, for subsections
    ^, for subsubsections
    ", for paragraphs

Install custom themes
=====================

Builtin themes:
  * http://sphinx-doc.org/theming.html

Cool themes:
  * https://pypi.python.org/pypi/sphinx-bootstrap-theme/
  * https://github.com/bitprophet/alabaster (?)
  * https://github.com/snide/sphinx_rtd_theme


Example::

  $ pip install sphinx_bootstrap_theme
  $ pip install sphinx_rtd_theme

then edit ``conf.py``:

.. code-block:: python

  # At the top.
  import sphinx_bootstrap_theme

  # ...

  # Activate the theme.
  html_theme = 'bootstrap'  # or "sphinx_rtd_theme"
  html_theme_path = sphinx_bootstrap_theme.get_html_theme_path()  # or "[sphinx_rtd_theme.get_html_theme_path()]"

Combine Sphinx and R-Markdown
=============================

The following guide explains how to integrate html reports generated with knitr
into sphinx. It is all a bit hackish but it works.

**1. Change the header of your .Rmd to:**

.. code-block:: markdown

  ---
  output:
    html_fragment:
  ---

This achieves a raw html output without css and java script that will screw
up the layout of our sphinx document.

**2. Save the following file as** ``/source/_static/r-markdown-tweaks.css``:

.. code-block:: css

    pre code {
        extends: highlight;
        white-space: pre;
    }

R-Markdown documents use different css classes than sphinx. The following css
code is required to ensure that the code boxes of your R-markdown generated
html look nice. This is tested with ``sphinx_rtd_theme``, other templates might
require other tweaks.

**3. Download** `highlight.js <https://highlightjs.org/download/>`_ **(for syntax highlighting)**
and save it to ``/source/_static/highlight/``.

**4. Save the following code to ** ``/source/_templates/layout.html``.

.. code-block:: html

      {% extends "!layout.html" %}
      {%- block extrahead %}
      <link rel="stylesheet" href="yoursphinxdir/source/_static/r-markdown-tweaks.css.css">
      <link rel="stylesheet" href="yoursphinxdir/source/_static/highlight/styles/default.css">
      <script src="yoursphinxdir/source/_static/highlight/highlight.pack.js"></script>
      <script>hljs.initHighlightingOnLoad();</script>
      {% endblock %}

This enables syntax highlighting via highlight.js and loads the css tweaks
from above

**5. Knitr your R-markdown document and integrate the output html at the
desired place into your sphinx document:**

.. code-block:: rst

  .. raw:: html
      :file: rmarkdownoutput.html



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

`matlab <file:///home/hoelk/Dropbox/Workspace/matlab/doc/_build/html/index.html>`_
`java <file:///home/hoelk/Dropbox/Workspace/java/doc/_build/html/index.html>`_
`django <file:///home/hoelk/Dropbox/Workspace/django/doc/_build/html/index.html>`_
`postgres <file:///home/hoelk/Dropbox/Workspace/postgres/doc/_build/html/index.html>`_
`r <file:///home/hoelk/Dropbox/Workspace/r/doc/_build/html/index.html>`_
