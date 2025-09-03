# High performance computing with Python and RS-DAT

## Introduction

This repository hosts the material for a workshop taught at the [EO Summer School 2025 - Data Science for Earth Observation](https://opengeohub.org/summer-school/summer-school-2025/) by [OpenGeoHub](https://opengeohub.org/)

During the workshop, we will demonstrate how to scale up the inference of a machine learning model to large EO data on HPC in an interactive session using [Jupyter](https://docs.jupyter.org/en/latest/) and [Dask](https://docs.dask.org/en/stable/index.html).

We will:

* Introduce the framework that we use to start Jupyter on a HPC system.
* Run through a short introduction to Dask.
* Present a use-case: we will train a toy water classification model on a cutout of a Sentinel-2 RGB scene, then apply the model to a larger mosaic involving multiple scenes, and predict its water classification mask.

We will run the use case on the [Spider](https://doc.spider.surfsara.nl/en/latest/Pages/about.html) cluster, a high-throuput data processing platform hosted by [SURF](https://www.surf.nl/).

## Repository structure

* [`notebooks/`](./notebooks/) contains the Jupyter notebooks that implement the use case.
* [`scripts/`](./scripts/) contains the batch job script to start a Jupyter session on Spider.
* [`.github/`](./github) contains the scripts that take care of building and publishing a container image with the required dependencies.
* [`environment.yml`](./environment.yml) is the environment file that define all the project dependencies.

## Data

The data used in this workshop is available on the Spider system in the following directory:
```
/project/remotesensing/Data/eo-summer-school/
```
The dataset is also published on Zenodo: [link](https://zenodo.org/records/16941613)

## Setup

In order to follow along with the instructor, you will need a laptop with the following software installed:

* OpenSSH client: should already be installed on macOS/Linux, it can be installed from Windows Apps on Windows 10+. Installation instructions can also be found [here](https://www.sshhandbook.com/installing-ssh/). Verify it works by typing the following command in a terminal window (it should return the OpenSSH version):
  ```shell
  ssh -V
  ```

* Python: Any recent Python version (3.10+) should work. It can be installed from [python.org](https://www.python.org/downloads/). Verify it works by typing the following command in a terminal window (it should return the Python version):
  ```shell
  python --version
  ```

Once this software is installed, follow the following setup steps:

1. Create a Python virtual environment. You can use any environment manager you are comfortable with (`venv`, `virtualenv`, `conda`, ...). Using `venv`, you can create the "myenv" environment with the following commands:
   ```shell
   python -m venv myenv
   source myenv/bin/activate
   ```

2. Install the Python tool hosted in [this repository](https://github.com/RS-DAT/JupyterDaskOnSLURM/tree/main/tools/jupyterdask):
   ```shell
   pip install -e "git+https://github.com/RS-DAT/JupyterDaskOnSLURM.git#egg=jupyterdask&subdirectory=tools/jupyterdask"
   jupyterdask --version  # check the command line tool is correctly installed
   ```

3. Download the following batch job script and save it to a known path (e.g. on your Desktop): [jupyterdask-spider.slurm](https://raw.githubusercontent.com/RS-DAT/2025-09-03-EO-summer-school/refs/heads/main/scripts/jupyterdask-spider.slurm)

4. Pick a Spider user account from [this document](https://nlesc-my.sharepoint.com/:w:/g/personal/m_grootes_esciencecenter_nl/EShepbH_bv1FskW2SIM_EBwBawh1ydjRsluF0zlkGWAnPQ?e=1WjykL) (the password to access the document will be given at the workshop). Add your name to the "Name" column, then download the private SSH key required to authenticate and save it to a known path (e.g. on your Desktop).

## Run

Start the Jupyter session on Spider with the following command:

```shell
jupyterdask -i /path/to/ssh/key --template /path/to/jupyterdask-spider.slurm --run <YOUR_USERNAME>@spider.surf.nl
```
