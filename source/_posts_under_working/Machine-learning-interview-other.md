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

Implementation & derive
- 写代码实现两层fully connected网络
- 手写CNN
- 手写KNN
- 手写K-means
- 手写softmax的back propagation
- 给一个LSTM network的结构 要你计算how many parameters
- convolution layer的outputsize怎么算?

项目经验类
- 训练好的模型在现实中不work问你可能的原因
- Loss趋于Inf或者NaN的可能的原因
- 生产和开发时候data发生了一些shift
- 应该如何detect和补救
- annotation有限的情況下你要怎麼Train model
- 假设有个model要放production了但是发现online one important feature missing不能重新train model你怎么办
- NLP/RNN相关
    - LSTM的公式是什么
    - why use RNN/LSTM LSTM比RNN好在哪
    - limitation of RNN
    - How to solve gradient vanishing in RNN
    - What is attention why attention
    - Language Model的原理
        - N-GramModel
        - What’s CBOW and skip-gram?
        - 什么是Word2Vec 
            - loss function是什么
            - negative sampling是什么
        - Bert
    - CNN/CV相关
        - max pooling conv layer是什么
        - 为什么做pooling为什么用conv lay
        - 什么是equivariant to-translationa in variant to translation 1x1filter
        - 什么是skipconnection
        
## Reference
- [Creation and manipulation of quantized vortices in Bose-Einstein condensates using reinforcement learning](https://arxiv.org/abs/2003.05149)
- [GP equation - Wikipedia](https://en.wikipedia.org/wiki/Gross%E2%80%93Pitaevskii_equation)
