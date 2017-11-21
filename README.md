# SemanticSegmentation

The goal of the project is to train an FCN-8 model which can segment portions of road in images.
The segmentation is to be achieved by coloring the pixels containing portion of road.

# FCN-8 Model
The encoder for FCN-8 is the VGG16 model pretrained on ImageNet for classification. The fully-connected layers are replaced by 1-by-1 convolutions. The decoder of FCN-8 constists of upsampling and skip connections. 

There are only 2 classes being used:
Class 1: Road
Class 2: No Road
So the output of FCN-8 would segment the image into "Road" and "No Road" segments

# Results

I am using the following Hyperparameters tuning:

Keep Probability for Dropouts: 0.5
Learning Rate : 0.0001
Epochs: 45
Batch Size: 4
Kernel Regularizer: L2 regularizer with lambda = 0.001

Observation:
* Keeping the number of epochs constant, and then increasing the Batch Size was degrading the performance
* Increasing the number of epochs was improving the performance

So there should be a nice balance between the Batch Size & Number of Epochs
But further improvement I was able to get by using kernel_initializer with a normal distribution of std deviation of 0.01

With progress of epoch, the average loss keeps decreasing. The loss decreases beyond 0.01. I have added early exit condition where if the loss reaches less than 0.01 then exit the training.

