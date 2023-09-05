# Python Environments

In this lecture, you will learn about Python environments and how best to use them to create reproducible pipelines. 

**Attribution**
*The content of this lecture are modified from three excellent sources: [Python Packages for Earth Data Science](https://www.earthdatascience.org/courses/intro-to-earth-data-science/python-code-fundamentals/use-python-packages/) from Earth Lab CU Boulder; [Managing Python Environments](https://earth-env-data-science.github.io/lectures/environment/python_environments.html) from Columbia University; [Introduction to Conda for (Data) Scientists](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/) from Software Carpentry; and [Managing a Development Environment](https://docs.descarteslabs.com/installation-conda.html) by Descartes Labs.*

## Background
Python and nearly all of the software packages in the scientific python ecosystem are open-source. They are maintained and developed by a community of scientists and programmers, some of whose work is supported by universities, non-profits, and for-profit corporations. This work mostly happens in the open, via github and other online collaboration platforms.

When working with a programming language, such as Python, that can do almost anything, one has to wonder how this is possible. You download Python, it has about 25 MB, how can everything be included in this small data package. The answer is - it is not. Python, as well as many other programming languages use external libraries or packages for being able to do almost anything. You can see this already when you start programming. After learning some very basics, you often learn how to *import* something into your script or session.

```{admonition} Definitions
**Module**: a collection of functions and variables, as in a script

**Package**: a collection of modules with an init.py file (can be empty), as in a directory with scripts

**Library**: a collection of packages with related functionality

Library/Package are often used interchangeably.
```

## Dependencies
A bit further into your programming career you may notice/have noticed that many packages do not just do everything on their own. Instead, they depend on other packages for their functionality. For example, the `SciPy` package is used for numerical routines. To not reinvent the wheel, the package makes use of other packages, such as `NumPy` (numerical python) and `matplotlib` (plotting) and many more. So we say that `NumPy` and `matplotlib` are dependencies of `SciPy`.

Many packages are being further developed all the time, generating different versions of packages. During development it may happen that a function call changes and/or functionalities are added or removed. If one package can depend on another, this may create issues. Therefore it is not only important to know that e.g. `SciPy` depends on `NumPy` and `matplotlib`, but also that it depends on `NumPy` version >= 1.6 and `matplotlib` version >= 1.1. `NumPy` version 1.5 in this case would not be sufficient.

This emphasizes the need for creating and recording environments (in virtual terms!) to run your Python code. 

## Environments

When starting with programming we may not use many packages yet and the installation may be straightforward. But for most people, there comes a time when one version of a package or also the programming language is not enough anymore. You may find an older tool that depends on an older version of your programming language (e.g. Pyhton 2.7), but many of your other tools depend on a newer version (e.g. Python 3.6). You could now start up another computer or virtual machine to run the other version of the programming language, but this is not very handy, since you may want to use the tools together in a workflow later on. Here, environments are one solution to the problem. Nowadays there are several environment management systems following a similar idea: Instead of having to use multiple computers or virtual machines to run different versions of the same package, you can install packages in isolated environments.

However, managing Python development environments can be tricky, especially if you are new to the language or less familiar with computer science concepts. In this course, we introduce tool to make it easy to manage and reproduce your Python environments on any machine (local computer/server/cloud).

```{figure} https://imgs.xkcd.com/comics/python_environment.png
---
name: xkcd-python-env
class: bg-primary mb-1
width: 500px
align: center
---
The complexity of Python environments as illustrated by [xkcd](https://xkcd.com/1987/). 
```

## Environment management

An environment management system solves a number of problems commonly encountered by (data) scientists.

- An application you need for a research project requires different versions of your base programming language or different versions of various third-party packages from the versions that you are currently using.
- An application you developed as part of a previous research project that worked fine on your system six months ago now no longer works.
- Code that was written for a joint research project works on your machine but not on your collaborators’ machines.
- An application that you are developing on your local machine doesn’t provide the same results when run on your remote cluster.

An environment management system enables you to set up a new, project specific software environment containing specific Python versions as well as the versions of additional packages and required dependencies that are all mutually compatible.

- Environment management systems help resolve dependency issues by allowing you to use different versions of a package for different projects.
- Make your projects self-contained and reproducible by capturing all package dependencies in a single requirements file.
- Allow you to install packages on a host on which you do not have admin privileges.


## Conda

[Conda](https://docs.conda.io/en/latest/) is an open-source package management system and environment management system that runs on Windows, macOS, and Linux. When you install one module using conda, such as JupyterLab, all of the required modules will also be downloaded and installed with compatible versions. It was created for Python programs but it can package and distribute software for any language (Python, R, Ruby, Lua, Scala, Java, JavaScript, C/ C++, FORTRAN)

Conda as a package manager helps you find and install packages. If you need a package that requires a different version of Python, you do not need to switch to a different environment manager because conda is also an environment manager. With just a few commands, you can set up a totally separate environment to run that different version of Python, while continuing to run your usual version of Python in your normal environment.

While there are multiple ways to install conda for Python, including [Anaconda Distribution](https://www.anaconda.com/download/) and [Miniconda Distribution](https://docs.conda.io/projects/miniconda/en/latest/). {numref}`miniconda-anaconda` shows the difference between Conda, Miniconda and Anaconda. Miniconda combines Conda with Python and a small number of core packages; Anaconda includes Miniconda as well as a large number of the most widely used Python packages (> 150).

We recommend Miniconda, the most lightweight and bare-minimum approach to using conda. While the Anaconda distribution has a lot of packages pre-installed, they are not used all together in most of the projects. Therefore, it is optimal to install Miniconda and benefit from the Conda package and environment management systems but avoid installing too many unnecessary packages. 


```{figure} ../lectures/figures/miniconda-vs-anaconda.png
---
name: miniconda-anaconda
class: bg-primary mb-1
width: 500px
align: center
---
Conda vs. Miniconda vs. Anaconda [Source: [Planemo Documentation](https://planemo.readthedocs.io/en/latest/writing_advanced_cwl.html)] 
```
<!-- ## Installing Miniconda






To create a new conda environment, -n sets the name of the environment. The -c denotes a channel, or repository from which to pull compatible package dependencies. conda-forge is a widely used and reliable channel for installations. To add additional packages to your environment, you activate it from anywhere as seen on the second line above. Once activated, you can begin installing packages via conda and pip. For more information on using conda, check out the conda documentation. -->


<p>&nbsp;</p>