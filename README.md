# Malaria Cell Detection

## Introduction

The purpose of this project is to create a Deep Learning Model that is able to differentiate between healthy cells and cells infected with malaria and classify them correctly. The aim is to achieve a very high sensitivity and specifiity on the test data (> 90%). 

One way to create such a model is by constructing a `Convolutional Neural Network` using `Keras` and `Tensorflow`.

<br/>
<br/>

## Data

The data used to train the model comes from [US'National Institues of Health](https://ceb.nlm.nih.gov/repositories/malaria-datasets/) and will be imported into the project from [`Tensorflow-Datasets`](https://www.tensorflow.org/datasets/catalog/malaria). This dataset has exactly `27,558` images of parasitized and uninfected cells from the thin blood smear slide images of segmented cells. The data was collected from 150 patients that were infected with Malaria and 50 healthy patients. The infected cells contain parasites called `Plasmodium Falciparum` that are responsible for causing Malaria.

<br/>

[<img src=images/example.png height=400 style="background-color:white;">](images/example.png)

<br/>

There are equal number of images for both the classes. The data was split into `training`, `validation` and `test` sets using a 80-10-10 split. All sets include almost equal instances of the two classes. 

<br/>

[<img src=images/training_counts_histogram.jpg height=250>](images/training_counts_histogram.jpg)
[<img src=images/validation_counts_histogram.jpg height=250>](images/validation_counts_histogram.jpg)
[<img src=images/test_counts_histogram.jpg height=250>](images/test_counts_histogram.jpg)

<br/>
<br/>


## Model

A summary of the model is provided below:

```
Model: "Malaria Detection"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 resizing (Resizing)      (None, 300, 300, 3)       0         
                                                                 
 conv2d (Conv2D)          (None, 298, 298, 16)      448       
                                                                 
 max_pooling2d (MaxPoolin  (None, 149, 149, 16)     0         
 g2D)                                                            
                                                                 
 conv2d (Conv2D)          (None, 147, 147, 16)      2320      
                                                                 
 max_pooling2d (MaxPoolin  (None, 73, 73, 16)       0         
 g2D)                                                            
                                                                 
 conv2d (Conv2D)          (None, 69, 69, 32)        12832     
                                                                 
 max_pooling2d (MaxPoolin  (None, 34, 34, 32)       0         
 g2D)                                                            
                                                                 
 conv2d (Conv2D)          (None, 28, 28, 64)        100416    
                                                                 
 max_pooling2d (MaxPoolin  (None, 14, 14, 64)       0         
 g2D)                                                            
                                                                 
 conv2d (Conv2D)          (None, 8, 8, 64)          200768    
                                                                 
 max_pooling2d (MaxPoolin  (None, 4, 4, 64)         0         
 g2D)                                                            
                                                                 
 flatten (Flatten)        (None, 1024)              0         
                                                                 
 dense (Dense)            (None, 256)               262400    
                                                                 
 dense (Dense)            (None, 1)                 257       
                                                                 
=================================================================
Total params: 579,441
Trainable params: 579,441
Non-trainable params: 0
_________________________________________________________________
```

In addition to the Convoltional layers and the Dense layers, a resizing layer was added to account for the discrete dimensions of images in the data. This can be fixed by preprocessing the data as well, but adding the `Resizing` layer saves time required to do the preprocessing the data. It also works better with the data type that `Tensorflow-Datasets` imports the data as.

The batch size for training the model was set to `16`. Due to hardware constraints, it is not possible to allocate memory for a bigger batch size during training. Using a smaller batch size can be considered, but it will increase the training time significantly.

`Adam` optimizer was used with an initial Learning Rate of 0.001. Given that this is a Binary Classification problem, `Binary Cross-Entropy` was used as the loss function. Other optimizers and loss functions can be tested out for changes in model performance.

<br/>
<br/>


## Results

The model achieved an accuracy of ~96% on the training set and ~93% on the test set. The model steadily increases an accuracy after a couple epochs and reaches its peak soon after. More epochs could be used in training but it will result in an overfit model that cannot generalise well. Due to memory constraints, it is also not possible to increase the complexity of the model.

<br/>

[<img src=images/accuracy.jpg height=250>](images/accuracy.jpg)
[<img src=images/loss.jpg height=250>](images/loss.jpg)

<br/>
<br/>

## Possible Improvements and Next Steps

- A web application that uses the model to detect parasites.
- Using a more complex model.
