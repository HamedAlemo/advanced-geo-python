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
width: 500px
align: center
---
JupyterLab interface (source: [JupyterLab Documentation](https://jupyterlab.readthedocs.io/en/stable/))
```

## JupyterLab Interface Overview

The JupyterLab interface is designed to facilitate efficient and interactive computing. Here are some key elements of the interface:






### Notebook Documents

JupyterLab primarily works with notebook documents, which are a combination of code cells and markdown cells. These notebooks can be used for code execution, documentation, and data visualization.

### File Browser

On the left-hand side of the interface, you'll find the file browser, which allows you to navigate your file system and create, open, and manage notebooks and other files.

### Tabs and Workspaces

JupyterLab supports multiple tabs, enabling you to work on multiple notebooks or files simultaneously. You can also organize your workspaces by creating customized layouts to suit your workflow.

### Kernel

The kernel is responsible for executing code within a notebook. You can choose different kernels for different programming languages (e.g., Python, R, Julia) depending on your analysis needs.

## Using JupyterLab

Now that you have JupyterLab installed and understand its interface, you can start using it for various data science and computational tasks. In the subsequent sections of this chapter, we will delve deeper into the following topics:

- **Creating and Running Notebooks:** Learn how to create and execute code cells in JupyterLab notebooks.

- **Data Visualization:** Explore how to create interactive data visualizations using libraries like Matplotlib and Plotly.

- **Data Analysis:** Perform data analysis, manipulation, and exploration using Pandas and other data science libraries.

- **Markdown Documentation:** Use markdown cells to document your code, experiments, and analysis.

- **Extensions and Customization:** Discover how to enhance JupyterLab's functionality through extensions and custom configurations.

- **Collaboration and Sharing:** Explore ways to collaborate with others and share your JupyterLab notebooks and workspaces.

JupyterLab is a versatile tool that can greatly enhance your productivity and creativity in data science and computational analysis. As you proceed through this chapter, you'll gain valuable skills that will empower you in your data-driven endeavors.