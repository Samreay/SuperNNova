
![Logo](docs/SuperNNova.png)

### Read the documentation
For the main branch:
[https://supernnova.readthedocs.io](https://supernnova.readthedocs.io/en/latest/)

For the DES branch you'll need to [Build the docs](#docs).


### Read the paper preprint

[Paper](https://arxiv.org/abs/1901.06384)


## Table of contents
1. [Repository overview](#overview)
2. [Getting Started](#start)
    1. [With Docker](#docker)
    2. [With Conda](#conda)
3. [Usage](#usage)
3. [Reproduce paper](#paper)
4. [Pipeline Description](#pipeline)
5. [Running tests](#test)
6. [Build the docs](#docs)

## Repository overview <a name="overview"></a>

    ├── supernnova              --> main module
        ├──data                 --> scripts to create the processed database
        ├──visualization        --> data plotting scripts
        ├──training             --> training scripts
        ├──validation           --> validation scripts
        ├──utils                --> utilities used throughout the module
    ├── tests                   --> unit tests to check data processing
    ├── sandbox                 --> WIP scripts

## Getting started <a name="start"></a>

### With Docker <a name="docker"></a>

    cd env

    # Build docker images
    make cpu  # cpu image
    make gpu  # gpu image (requires NVIDIA Drivers + nvidia-docker)

    # Launch docker container
    python launch_docker.py (--use_gpu to run GPU based container)

### With Conda <a name="conda"></a>

    cd env

    # Create conda environment
    conda create --name <env> --file <conda_file_of_your_choice>

    # Activate conda environment
    source activate <env>

For more detailed instructions, check the full [setup instructions](https://supernnova.readthedocs.io/en/latest/installation/python.html)


## Usage <a name="usage"></a>

    # Create data
    python run.py --data  --dump_dir tests/dump

    # Train a baseline RNN
    python run.py --train_rnn --dump_dir tests/dump

    # Train a variational dropout RNN
    python run.py --train_rnn --model variational --dump_dir tests/dump

    # Train a Bayes By Backprop RNN
    python run.py --train_rnn --model bayesian --dump_dir tests/dump

    # Train a RandomForest
    python run.py --train_rf --dump_dir tests/dump

## Reproduce (soon to be published) results <a name="paper"></a>

    python run_paper.py

## General pipeline description <a name="pipeline"></a>

- Parse raw data in FITS format
- Create processed database in HDF5 format
- Train Recurrent Neural Networks (RNN) or Random Forests (RF) to classify photometric lightcurves
- Validate on test set


## Running tests with py.test <a name="tests"></a>

    PYTHONPATH=$PWD:$PYTHONPATH pytest -W ignore --cov supernnova tests


## Build docs <a name="docs"></a>

    cd docs && make clean && make html && cd ..
    firefox docs/_build/html/index.html
