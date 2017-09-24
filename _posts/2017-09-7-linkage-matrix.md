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

`Dendrogram`을 절단하는 방법이다. 가능한 방법은 2가지가 있다. 클러스터의 갯수 및 클러스터 간의 거리를 이용하는 방법이 있다. 먼저 클러스터의 갯수를 이용하는 방법은 `truncate_mode`를 `lastp`로 설정한다. 다음 코드를 보자:

```py
plt.figure()
plt.title('Hierarchical Clustering Dendrogram (truncated)')
plt.xlabel('sample index')
plt.ylabel('distance')
dendrogram(
    Z,
    truncate_mode='lastp',  # show only the last p merged clusters
    p=3,  # show only the last p merged clusters
    show_leaf_counts=False,  # otherwise numbers in brackets are counts
    leaf_rotation=90.,
    leaf_font_size=12.,
    show_contracted=True,  # to get a distribution impression in truncated branches
)
# plt.show()
plt.savefig('figure-test2.png')
```

거리를 기준으로 클러스터의 갯수를 정할때에는 `dendrogram`의 y축인 `distance`값을 살펴보고, 이로부터 클러스터의 갯수를 정해서 `p`값을 정해주면 된다.

**Automated Cut-Off selection**

클러스터링과 관련해서 공통적인 문제는 클러스터의 갯수를 정하는 문제일 것이다. [wiki](https://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set)에 관련한 내용이 작성되어 있다. 일반적으로 클러스터의 갯수가 자동으로 정해지도록 하는 것은 좋지 않다. 데이터에 대해서 잘 이해해야 하고, 클러스터의 갯수를 정할때에는 신중히 해야 한다. 

`inconsistency method`를 포함하여 몇개의 방법들이 있다. 살펴보자. 

`inconsistency method`는 각 `hierarchical cluster`의 각 링크에 대한 `inconsistency coefficient`를 계산한다. 여기서 Z는 `linkage`함수에 의해서 계산된 (m-1)-by-3 행렬이다. 

`inconsistency coefficient`는 클러스터를 연결하는 각 링크의 높이(클러스터간 거리)를 같은 레벨에 위치한 다른 링크들과 비교함으로써 계산된다. 이 값이 크면 클수록, 링크에 의해서 연결된 클러스터들의 유사성은 낮아진다. 

Matlab에서도 `inconsistent` 함수를 지원한다. 
https://kr.mathworks.com/help/stats/inconsistent.html


> 이 내용은 [여기](https://joernhees.de/blog/2015/08/26/scipy-hierarchical-clustering-and-dendrogram-tutorial/)에서 가져온 것이다. 

