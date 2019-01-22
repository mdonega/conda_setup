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

### Untested installation script

```
#!/bin/bash

# Install anaconda
CONDA_FOLDER=$1 && shift 

[[ -n $CONDA_FOLDER ]] || exit
[[ -e $CONDA_FOLDER ]] && exit

wget https://repo.continuum.io/archive/Anaconda3-2018.12-Linux-x86_64.sh -O /tmp/Anaconda3-2018.12-Linux-x86_64.sh

bash /tmp/Anaconda3-2018.12-Linux-x86_64.sh -b -p $CONDA_FOLDER

export PATH=$CONDA_FOLDER/bin:$PATH


# Set-up environments
ENVIRONMENTS="tensorflow pytorch cern_root"

conda env update -f conda_base.yml
source activate base 
pip install -r conda_base_pip.txt
source deactivate

for env_name in  in $ENVIRONMENTS; do
    conda env create -f env_${env_name}.yml
    source activate ${env_name}
    pip install -r conda_${env_name}.txt
    source deactivate
done

```
