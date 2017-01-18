---
title: 'Stable Motifs of Boolean Network'
date: '2017-01-18 10:00'
layout: post
published: True
---

새로운 치료제의 개발이나 줄기세포를 리프로그래밍하는 실용적 응용분야들이 추구하는 궁극적 목표는 생체 네트워크의 제어방법을 찾아내는 것입니다. (Zañudo and Albert, 2015)가 제안한 Stable Motif기반의 네트워크 제어표적 예측알고리즘은 구조 및 기능적 정보를 통합하여 이진네트워크가 원하는 어트랙터 상태에 위치하도록 제어하는 제어표적 예측 프레임워크입니다.

이 방법을 통하여 암치료 및 세포분화 네트워크에 대한 제어목표를 예측하였고, 이를 백혈병 신호전달 네트워크 및 헬퍼T셀의 분화를 제어하는 네트워크에 적용함으로써 이 방법의 잠재적 능력을 살펴보았습니다. 예측된 제어목표는 광범위한 동적프레임워크에서 효과적, 즉 강인성을 가지고 있다는 것을 알수 있었고, 더욱이 예측된 제어표적 중 일부는 실험을 통하여 검증하였습니다.

### Stable Motifs

안정모티프(Stable Motifs)는 구성노드의 집합과 그들의 상태로 정의됩니다. 구성노드들은 MSCC(minimum strongly connected component)를 형성하며 그 상태는 부분고정점(partical fixed point)을 형성합니다. 여기서 부분고정점이란, 구성노드들의 값이 업데이트에 대해서 뿐만 아니라 이 집합이외의 노드에 변화를 주어도 불변한다는 것을 의미합니다.

<div style="text-align:center" markdown="1">
![]({{ site.url }}/assets/images/StableMotifs-1.png){:height="300px"}

Figure 1. Stable Motifs
</div>

안정모티프는 네트워크의 안정한 상태들, 즉 어트랙터 형성의 구조적 원천이라고도 이해할 수 있겠습니다. 이들 안정모티프는 다른 일반 노드들을 통해서 서로 연결되어 있습니다.

### Stable motif control implies network control

<div style="text-align:center" markdown="1">
![]({{ site.url }}/assets/images/StableMotifs-2.png){:height="300px"}

Figure 2. Stable motif succession diagram for the example in Figure 1.
</div>

그림2의 안정모티프 계승다이어그램은 어트랙터 검색과정에서 순차적으로 얻어지는 안정모티프들을 보였습니다. 순차적으로 안정모티프들이 출현하다가 결국에는 어트렉터로 수렴하게 됩니다. 이러한 안정모티프들의 발생순서는 시스템수준에서 일어나는 일입니다. 이 연구에서는 이러한 안정모티프들이 발생하는 순서에 관한 정보를 활용함으로써 우리가 원하는 어트렉터로 시스템을 가이드할 수 있다고 제안합니다. 이 연구에서는 이러한 제어방식을 안정모티프제어(stable motif control)이라고 명명하였습니다.

안정모티프제어의 근간이 되는 생각은 안정모티프계승다이어그램에서 모티프의 출현순서가 어트렉터를 유일하게 결정하기 때문에, 각각의 안정모티프들을 제어하는 것은 시스템이 그 어트렉터를 향해 가도록 재촉할 것이라는 겁니다. 그러므로 원하는 어트렉터로 시스템의 상태를 제어하기 위해서는 안정모티프계승다이어그램에서 그 어트렉터를 찾고, 관련된 안정모티프들을 제어하면 된다는 것입니다.

한 안정모티프가 원하는 상태를 가지도록 하기 위해서는 다른 안정모티프들을 제외후, 안정모티프가 원하는 상태로 고정되는 노드의 부분집합을 찾으면 됩니다.

[참고문헌](https://www.dropbox.com/s/xud8eudz01sms80/Za%C3%B1udo%20%EA%B7%B8%EB%A6%AC%EA%B3%A0%20Albert%20-%202015%20-%20Cell%20Fate%20Reprogramming%20by%20Control%20of%20Intracellula.PDF?dl=0)
