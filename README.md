# 2025-09-03-EO-summer-school

Material for the EO Summer School 2025 by OpenGeoHub

## In this workshop: inference of a machine learning model at scale

During this workshop, we will use a simple random forest classifier as an example to demonstrate how to scale up the inference of a machine learning model to large EO data on HPC. 

In the presented use case, a binary waterbody classification model is trained on a cutout of a Sentinel-2 RGB image. The model is then applied to a larger Sentinel-2 mosaic, predicting a water classification mask.

## Repository structure

In the `notebook` directory, we prepared two example:

- step1_train_on_cutout.ipynb: training a simple binary classifier on a scene cutout;
- step2_prediction_on_large_data.ipynb: apply the trained model on a larger RGB mosaic;

Besides the examples, in `data_preparation/data_preparation.ipynb` the process of generating the example datasets is demonstrated.

## Data

The data used in this workshop can be found on Zenodo: [link](https://zenodo.org/records/16941613).
