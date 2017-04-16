---
title: 'Generative and discriminative models'
date: '2017-4-16 10:00'
layout: post
published: true
---

패턴 인식분야에서, 분류에 쓰이는 모델은 크기 두가지로 분류되는데, 이들은 Generative Model(생성 모델)과 Discriminative Model(판별 모델)입니다. 이 둘은 어떤 차이가 있을까요? 

> Generative models model the distribution of individual classes. Discriminative models learn the (hard or soft) boundary between classes

즉, 생성모델은 데이터셋에 포함된 각 클래스들의 확률 분포를 모사하는 모델입니다. 확률 분포에 대한 모델이 있으면 그 데이터셋을 역으로 생성하는 것이 가능합니다. 반면, 판별 모델은 클래스 사이의 경계를 학습합니다. 그러므로 판별 모델은 경계를 통해 샘플데이터가 어느 클래스에 속하게 될지를 직접적으로 판별할 수 있습니다. 

SVM(Support Vector Machine)과 의사결정트리(Decision Tree)는 판별 모델입니다. 그 이유는 그들이 클래스간의 명확한 경계가 어디인지를 학습하기 때문입니다. SVM은 최대마진분류기입니다. 즉, 주어진 커널에 대해서 두 클래스 내의 샘플간 거리를 최대로하는 경계를 학습한다는 의미입니다. 샘플과 학습된 경계사이의 거리는 SVM을 Soft Classifier로 만들기 위한 척도로 사용할 수 있습니다. Decision Tree는 Information Gain이 최대화 되도록 Feature Space를 재귀적으로 나눔에 의해서 의사결정의 경계를 학습합니다.

입력데이터 $x$가 있고, 라벨$y$로 데이터를 분류하려는 상황을 생각해 봅시다.

Let's say you have input data x and you want to classify the data into labels y. A generative model learns the joint probability distribution p(x,y) and a discriminative model learns the conditional probability distribution p(y|x) - which you should read as "the probability of y given x".

Here's a really simple example. Suppose you have the following data in the form (x,y):



```
      y=0   y=1
     -----------
x=1 | 1/2   0
x=2 | 1/4   1/4
```



### References

http://stackoverflow.com/questions/879432/what-is-the-difference-between-a-generative-and-discriminative-algorithm

https://stats.stackexchange.com/questions/12421/generative-vs-discriminative/223850#223850



