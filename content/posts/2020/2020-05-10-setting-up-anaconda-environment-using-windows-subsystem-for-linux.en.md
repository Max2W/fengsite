---
title: "Setting up anaconda environment using Windows Subsystem for Linux"
author: "Feng Wang"
date: '2020-05-10'
comments: no
images: null
slug: setting-up-anaconda-environment-using-windows-subsystem-for-linux
tags:
- WSL
- Anaconda
- Jupyter
- Cmder
categories: []
---

## Enabling WSL in Windows 10
#### Using the GUI for enabling Windows features
1. Open the Start Menu and search Turn Windows features on or off 
2. Select Windows Subsystem for Linux 
3. Click OK 
4. Restart your computer when prompted

#### Using PowerShell
   1. Open PowerShell as Administrator and run:
   `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
   2. Restart your computer when prompted 

## Installing Ubuntu on WSL via the Microsoft Store (Recommended)
1. The following Ubuntu releases are available as apps on the Microsoft Store: 
  - Ubuntu 16.04 LTS (Xenial) is the first release available for WSL. It supports the x64 architecture only. (offline installer: x64) 
  - Ubuntu 18.04 LTS (Bionic) is the current LTS release and the first one supporting ARM64 systems, too. (offline installers: x64, ARM64) 
  - Ubuntu (without the release version) always follows the recommended release, switching over to the next one when it gets the first point release. Right now it installs Ubuntu 18.04. 
  
2. Each app creates a separate root file system in which Ubuntu shells are opened but app updates don’t change the root file system afterwards. Installing a different app in parallel creates a different root file system allowing you to have both Ubuntu LTS releases installed and running in case you need it for keeping compatibility with other external systems. You can also upgrade your Ubuntu 16.04 to 18.04 by running ‘do-release-upgrade’ and have three different systems running in parallel, separating production and sandboxes for experiments. 
REF： [https://wiki.ubuntu.com/WSL](https://wiki.ubuntu.com/WSL) 

## Install Anaconda on WSL (Python/R in anaconda)
1. Go to [https://repo.anaconda.com/archive/](https://repo.anaconda.com/archive/) to select the release you want. 
2. From the terminal run `wget [https://repo.anaconda.com/archive/VERSION.sh]`
3. Run the installation script: `$ bash [YOUR VERSION.sh]` 
4. Read the license agreement and follow the prompts to accept. 
5. Configure environment variables, choose one of the following options
  - Add anaconda bin folder to your PATH. e.g. `export PATH=/home/xxx/anaconda3/bin:$PATH` to the bottom of my ~/.bashrc or ~/.zshrc file. 
  - If you don’t want to set global env viables, run `source ~/anaconda3/bin/activate` 
6. Set up channels：After installing conda you will need to add the bioconda channel as well as the other channels bioconda depends on. **It is important to add them in this order** so that the priority is set correctly (that is, conda-forge is highest priority).
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

7. Install packages：Browse the packages to see what’s available. Bioconda is now enabled, so any packages on the bioconda channel can be installed into the current conda environment:

```
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
```
$ cd ~
$ ln -s /mnt/c/Users/Username/Desktop .
$ ls -al
```

## Setting up Jupyter notebook on WSL

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

  1. There are conda packages for the notebook extensions and the [jupyter_nbextensions_configurator](https://github.com/Jupyter-contrib/jupyter_nbextensions_configurator) available from [conda-forge](https://conda-forge.org/). You can install both using

```
conda install -c conda-forge jupyter_contrib_nbextensions.
-- This also automatically installs the Javascript and CSS files (using jupyter contrib nbextension install --sys-prefix), so the second installation step below can therefore be skipped.
```

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
  1. [https://towardsdatascience.com/setting-up-a-data-science-environment-using-windows-subsystem-for-linux-wsl-c4b390803dd](https://towardsdatascience.com/setting-up-a-data-science-environment-using-windows-subsystem-for-linux-wsl-c4b390803dd)
  2. [https://towardsdatascience.com/jupyter-notebook-extensions-517fa69d2231](https://towardsdatascience.com/jupyter-notebook-extensions-517fa69d2231)

## Setting up zsh + oh-my-zsh + cmder

[1. ] Install zsh; git; oh-my-zsh

```
sudo apt-get install zsh

sudo apt-get install git

sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
[2. ] Configure zsh/oh-my-zsh

```
nano ~/.bashrc
--add the following codes after the first comments:
if test -t 1; then
exec zsh
fi
```
[3. ] Save (ctrl+Shift+X) and restart WSL shell.
[4. ] Install cmder 
    - Download the latest Mini version at [https://cmder.net/](https://cmder.net/)
    - Extract the archive. Note: This path should not be C:\Program Files or anywhere else that would require Administrator access for modifying configuration files
    - Run Cmder.exe
    - Settings -> Start-up -> Choose Command line ->fill in bash -cur_console:p -> Save settings
[5. ] "Open Cmder Here" in context menu
    - Set up a new Environment variable CMDER_ROOT to point to the path of your installation C:\Cmder\Cmder.exe.
    - To add an entry in the Windows Explorer context menu to open Cmder in a specific directory, paste this into a OpenCmderHere.reg file and double-click to install it.
    ```
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\Directory\Background\shell\Cmder]
@="Open Cmder Here"
"Icon"="C:\\Cmder\\Cmder.exe,0"

[HKEY_CLASSES_ROOT\Directory\Background\shell\Cmder\command]
@="\"C:\\Cmder\\Cmder.exe\" \"%V\""

[HKEY_CLASSES_ROOT\Directory\shell\Cmder]
@="Open Cmder Here"
"Icon"="C:\\Cmder\\Cmder.exe,0"

[HKEY_CLASSES_ROOT\Directory\shell\Cmder\command]
@="\"C:\\Cmder\\Cmder.exe\" \"%1\""
   ```
    - Restart the computer.
