# Installing R and RStudio via Anaconda for Biologists

This guide will take users through installation of R in a new Anaconda virtual environment. I always recommend biologists use
Anaconda for managing R and its dependencies, because it gives us access to the Bioconda channel. The Bioconda channel
is an incredibly powerful hub for many of the most important bioinformatic software. Not only does it consolidate the packages
into a single channel, it manages version dependencies between them.

Any software stack that can be built with Anaconda can be replicated on any other similar system with ease. Reproduce-ability
of environments and results is a must for biological research in the computer age.

We will make frequent mention of Python in this guide. This is because, at its core, Anaconda is a virtualizer for Python. There
is a close relationship between Python and R in the biology community, so they are managed simultaneously by Anaconda. The
principles in this guide can be similarly applied to creating Python environments. See the relevant section of the related
guide in this repository on installing Python.

## Installing and Setting Up Anaconda (UNIX)

Download Anaconda version 4.3.1 (for Python 3.6) for the appropriate system here: https://www.continuum.io/downloads

On UNIX-like systems, install with the following command:
`bash Anaconda3-4.3.1-Linux-x86_64.sh`

You are encouraged to use the `bash` command regardless whether or not you are in a bash shell. It is very important that Linux users do not run this with `sudo`, as it will confuse Anaconda, causing it to install in the `/root/` directory.

When prompted to append the Anaconda path to your system's `$PATH`, it is advised you say `[no]` unless you intend for Anaconda Python to overwrite your system Python.

Test by navigating to the installation directory, then navigating to `bin/` and running `conda --version`.

For example:

```
cd ~/anaconda3/bin
conda --version
```


## Installing and Setting Up Anaconda (Windows)

Download Anaconda3 version 4.3.1 (for Python 3.6) for the appropriate system here: https://www.continuum.io/downloads

On Windows, simply run the installer with the default settings.

Windows users may want to untick the box that overwrites the system Python with Anaconda Python 3.6.1.

To verify a successful installation, open the Anaconda Prompt executable (typically found by searching in your taskbar) and run `conda --version`. Locate the
Anaconda Prompt by searching for it in your Windows Taskbar.




## Symlinking Anaconda Commands (UNIX)

If you opted not to say `[no]` to adding Anaconda to your `$PATH` variables (which was advised) you may have to symlink common anaconda commands to continue using this guide. This
section does not apply to Windows users, as we will assume they are working out of the Anaconda prompt rather than their system prompt.

Recall the installation location of Anaconda. If you went with the default paths it will be installed at `~/anaconda3` for Linux users. We want to symlink `conda`, `activate`, and `deactivate` so that we can manage virtual environments without messing with our system `$PATH` variables. Use the following commands to symlink the Anaconda commands.

**NOTE:** Make sure these do not interfere with any existing shell commands and adjust if necessary. For most people, this will not be a problem.

```
sudo ln -s /home/<user>/anaconda3/bin/conda /usr/bin/conda
sudo ln -s /home/<user>/anaconda3/bin/activate /usr/bin/activate
sudo ln -s /home/<user>/anaconda3/bin/deactivate /usr/bin/deactivate
```

Test by running `conda --version` from outside the Anaconda installation directory.



## Creating a Virtual Environment (UNIX)

We will reference this document: https://conda.io/docs/using/envs.html#create-an-environment throughout.

We will name our environment "BioSandbox" for these examples.

To create an environment: `conda create --name BioSandbox python=3.5`
To activate the environment: `source activate BioSandbox`
To deactivate the environment: `source deactivate BioSandbox`
To list environments: `conda info --envs`
To remove an environment: `conda remove --name BioSandbox --all`

After activating the environment, the command line will be prepended by `(BioSandbox) ` and the `$PATH` variable will be modified to point to `anaconda3/envs/BioSandbox/bin`.

We will install dependencies to the virtual environment, so make sure the `(BioSandbox)` environment is active for the next steps.


## Creating a Virtual Environment (Windows)

We will reference this document: https://conda.io/docs/using/envs.html#create-an-environment throughout.

Windows users will run these commands in the Anaconda Prompt. The only difference is Windows users will ignore the `source` command when acitvating and deactivating virtual environments.

To create an environment: `conda create --name BioSandbox python=3.5`
To activate the environment: `activate BioSandbox`
To deactivate the environment: `deactivate BioSandbox`
To list environments: `conda info --envs`
To remove an environment: `conda remove --name BioSandbox --all`

After activating the environment, the command line will be prepended by `(BioSandbox) ` and the `$PATH` variable will be modified to point to `anaconda3/envs/BioSandbox/bin`.

We will install dependencies to the virtual environment, so make sure the `(BioSandbox)` environment is active for the next steps.



## Installing R and RStudio

Run these commands in order. This will install R, RStudio, and add various channels for future package installations. 

```
conda config --add channels conda-forge
conda config --add channels defaults
conda config --add channels r
conda config --add channels bioconda
conda install r
conda install rstudio
```

## Using the Anaconda Environment

Now, whenever you are working on this project, make sure you are operating in the `(BioSandbox)` virtual environment. When you are using an IDE, you may have to tweak the settings to make sure it is using the `(BioSandbox)` environment. When you are using the command line, make sure that you have activated the environment and `(BioSandbox)` is prepended to the command line.

For maximum convenience, start RStudio from the Anaconda Prompt or command line by running `rstudio` from your virtual environment. This will load
RStudio with your virtual environment's R installation rather than your system's R installation.


## Installing Bioconda Packages

Most of the popular bioinformatics packages that you will encounter are managed by Bioconda. In addition,
most of them are UNIX-only. Use the following commands to install a few you may be interested in:

```
conda install bioconductor-phyloseq
conda install bioconductor-rsamtools
conda install bwa
conda install fastqc
conda install multiqc
conda install delly
conda install bowtie
conda install bedtools
```

