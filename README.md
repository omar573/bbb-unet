# Unet: Deep Learning Model for Cell Segmentation
 
Credit: O. Ronneberger and P. Fischer and T. Brox. [U-Net: Convolutional Networks for Biomedical Image Segmentation](http://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/).
Medical Image Computing and Computer-Assisted Intervention (MICCAI), Springer, LNCS, Vol.9351 (2015): pp. 234-241.
 
---
 
## Introduction
 
The motivation behind pursuing this tool stems from the need to quantify a multitude of cell data, in this case Blood-Brain Barrier cell data,
for the purpose of analyzing the impacts of HIV-1 Tat Proteins on the Blood-Brain Barrier (BBB hereafter). While manual segmentation by hand is an option,
it is very slow and time-consuming. Researchers face a high opportunity cost on time when engaging in this time-consuming process of manual segmentation. However, a trained Unet deep
learning model can segment thousands of cells in a few seconds versus manual segmentation by hand which takes, on average, 15 minutes
per image to complete.
 
This repository contains implementations that allow one to start from the elementary stage of raw microscopy images to producing a data frame that contains quantitative features like area and perimeter belonging to each cell.
 
Here is an example of what a sample data frame looks like:
 
![img/df_sample.jpg](img/df_sample.jpg)
 
 
## Data
 
The raw input datadata consist of microscopy images of BBB cells like the following:
 
![data/membrane/train2/image/0.png](data/membrane/train2/image/0.png)
 
 
data/membrane contains sample microscopy images and corresponding masks used for training Unet.
 
 
 
 
 
### Model
 
![img/u-net-architecture.png](img/u-net-architecture.png)
 
Credit: O. Ronneberger and P. Fischer and T. Brox. [U-Net: Convolutional Networks for Biomedical Image Segmentation](http://lmb.informatik.uni-freiburg.de/people/ronneber/u-net/).
Medical Image Computing and Computer-Assisted Intervention (MICCAI), Springer, LNCS, Vol.9351 (2015): pp. 234-241.
 
 
 
### Results
 
The trained model achieves good results with 98% accuracy. This visualization illustrates the successful implementation of Unet on BBB microscopy images:
 
![img/with_fitc.gif](img/with_fitc.gif)
 
 
The left column shows how Unet improves with each epoch. The right column shows masks from a test set (segmented manually by hand).

Credit: Will Dampier, Informatics, Drexel University , 2019. 
 
 
 
### Post-processing
 
The deep learning implementation produces predicted masks for each microscopy image. Predicted masks require post-processing to turn them into
quantitative data that are suitable for statistical analysis. The file named "JSON mask parser.ipynb" contains code that parses cell coordinates from predicted masks, extracts features like area, aspect ratio and perimeter, and produces an organized data frame in CSV format.
For some exploration of a sample data frame using Pandas and Seaborn, please see the file named "Descriptives and visualizations.ipynb". The file named "autoencoder" includes a machine learning model called autoencoder that helps in detecting anomalies in the data before preforming statistical analyses. I included a visualization at the end of the autoencoder file that shows how the autoencoder can identify irregularly shaped cells (labeled in blue) versus regularly shaped cells (labeled in black).
 

