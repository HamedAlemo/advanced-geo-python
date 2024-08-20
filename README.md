# Advanced Geospatial Analytics with Python

This book is designed for those interested to learn advanced geospatial analytics with Python along with basics of developing reproducible code. The content is developed as part of the **GEOG 213/313 Advanced Geospatial Analytics with Python** course taught at Clark University by Dr. [Hamed Alemohammad](https://hamedalemo.github.io/). 

## Usage

All the content in this book is published under a Creative Commons Attribution 4.0 International (CC BY 4.0) license which in simple terms means you can use the content in any work by citing the source. 

## Contribute

If you use the book content and want to contribute to it, or simply want to report a bug or error please submit an issue in this repo. 

## Note to Developers

### Building the book

If you'd like to develop and/or build the Advanced Geospatial Analytics with Python book, you should:

1. Clone this repository
2. Run `pip install -r requirements.txt` (it is recommended you do this within a virtual environment)
3. (Optional) Edit the books source files located in the `advanced-geo-python/` directory
4. Run `jupyter-book clean advanced-geo-python/` to remove any existing builds
5. Run `jupyter-book build advanced-geo-python/`

A fully-rendered HTML version of the book will be built in `advanced-geo-python/_build/html/`.

### Hosting the book

Please see the [Jupyter Book documentation](https://jupyterbook.org/publish/web.html) to discover options for deploying a book online using services such as GitHub, GitLab, or Netlify.

For GitHub and GitLab deployment specifically, the [cookiecutter-jupyter-book](https://github.com/executablebooks/cookiecutter-jupyter-book) includes templates for, and information about, optional continuous integration (CI) workflow files to help easily and automatically deploy books online with GitHub or GitLab. For example, if you chose `github` for the `include_ci` cookiecutter option, your book template was created with a GitHub actions workflow file that, once pushed to GitHub, automatically renders and pushes your book to the `gh-pages` branch of your repo and hosts it on GitHub Pages when a push or pull request is made to the main branch.


## Credits

This book is created using the excellent open source [Jupyter Book project](https://jupyterbook.org/) and the [executablebooks/cookiecutter-jupyter-book template](https://github.com/executablebooks/cookiecutter-jupyter-book).
