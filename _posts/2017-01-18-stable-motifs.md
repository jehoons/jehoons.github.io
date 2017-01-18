---
title: 'Stable Motifs of Boolean Network'
date: '2017-01-18 10:00'
layout: post
published: True 
---

새로운 치료제의 개발이나 줄기세포를 리프로그래밍하는 실용적 응용분야들이 추구하는 궁극적 목표는 생체 네트워크의 제어방법을 찾아내는 것입니다. (Zañudo and Albert, 2015)가 제안한 Stable Motif기반의 네트워크 제어표적 예측알고리즘은 구조 및 기능적 정보를 통합하는 새로운 제어 프레임워크입니다.

이 방법을 통하여 암치료 및 세포분화 네트워크에 대한 제어목표를 예측하였고, 이를 백혈병 신호전달 네트워크 및 Helper T셀의 분화를 제어하는 네트워크에 적용함으로써 이 방법의 잠재적 능력을 살펴보았습니다. 예측된 제어목표는 광범위한 동적프레임워크에서 효과적, 즉 강인성을 가지고 있다는 것을 알수 있었고, 더욱이 예측된 제어표적 중 일부는 실험을 통하여 검증하였습니다.

### Stable Motifs

Stable Motif는 구성노드의 집합과 그들의 상태로 정의됩니다. 구성노드들은 MSCC(minimum strongly connected component)를 형성하며 그 상태는 부분적 고정점(partical fixed point)를 형성합니다. 여기서 부분적 고정점이란, 구성노드들의 값이 업데이트에 대해서 뿐만 아니라 이 집합이외의 노드에 변화를 주어도 불변한다는 것을 의미합니다.

<div style="text-align:center" markdown="1">
![]({{ site.url }}/assets/images/StableMotifs-1.png){:height="300px"}

Figure 1. Stable Motifs
</div>

[참고문헌](https://www.dropbox.com/s/xud8eudz01sms80/Za%C3%B1udo%20%EA%B7%B8%EB%A6%AC%EA%B3%A0%20Albert%20-%202015%20-%20Cell%20Fate%20Reprogramming%20by%20Control%20of%20Intracellula.PDF?dl=0)

