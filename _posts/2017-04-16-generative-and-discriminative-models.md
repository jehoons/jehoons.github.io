---
title: 'Generative and discriminative models'
date: '2017-4-16 10:00'
layout: post
published: true
---

패턴 인식분야에서 분류에 쓰이는 모델은 크게 두가지로 분류될 수 있는데, 이들은 각각 Generative Model(생성 모델)과 Discriminative Model(판별 모델)입니다. 이 둘은 어떤 차이가 있을까요? 

> Generative models model the distribution of individual classes. Discriminative models learn the (hard or soft) boundary between classes

즉, 생성모델은 데이터셋에 포함된 각 클래스들의 확률 분포를 모사하는 모델입니다. 확률 분포에 대한 모델이 있으면 그 데이터셋을 역으로 생성하는 것이 가능합니다. 반면, 판별 모델은 클래스 사이의 경계를 학습합니다. 그러므로 판별 모델은 경계를 통해 샘플데이터가 어느 클래스에 속하게 될지를 직접적으로 판별할 수 있습니다. 

SVM(Support Vector Machine)과 의사결정트리(Decision Tree)는 판별 모델입니다. 그 이유는 그들이 클래스간의 명확한 경계가 어디인지를 학습하기 때문입니다. SVM은 최대마진분류기입니다. 즉, 주어진 커널에 대해서 두 클래스 내의 샘플간 거리를 최대로하는 경계를 학습한다는 의미입니다. 샘플과 학습된 경계사이의 거리는 SVM을 Soft Classifier로 만들기 위한 척도로 사용할 수 있습니다. Decision Tree는 Information Gain이 최대화 되도록 Feature Space를 재귀적으로 나눔에 의해서 의사결정의 경계를 학습합니다.

입력데이터 $x$ 가 있고, 라벨 $y$ 로 데이터를 분류하는 상황을 생각해 봅시다. 생성 모델은 $p(x,y)$ 의 결합확률 분포를 학습하고 판별 모델은 조건부확률 분포, $p(y \mid x)$ 을 학습합니다. 간단한 다음의 예를 봅시다. $(x,y)$ 에 관한 샘플데이터, (1,0), (1,0), (2,0), (2, 1)가 주어졌습니다. $p(x,y)$ 는 다음과 같이 계산될 것입니다:

```
      y=0   y=1
     -----------
x=1 | 1/2   0
x=2 | 1/4   1/4
```

$p(y \mid x)$  는 다음과 같이 계산될 것입니다:

```
      y=0   y=1
     -----------
x=1 | 1     0
x=2 | 1/2   1/2
```

$p(y \mid x)$  는 샘플 $x$ 가 주어졌을때, $y$ 가 될 확률값을 줍니다. 그러므로 샘플 $x$를 $y$ 로 분류하기 위한 자연스러운 확률분포이며, 왜 discriminative model이라고 부르는지 알 수 있습니다. 

생성모델 $p(x,y)$ 는 Bayes Rule을 적용하여 $p(y \mid x)$  로 변환할 수 있고, 그러므로 분류 목적으로 이용할 수도 있을 것입니다. 하지만, 생성모델의 흥미로운 응용은 $p(x,y)$ 를 이용하여 학습데이터셋과 유사한 통계적인 특성을 가지는 $(x,y)$ 쌍을 생성하는 것입니다.

어쩌면 생성모델이 판별모델에 비해서 일반적으로 더 우수하다고 생각될수도 있겠습니다. 하지만, 실질적인 상황은 단순하지 않습니다. 연구에 의하면, 일반적으로 판별 모델들이 분류작업에 대해서 생성모델보다 우수하다는 것이 알려져 있습니다. 

### References

[discussion from stackoverflow](http://stackoverflow.com/questions/879432/what-is-the-difference-between-a-generative-and-discriminative-algorithm)

[discussion from stackexchange](https://stats.stackexchange.com/questions/12421/generative-vs-discriminative/223850#223850)

[Adrew Ng's paper](http://papers.nips.cc/paper/2020-on-discriminative-vs-generative-classifiers-a-comparison-of-logistic-regression-and-naive-bayes.pdf)

[Adrew Ng's note](http://cs229.stanford.edu/notes/cs229-notes2.pdf)
