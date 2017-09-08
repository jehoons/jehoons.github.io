---
title: 'About linkage matrix'
date: '2017-9-7 10:00'
layout: post
published: true
---

Hierarchical clustering에서 Linkage matrix가 무엇인지 예제를 통해서 알아보자.

```python
from scipy.cluster import hierarchy
import matplotlib.pyplot as plt

# 여기서 A는 데이터셋이다.
A = np.array([[0.1,2.5],[1.5,.4],[0.3,1],[1,.8],[0.5,0],[0,0.5],[0.5,0.5],[2.7,2],[2.2,3.1],[3,2],[3.2,1.3]])

# Z는
Z = hierarchy.linkage(A, 'single')
```

A, Z를 보자.

```python
(Pdb++) A
array([[ 0.1,  2.5],
       [ 1.5,  0.4],
       [ 0.3,  1. ],
       [ 1. ,  0.8],
       [ 0.5,  0. ],
       [ 0. ,  0.5],
       [ 0.5,  0.5],
       [ 2.7,  2. ],
       [ 2.2,  3.1],
       [ 3. ,  2. ],
       [ 3.2,  1.3]])

(Pdb++) Z
array([[  7.        ,   9.        ,   0.3       ,   2.        ],
       [  4.        ,   6.        ,   0.5       ,   2.        ],
       [  5.        ,  12.        ,   0.5       ,   3.        ],
       [  2.        ,  13.        ,   0.53851648,   4.        ],
       [  3.        ,  14.        ,   0.58309519,   5.        ],
       [  1.        ,  15.        ,   0.64031242,   6.        ],
       [ 10.        ,  11.        ,   0.72801099,   3.        ],
       [  8.        ,  17.        ,   1.2083046 ,   4.        ],
       [  0.        ,  16.        ,   1.5132746 ,   7.        ],
       [ 18.        ,  19.        ,   1.92353841,  11.        ]])
```

A는 11개의 데이터 포인트를 가지고 있다. Z는 연결관계를 매핑한 소위, `linkage matrix`이다. Z가 A에 대한 정보를 어떻게 인코딩하고 있는지 알아보자.

column 1. index of a class

column 2. index of other class

column 3. distance between class

column 4. sum of the numbers in a class and other class.

컬럼1, 컬럼2는 가장 근접한 두개의 `point` (또는 `class`)이다. `class`는 1개 이상의 `point`를 가질 수 있다. 가장 인접한 두개의 `class`들은 그것을 가지는 하나의 `class`가 된다. 예를 들면, (7,9) 클래스의 `index`는 12가 된다. 이것은 1-11까지의 `index`는 이미 11개의 `point`들에 부여하였기 때문이다. (4,6) 클래스의 index는 13이다. (5,12)는 14, (2,13)은 15, (3,14)는 16, (1,15)는 17, (10,11)은 18, (8,17)은 19이다.

> 이 내용은 [여기](https://stackoverflow.com/questions/9838861/scipy-linkage-format)에서 가져온 것이다.

다른 예제를 더 살펴보자.

**Generating Sample Data**

```python
from matplotlib import pyplot as plt
from scipy.cluster.hierarchy import dendrogram, linkage
import numpy as np
# generate two clusters: a with 100 points, b with 50:
np.random.seed(4711)  # for repeatability of this tutorial
a = np.random.multivariate_normal([10, 0], [[3, 1], [1, 4]], size=[100,])
b = np.random.multivariate_normal([0, 20], [[3, 1], [1, 4]], size=[50,])
X = np.concatenate((a, b),)
print (X.shape)  # 150 samples with 2 dimensions
plt.scatter(X[:,0], X[:,1]); plt.show()
```

**Plotting a Dendrogram**

```python
# generate the linkage matrix
Z = linkage(X, 'ward')

plt.figure(figsize=(25, 10))
plt.title('Hierarchical Clustering Dendrogram')
plt.xlabel('sample index')
plt.ylabel('distance')
dendrogram(
    Z,
    leaf_rotation=90.,  # rotates the x axis labels
    leaf_font_size=8.,  # font size for the x axis labels
)
# plt.show()
plt.savefig('figure-test1.png')
```

**Dendrogram Truncation**

```py
plt.figure()
plt.title('Hierarchical Clustering Dendrogram (truncated)')
plt.xlabel('sample index')
plt.ylabel('distance')
dendrogram(
    Z,
    truncate_mode='lastp',  # show only the last p merged clusters
    p=6,  # show only the last p merged clusters
    show_leaf_counts=False,  # otherwise numbers in brackets are counts
    leaf_rotation=90.,
    leaf_font_size=12.,
    show_contracted=True,  # to get a distribution impression in truncated branches
)
# plt.show()
plt.savefig('figure-test2.png')
```
