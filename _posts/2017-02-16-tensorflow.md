---
title: 'Tensorflow learning'
date: '2017-2-16 10:00'
layout: post
published: true
---
경사하강법(Gradient Descent)을 이용해서 linear regression모델의 파라미터 $$W$$와 $$b$$를 추정해 봅시다.

```python 
import tensorflow as tf
import numpy as np
from numpy.random import normal

# 샘플데이터의 갯수 
num_samples = 10000

# 선형회귀모델의 계수 - 샘플데이터는, 이 파라미터를 이용하여 생성할 것이고, 
# 생성된 데이터를 이용하여 원래의 W, b가 무엇이었는가를 추정할 것입니다.
W,b = [0.1, 0.2], 0.3

# X데이터와 y데이터를 각각 생산합니다. 모델을 이용하여 관측 (또는 실험) 데이터인 
# y를 계산합니다. 관측시에는 가우시안 노이즈가 섞인다고 가정하였습니다. 
x_data = np.float32(np.random.rand(2, num_samples))
y_data = np.dot(W, x_data) + b + normal(0, 1, [1,num_samples])

# 우리는 W, b가 무엇인지 추정하고자 합니다. 이 변수들은 b_hat, W_hat으로 
# 명명합니다. 그리고 초기값을 넣어줍니다. 
b_hat = tf.Variable(tf.zeros([1]))
W_hat = tf.Variable(tf.random_uniform([1, 2], -1.0, 1.0))

# 모델을 이용하여 예측한 y는 특별히 y_hat이라고 명명합니다. 
y_hat = tf.matmul(W_hat, x_data) + b_hat

# epilon은 예측치와 실험치와의 차이인데, 이것은 최적화 알고리즘이 
# 최소화 시키는 대상입니다.
epsilon = tf.reduce_mean(tf.square(y_hat - y_data))

# 최적화함수 에러함수를 이용하면 학습(train)을 정의할 수 있습니다. 
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(epsilon)

# 코드의 실행은 session에 의해서 실행됩니다. 
sess = tf.Session()
init = tf.initialize_all_variables()

# session은 우선 초기화를 거쳐야 하고, 이후 반복적으로 실행되면서 epsilon을 
# 최소화 시킵니다. 
sess.run(init)
for step in range(0, 1000):
    sess.run(train)
    if step % 100 == 0:
        print (step, 'fitness:', sess.run(epsilon))

```
