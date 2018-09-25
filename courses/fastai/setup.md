# Setup

This guide will help setting up fastai on a fresh Ubuntu machine. Also has notes on remote setup


1. [Main guide](http://files.fast.ai/setup/paperspace) (if not Ubuntu, replace `apt-get` with appropriate package manager)

> note: `bash Anaconda3-5.0.1-Linux-x86_64.sh -b` takes forever, don't freak out if it hangs (maybe try to find detailed output flag?)

> Tip: download datasets **after** you install everything, incase you exceed space and cant install stuff

> Tip: might want to delete the zip files of things if you're space-constrained

2. [Post-install install](https://medium.com/@GuruAtWork/fast-ai-lesson-1-7fc38e978d37)

```bash
# in the fastai/ directory...

# update things. could take ages...
conda env update

# install things
conda install -c anaconda bcolz

pip install --upgrade pip

# install missing fastai packages
pip install isoweek
pip install sklearn_pandas
pip install graphviz
pip install opencv-python
pip install pandas_summary
pip install torchtext
pip install feather-format
pip install jupyter_contrib_nbextensions
pip install plotnine
pip install docrepr
pip install awscli
pip install kaggle-cli
pip install pdpbox
pip install seaborn

# install pytorch things
conda install mkl=2018
conda install pytorch torchvision -c pytorch
```

3. [Setup for remote Jupyter notebook](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook)
