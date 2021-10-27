# 1. Clone the repository
First, clone the repo to make a local copy. To do so, open a new terminal and navigate to
the directory where you want to clone the repo. It does not matter where, as long as you
have full permissions. If you are unsure, choose your home directory.

```bash
git clone https://gitlab.com/bioinfo-lessons/
```

# 2. Install R and the required packages for the course with conda
Open a new terminal and navigate to your fresh local copy of the repo. Once there, go to the envs directory:

```bash
cd envs
```
There you will find a conda YAML (YAML Ain't Markup Language) called intro_r.yaml.  YAML files are commonly used to distribute conda environments. We can create a new conda environment from this file by typing:

```bash
conda env create -f intro_r.yaml
```
Accept the download when prompted and you are good to go.

## Contents of the environment
We have installed the following R libraries:


1. Airway package: an example RangedSummarizedExperiment object from an RNASeq assay. This library is installed using bioconductor so expect conda to pull other bioconductor libraries such as biobase or biocgenerics.

1. tidyverse: a collection of R libraries focused on data loading, manipulation, tidying and plotting. Some of the included libraries are tidyr, dplyr or ggplot2. These are fully compatible with each other and share a common syntax. They greatly expand R base capabilities. Want to know more? Check the official website.

1. stringi, which is a dependency of the above collection but tends to not get pulled when installing the tidyverse. So we are explicitly installing it just in case.

1. R itself. Conda automatically installs the newest version of R compatible with these packages as R itself is a dependency.


# 3. Install RStudio
If you haven't installed it yet, do so now. Rstudio is an IDE (Integrated Development Environment) which also allows us to explore R objects, visualize graphs and debug scripts on the fly.  **DO NOT install Rstudio from conda**, as you will be pulling an ancient version of the software and its dependencies, which in turn will downgrade your R installation. Install it from the official website instead as a deb package.

You can download it [here].(https://www.rstudio.com/products/rstudio/download/)

# 4. Launch RStudio
To launch RStudio from a suitable conda installation of R, open up a new terminal session and load your conda environment by typing:

```bash
conda activate intro_y
```

Now navigate to your  conda installation directory. By default conda is installed in 

```bash
~/miniconda3
```

There, cd to the lib directory

```
cd ~/miniconda3/lib
```

Finally, launch RStudio with

```bash
rstudio
```

## Why are we launching Rstudio from miniconda3/lib?

You can launch RStudio from any directory, as long as you have an R installation in your active conda environment. However,you may find that RStudio fails to load
certain libraries from time to time, even if they are successfully installed. By setting lib to the default local path, these issues go away.

