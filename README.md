# Advanced Geospatial Analytics with Python

This book is designed for those interested to learn advanced geospatial analytics with Python along with basics of developing reproducible code. The content is developed as part of the **GEOG 213/313 Advanced Geospatial Analytics with Python** course taught at Clark University by Dr. [Hamed Alemohammad](https://hamedalemo.github.io/). 

## Usage

All the content in this book is published under a Creative Commons Attribution 4.0 International (CC BY 4.0) license which in simple terms means you can use the content in any work by citing the source. 

## Contribute

If you use the book content and want to contribute to it, or simply want to report a bug or error please submit an issue in this repo. 

## Note to Developers

### Setting up the environment

This repository uses [pixi](https://pixi.sh) to manage its environment. All dependencies are defined in `pixi.toml` and pinned in `pixi.lock`.

1. [Install pixi](https://pixi.sh/latest/#installation)
2. Clone this repository and `cd` into it
3. Run `pixi install` to create the environment

### Building the book

The following tasks are defined in `pixi.toml` and can be run from anywhere inside the repository:

| Task | Command it runs | Description |
| --- | --- | --- |
| `pixi run clean` | `jupyter-book clean advanced-geo-python/` (from the parent directory) | Removes any existing builds |
| `pixi run build` | `jupyter-book build --all advanced-geo-python/` (from the parent directory) | Builds the book |
| `pixi run publish` | `ghp-import -n -p -f _build/html` (from the repository root) | Pushes the built HTML to the `gh-pages` branch |

A fully-rendered HTML version of the book will be built in `_build/html/`. Since `build` and `clean` run from the parent directory, the repository folder must keep its default name, `advanced-geo-python`.

### Hosting the book

The book is hosted on GitHub Pages from the `gh-pages` branch. To publish an update:

```bash
pixi run clean
pixi run build
pixi run publish
```

See the [Jupyter Book documentation](https://jupyterbook.org/publish/web.html) for other deployment options.

## Credits

This book is created using the excellent open source [Jupyter Book project](https://jupyterbook.org/) and the [executablebooks/cookiecutter-jupyter-book template](https://github.com/executablebooks/cookiecutter-jupyter-book).
