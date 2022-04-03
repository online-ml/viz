# Contributing

## Getting Started

## Development

Whether you want to preview locally or add an example, you'll need to first
install dependencies and build the same. We recommend using a virtual environment:

```bash
$ python -m venv env
$ source env/bin/activate
```

Then install dependencies

```bash
$ pip install -r requirements.txt
```

and pandoc:

```bash
$ conda install pandoc
```

### Adding or Updating an Example

All examples can be found within [examples](https://github.com/online-ml/viz/blob/main/examples) and generally the structure
mirrors what you see in the web interface. Examples in the top level are introductory
or general, and then each subfolder is a specific kind of example, meaning an algorithm
or model flavor.

```bash
    examples/           # base 'Gallery of Examples' directory
    ├── README.txt
    ├── <.py files>     # introductory or basic examples
    └── cluster/        # generates the 'Cluster examples' sub-gallery
        ├── README.txt
        └── <.py files>
```

This means when you add a new folder (gallery) you should add a corresponding `README.txt`. 
The easiest thing to do is copy another one as an example, and modify the content for
the gallery. Since there are almost infinite visualization options for river, we recommend
that you organize sub-galleries based on either the flavor and/or the underlying software.
Follow the existing convention for instruction. If you add a new dependency, please
don't forget to add to requirements.txt. If you want to chat about how to add your contribution
before opening a pull request (suggested) please [open an issue](https://github.com/online-ml/viz/issues).

Note that you can add rst (restructured syntax) within the example as follows (or just view
the current examples for better example):

```rst
#%%
# Here is text in the middle of an example that will be nicely rendered into either
# Python, notebook, or other downloaded file. You can use any kind of rst here.
```

Note that you can add as many python example files in a gallery as you'd like! The
thumbnail is generated automatically. For a good set of examples, see [this sphinx-gallery](https://sphinx-gallery.github.io/stable/auto_examples/index.html)
example gallery. For every example, you can click to view the source, or simply see it
raw [in the repository](https://github.com/sphinx-gallery/sphinx-gallery/tree/master/examples).
If you want to do something that is not yet supported, please [open an issue](https://github.com/online-ml/viz/issues).

When you are ready to build the site:

```bash
$ make html
```

This will generate a `_build/html` directory that you can cd into and open a web browser to see.

```bash
$ cd _build/html
$ python -m http.server 9999
```

The above would allow you to open `http://127.0.0.1:9999` or `http://localhost:9999`
to see the rendering. Note that when you rebuild, the original content is not removed.
If you see any rendering issues, it's helpful to remove the entire thing and gallery
directory (or your specific example) and build again.

```bash
$ rm -rf _build/html
$ rm -rf auto_examples
$ make html
```

Note that your examples need to be prefixed with `plot_` to be detected as examples to render!

```bash
Sphinx-Gallery successfully executed 1 out of 1 file subselected by:

    gallery_conf["filename_pattern"] = '/plot'
    gallery_conf["ignore_pattern"]   = '__init__\\.py'

after excluding 0 files that had previously been run (based on MD5).
```


### Adding a New Page

We don't have a lot of pages currently, as the site is intended for examples. However,
if you want to add a new page, we recommend creating a directory (e.g., `getting_started`)
with an `index.rst` and then associated pages. You'll then need to include it in `index.rst`
in the root (or another place) so it gets included in the site.


### Changing the Style

You can "override" any style setting by editing the [_static/custom.css](https://github.com/online-ml/viz/blob/main/_static/custom.css) file.

### Updating this contributing document

Since this file is also rendered in the web interface, make sure that you include full paths for links to assets
in GitHub. A relative path will issue a build warning, and is likely to 404 in the online interface.

### Learning Re-structured Syntax

If you want any help with custom syntax, [this document](https://github.com/bashtage/sphinx-material/blob/main/docs/specimen.rst)
and [this document](https://github.com/bashtage/sphinx-material/blob/main/docs/additional_samples.rst) are helpful.
If you are new to restructured syntax, there is a good [guide here](https://github.com/bashtage/sphinx-material/blob/main/docs/basics.rst).


## Frequently Asked Questions

> Why does it say WARNING multiple files found for the document...

Sphinx gallery is taking a single Python example and generating multiple files, and sphinx detects this as "oh no I don't know which one to choose."
This is a warning that can be safely ignored - if you look toward the bottom you'll see that it ultimately chooses the .rst extension. The others
are provided for the reader to download in different formats (notebook, etc.)

> WARNING: document isn't included in any toctree

If this is referencing an example, you are again fine - the sphinx-gallery will handle ensuring that it is linked! However if the warning is referencing a page
that you recently added, it means that you haven't linked it from anywhere. A "toctree" example can be found in `index.rst` - you basically want to add it there or to some other link from a page that is rendered.
