---
title: 'Cancer subtypes as attractors of hopfiled networks'
date: '2017-1-4 10:00'
layout: post
published: true
---
In general, cancer subtypes are determined by traditional clustering algorithms such as k-means clustering algorithms. (Maetschke et al., 2014) suggests a method to detect cancer subtypes based on Hopfield network model. Subtypes are detected dynamically, and interestingly this method integrates network identification, feature selection, clustering, and visualization.

#### Hopfield network
A Hopfield network is a form of recurrent artificial neural network popularized by John Hopfield in 1982. A Hopfield network is a recrruent neural network having symmetric weights. The symmetric weight means that there is no negative feedback, and consequently the network becomes stable. Two nodes in Hopfield networks can activate each other, or inhibit each other. This network model is useful especially in modeling associative memory.

#### Visualization 
This paper introduces a method to map high dimensional data into 2 dimensional data, calculate potential energy, and draw landscape plot. Let's assume that $$D_{n\times m}$$ be a matrix data with $$n$$ samples and $$m$$ genes. Then, the visualization is composed with following three steps. First, tranform the high dimensional data into 2 dimensional data with following equation.

$$\mathbf{D}_{n\times2} = \mathbf{D}_{n\times m} \mathbf{T}_{m\times 2}$$

Second, transform the 2-dimensional points into high dimensional space. This is done by the equation, 

$$[\mathbf{G}_{k\times 2}, \mathbf{Z}_{k \times m-2}] \mathbf{T}^{-1}$$

where $$\mathbf{Z}$$ is a matrix filled with zeros.

Third, for high dimensional gene data, energy can be calculated with following equation.

$$ \mathbf{E}(\mathbf{S})=-\frac{1}{2} \mathbf{S}^{T}\mathbf{W}\mathbf{S}$$

여기서, 고차원 좌표들에 대해서 얻어진 에너지는 고차원 좌표들을 2차원으로 변환하여 얻어진 좌표들의 에너지라는 점에 유의하자. 그러면, 손쉽게 2차원 좌표에서의 에너지를 z축으로 하는 3차원 그래프를 얻을 수 있다.

### 참고문헌
[Maetschke, S.R., and Ragan, M.A. (2014). Characterizing cancer subtypes as attractors of Hopfield networks. Bioinformatics 30, 1273–1279.](https://www.dropbox.com/s/yefngghs5ylzejq/Maetschke_Ragan_2014_Characterizing%20cancer%20subtypes%20as%20attractors%20of%20Hopfield%20networks.pdf?dl=0)

[http://www.scholarpedia.org/article/Hopfield_network](http://www.scholarpedia.org/article/Hopfield_network)

