---
title: 'Cancer subtypes as attractors of Hopfiled networks'
date: '2017-1-4 10:00'
layout: post
published: true
---
In general, cancer subtypes are determined by traditional clustering algorithms such as k-means clustering algorithms. (Maetschke et al., 2014) suggests a method to detect cancer subtypes based on Hopfield network model. Subtypes are detected dynamically, and interestingly this method integrates network identification, feature selection, clustering, and visualization.

A Hopfield network is a form of recurrent artificial neural network popularized by John Hopfield in 1982. A Hopfield network is a recrruent neural network having symmetric weights. The symmetric weight means that there is no negative feedback, and consequently the network becomes stable. Two nodes in Hopfield networks can activate each other, or inhibit each other. This network model is useful especially in modeling associative memory function. 

One of the most interesting part of this paper is visualizing. This paper introduces a method to map high dimensional data into 2 dimensional data, calculate potential energy, and draw landscape plot. Let's assume that $$ \mathbf{D}_{n\times m}$$ be a matrix data with $$n$$ samples and $$m$$ genes. Then, the visualization is composed with following three steps. First, tranform the high dimensional data into 2 dimensional data with following equation.

$$\mathbf{D}_{n\times2} = \mathbf{D}_{n\times m} \mathbf{T}_{m\times 2}$$

Second, transform the 2-dimensional points into high dimensional space. This is done by the equation, 

$$\mathbf{G}_{k\times m}=[\mathbf{G}_{k\times 2}, \mathbf{Z}_{k \times m-2}] \mathbf{T}^{-1}$$
> 여기서 좌변의 고차원 상태값들에 대해서는 그것의 에너지를 모두 계산할 수 있다.

where $$\mathbf{Z}$$ is a matrix filled with zeros.

Third, for high dimensional gene data, energy can be calculated with following equation.

$$ \mathbf{E}(\mathbf{S})=-\frac{1}{2} \mathbf{S}^{T}\mathbf{W}\mathbf{S}$$

Here, the energy can be computed for each high dimensional state vectors. 

```matlab
X = rand(100,3); 
[coeff, score, latent] = pca(X); 
Xpca = X*coeff; 
space_2d = rand(1000,2); 

space_2d_p = [space_2d zeros(1000,1)];
space3d = space_2d_p*coeff^-1;
```

### References
Maetschke, S.R., and Ragan, M.A. (2014). Characterizing cancer subtypes as attractors of Hopfield networks. Bioinformatics 30, 1273–1279.