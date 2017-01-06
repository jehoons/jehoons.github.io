---
title: 'Cancer subtypes as attractors of hopfiled networks (작성중)'
date: '2017-1-4 10:00'
layout: post
published: true
---
우리는 수학적 세포에 관한 수학적 모델을 만들고 시뮬레이션을 통해서 세포의 행동을 예측할 수 있다. 암은 이질적인 세포들로 구성되어 있는데, 다른 말로는 다양한 서브타입들로 암조직이 구성된다는 의미이다. 그러면, 각각의 세포들을 구별해서 모델링할 수 있을까. 일반적으로 유전자발현등과 같은 정보를 이용해서 암세포를 모델링하는 것은 계산량이 많아서 어렵다. (왜냐하면 파라미터 최적화 등의 문제가 있기때문에 ... )

여기서는 유전자 발현량을 이용하여 홉필드 네트워크를 구축하고 hopfield network의 attractor를 이용하여 암의 서브타입들을 정하는 방법을 소개한다. 

어트랙터는 비선형동역학 시스템의 정상상태를 말한다.

#### 홉필드 네트워크 (Hopfield network)
홉필드 네트워크는 1982년 물리학자 존 홉필드가 제안한 신경망의 물리적 모델로써 연상기억(associative memory)에 대한 수학적 모델로써 주로 사용된다.

홉필드 네트워크 참고자료 
http://www.scholarpedia.org/article/Hopfield_network

#### Visualization 
이 연구에서는 고차원 상태끌개를 2차원으로 매핑하고 이를 시각화하는 방법을 소개하였다.
$$D_{n\times m}$$가 n개의 샘플과 m개의 유전자로 구성된 행렬이라고 하자. 그러면, 

$$D_{n\times2}=D_{n\times m}T_{m\times 2} $$

### 참고문헌
[Maetschke, S.R., and Ragan, M.A. (2014). Characterizing cancer subtypes as attractors of Hopfield networks. Bioinformatics 30, 1273–1279.](https://www.dropbox.com/s/yefngghs5ylzejq/Maetschke_Ragan_2014_Characterizing%20cancer%20subtypes%20as%20attractors%20of%20Hopfield%20networks.pdf?dl=0)
