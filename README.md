### General Context:

Deforestation is the permanent removal of standing forests, which occurs for a variety of reasons and has many devastating consequences. The loss of trees and other vegetation can cause climate change, desertification, soil erosion, fewer crops, flooding, increased greenhouse gases in the atmosphere. In the last 13 years, more than 43 million hectares of forest have been devastated in the world, an area the size of California, USA.

It is important to stop deforestation as soon as possible, before the damage is irreversible. There are many ways to fight deforestation. This challenge will consist of using satellites' images of the earth's surface in order to detect, as soon as possible, areas in the midst of deforestation and prevent its expansion.


### How to run:

In order to run our code, you need to create a folder named 'hackaton_deforestation' in your google drive and insert all the datasets

### Dataset:

For this challenge, you have satellite images and information about their latitude, longitude, year of shoot and type of deforestation.


### Features:

1- latitude: Where the photo latitude was taken.

2- longitude: Where the photo longitude was taken.

3- year: Year, in which the photo was taken.

4- example_path: Path where the sample image is located.

We decided to ignore features 1, 2 and 3 since we considered they wouldn't give us useful information for the models we were planning to use in the future.


### Goal:

Predict the class of the deforested area.


### Additional Information

There are three downloadable files:

train_SE.csv: It is a table that relates the images of the training dataset with the attributes of the image. Download train_SE.csv

test.csv: It is a table that relates the images of the testing dataset with the attributes of the image. Download test.csv

train_test_data.zip: It is a zipped folder containing the training image datasets and testing datasets. The weight of this folder is 309MB. Download train_test_data.zip 


### Expected outcomes:

label: In this column you will have the following categories:
    
0. Plantation: Encoded with number 0, Network of rectangular plantation blocks, connected by a well-defined road grid. In hilly areas the layout of the plantation may follow topographic features. In this group you can find: Oil Palm Plantation, Timber Plantation and Other large-scale plantations.

1. Grassland/Shrubland: Encoded with number 1, Large homogeneous areas with few or sparse shrubs or trees, and which are generally persistent. Distinguished by the absence of signs of agriculture, such as clearly defined field boundaries.

2. Smallholder Agriculture: Encoded with number 2, Small scale area, in which you can find deforestation covered by agriculture, mixed plantation or oil palm plantation.

### Data Augmentation

To improve our model's performance, we performed data augmentation on the train set. The augmented images include transformations such as: normalization, scaling, rotation, width and height shift, horizontal flip, zoom and brightness transformations.

### Modeling: Transfer Learning - Resnet50:

In order to solve the problem of the vanishing/exploding gradient, the ResNet architecture introduced the concept called Residual Blocks. In this network, we use a technique called skip connections. The skip connection connects activations of a  layer to further layers by skipping some layers in between. This forms a residual block. Resnets are made by stacking these residual blocks together.

We used ResNet50 model from Tensorflow library with pre-trained weights. We have frozen the convolutional layers and then added two Dense layers: the first with 512 neurons + ReLu activation function and the second with 3 neurons + softmax activation.

We then compiled the model using the Adam optimizer with initial learning rate 0.001 and used the categorical cross entropy loss given that the outputs are non binary discrete values.

After that we trained the last layers of the model (about 1M parameters) with a batch size of 32.

### Conclusion

During the day we tried multiple approaches to preprocess the images including visualizing bands, openCV Canny and Sobel transformations. However, none of these approaches seemed to improve the F1-score. The only big improvement that we were able to get was when we included data augmentation in the model.

For these reasons, we believe that preprocessing the images is one of the most essential aspects to solve the problem and without this phase completed the model stabilizes with accuracy values around 0.6.





