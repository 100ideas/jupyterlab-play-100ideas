# jupyterlab extensions

## kernels
- ijavascript: https://github.com/n-riesco/ijavascript  
- fsharp: https://github.com/fsprojects/IfSharp

## docs
jupyter: http://jupyter.readthedocs.io/en/latest/install-kernel.html#id3pip
ipython: https://ipython.readthedocs.io/en/latest/interactive/reference.html
jupyter command: http://jupyter.readthedocs.io/en/latest/projects/jupyter-command.htmln
kernels: http://jupyter-client.readthedocs.io/en/latest/kernels.html#kernelspecs
jupyterlab: http://jupyterlab.readthedocs.io/en/stable/user/extensions.html


installed kernels: `jupyter-kernelspec list`
installed jupyterlab exensions: `jupyter labextension list`

```js
console.log("hi")
```

```python
a = "auto-run code blocks in md: \n\
     1. open console for document (right-click) \n\
     2. place curser inside, then shift+enter \n\
     3. thats it."
print(a)
```


---jupyter pixiedust install
(rst format!)

JupyterLab Application Directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The JupyterLab application directory contains the subdirectories
``extensions``, ``schemas``, ``settings``, ``staging``, ``static``, and
``themes``.

.. _extensions-1:

extensions
''''''''''

The ``extensions`` directory has the packed tarballs for each of the
installed extensions for the app. If the application directory is not
the same as the ``sys-prefix`` directory, the extensions installed in
the ``sys-prefix`` directory will be used in the app directory. If an
extension is installed in the app directory that exists in the
``sys-prefix`` directory, it will shadow the ``sys-prefix`` version.
Uninstalling an extension will first uninstall the shadowed extension,
and then attempt to uninstall the ``sys-prefix`` version if called
again. If the ``sys-prefix`` version cannot be uninstalled, its plugins
can still be ignored using ``ignoredPackages`` metadata in ``settings``.

schemas
'''''''

The ``schemas`` directory contains `JSON
Schemas <http://json-schema.org/>`__ that describe the settings used by
individual extensions. Users may edit these settings using the
JupyterLab Settings Editor.

settings
''''''''

The ``settings`` directory contains ``page_config.json`` and
``build_config.json`` files.

.. _page_configjson:

page_config.json


The ``page_config.json`` data is used to provide config data to the
application environment.

Two important fields in the ``page_config.json`` file enable control of
which plugins load:

1. ``disabledExtensions`` for extensions that should not load at all.
2. ``deferredExtensions`` for extensions that do not load until they are
   required by something, irrespective of whether they set ``autostart``
   to ``true``.

The value for each field is an array of strings. The following sequence
of checks are performed against the patterns in ``disabledExtensions``
and ``deferredExtensions``.

-  If an identical string match occurs between a config value and a
   package name (e.g., ``"@jupyterlab/apputils-extension"``), then the
   entire package is disabled (or deferred).
-  If the string value is compiled as a regular expression and tests
   positive against a package name (e.g.,
   ``"disabledExtensions": ["@jupyterlab/apputils*$"]``), then the
   entire package is disabled (or deferred).
-  If an identical string match occurs between a config value and an
   individual plugin ID within a package (e.g.,
   ``"disabledExtensions": ["@jupyterlab/apputils-extension:settings"]``),
   then that specific plugin is disabled (or deferred).
-  If the string value is compiled as a regular expression and tests
   positive against an individual plugin ID within a package (e.g.,
   ``"disabledExtensions": ["^@jupyterlab/apputils-extension:set.*$"]``),
   then that specific plugin is disabled (or deferred).

.. _build_configjson:

build_config.json


The ``build_config.json`` file is used to track the local directories
that have been installed using
``jupyter labextension install <directory>``, as well as core extensions
that have been explicitly uninstalled. An example of a
``build_config.json`` file is:

.. code:: json

    {
        "uninstalled_core_extensions": [
            "@jupyterlab/markdownwidget-extension"
        ],
        "local_extensions": {
            "@jupyterlab/python-tests": "/path/to/my/extension"
        }
    }

staging and static
''''''''''''''''''

The ``static`` directory contains the assets that will be loaded by the
JuptyerLab application. The ``staging`` directory is used to create the
build and then populate the ``static`` directory.

Running ``jupyter lab`` will attempt to run the ``static`` assets in the
application directory if they exist. You can run
``jupyter lab --core-mode`` to load the core JupyterLab application
(i.e., the application without any extensions) instead.

themes
''''''

The ``themes`` directory contains assets (such as CSS and icons) for
JupyterLab theme extensions.