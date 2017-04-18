---
title: 'Kalman filter'
date: '2017-4-17 10:00'
layout: post
published: true
---

FIR(Finite Impulse Response), IIR(Infinite Impulse Response) 필터는 신호와 노이즈가 존재하는 주파수영역의 경계를 알고 있다는 가정하에서 특정주파수영역의 신호를 선택합니다. 이와 달리 칼만필터는 신호를 생산하는 대상을 알고 있다고 가정합니다. 정확히는 대상의 동역학적 모델이 무엇인지 알고 있다고 가정합니다. 

노이즈가 포함된 Linear System Model(LSM)로부터 얻은 real state, $x_k$ :

$$x_k = F_{k-1} x_{k-1} + w_{k-1}$$

노이즈가 포함되지 않은 LSM으로부터 얻은 사전 추정값 $x_k^-$ :

$$x_k^-=F_{k-1}x_{k-1}^-$$

real state를 측정한 측정치 $y_k$ : 

$$y_k = H x_k + \nu_k$$

칼만필터가 출력하는 것

센서값을 이용한 사후 추정값 $x_k^+$ :

사후추정치 $x_k^+$는 사전추정치와 센서값의 중간값, 즉 선형보간(linear interpolation)으로 계산합니다. 여기서 센서값이 매우 정확한 경우, 즉 노이즈의 크기가 작은 경우에는 센서값에 가까운 값을 정하고 노이즈의 크기가 큰경우에는 센서값보다는 LSM으로부터 추정한 사전추정치에 더 가까운 값을 참값에 가깝다고 가정합니다. 그러므로 다음과 같습니다: 

$$x_k^+=x_k^- + K_{gk}(y_k-Hxk^-)=(I-K_{gk}H)x_k^- + K_{gk}y_k$$

$H$가 1인 경우를 고려한다면, 사전추정치와 센서값의 선형보간이 된다는 것을 알 수 있습니다. 



<div style="text-align:center" markdown="1">
![]({{ site.url }}/assets/images/xxx.png){:height="500px"}

Figure 1. ML vs EM
</div>

### References



