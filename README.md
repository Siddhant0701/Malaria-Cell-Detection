# Malaria Cell Identification

## Introduction

The purpose of this project is to create a Deep Learning Model that is able to differentiate between healthy cells and cells infected with malaria and classify them correctly. The aim is to achieve a very high sensitivity and specifiity on the test data (> 99%). One way to create such a model is by constructing a `Convolutional Neural Network` using `Keras` and `Tensorflow`.

## Data

The data used to train the model comes from [`Tensorflow-Datasets`](https://www.tensorflow.org/datasets/catalog/malaria). This dataset has exactly `27,558` images of parasitized and uninfected cells from the thin blood smear slide images of segmented cells, split evenly between the two classes. The data was aplit into `training`, `validation` and `test` sets using a 80-10-10 split. All sets include almost equal instances of the two classes. 

<br/>

[<img src=images/training_counts_histogram.jpg height=250>](images/training_counts_histogram.jpg)
[<img src=images/validation_counts_histogram.jpg height=250>](images/validation_counts_histogram.jpg)
[<img src=images/test_counts_histogram.jpg height=250>](images/test_counts_histogram.jpg)

<br/>
