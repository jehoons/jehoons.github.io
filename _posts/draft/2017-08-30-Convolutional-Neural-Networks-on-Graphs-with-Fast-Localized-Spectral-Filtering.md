---
title: 'Convolutional Neural Networks on Graphs'
date: '2017-8-28 10:00'
layout: post
published: false
---
이 연구에서는 `Spectral Graph Theory`의 컨텍스트에서 `CNN`에 대한 형식화를 소개한다.

(작성중)

그래프 위의 노드를 학습 데이터로 하는 머신러닝 기법이다.

그래프의 노드를 분류하거나 노드의 출력치를 예측가능하다.

## Terms

**Laplacian matrix**

일단, `Laplacian matrix`는 미적분학에서의 `Laplacian`연산자에 대한 이산수학 버전인데, 미적분학에서와 비슷한 역할을 가진다. `Laplacian`은 구조적 특성을 인코딩하며, 그래프위의 랜덤워크와 전자회로를 분석하는데 활용된다. 또한 그래프위에서 `Schrödinger equation`을 기술하는데 활용할 수도 있다. 라플라시안에 의해서 정의되는 `quadratic form`은 전자회로에서 각 에지에서 주어진 전압에 대해서 단위 저항당 소비하는 전력량이 된다.

**Spectral graph theory**

여기서 `graph invariance` 성질이 중요

SGT는

## Reference

Defferrard, M., Bresson, X., and Vandergheynst, P. (2016). Convolutional Neural Networks on Graphs with Fast Localized Spectral Filtering. ArXiv:1606.09375 [Cs, Stat].

[math.stackexchange.com](https://math.stackexchange.com/questions/18945/understanding-the-properties-and-use-of-the-laplacian-matrix-and-its-norm)

[The Laplacian spectrum of graphs](https://github.com/jehoons/jehoons.github.io/blob/master/assets/papers/Mohar%20et%20al_1991_The%20Laplacian%20spectrum%20of%20graphs.pdf))
