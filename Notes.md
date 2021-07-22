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

2 samples have a Tomek Link if they are nearest neighbours and are from a different class. This undersampling method removes Tomek links by removing the datapoint from the majority class - this behavior can be tweaked to remove the corresponding point the minority class as well-. The final dataset distribution will change. The assumption of this technique is that boundary points are noise.

### One-sided selection

This is considered an improvement on both CNN and Tomek's link. It's a two-step method. First, apply CNN and then apply Tomek's link. 

CNN selects samples of the majority class that are similar to those of the minority class. Thus, it is prone to introduce some noise. With Tomek links, this procedure aims to remove this "noise".

### Edited Nearest Neighbours

This method uses KNN and if the nearest points have the same label as the class of the observation considered, it is removed from the dataset. This method removes samples that are close to the decision boundary (Those that are too similar to observations of the minority class - opposite of CNN).

### Repeated Edited Nearest Neighbours

Repeat the Edited Nearest Neighbours until no more observations are removed or until a maximum # of cycles is reached. The same number of nearest neighbours is used in each pass over the data.

### All KNN

This algorithm works in the same way as Repeated Edited Nearest Neighbours but adds 1 neighbour to KNN at each pass. This algorithm is more stringent than RENN.

### Neighborhood cleaning rule

First apply *Edited Nearest Neighbours* to remove points from the majority class. Then look at the neighbours of the minority class and if any of the neighbours can cause a misclassification, remove it. In the second step, one could set a threshold that represents (from imbalanced-learn doc):

![image-20210722134746398](_assets/Notes/image-20210722134746398.png)

### NearMiss

This method is a fixed method. The final size of the dataset is 2 * size of minority class. There are 3 versions of it.

- *NearMiss 1*: Retains points in the majority class that are the closest to their neighbours. Usually, it retains points that are far away from the main cluster of the majority class
  - Select the 3 nearest neighbours for each point in the majority class from the minority class
  - Select the points from the majority class with the smallest average distance to the minority neighbours.
- *NearMiss 2*: Retain points in the majority class that are the closest to the farthest points from the minority class. Usually, it keeps points from the majority class that are in the middle with respect to the points of the minority class
  - For each point of the majority class, select the 3 furthest points in the minority class
  - Select the points from the majority class that have the smallest average distance to the corresponding points in the minority class
- *NearMiss 3*: This method removes points from majority class that are very far from the main cluster of points and very close to the decision boundary
  - For each point in the minority class, select the 3 neighbours from the majority class. We then remove all points that are far away from the majority class
  - For each point in the majority class, select the 3 closest neighbours from the minority class, calculate the average distance and select only those whose average distance is the largest.

Here are some alternative definition from [machinelearningmastery](https://machinelearningmastery.com/undersampling-algorithms-for-imbalanced-classification/):

![image-20210722173531843](_assets/Notes/image-20210722173531843.png)

### Instance Hardness Threshold

Train a classifier and remove the points that are very hard to classify in the majority class. A probability threshold is defined to say when the instance is considered as hard to classify.

For a more thorough explanation, please read [this blog](https://towardsdatascience.com/instance-hardness-threshold-an-undersampling-method-to-tackle-imbalanced-classification-problems-6d80f91f0581)

## Oversampling

![image-20210722220020700](_assets/Notes/image-20210722220020700.png)

### Random Oversampling

Duplicate observations at random from the minority class until a certain balancing ratio is reached. This increases the likelihood of overfitting.
