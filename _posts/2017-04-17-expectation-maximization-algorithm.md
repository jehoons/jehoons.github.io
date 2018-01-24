---
title: 'What is the expectation maximization algorithm?'
date: '2017-4-17 10:00'
layout: post
published: true
---

만약 통계 모델이 관측되지 않은 변수에 종속적이라면 모델의 파라미터는 어떻게 구해야 할까? EM 알고리즘은 데이터셋으로부터 얻는 정보가 불완전할 때, 모델의 파라미터를 추정하는 *iterative algortithm*으로써 Expectation(E) 단계와 Maximizing(M) 단계로 구성된다. 

<div style="text-align:center" markdown="1">
![](../assets/images/EM-algorithm-1.png){:height="500px"}

Figure 1. ML vs EM
</div>

A, B 두개의 동전이 주어진다. 여기서 각 동전의 앞면이 나올 기대값이 얼마일지 계산하는 것이 목표이다. 우리는 한번에 A, B중에서 하나의 동전을 선택하고 10번의 던지기 실험을 한다. 그리고 앞면과 뒷면이 나온 횟수를 각각 카운트한다. 다른 동전을 선택하고 10번의 던지기 실험을 반복한다. 그러면 어렵지 않게 두 동전의 앞면이 나올 확률 기대값을 계산할 수 있을 것이다(Fig.1a).

여기서 선택하는 동전의 종류가 무엇인지 알지 못한다는 가정을 해보자(Fig.1b). 이런 세팅에서도 동전의 앞면에 대한 기대값을 얻을 수 있을까?

### References

[What is the expectation maximization algorithm?](https://www.nature.com/nbt/journal/v26/n8/pdf/nbt1406.pdf)

[A Statistical MT Tutorial Workbook](http://www.isi.edu/natural-language/mt/wkbk.pdf)

