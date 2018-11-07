# Setup

This guide will help setting up fastai on a fresh Ubuntu 16.04 installation. Also has notes on usage on a remote machine

## 1. Initial setup

> based on [Main guide](http://files.fast.ai/setup/paperspace) (if not Ubuntu, replace `apt-get` with appropriate package manager)

```bash
#!/usr/bin/env bash

set -e
set -o xtrace
DEBIAN_FRONTEND=noninteractive

sudo apt update
sudo apt upgrade -y
sudo apt install -y unzip git qtdeclarative5-dev qml-module-qtquick-controls
sudo apt-get -y autoremove
sudo ubuntu-drivers autoinstall
sudo add-apt-repository ppa:graphics-drivers/ppa -y
sudo apt update
sudo apt upgrade -y
sudo ufw allow 8888:8898/tcp

# install cuda
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo apt update
sudo apt install cuda -y

# install cudnn
wget http://files.fast.ai/files/cudnn-9.1-linux-x64-v7.tgz
tar xf cudnn-9.1-linux-x64-v7.tgz
sudo cp cuda/include/*.* /usr/local/cuda/include/
sudo cp cuda/lib64/*.* /usr/local/cuda/lib64/

# Install Anaconda
#### NOTE #### - go to the Anaconda website to get the latest version for Ubuntu 16.04
wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
bash Anaconda3-5.0.1-Linux-x86_64.sh -b

cd
git clone https://github.com/fastai/fastai.git
cd fastai/
export PATH=~/anaconda3/bin:$PATH
conda env update

echo 'export PATH=~/anaconda3/bin:$PATH' >> ~/.bashrc
echo 'source activate fastai' >> ~/.bashrc
source ~/.bashrc

jupyter notebook --generate-config
echo "c.NotebookApp.ip = '*'" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py
echo "c.NotebookApp.allow_remote_access = True" >> ~/.jupyter/jupyter_notebook_config.py

pip install --upgrade pip
pip install ipywidgets

jupyter nbextension enable --py widgetsnbextension --sys-prefix
```

At this point, check if a fastai course notebook works by:

- opening the notebook
- exectuing the import lines

It probably wont, at which point:

```bash
# in the fastai/ directory...
conda install -c anaconda bcolz
```

Try the notebook again, if not

```bash
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

conda install mkl=2018
conda install pytorch torchvision -c pytorch
```

([Source](https://medium.com/@GuruAtWork/fast-ai-lesson-1-7fc38e978d37))

> Tip: might want to delete the zip files of things if you're space-constrained

Finally, download dogscats dataset

```bash
mkdir ~/data
cd data
wget http://files.fast.ai/data/dogscats.zip
unzip -q dogscats.zip

ln -s ~/data ~/fastai/courses/dl1/data
```

# 2. [Setup for remote Jupyter notebook](https://amber-md.github.io/pytraj/latest/tutorials/remote_jupyter_notebook)
