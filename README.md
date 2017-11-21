# Semantic Segmentation
[//]: # (Image References)

[image1]: ./output/train_hist.png "Sample 1"
[image2]: ./output/valid_hist.png "Sample 2"
[image3]: ./output/train_aug_hist.png "Sample 3"
[image4]: ./output/valid_aug_hist.png "Sample 4"
[image5]: ./output/color.png "Sample 5"
[image6]: ./output/gray.png "Sample 6"
[image7]: ./output/vanalla_loss.png "Sample 7"

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

So there should be a nice balance between the Batch Size & Number of Epochs. Still it was giving coarse segmentation.
But further improvement I was able to get by using kernel_initializer with a normal distribution of std deviation of 0.01.
By doing this, I was able to get finer segmentation.

With progress of epoch, the average loss keeps decreasing. The loss decreases beyond 0.01. I have added early exit condition where if the loss reaches less than 0.01 then exit the training.

Few sample output images in which segmentation is working well

![alt text][image1]

![alt text][image2]

![alt text][image3]

![alt text][image4]

![alt text][image5]

![alt text][image6]

![alt text][image7]
