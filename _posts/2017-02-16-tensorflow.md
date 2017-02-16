---
title: 'Tensorflow learning'
date: '2017-2-16 10:00'
layout: post
published: false
---
경사하강법(Gradient Descent)을 이용해서 linear regression모델의 파라미터 $$W$$와 $$b$$를 추정해 봅시다.

```python 
import tensorflow as tf
import numpy as np
from numpy.random import normal

num_samples = 10000
W = [0.1, 0.2]
b = 0.3
x_data = np.float32(np.random.rand(2, num_samples))
y_data = np.dot(W, x_data) + b + normal(0,0.1,[1,num_samples])

b = tf.Variable(tf.zeros([1]))
W = tf.Variable(tf.random_uniform([1, 2], -1.0, 1.0))
y = tf.matmul(W, x_data) + b

loss = tf.reduce_mean(tf.square(y - y_data))
optimizer = tf.train.GradientDescentOptimizer(0.5)
train = optimizer.minimize(loss)

sess = tf.Session()
init = tf.initialize_all_variables()

sess.run(init)
for step in range(0, 1000):
    sess.run(train)
    if step % 100 == 0:
        print (step, 'fitness:', sess.run(loss))

```