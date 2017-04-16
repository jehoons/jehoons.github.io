---
title: 'Paper: Structured inference networks for nonlinear state space models'
date: '2017-4-15 10:00'
layout: post
published: false
---

가우시안 상태공간 모델들은 오랜 세월동안 시퀀셜데이터에 대한 생성모델로써 사용되어 왔습니다.

### What is difference between a generative and discriminative model?

패턴 인식분야에서, 분류에 쓰이는 모델은 크게 Generative model(생성 모델)과 discriminative model(판별 모델)로 구분해서 살펴볼수 있습니다.

이 둘은 어떤 차이가 있을까요? 

> Generative models model the distribution of individual classes. Discriminative models learn the (hard or soft) boundary between classes

즉, 생성모델은 데이터셋에 포함된 각 클래스들의 확률 분포를 모사하는 모델입니다. 확률 분포에 대한 모델이 있으면 그 데이터셋을 역으로 **생성**하는 것이 가능합니다. 반면, 판별 모델은 클래스 사이의 경계를 학습합니다. 그러므로 판별 모델은 경계를 통해 샘플데이터가 어느 클래스에 속하게 될지를 직접적으로 **판별**할 수 있습니다. 

SVM(Support Vector Machine)과 의사결정트리(Decision Tree)는 판별 모델입니다. 그 이유는 그들이 클래스간의 명확한 경계가 어디인지를 학습하기 때문입니다. SVM은 최대마진분류기입니다. 즉, 주어진 커널에 대해서 두 클래스 내의 샘플간 거리를 최대로하는 경계를 학습한다는 의미입니다. 샘플과 학습된 경계사이의 거리는 SVM을 Soft Classifier로 만들기 위한 척도로 사용할 수 있습니다. Decision Tree는 Information Gain이 최대화 되도록 Feature Space를 재귀적으로 나눔에 의해서 의사결정의 경계를 학습합니다.



### References

http://stackoverflow.com/questions/879432/what-is-the-difference-between-a-generative-and-discriminative-algorithm

https://stats.stackexchange.com/questions/12421/generative-vs-discriminative/223850#223850



