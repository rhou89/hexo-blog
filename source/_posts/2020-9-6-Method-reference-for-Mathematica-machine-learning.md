---
title: Method reference for machine learning with MMA
date: 2020-9-6
tags:
- Coding
- Machine Learning
categories:
- [Computer Science, Machine Learning]
- [Computer Science, Coding]
---

Mathematica (MMA) is known for its comprehensive library that covers almost everything you need in mathematics, physics and engineering. While I'm a big fan of MMA and MMA released its machine learning (ML) features long time ago, I used to use Python for ML practices because Python is more widely accepted by the data science community and thus, provides better supports. However, it has been 4 years after MMA 11's first release, the ML features in MMA are getting much better than before. So, I've spent sometime playing with MMA ML and made such a reference for later conveniences.

<!-- more -->

## Data preprocess
- *RandomSample*: gives a pseudorandom sample of a list. I used this for splitting my data into training and testing (and sometimes validating) sets.
- *Standardize*: the Standardization process. Namely, shifts and rescales the elements so that the list has zero mean and unit variance.
- Statistics methods:
  - *Mean*
  - *Variance* ($S^2$)
  - *StandardDeviation* ($S$)
- *Chop* or *Threshold*: replaces data that is close to zero by exact zero.
- *Interpolation*: constructs an interpolation from a list. 
- *CountsBy*: count the unique elements and their frequency according to a given set of rules.
- *GroupBy*: gives an association that groups the elements and into lists associated with distinct keys.
  - Keys: returns the keys.
- *SortBy*: sort the list following a given set of rules.
- *LogisticSigmoid*: Everyone knows this function but I used to write it down as $1/(1+e^{-x})$.
  - MMA provides many similar special numerical functions like *UnitStep*, *HeavisideTheta*, *DiracDelta*, *KroneckerDelta*, etc.

## Function fittings
- *LinearModelFit*: constructs a linear model fitting $y=kx+b$.
- *FindFormula*: finds a pure function that approximates the given list.
- *FindFit*: similar to FindFormula but you have to provide a parameterized function form and it returns a fitting values of the parameters.
- *FindSequenceFunction*: find a simple function that yields the given sequence. With this, you would never fail a number series reasoning question! 
- *TimeSeriesModelFit*: constructs a time series model for a given list and you may specify the model and/or parameterization here.
  - The keyword "PredictionLimits" returns the lower and upper bound at a given time.

## General ML methods
- *FeatureExtraction*: extracts features from given data
  - Can be applied to numerical data, nominal data, text, images and audio objects.
- *DimensionReduce*: projects input data onto lower-dimensional subspace.
  - Performance options: "Quality" or "Speed"
  - Some available methods: "Linear", "LLE" (locally linear embedding), "PrincipalComponentsAnalysis" (PCA), "Isomap" (isometric mapping), etc.
- *Classify*: the usage of this method is diverse but you know its job by its name.
  - There are some useful built-in classifier: "CountryFlag", "FacialAge", "FacialExpression", "FacialGender", "Language" (recognizes which natural language text is in), "NotablePerson", "ProgrammingLanguage", "Spam", etc.
  - Available option for training goal: "Quality" (maximize accuracy), "Speed" (maximize speed), "TrainingSpeed" (minimize time spent on training), etc.
- *Predict*: generates a predictor based upon a list of ordered pair $a->b$. The usage of this method can also be versatile.
  - The available training models include: "DecisionTree", "GradientBoostedTrees", "LinearRegression", "NearestNeighbors", "NeuralNetwork" and "RandomForest".
- *ClassifierMeasurements*: gives measurements associated with a given property when a classifier is evaluated on some test sets.
  - Some examples of available properties: "Accuracy", "CohenKappa", "Error" (fraction of incorrectly classified examples), "GeometricMeanProbability", "LogLikelihood", "MeanCrossEntropy", etc.
- *PredictorMeasurements*: similar to ClassifierMeasurements but comes with some visualization features.
- *ClusterClassify*: performs clustering on a given data.

Note added 09/07/2020: A new feature is added recently in MMA 12: SequencePredict.

## Specific ML methods
- Neural networks
  - *NetModel*, *NetTrain*, *NetGraph*, etc.
- Computer visions
  - *ImageIdentify*: attempts to identify what a given image is a picture of.
  - *FindFaces*: attempts to find human faces in a given image.
  - *TextRecognize*: recognizes text in a given image.
- Natural language processing
  - *LanguageIdentify*: attempts to determine what human language is.
  - *TextStructure*: returns the grammatical structure of natural language text.
  - *FindTextualAnswer*: gives the substring of the given text that best appears to answer a given question.