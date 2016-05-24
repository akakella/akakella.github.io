---
layout: post
title: Road Detection
description: Free-Space Road Detection for Autonomous Driving
img: /img/road_cover.png
---

For a course project (CS 280, Computer Vision) in graduate school, I developed a technique for detecting "free-space" road regions for autonomous driving applications. The
goal was to use forward-facing photographs of roads under a variety of conditions (curvature, traffic, various markings), and accurately locate the regions the car
would be allowed to travel to. 

The algorithm consists of two major components: a line detection algorithm that searches for road boundaries, and a convolutional neural network for recognizing and
classifying oncoming traffic, pedestrians, and other obstacles.

<div class="img_row">
	<img class="col three" src="{{ site.baseurl }}/img/default_road.png" alt="" title="Default Road Image"/>
</div>
<div class="col three caption">
	Sample road image taken from the <a href="http://www.cvlibs.net/datasets/kitti/">KITTI dataset for road detection.</a>
</div>

The first stage of the algorithm uses a fully convolutional network, trained for object classification, to identify oncoming traffic and pedestrians. The network
architecture is based on the model proposed by <a href="https://github.com/shelhamer/fcn.berkeleyvision.org">Long, et al.</a>, and trained on the <a href="http://host.robots.ox.ac.uk/pascal/VOC/">PASCAL</a> segmentation dataset. The resulting areas containing obstacles are then subtracted from the original image before being passed through the line detection phase of the algorithm.

The second stage of the algorithm involved a series of steps:

* The first is a low pass filter, performed by convolution with a Gaussian kernel.
* This is followed by an HSV-segmentation filter, which only passes through colors resembling the grayish black of asphalt and ignores everything else.
* A canny edge detection process is then applied to search for the strongest edge in the resulting image.
* Then, a hough transform is used to determine orientation of each line, and discard lines that couldn't be part of the desired road boundary.
* Finally, these lines are connected from left to right to form a free-space region.

The results from both stages are then composed to produce the final understanding of the car's environment. Sample results are shown below.

<div class="img_row">
	<img class="col three" src="{{ site.baseurl }}/img/result1_driving.png" alt="" title="Result 1"/>
</div>
<div class="img_row">
	<img class="col three" src="{{ site.baseurl }}/img/result2_driving.png" alt="" title="Result 2"/>
</div>
