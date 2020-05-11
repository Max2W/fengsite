---
title: Setting up Jupyter notebook on WSL
author: Feng Wang
date: '2020-05-11'
slug: setting-up-jupyter-notebook-on-wsl
categories: []
tags:
  - Jupyter
  - WSL
toc: no
images: ~
---


#### Jupyter notebook is installed in anaconda by default.

#### Auto launching Jupyter notebook to Windows browser on WSL

1. add to the bottom of /.bashrc: 
   `<alias firefox="/mnt/c/mnt/c/Program\ Files/Mozilla\ Firefox/firefox.exe">`
2. Disable the file-based redirect method that later versions of Jupyter use to launch notebook windows, in favor of the older, token-based approach. 

```
jupyter notebook --generate-config
echo c.NotebookApp.use_redirect_file = False >> ~/.jupyter/jupyter_notebook_config.py
echo c.NotebookApp.browser = u'/mnt/c/Program\ Files/Mozilla\ Firefox/firefox.exe %s'
```

#### Setting up extensions for Jupyter Notebook

1. There are conda packages for the notebook extensions and the [jupyter_nbextensions_configurator](https://github.com/Jupyter-contrib/jupyter_nbextensions_configurator) available from [conda-forge](https://conda-forge.org/). You can install both using `conda install -c conda-forge jupyter_contrib_nbextensions` This also automatically installs the Javascript and CSS files (using jupyter contrib nbextension install --sys-prefix), so the second installation step below can therefore be skipped.

2. Next you’ll be presented by a new tab when you launch your notebooks called “Nbextensions”

3. Some useful extensions recommended here:

    - Hinterland — For easier auto-correction.
    - Table of Contents (2) — For automatically generating a ToC from your Markdown headings and sub-headings.
    - Toggle all line numbers — For easier debugging.
    - Variable Inspector — For an R-like variable overview, really useful!
    -	ExecuteTime — For timing your cell executions.
    -	Autopep8 — For automatically formatting your code to pep8 standards.
    -	Collapsible Headings — For easy hiding of parts of your notebook.

Ref

- [https://towardsdatascience.com/jupyter-notebook-extensions-517fa69d2231](https://towardsdatascience.com/jupyter-notebook-extensions-517fa69d2231)

