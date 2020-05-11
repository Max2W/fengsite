---
title: Installing Anaconda on WSL
author: Feng Wang
date: '2020-05-11'
slug: installing-anaconda-on-wsl
categories: []
tags:
  - WSL
  - Anaconda
toc: no
images: ~
---

1. Go to [https://repo.anaconda.com/archive/](https://repo.anaconda.com/archive/) to select the release you want. 
2. From the terminal run `wget [https://repo.anaconda.com/archive/VERSION.sh]`
3. Run the installation script: `$ bash [YOUR VERSION.sh]` 
4. Read the license agreement and follow the prompts to accept. 
5. Configure environment variables, choose one of the following options

  - Add anaconda bin folder to your PATH. e.g. `export PATH=/home/xxx/anaconda3/bin:$PATH` to the bottom of my ~/.bashrc or ~/.zshrc file. 
  - If you don’t want to set global env viables, run `source ~/anaconda3/bin/activate` 

6. Set up channels：After installing conda you will need to add the bioconda channel as well as the other channels bioconda depends on. **It is important to add them in this order** so that the priority is set correctly (that is, conda-forge is highest priority).

```shell
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

7. Install packages：Browse the packages to see what’s available. Bioconda is now enabled, so any packages on the bioconda channel can be installed into the current conda environment:

```shell
conda search multiqc
conda install multiqc(=vesion#)  
--the latest version is installed unless you set specific version.

--Or a new environment can be created, e.g. R in anconda
conda create -n renv r-essentials r-base
conda activate renv

conda info -e
conda info --envs
conda env list
```

8. Tips: setting a soft linke between WSL and Windows so that make it easier to transfer data. 

```shel
$ cd ~
$ ln -s /mnt/c/Users/Username/Desktop .
$ ls -al
```


