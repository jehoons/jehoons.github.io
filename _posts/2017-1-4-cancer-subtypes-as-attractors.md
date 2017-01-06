---
title: 'Cancer subtypes as attractors of hopfiled networks (작성중)'
date: '2017-1-4 10:00'
layout: post
published: true
---
우리는 수학적 세포에 관한 수학적 모델을 만들고 시뮬레이션을 통해서 세포의 행동을 예측할 수 있다. 암은 이질적인 세포들로 구성되어 있는데, 다른 말로는 다양한 서브타입들로 암조직이 구성된다는 의미이다. 그러면, 각각의 세포들을 구별해서 모델링할 수 있을까. 일반적으로 유전자발현등과 같은 정보를 이용해서 암세포를 모델링하는 것은 계산량이 많아서 어렵다. (왜냐하면 파라미터 최적화 등의 문제가 있기때문에 ... )

여기서는 유전자 발현량을 이용하여 홉필드 네트워크를 구축하고 hopfield network의 attractor를 이용하여 암의 서브타입들을 정하는 방법을 소개한다. 

어트랙터는 비선형동역학 시스템의 정상상태를 말한다.

#### Hopfield network
홉필드 네트워크는 1982년 물리학자 존 홉필드가 제안한 신경망의 물리적 모델로써 연상기억(associative memory)에 대한 수학적 모델로써 주로 사용된다.

#### Visualization 
This paper introduces a method to map high dimensional data into 2 dimensional data, calculate potential energy, and draw landscape plot. Let's assume that $$D_{n\times m}$$ be a matrix data with $$n$$ samples and $$m$$ genes. Then, the visualization is composed with following three steps.

First, tranform the high dimensional data into 2 dimensional data with following equation.

$$D_{n\times2}=D_{n\times m}T_{m\times 2}$$

Second, transform the 2-dimensional points into high dimensional space. This is done by the equation, 

$$[G_{k\times 2}, Z_{k\times m-2}] T^{-1}$$

Here, $$Z$$ is a matrix filled with zeros.

셋째, 고차원의 유전자, 공간샘플좌표들에 대해서 다음 식을 이용하여 에너지를 구할 수 있다. 

$$E(S)=-\frac{1}{2}S^{T}WS$$

여기서, 고차원 좌표들에 대해서 얻어진 에너지는 고차원 좌표들을 2차원으로 변환하여 얻어진 좌표들의 에너지라는 점에 유의하자. 그러면, 손쉽게 2차원 좌표에서의 에너지를 z축으로 하는 3차원 그래프를 얻을 수 있다.

### 참고문헌
[Maetschke, S.R., and Ragan, M.A. (2014). Characterizing cancer subtypes as attractors of Hopfield networks. Bioinformatics 30, 1273–1279.](https://www.dropbox.com/s/yefngghs5ylzejq/Maetschke_Ragan_2014_Characterizing%20cancer%20subtypes%20as%20attractors%20of%20Hopfield%20networks.pdf?dl=0)

[http://www.scholarpedia.org/article/Hopfield_network](http://www.scholarpedia.org/article/Hopfield_network)

