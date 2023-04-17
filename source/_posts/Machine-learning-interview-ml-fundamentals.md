title: Machine Learning Interview Prep -- ML Fundamentals
date: 2023-1-24
tags:
- Machine Learning
- Study
categories:
- [Computer Science, Machine Learning]
---

This is a series of notes that I prepared during my job seeking in the last few months and there will be four separate notes in total:
- **Fundamentals of Machine Learning** (This note)
- Fundamentals of Deep Learning
- Machine Learning Models
- Derivation, Implementation & Experience

This note will cover some very basic concepts of machine learning and will focus on the application, instead of the theory.

<!-- more -->

Although there's a *fundamental* in the title, this note is not a good material for someone to study ML. While the notes cover a plethora of topics, it doesn't contain the necessary details for you to understand if you are unfamiliar with them. If you would like to learn machine learn, some books that I find very useful are:
- *Pattern Recognition and Machine Learning* by Christopher Bishop,
- *Machine Learning* by Zhihua Zhou,
- *Deep Learning* by Aaron Courville, Ian Goodfellow, and Yoshua Bengiob,
- and *Reinforcement Learning: An Introduction* by Richard S. Sutton, Andrew Barto.

For those who want to prepare them for a machine learning system design interview, the following books are commended:
- *Designing Data-Intensive Applications* by Martin Kleppmann
- *Machine Learning Systems Design (Stanford CS 329S)* or you can find the book *Designing Machine Learning Systems* by Chip Huyen

You can also find at the end of this note some useful references.

Personally, I do find it useful to go through these key points to refresh my knowledge from time to time and it helps with both work and research.

# Fundamentals of machine learning

## Overfitting/Underfiting
- Overfitting happens when the model performs better on training data but worse on test/validation data
    - Usually happens with complex model; Can be a result of fitting noises/outliners in the training data
    - Some common methods to detect, treat and avoid overfitting
        - Use cross-validation to detect overfitting
        - Consider simple models, regularization & early stop
        - Data augmentation & feature selection
        - Dropout & hyperparameter tuning (mostly for DNN)
- Underfitting happens when model fails to fit the training data
    - Simple model tends to underfit.
    - Common practices to avoid underfitting
        - Increase training data and/or epochs.
        - More complex model including more features and/or less regularizations.

## Bias-variance tradeoff
- Bias measures the difference between model predictions and ground truth.
- Variance measures how prediction changes with varying inputs.
    - Simple model tends to have high bias & low variance (extreme case: model outputs a constant), corresponding to underfeeding
    - Complex model tends to have low bias & high variance, corresponding to overfitting.
- Error = bias^2 + variance + irreducible errors

## Generative vs Discriminative
- Generative model estimates P(x|y) then deduces P(y|x)
    - Learn a distribution of the data, examples like GDA, Naive Bayes
- Discriminative model estimates P(y|x) directly
    - Learns a decision boundary, examples like SVMs, DNN & regressions

## Regularization
- L1 regularization or LASSO: sum of absolute value, 1-norm (special case of p-norm)
    - Makes the model more sparse (more weights become zero)
        - Ideal for feature selection
    - Bayesian regression with a Laplacian prior
- L2 regularization or ridge: square root of sum of square
    - Effectively simplify the model (more weights become small, smaller high-order contributions)
        - It won’t give too many zeros since the gradient becomes small around 0 while L1 has a constant gradient.
    - Bayesian regression with a Gaussian prior, 2-norm
- Why we don’t use L3, L4 or higher order in practice?
    - Unnecessary since a liner combination of L1 and L2 approximates higher-order ones at the origin
- See a good article from MLOps Blog for more details

## Metrics & Evaluation
- precision and recall trade-off
    - Precision P = TP/(TP+FP), used when FP comes with higher costs
    - Recall R = TP/(TP+FN), used when FN comes with higher costs
    - Increasing/decreasing the threshold leads to higher/lower precision & lower/higher recall (see Andrew Ng’s lecture)
- F1 is harmonic mean of recall and precession: 2/F1 = 1/P + 1/R
    - Better than accuracy when the data is imbalanced
    - Macro F1: average of F1 using all confusion matrices
    - Micro F1: get the average P & R using all confusion matrices and then compute F1
- ROC (Receiver Operating Characteristic)
    - X-axis as FPR = FP/(TN+FP); Y-axis as TPR=R=TP/(TP+FN)
    - Model is better if appears on the upper-left corner
- AUC (Area Under ROC Curve)
    - Plotted in ROC using different threshold for positive and negative prediction.
        - The probability of predicting a higher score for a randomly selected positive than negative.
        - Lowering the threshold allows more items to be classified as positive, thus increasing both true positive rate and false positive rate.
    - Pros
        - AUC is scale-invariant. It measures how well predictions are ranked rather than their absolute values.
        - AUC is classification-threshold-invariant.
- Imbalanced data
    - F1 and Precision-Recall Metrics work well if positive classes are more important
    - We can use Sensitivity-Specificity Metrics if both classes are equally important
        - Sensitivity or Recall R = TP / (TP + FN); Sensitivity S = TP / (TP + FN)
        - Geometric mean or G-mean = (R+S)^1/2

## Common loss functions
- MSE: (f(x)-y)^2, where f(x) is prediction and y is ground truth
    - MSE with linear regression is convex but not with logistic regression
    - Ordinary least square or OLS uses MSE as loss function; Maximum likelihood estimation or MLE assumes that the error follows a Gaussian distribution and it’s eventually equivalent to OLS.
- Log loss: -y*log(f(x))
    - Also known as log-likelihood loss, logistic loss or cross-entropy loss (CE is equivalent to log loss when we assume Bernoulli distribution)
    - Some basic concepts
        - Information: I = -log(p)
        - Entropy: H = -p*I = -p*log(p)
        - Cross Entropy or CE: CEH = -p*log(q)
        - Relative Entropy or KL Divergence: KL = p*log(p/q) = CEH - H
    - In ML, we assume p is known so CEH and KL is equivalent up to some constants
    - Logistic regression with sigmoid (or generally softmax) using log loss is convex
- Other losses
    - Focal loss, Hinge loss, Margin loss, Triplet loss, Contrastive loss, etc.


## Reference (English)
Reference
- [Machine Learning Interview Questions by InterviewBit](https://www.interviewbit.com/machine-learning-interview-questions/)
- [Github: alirezadir/machine-learning-interview-enlightener](https://github.com/alirezadir/machine-learning-interview-enlightener); Especially [Section 4. ML Breadth/Fundamentals](https://github.com/alirezadir/machine-learning-interview-enlightener/blob/main/ml-breadth.md)
- [Github:nxpeng9235/MachineLearningFAQ](https://github.com/nxpeng9235/MachineLearningFAQ/blob/main/syllabus.jpg)
- [Tour of Evaluation Metrics for Imbalanced Classification](https://machinelearningmastery.com/tour-of-evaluation-metrics-for-imbalanced-classification/)
- [AllenCX/DS-ML-Interview-Questions](https://github.com/AllenCX/DS-ML-Interview-Questions)

## Reference (Chinese)
- [机器学习八股文（三）以及一些准备建议](https://www.1point3acres.com/bbs/thread-714558-1-1.html)
    - [机器学习八股文（一）- 快问快答](https://northern-dracopelta-98c.notion.site/5b22e124e16d4b2d937940367ca20eb0?v=19feabb85e9e4b54bc498579b3c7f1c5)
    - [机器学习面试笔试求职必背！八股文（1/5）](机器学习面试笔试求职必背！八股文（1/5）)(Also 2, 3, 4 & 5,但是回答质量一般，建议作为flash card查漏补缺就行)
    - [深度学习面试79题：涵盖深度学习所有考点（1-50）](https://zhuanlan.zhihu.com/p/231171098)
- [关于辛普森悖论的深度解析](https://zhuanlan.zhihu.com/p/348967975)

## Recommended study materials (Chinese)
- [ShowMeAI 之 图解机器学习系列](https://www.showmeai.tech/article-search?keyword=%E5%9B%BE%E8%A7%A3%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0)
- [计算广告与机器学习－技术分享平台](http://www.52caml.com/home/)
- [机器学习基础复习](https://www.zhihu.com/column/c_1417097003608666112)