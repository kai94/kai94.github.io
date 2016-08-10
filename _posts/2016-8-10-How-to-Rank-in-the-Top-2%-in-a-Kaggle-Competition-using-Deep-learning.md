---
layout: post
title: How to Rank in the Top 2% in a Kaggle Competition using Deep learning
---

## Introduction
I managed to finish in the Top 2%(28th out of 1440 contestants) in Kaggle's State Farm Distracted Driver Detection Competition [link](https://www.kaggle.com/c/state-farm-distracted-driver-detection).

The goal of this competition was to categorize what the driver was doing in a given image into 10 categories.

These are examples of image labeled drinking and talking on the phone - left.

![an image alt text]({{ site.baseurl }}/images/rsz_img_195.jpg "an image title")

![an image alt text]({{ site.baseurl }}/images/rsz_img_7875.jpg "an image title")

The challenge in this competition was how to deal with this very similar dataset. Few of the categories were quick hard to predict correctly even for me and also there were only 26 unique drivers in the dataset which means it was very easy for the models to overfit.

____

## Approaches
My approach in this competion was to use convolutional neural networks(Convnets). Convnets are increasing in popularity from reading zip code on post cards in the 90's to self driving cars lately. Because use of pre trained nets were allowed in this competition, all of the models I used were pre trained nets. Also using semi supervied learning(training the model on the test data using the predictions as label) was allowed, I incorporated it into my models.
____

### Base line Approach
My base line approach was to use VGG16 network. See [Original Paper](http://arxiv.org/pdf/1409.1556v6.pdf) for details. The only preprocessing performed was to resized the images to 224x224 and subtracted the mean pixels of the images. I split the data into training set and validation set by driver to get accurate validation results.

With this approach I got to 0.30 on the Leaderboard.

____

### Dealing with Overfitting
As stated earlier, it was very easy for the network to overfit to this dataset. One way to combat overfitting was to compute small region of interest per class and insert it into the training set. By doing so, I was able to slow the convergence and reduce overfitting.

____

### Region cropping the dataset
In the beginning of the competition, the first thing that came to my mind was to crop the region with the driver to reduce the noise in the dataset. I used the yolo framework. [link](http://pjreddie.com/darknet/yolo/). However the performance was worse than the Base line Approach, so I quickly abandoned this idea. But around 2days before the deadline day, I was strucking to improve my score so I ended trying the same idea using the Faster-RCNN framework [link](http://arxiv.org/abs/1506.01497). By using both the original data and region cropped data, I was able to increase the peformance of the model slightly. If I had hand labeled some of the region in the training data, I'm sure I would have got a better result.

____

### Final model
The final model was an ensemble of VGG16, VGG19, Googlenet and VGG16 + average pooling + softmax. They were all trained using the technique explained above. Since the public/private Leaderboard split was said to be random, I wasn't too afraid of dropping on the private leaderboard. But some people improved their score substantially on private leaderboard, so maybe the split wasn't random.

____

## Conclusion
Never give up:) Even if there isn't much time, you can try new idea to improve your score.
