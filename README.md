# Cancer-Detection

We collected datasets from the following sources
1. TUPAC 16' challenge.
2. ICPR'14 challenge.
3. ICPR'12 challenge.

The entire dataset gave use us 74 patients for training, 24 patient samples for testing and 11 patient samples for validation.

# Preprocessing:
The dataset went through the following Preprocessing procedure.
1. Stain Normalization:
  This is an important step since the data color variation between the images is very large and it will create difficulty in training. Stain Nomalization will reduced color variation and will bring images to the same color space.

2. Binary Masks Generation:
   Images from the challenge came with csv files which indicated the area where the tumor was present. TUPAC'16 and ICPR'14 csv files contained only x and y location of the tumor so we created white circle on that location of randon radius (10-17 pixels) since we do not know the actual size of the tumor. ICPR'12 came with csv files that contained x and y locations of the entire tumor.
   
Add Image Here


# Detection
For detection we used a Mask RCNN. The Mask RCNN works towards the problem of Detection and Segmentation. We used Detectron 2, Mask RCNN for this problem. It had the following architecture. 

Add image here


It was trained on the a Tesla K80 GPU with a batch size of 20 and a learning rate of 0.00025. l1-loss and cls-loss were used for detection and pixel-wise cross entropy loss for pixel wise segmentation.

# Dataset prep for classification
The detected cell of Mask RCNN are extracted and fed to a saperate classifier trained for classification of mitotic and non-mitotic cells. Due the limitation of the dataset, it went throught data augmentation.

# Classification
Several models like SVM, Naive Bayes and Deep Learning models like CNN and VGG16 were used for classification but CNN had the best results.

CNN:
The CNN used had three convolutional blocks along with Max Pooling and Drop out of 0.2 and two dense layer and a softmax layer for classification. 
The model was first trained on a large balanced Malaria cell dataset. After that transfer learning was used to train it on own cancer dataset and first and second convolutional blocks were frozen while 3rd block and dense layers were trained again as part of the fine tuning step.

The model was trained on a Tesla K80 GPU, Framework used was Keras, optimizer used was Adam.
[Image here]


The CNN achieved the highest results with a F-score of 0.78. It preformed better then VGG16 because it is a smaller network suited for small dataset and it was first trained on a cell dataset and transfer learning was used.


