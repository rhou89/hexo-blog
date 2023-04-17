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

# Machine Learning Models

- Regression
    - LinearRegression的基础假设是什么 (Derivation of linear regression with regularization) [https://blog.csdn.net/qq_45537774/article/details/115695866?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0.essearch_pc_relevant&spm=1001.2101.3001.4242]
    - what will happen when we have correlated variables? how to solve 
    - explain regression coefficient 
    - what is the relationship between minimizing squared error and maximizing the likelihood?
    - How could you minimize the inter-correlation between variables with LinearRegression?
    - if the relationship between y and x is nolinear, can linear regression solve that 
    - why use interaction variables
    - Logistic Regressionlogisticregression和svm的差别（我想这个主要是想问两者的loss的不同以及输出的不同一个是概率输出一个是score）LR大部分面经集中在logloss和regularization
- Clustering and EM
    - K-means clustering(explain the algorithm in detail;whether it willconverge收敛到global or local optimums
    - how to stop )EM算法是什么GMM是什么和Kmeans的关系
- Decision Tree
    - How regression/classification DT splitnodes?
    - How to prevent overfitting in DT?
    - How to do regularizationin DT?
- Ensemble Learning
    - difference between bagging and boostingg
        - bdt和randomforest区别pros and cons
        - explaing bdt/randomforest 
        - will random forest help reduce bias or variance
        - why randomforest can help reduce variance
- Other common models 
    - Naive bayes
        - Use Bayesian theorem to estimate P(y|x), where x are evidences
            - Naive means it assume x are iid so that the joint probability distribution can be simplified as P(y|x1,x2,..,xn) = P(y|x1)*P(y|x2)*…*P(y|xn)
        - Pros: Simple but stable; Perform good on small datasets as well as multi-class classification; Not sensitive to missing data and/or outliers; No overfitting
        - Cons: iid assumption is too strong; Rely heavily on priori estimation; Bias could be high
    -  SVM
        - Use a hyperplane as the decision boundary and maximize (soft or hard) margin. One can use kernel method if the data is not linearly separable.

    - Generative Model和Discrimitive模型比起来Generative更容易overfitting还是underfitting
    - NaïveBayes的原理基础假设是什么
    - LDA/QDA是什么假设是什么
    - Explain SVM如何引入非线性
    - Explain PCA
    - Explain kernel methods, why to use what kernels
    - do you know怎么把SVM的output按照概率输出
    - ExplainKNN!
    - 所有模型的pros and cons（最高频的一个问题）
    - 数据处理类怎么处理imbalanced data high-dim classification有什么问题以及如何处理missing dat
    - 如何处理how to do feature selection 
    - how to capture feature interaction
Attention (This is a very good blog on attention and transformer [https://jalammar.github.io/illustrated-transformer/])
LDA vs PCA [http://alexhwilliams.info/itsneuronalblog/2016/03/27/pca/]
NB vs KNN
GBDT vs RF
KNN vs KMeans
GMM and EM
FM [https://mp.weixin.qq.com/s?__biz=Mzg5NTYyMDgyNg==&mid=2247489278&idx=1&sn=f3652394955d719bf02a91ca3b179ed2&source=41#wechat_redirect]
        
## Reference
- [Creation and manipulation of quantized vortices in Bose-Einstein condensates using reinforcement learning](https://arxiv.org/abs/2003.05149)
- [GP equation - Wikipedia](https://en.wikipedia.org/wiki/Gross%E2%80%93Pitaevskii_equation)
