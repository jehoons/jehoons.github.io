---
title: 'Stable Motifs of Boolean Network'
date: '2017-01-18 10:00'
layout: post
published: True 
---

생물학적 네트워크에 대한 제어방법을 식별하는 것은 질병치료제나 줄기세포의 프로그램을 바꾸는 등의 실용적인 응용분야가 추구하는 궁극적인 목표입니다. Stable Motif는 세포내 상호작용 네트워크에 대한 제어표적을 예측하기 위하여, 구조 및 기능적인 정보를 통합하는 새로운 네트워크 제어 프레임워크입니다.

암치료 및 세포분화에 대하여 이 방법을 통해 제어목표를 예측하였고, 이를 백혈병 신호전달 네트워크 및 Helper T셀의 분화를 제어하는 네트워크에 적용합으로써 이 방법의 잠재적 능력을 보였습니다. 예측된 제어목표는 광범위한 동적 프레임워크에서 효과적, 즉 강인성을 가지고 있다는 것을 알수 있었고, 더욱이, 예측된 콘트롤의 일부는 실험을 통해서 검증하였습니다. 

### Stable Motifs

Stable Motif는 구성노드의 집합과 그들의 상태로 정의되는데, 구성노드들은 MSC(minimum strongly connected component)를 형성하며 그들의 상태는 부분적 고정점(partical fixed point)를 형성합니다. 여기서 부분적 고정점이란, 부분집합 노드의 상태를 의미하며 이들은 노드값들을 업데이트해도 변하지 않으며 이 집합외부의 노드에 변화를 주어도 바뀌지 않는 특징을 가지고 있습니다.

<div style="text-align:center" markdown="1">
![]({{ site.url }}/assets/images/StableMotifs-1.png){:height="300px"}

Stable Motifs
</div>

[참고문헌](https://www.dropbox.com/s/xud8eudz01sms80/Za%C3%B1udo%20%EA%B7%B8%EB%A6%AC%EA%B3%A0%20Albert%20-%202015%20-%20Cell%20Fate%20Reprogramming%20by%20Control%20of%20Intracellula.PDF?dl=0)