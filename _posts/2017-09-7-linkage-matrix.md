---
title: 'About linkage matrix'
date: '2017-9-7 10:00'
layout: post
published: true
---

Linkage matrix?

아래의 코드를 고려해 보자.

```python
from scipy.cluster import hierarchy
import matplotlib.pyplot as plt
A = np.array([[0.1,2.5],[1.5,.4],[0.3,1],[1,.8],[0.5,0],[0,0.5],[0.5,0.5],[2.7,2],[2.2,3.1],[3,2],[3.2,1.3]])
Z = hierarchy.linkage(A, 'single')
```

여기서 A는 데이터셋이다.

```
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

여기서 A는 11개의 데이터 포인트이다. Z는 연결관계를 매핑한 소위, `linkage matrix`이다. Z가 A에 대한 정보를 어떻게 인코딩하고 있는지 알아보자.

column 1. index of a class

column 2. index of other class

column 3. distance between class

column 4. sum of the numbers in a class and other class.

`class`는 하나 또는 하나 이상의 member를 가질 수 있다. member라는 용어를 쓰지 않아도 된다. 여기서 데이터의 갯수가 11개 인데, 11보다 큰 index를 가지는게 혼란스럽다. (7,9) 클래스의 index는 11보다 하나 큰 index인 12가 된다. (4,6) 클래스의 index는 13이다. (5,12)는 14, (2,13)은 15, (3,14)는 16, (1,15)는 17, (10,11)은 18, (8,17)은 19이다.

> 이 내용은 [여기](https://stackoverflow.com/questions/9838861/scipy-linkage-format)에서 가져온 것이다.
