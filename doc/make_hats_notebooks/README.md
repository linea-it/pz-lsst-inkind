# Conda Environment and Kernel Configuration for Open OnDemand (LIneA) – Make HATS Notebooks

Author: Luigi Silva
Last reviewed: Jun. 26, 2025

---

## Accessing Open OnDemand
To access the Open OnDemand platform, follow the steps below:

1. Go to: [ondemand.linea.org.br](https://ondemand.linea.org.br)
2. On the main page, click on: **Clusters -> LIneA Shell Access**

---

## Setting Up the Environment for Make HATS Notebooks

### 1. Go to your `$SCRATCH` directory, download and install Miniconda
Run the following commands in the terminal:

```bash
cd $SCRATCH
curl -L -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh -p $SCRATCH/miniconda
source miniconda/bin/activate
```

### 2. Clone the repository into your `$SCRATCH` directory
```bash
cd $SCRATCH
git clone https://github.com/linea-it/pz-lsst-inkind.git
```

### 3. Setup the channels and the solver
First of all, add the following channels to your environment:
```bash
conda config --add channels conda-forge
conda config --add channels defaults
conda config --add channels anaconda
conda config --add channels pyviz
```
I also strongly recomend you to use the mamba solver. See instructions in the following web page:
https://conda.github.io/conda-libmamba-solver/user-guide/

### 4. Create the Conda environment
Use the `environment.yaml` provided in the project directory:
```bash
conda env create -p $SCRATCH/make_hats_env -f $SCRATCH/pz-lsst-inkind/doc/make_hats_notebooks/environment.yaml
```
To activate the environment:
```bash
conda activate $SCRATCH/make_hats_env
```

### 5. Configure `JUPYTER_PATH` and create the Jupyter Kernel
With the environment activated, set the required Jupyter path and install the kernel:

```bash
JUPYTER_PATH=$SCRATCH/.local
export JUPYTER_PATH
python -m ipykernel install --prefix=$JUPYTER_PATH --name 'make_hats_env'
```

---

### Final Notes
After following the steps above, the kernel named `make_hats_env` will be available in the Jupyter interface on Open OnDemand. Simply select it when opening the notebooks in `doc/make_hats_notebooks`.

---

## References
- https://docs.linea.org.br/processamento/uso/openondemand.html

---