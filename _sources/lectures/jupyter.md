# JupyterLab for Interactive Computing

## Introduction

[JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) is an open-source, web-based integrated development environment ([IDE](https://www.codecademy.com/article/what-is-an-ide)) for notebooks, code, and data. It has a flexible and powerful interface for interactive computing, data analysis, and scientific computing. JupyterLab is a part of the [Jupyter Project](https://jupyter.org/), which aims to provide a platform-agnostic, interactive computing experience. JupyterLab builds upon the functionality of traditional Jupyter notebooks by offering a more feature-rich environment for data scientists, researchers, and students.



## Installing JupyterLab

To Install JupyterLab, follow the steps below:

**Using `pip`**
```
$ pip install jupyterlab
```

**Using Conda**

```
$ conda install jupyterlab
```

**Note:** You need to install JupyterLab in each environment that you need to use it. In most scientific projects, JupyterLab is always included in the `environment.yml`. Just make sure you use the latest version to take advantage of all the new features. 

## Launching JupyterLab

You can launch JupyterLab using the following command:

```
$ jupyter lab
```

This will open a new tab in your web browser, displaying the JupyterLab interface. 

Let's look into what's happening when you run JupyterLab. Behind the scene, JupyterLab runs a Jupyter server that is hosted on your computer and accessible through port `8888` (default) of localhost. After you run `jupyter lab`, several lines will be printed in your terminal which indicates the path to the Jupyter server on your machine, and the URL to access it. The URL has a format like this:
```
http://127.0.0.1:8888/lab?token=TOKEN
```

`127.0.0.1` is the IP of your local host, `8888` is the port number, and TOKEN is a randomly generated string that is used to authenticate access to the notebook server. If JupyterLab doesn't automatically open in your browser, you can copy the link from terminal and paste it in your browser. We will use this later on when we deploy JupyterLab inside a Docker container. 


```{figure} ../lectures/figures/jupyterlab.png
---
name: jupyterlab
class: bg-primary mb-1
width: 700px
align: center
---
JupyterLab interface (source: [JupyterLab Documentation](https://jupyterlab.readthedocs.io/en/stable/))
```

## JupyterLab Interface Overview

{numref}`jupyterlab` shows the latest JupyterLab interface at the time of this writing (Sep 2023). The interface has multiple sections:

**Launcher**

Launcher is a tab that contains shortcuts to launch a notebook, terminal, mardown file, python file, etc. You can access launcher under *File* or by clicking the large blue button on the top left of the screen. 

**File Browser**

On the left-hand side of the interface, you'll find the file browser, which allows you to navigate your file system and create, open, and manage notebooks and other files. The files and directories that you can access here are the ones that are located in the directory you launched JupyterLab from. 

**Tabs and Workspaces**

JupyterLab supports multiple tabs, enabling you to work on multiple notebooks or files simultaneously. You can also organize your workspaces by creating customized layouts to suit your workflow.

**Kernel**

The kernel is responsible for executing code within a notebook. You can choose different kernels for different programming languages (e.g., Python, R, Julia) depending on your analysis needs. You can see all running kernels on the left had side by clicking on the kernels icon. 