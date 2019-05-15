## Anaconda installation

1. Install anaconda3 from the anaconda [website](https://www.anaconda.com/download/#linux)
1. Put anaconda in the path `export PATH=<CONDA_FOLDER>/bin:$PATH`
1. Update the base environment.
1. Create extra environments using configuration files. 

### Creating and updating environements

For each environement there are two packages lists:
- `conda_<env>.yml` for conda packages
- `conda_<env>_pip.txt` for additional pip packages

The conda yml file can be used to either create or update the environments

- create: `conda env create -f conda_<env>.yml`
- update: `conda env update -f conda_<env>.yml`

Once the enviroment has been created pip packages can be added (**note**: for this to work pip must be installed in each enviroment by putting it in the yml file).

1. activate the environment: `source activate <env>`
1. install packages: `pip install -r conda_<env>_pip.txt`


# In practice:

First install anaconda:
Download the installation script from https://www.anaconda.com/distribution/#linux
> ./Anaconda3-2018.12-Linux-x86_64.sh

Add anaconda in your PATH:
```
export PATH=$CONDA_FOLDER/bin:$PATH <br>
```

Native python2.7 environment
```
conda create -n python2 python=2.7 anaconda
conda env update -f conda_python2.yml
source activate python2
pip install -r conda_python2_pip.txt
source deactivate
```

Tensorflow for CPU
```
conda env create -f conda_tensorflow.yml
source activate tensorflow
pip install -r conda_tensorflow_pip.txt
source deactivate
```

XGBOOST: works for both CPU and GPU
```
conda env create -f conda_xgboost.yml
source activate xgboost
pip install -r conda_xgboost_pip.txt
source deactivate
```
