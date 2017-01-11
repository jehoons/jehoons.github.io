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

where $$\mathbf{Z}$$ is a matrix filled with zeros.

Here, we can compute all the energy values for high dimensional data. Thus, we also can do that for right hand side of the above equation, that is $$\mathbf Z$$-axis of the 2dimensional data. Third, for high dimensional gene data, energy can be calculated with following equation.

$$ \mathbf{E}(\mathbf{S})=-\frac{1}{2} \mathbf{S}^{T}\mathbf{W}\mathbf{S}$$

Here, the energy can be computed for each high dimensional state vectors. I think it is also possible that we can extend this method into boolean network, and vector field, and so on. 

```
numpy.savetxt('hebbian_plots/output_lr'+str(learning_rate)+'_nHidden'+str(n_hidden_list)+'_epoch'+str(epoch)+'_bs'+str(batch_size)+'.txt',output,fmt='%f')
numpy.savetxt('hebbian_plots/labels_lr'+str(learning_rate)+'_nHidden'+str(n_hidden_list)+'_epoch'+str(epoch)+'_bs'+str(batch_size)+'.txt',labels[0:n_tsne],fmt='%f')
            
if __name__ == '__main__':
    n_epochs=200
    n_hidden_list=[9]
    sgd_optimization_mnist(n_epochs=n_epochs,n_hidden_list=n_hidden_list)
```

### References
Maetschke, S.R., and Ragan, M.A. (2014). Characterizing cancer subtypes as attractors of Hopfield networks. Bioinformatics 30, 1273–1279.

