# Pedestrian detection using Faster RCNN
Faster R-CNN is a region-based convolutional neural network used for object detection. It is a single, end-to-end, unified network that can accurately and quickly predict the locations of different objects [1]. 
The general structure of faster RCNN consist of three stages including features extraction, region proposal network (RPN), object detection (region of interest (RoI) Pooling, Classification, Regression) as shown in Figure below:

![RCNN_Structure](https://user-images.githubusercontent.com/89004966/163299142-eae725e6-bb4f-41cf-ba18-896f0a19f709.gif)

The First CNN performs feature extraction over the input image to produce feature map which is the input to RPN. The RPN is a fully convolutional network that takes feature map as input and generates proposals with various scales and aspect ratios. These proposals tell the object detection module where to look. 

Since the RBN is the backbone of faster RCNN, the structure describing how it works is shown in Figure below:

![RPN](https://user-images.githubusercontent.com/89004966/163299717-c3261afb-06db-44f6-bae5-ddc30ae11fb4.gif)


A 3×3 sliding window moves across the feature map and maps it to a lower dimension vector.
For each sliding window location, it generates multiple possible regions based on k fixed-ratio anchor boxes. Each region proposal consists of two main parts. The first one is the objectnes score for that region, so classification loss will be used to classify the region as background or foreground i.e., object or not. The second part is the 4 coordinates representing the bounding box of the region, so a regression loss will be used to refine the bounding box.
For all obtained region proposals from RPN, a fixed-length feature vector is extracted from each region using the ROI pooling layer that splits each region proposal into a grid of cells and apply max pool operation to each cell in the grid to return a single value. Then, this extracted feature vector is passed to fully connected layers. The output of the last layer is split into 2 layers including Softmax classification to predict the class scores (i.e., the object is pedestrian) and regression to predict the bounding boxes of the detected objects.

## Faster RCNN Training

Faster RCNN has been trained on a sample of 269 images taken from PennFudanPed (few people) and WiderPerson (crowd people) with 9/1 train validation split. 

The training and validation done with 15 epochs using PyTorch and OpenCV on Google Colab. 

Training and validation loss over time have been obtained as shown in Fig. 3 and Fig. 4 respectively.

![image](https://user-images.githubusercontent.com/89004966/163299977-2b84f7c5-7b4a-48f8-afa9-d913a55caf30.png)
