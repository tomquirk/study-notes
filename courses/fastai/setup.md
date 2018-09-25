# Setup

This guide will help setting up fastai on a fresh Ubuntu machine. Also has notes on remote setup

# 1. Install deps

> based on [Main guide](http://files.fast.ai/setup/paperspace) (if not Ubuntu, replace `apt-get` with appropriate package manager)

```bash
sudo apt-get update
sudo apt-get install unzip git -y
sudo apt-get -y upgrade
sudo apt-get -y autoremove
sudo ubuntu-drivers autoinstall
sudo add-apt-repository ppa:graphics-drivers/ppa -y
```

Download `.deb` CUDA from [website](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal)

- Probably tick `(y)` on all the prompts (just for safety)
- If anyting about Noveau, follow [this guide](https://linuxconfig.org/how-to-disable-nouveau-nvidia-driver-on-ubuntu-18-04-bionic-beaver-linux)

```bash
wget http://files.fast.ai/files/cudnn-9.1-linux-x64-v7.tgz
tar xf cudnn-9.1-linux-x64-v7.tgz
sudo cp cuda/include/*.* /usr/local/cuda/include/
sudo cp cuda/lib64/*.* /usr/local/cuda/lib64/
```

Follow [this guide](https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart) to install Anaconda

> note: `bash Anaconda3-5.0.1-Linux-x86_64.sh -b` takes forever, don't freak out if it hangs (maybe try to find detailed output flag?)

```bash
cd
git clone https://github.com/fastai/fastai.git
cd fastai/

echo 'export PATH=~/anaconda3/bin:$PATH' >> ~/.bashrc
export PATH=~/anaconda3/bin:$PATH

conda update -n base conda
conda env update

echo 'source activate fastai' >> ~/.bashrc
source activate fastai
source ~/.bashrc

jupyter notebook --generate-config
echo "c.NotebookApp.ip = '*'" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py
pip install ipywidgets
jupyter nbextension enable --py widgetsnbextension --sys-prefix
```

At this point, check if a fastai course notebook works by:

- opening the notebook
- exectuing the import lines

It probably wont, at which point:

```bash
# in the fastai/ directory...

pip install --upgrade pip

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

conda install -c anaconda bcolz
conda install mkl=2018
conda install pytorch torchvision -c pytorch
```

([Source](https://medium.com/@GuruAtWork/fast-ai-lesson-1-7fc38e978d37))

> Tip: might want to delete the zip files of things if you're space-constrained

# 2. [Setup for remote Jupyter notebook](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook)
