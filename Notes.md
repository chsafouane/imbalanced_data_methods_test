## Overview

**Factors** that influence the ability of a classifier to identify rare events are:

- Small sample size: Imbalanced classes may not be a problem if the data is big enough
- Class separability: if the classes are linearly separable for e.g, this is not a hard problem
- Within-class imbalance: In some classification problems, a class contains many subclasses; the class is not homogeneous and some subclasses are imbalanced between each others.

<img src="_assets/image-20210713213134558.png" alt="image-20210713213134558" style="zoom:50%;" />

Three **approaches** are usually used to tackle imbalanced data: Data approaches, cost-sensitive approaches and ensembling.

## Metrics

## Undersampling

The **Balancing ratio** is the ratio of the minority class to the majority class. 	

There are two families of methods:

- **Fixed**: reduce the majority class to the same # of observations as the minority class
- **Cleaning**: Clean the majority class based on some criteria

### Random undersampling

This is a naïve technique that undersamples the majority class till reaching the balancing ratio that we want. Some problems with this method

- Some majority classes classes might be hard to learn
- The # of samples in a minority class might be very limited and reaching a certain balancing ratio would eliminate so much information about the majority class

![image-20210719173921526](_assets/Notes/image-20210719173921526.png)

### Condensed Nearest Neighbours

This is a cleaning method that extracts observations from the majority class(es) at the boundary between 2 or more classes. The final dataset shape varies and boundary(ies) matters.

To understand this method, please refer to this video: https://youtu.be/H7f_J4HjlWE. The difference with the video is that the starting set of points S consists of the points in the minority class + 1 point from the majority class. The final version of S is the undersampled dataset.

### Tomek links

2 samples are Tomek Links if they are nearest neighbours and are from a different class. This undersampling method removes Tomek links from the majority class - this behavior can be tweaked to remove tomek links even from the minority class-, and so the final dataset distribution will change. The assumption of this technique is that boundary points are noise.

