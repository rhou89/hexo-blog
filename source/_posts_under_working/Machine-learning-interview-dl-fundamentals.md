title: Machine Learning Interview Prep -- ML Fundamentals
date: 2023-1-24
tags:
- Machine Learning
- Study
categories:
- [Computer Science, Machine Learning]
---

This is a series of notes that I collected during my job seeking in the last few months and there will be four separate notes in total:
- **Fundamentals of Machine Learning** (This note)
- Fundamentals of Deep Learning
- Machine Learning Models
- Derivation, Implementation & Experience

<!-- more -->

# Fundamentals of deep learning
- DNN为什么要有biasterm
    - The bias allows the activation function to be shifted to the left or right to better fit the data.
    - biasterm的intuition是什么
- 什么是Back Propagation
    - 梯度消失和梯度爆炸是什么 怎么解决
    - Common practices to resolve vanishing gradient
        - Use other activation functions such as ReLU.
        - Use residual networks.
        - Use batch normalization.
        - Check weight initialization & reduce layer depth.
    - 神经网络初始化能不能把weights都initialize成0
        - Initializing weights with 0s leads to neurons to learn the same features because the derivatives will remain same for every weight. Any same constant initialization will produce a poor result.
- DNN和LogisticRegression的区别
    - 你为什么觉得DNN的拟合能力比LogisticRegression强how to do hyperparameter tuningin DL/random search grids earch
    - Basically, we can think of logistic regression as a one layer neural network.
    - The complicated structure of MLP make neural network able to extract useful features. While logistic regression cannot learn the features itself.
    - It is possible to train logistic regression with second-order methods such as newton method. But this computation is not efficient for larger NNs. So the slight different lies in the possible optimizers.
- DeepLearning有哪些预防overfitting的办法
    - 什么是Drop out A good article on dropout (Chinese version) [https://zhuanlan.zhihu.com/p/38200980]
    - Dropout refers to ignore p neuron activations randomly during a particular forward or backward training phase. It helps to prevent overfitting.
    - It is not needed during testing. But to account for the missing activations during training, the trick is to divide the outputs of each neuron by 1-p.
        - why it works 
        - dropout的流程是什么(训练和测试时的区别)
- 什么是Batch Norm 
    - why it works
    - BN的流程是什么(训练和测试时的区别)
    - BN is a technique that standardizes the inputs to a layer for each mini-batch. This has the effect of stabilizing the learning process and dramatically reducing the number of the training epochs.
    - During training, the mean and variance are calculated based on the specific batch while they are calculated based on all the batches during testing phase.
- common activation functions
    - sigmoid tanh relu leak yrelu 是什么以及每个的优缺点
    - Sigmoid
Pros:
        1. It is nonlinear so it can be used to activate hidden layers in a neural network.
        2. It is differentiable everywhere so gradient-based backpropagation can be used with it.
        3. Its output ranges from 0 to 1 so it can generate probabilities.
Cons:
        1. The gradient for inputs that are far from the origin is near zero, so gradient-based learning is slow for saturated neurons using sigmoid.
        2. When used as the final activation in a classifier, the sum of all classes is not necessarily 1.
    - Tanh
        - Pros: same as sigmoid but the result ranges between (-1, 1).
        - Cons: vanishing gradient: the inputs that are far from the origin are near zero.
    - 为什么需要nonlinear activation functions
        - It can produce a nonlinear decision boundary via nonlinear combinations of the weights and inputs.
- Different optimizers
    - SGD RMS prop Momentum Adagrad Adam 的区别
    - Batch和SGD的优缺点
    - Batchsize的影响
        - Large batch size results in faster convergence but sometimes it may make the model stuck with local minimum and requires more epochs. Small batch makes convergence slow but may have better results since more randomness is introduced.
    - learningrate过大过小对于模型的影响
        - Problem of Plateau saddle point 
        - A larger learning rate allows the model to learn faster, at the cost of arriving on a sub-optimal final set of weights. A smaller learning rate may allow the model to learn a more optimal set of weights but takes longer time to train, and increases the risk of overfitting.
    - SGD is a stochastic approximation of gradient descent optimization. It replaces the actual gradient that is calculated from the entire dataset by an estimate that is calculated from a randomly selected subset of the data.
    - SGD oscillates across the slops of the ravine while only making hesitant progress along the bottom towards the local optimum. Momentum helps accelerate SGD in the relevant direction and dampens oscillations.
    - Adam computes the adaptive learning rates for each parameter. In addition to storing an exponentially decaying average of past squared estimated gradients of the first moment, it also keeps an exponentially decaying average of the past estimated gradients of the second moment.
    - RMSprop stands for root mean square propagation. It is a gradient descent optimization algorithm for mini-batch learning of neural networks. It uses a moving average of squared gradients to normalize the gradient to deal with the vanishing and exploding gradient problems. Simply put, it uses an adaptive learning rate instead of treating the learning rate as a hyperparameter.
- When transfer learning makes sense
        
## Reference
- [Creation and manipulation of quantized vortices in Bose-Einstein condensates using reinforcement learning](https://arxiv.org/abs/2003.05149)
- [GP equation - Wikipedia](https://en.wikipedia.org/wiki/Gross%E2%80%93Pitaevskii_equation)
