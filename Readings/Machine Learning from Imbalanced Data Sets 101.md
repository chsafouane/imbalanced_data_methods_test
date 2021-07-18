# Machine Learning from Imbalanced Data Sets 101

Note: This article was published in the year 2000.

## Idea 1: Play with the threshold of the classifier

Most ML algorithms have two main assumptions:

- Maximizing the accuracy is the goal
- The classifier will operate on the same data as the training data

When working with imbalanced data, one should start/always adjust the threshold of the output classifier before using other methods

## Idea 2: Need for better sampling strategies

Rebalancing classes artificially doesn't always work:

- Some classifiers are insensitive to stratification
- What is the appropriate sampling strategy for a given dataset. Classes in the same dataset might not be equally difficult. E.g: Downsampling a majority class that is hard to learn might be a very bad idea.

## Idea 3: When profiling comes to the rescue!

When you have too few data of some class that you end up with a complete lack of representation of certain of its aspects, methods for profiling the majority class might be the solution

