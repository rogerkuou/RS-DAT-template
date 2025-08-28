# High performance computing with Python and RS-DAT

## Introduction

This repository hosts the material for a workshop taught at the [EO Summer School 2025 - Data Science for Earth Observation](https://opengeohub.org/summer-school/summer-school-2025/) by [OpenGeoHub](https://opengeohub.org/)

During the workshop, demonstrate how to scale up the inference of a machine learning model to large EO data on HPC.

We will use a simple random forest classifier as an example. We will train a toy water classification model on a cutout of a Sentinel-2 RGB scene. We will then apply the model to a larger mosaic involving multiple scenes, and predict its water classification mask.

## Repository structure

* [`notebooks/`](./notebooks/) contains the Jupyter notebooks that implements the use case.
* [`scripts/`](./scripts/) contains the batch job script to start a Jupyter server on Spider.
* [`.github/`](./github) contains all the scripts that build the container image with the required enviroment.
* [`environment.yml`](./environment.yml) is the conda environment file that contains all the project dependencies.

## Data

The data used in this workshop is published [on Zenodo](https://zenodo.org/records/16941613) and is available on the Spider system in the following directory: `/project/remotesensing/Data/2025-09-03-eo-summer-school/`.

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

3. Download the following batch job script and save it to a known path (e.g. on your Desktop): [spider-job.bsh]()

4. Pick a Spider user account from [this document]() (the password to access the document will be given at the workshop). Add your name to the "Name" column, then download the private SSH key required to authenticate and save it to a known path (e.g. on your Desktop).
