:orphan:
# Documentation

To Build the documentation:

## Requirments:

- [Sphinx](http://www.sphinx-doc.org/en/master/) - Python documentation generator
- [Read the Docs Sphinx Theme](https://sphinx-rtd-theme.readthedocs.io/en/stable/) - Theme for final output
- [recommonmark](https://github.com/miyakogi/m2r) - Markdown to reStructuredText


```
pip install sphinx sphinx_rtd_theme recommonmark sphinx-autobuild
```

## Building

```bash

# from project root
sphinx-autobuild docs docs/_build/html

# from docs root
sphinx-autobuild . _build/html
```


## Read the docs

The documentation is available at https://escalate.readthedocs.io

It updates automatically when changes are pushed do the repo

