Jupyter reveal
==============

Presentation slides for `Jupyter notebooks <https://jupyter.org/>`_.

|Contributors| |License| |Pyup|

.. |Contributors| image:: https://img.shields.io/github/contributors/cusyio/jupyter-reveal.svg
   :target: https://github.com/cusyio/jupyter-reveal/graphs/contributors
.. |License| image:: https://img.shields.io/github/license/cusyio/jupyter-reveal.svg
   :target: https://github.com/cusyio/jupyter-reveal/blob/main/LICENSE
.. |Pyup| image:: https://pyup.io/repos/github/cusyio/jupyter-reveal/shield.svg
   :target: https://pyup.io/repos/github/cusyio/jupyter-reveal/

Motivation
----------

We spent too much time designing our presentation slides using PowerPoint or
Keynote. Then we needed additional tools for syntax highlighting. Since we were
already working a lot with Jupyter notebooks, it was obvious to use them to
create the slides as well.

Features
--------

Write Markdown
    In Jupyter notebooks we can use `Markdown Cells
    <https://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/Working%20With%20Markdown%20Cells.html>`_.
Built-in syntax highlighting
    You get the appropriate syntax highlighting, e.g. for Python with

    .. code-block:: md

        ```python
        s = "Syntax Highlighting for Python"
        print(s)
        ```

Support for mathematical operators and symbols
    Mathematical operators and symbols are supported with `MathJax
    <https://www.mathjax.org/>`_. You can use them in Markdown and code cells.
    So, e.g. ``$\sqrt{k}$`` becomes |mathematical operators and symbols| and

    .. |mathematical operators and symbols| image:: img/markdown.png

    .. code-block:: python

        from IPython.display import Math
        Math(r'F(k) = \int_{-\infty}^{\infty} f(x) e^{2\pi i k} dx')

    becomes

    .. image:: img/math.png

    However, you can also use other latex modes, e.g. ``eqnarray`` in

    .. code-block:: python

        from IPython.display import Latex
        Latex(r"""\begin{eqnarray}
        \nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \\
        \end{eqnarray}""")

    becomes

    .. image:: img/latex.png

Themable
    You can use the `reveal themes <https://revealjs.com/themes/>`_ or `create
    your own
    <https://github.com/hakimel/reveal.js/blob/master/css/theme/README.md#creating-a-theme>`_.

PDF export
    The slides can be easily converted to PDFs.

Installation
------------

#. Download and unpack:

   .. code-block:: console

    $ curl -O https://codeload.github.com/cusyio/slides/zip/main
    $ unzip main
    Archive:  main
    …
       creating: slides-main/
    …

#. Install Pipenv

.. code-block:: console

    $ python3 -m pip install --user pipenv
      Downloading pipenv-2018.7.1-py3-none-any.whl (5.0MB): 5.0MB downloaded
    Requirement already satisfied (use --upgrade to upgrade): virtualenv in /usr/lib/python3/dist-packages (from pipenv)
    Installing collected packages: pipenv, certifi, pip, setuptools, virtualenv-clone
    …
    Successfully installed pipenv certifi pip setuptools virtualenv-clone
    Cleaning up...

.. note::

   If pipenv is not available in the shell after the installation, the
   ``USER_BASE/bin`` directory may have to be specified in ``PATH``.

   * On Linux and MacOS the ``USER_BASE`` can be determined with:

        $ python3 -m site --user-base
        /Users/veit/.local

     Then the ``bin`` directory must be appended and added to ``PATH``.
     Alternatively, ``PATH`` can be set permanently by changing ``~/.profile``
     or ``~/.bash_profile``, in my case::

        export PATH=/Users/veit/.local/bin:$PATH

   * On Windows, the directory can be determined with ``py -m site --user-site``
     and then ``site-packages`` can be replaced by ``Scripts``. his then gives,
     for example:

     .. code-block:: console

        C:\Users\veit\AppData\Roaming\Python36\Scripts

     In order to be permanently available, this path can be entered in ``PATH``
     in the control panel

Further information on user-specific installations can be found in `User
Installs <https://pip.readthedocs.io/en/latest/user_guide.html#user-installs>`_.

#. Install Python packages:

   .. code-block:: console

    $ cd slides-main
    $ pipenv install
    Creating a virtualenv for this project…
    …
    Installing dependencies from Pipfile.lock (fbb457)…
    …
    $ pipenv run jupyter nbextension enable highlighter/highlighter
        Enabling notebook extension highlighter/highlighter...
              - Validating: OK

#. Install the `Jupyter Notebook Extensions
   <https://jupyter-contrib-nbextensions.readthedocs.io/>`_ Javascript and CSS
   files:

   .. code-block:: console

    $ pipenv run jupyter contrib nbextension install --user
    jupyter contrib nbextension install --user
    Installing jupyter_contrib_nbextensions nbextension files to jupyter data directory
    …
    Successfully installed jupyter-contrib-core-0.3.3 jupyter-contrib-nbextensions-0.5.1
    jupyter-highlight-selected-word-0.2.0 jupyter-latex-envs-1.4.6
    jupyter-nbextensions-configurator-0.4.1
    …
    $ pipenv run jupyter nbextension enable latex_envs --user --py
    Enabling notebook extension latex_envs/latex_envs...
          - Validating: OK

#. Start the Jupyter notebook:

   .. code-block:: console

    $  pipenv run jupyter notebook

#. Turn notebooks into slides with
   :menuselection:`View --> Cell Toolbar --> Slideshow`

#. Create slides with
   :menuselection:`File --> Download as --> Reveal.js slides (.slides.html)`

   or

   .. code-block:: console

    $ pipenv run jupyter nbconvert my-slides.ipynb --to slides --post serve

#. Fix link to cusy styles

   In the generated ``.html`` file you have to insert the link to the CSS file
   before the body tag:

   .. code-block:: html

    …
    <link rel="stylesheet" href="../dist/theme/cusy.css" id="theme">
    </head>
    …
#. Remove Jupyter styles

   The styles were swapped out to ``dist/theme/jupyter.css`` and then adapted
   for the Cusy style. Therefore you should delete the style instructions from
   about line 68–14379 in your HTML file.

#. Create a PDF file:

   #. Open the ``.html`` file
   #. Add ``?print-pdf`` to the URL.
   #. Print to PDF with background images.

Update styles
-------------

#. Install Sass

   .. code-block:: console

    $ npm install

    added 860 packages, and audited 927 packages in 3m

    1 low severity vulnerability

    To address all issues, run:
      npm audit fix

    Run `npm audit` for details.

#. Generate the CSS theme

   .. code-block:: console

    $ npm run build -- css-themes

    > reveal.js@4.1.0 build
    > gulp "css-themes"

    [22:14:52] Using gulpfile ~/cusy/comm/slides/reveal.js/gulpfile.js
    [22:14:52] Starting 'css-themes'...
    [22:14:52] Finished 'css-themes' after 64 ms

   This generates the CSS file ``dist/theme/cusy.css``.
