---
title: 'Cancer Dependency Map'
date: '2017-8-14 10:00'
layout: post
published: true
---
암세포는 정상세포와 다르다. 만약 암의 생존에 밀접한 연관성을 가지는 유전자가 무엇인지 식별할수 있다면, 이를 우선적으로 타겟해서 치료의 관점에서 그 효능을 조사해 볼 수 있을 것이다.

대부분의 암세포에는 분자수준에서, 중요한 또는 사소한 많은 변화가 발생하기 때문에 정확히 어떤 변화가 암의 생존에 중요할지 예측하기 어렵다. 만약 정상의 세포와 구별되는, 특별히 암의 생존과 밀접한 연관성을 가지는 유전자가 무엇인지 식별할 수 있다면 암의 치료에 중요한 기여를 할 수 있을지도 모른다. (Tsherniak et al., 2017)는 501개의 세포주에 대해서 지놈스케일의 loss-of-function 스크린을 수행하였고, 그 결과 769개의 유전자들이 평균보다 6표준편차의 수준으로 암세포들의 생존에 관련이 있다는 것을 식별하였다. 우리는 426개의 종속성(55%)을 예측할 수 있으며 66,646개의 피처를 가지는 비선형 리그레션 모델을 수립하였다. 흥미롭게도 상위(높은 예측력을 가지는) 바이오마커들은 유전자의 발현량에 기반한다는 것을 발견하였다. 우리는 또한 UBB 유전자의 하이퍼메틸레이션이 UBC 유전자에 대한 종속성과 연관되어 있음을 증명하였다. 종합하면, 이러한 관측은 표적에 대한 우선 순위를 어떻게 정해야할지를 정하는데 필요한 암의존성맵의 기반이 되는 정보를 제공한다.

**Cancer Dependency?**

암세포의 증식(proliferation)과 생존(survival)이 유전자에 종속적일 것이라는 개념이다.

**On-, Off-target effect의 분리**

shRNA 시퀀스들은 설계할때 seed시퀀스(여러 표적을 가질 수 있는)가 포함되기 때문에 On-, Off-target effect를 조사하고 이를 분리할 필요가 있다. 사실상, RNAi기반의 스크리닝에서는 off-target effect를 배재하는 방법이 중요하게 여겨지고 있다. On-target effect만을 분리함으로써 정확하게 유전자-암세포간의 연관성을 분석할 수 있다. Off-target effect는 RNAi seed effect라고도 부른다.

**Predicting Dependencies from Molecular Features**

암세포의 특성으로부터 `Cancer Dependency`를 예측하는 모델이 있다면, 이를 환자를 분류하는 데에도 활용할 수 있지 않을까? 이 연구에서는 `Cancer Dependency`와 관련이 있는 genetic feature가 무엇인지 추출하고 이로부터 Dependency에 관련이 있는 유전자가 무엇인지 예측한다. 결과적으로, genetic feature는 변이나 사본수가 아닌, 유전자발현으로 식별되었다. 이것은 사실 다른 연구자의 실험결과와도 부합하는 결론이다.

> 그렇다면, 유전자 변이에 주로 정보가 있을 것이라는 생각은 수정되어야 하는 것일까? 변이는 디스크리트한 이벤트이다. 나는  그것의 진정한 효과를 알기 위해서는 네트워크를 고려한, 일종의 시뮬레이션이 필요할 것이라고 추측하였다. 어쩌면 유전자발현 정보가 시뮬레이션과 가장 유사한 것인지도 모르겠다. 다시말해, 유전자 발현에는 변이에 의한 효과가 이미 반영되어 있는 것이라는 거다.

**DEMETER model**

DEMETER는 off-target effect (원치않는 표적효과)를 배제하기 위한 알고리즘이다.

$$H_{ij} = \sum_{k\in seed(i)}\alpha_{ik}S_{jk}+\sum_{l\in gene(i)}\beta_{il}G_{lj}+\mu_{ib_{j}}+\epsilon$$

여기서 $H_{ij}$는 shRNA를 암세포에 투여하였을때의 실험결과(증식 및 생존의 정도), $S_{kj}$는 씨드 효과, $G_{lj}$는 유전자에 의한 효과이다. $H_{ij}$는 $S_{kj}$와 $G_{lj}$로 이루어져 있다고 생각하는 것이다.

**RNAi이외의 방법들**

RNAi를 이용하는 방법이외에 CRSPR-Cas9방법에 의해서도 스크리닝을 할 수 있다. 비록 CRSPR-Cas9의 구별력(Specificity)이 높긴 하지만 DNA손상으로 인식되어 cellcycle 정지가 일어나는 문제가 있다.

**Synthetic Lethal과의 관계?**

이 연구의 후속으로써, Cancer Dependency가 Synthetic Lethal이 어떤 관계를 가지는 지를 알아보기 위한 연구가 있다(McDonald et al., 2017). 함께 살펴보면 재미있을 것이다.

#### Data and software availability

shRNA data [Achilles](https://portals.broadinstitute.org/achilles),
Analysis results [RNAi](https://depmap.org/rnai),
Code for DEMETER and ATLANTIS [Github](https://github.com/cancerdatasci),
Cell line molecular features [CCLE](https://portals.broadinstitute.org/ccle)

#### Reference

Tsherniak, Aviad, Francisca Vazquez, Phil G. Montgomery, Barbara A. Weir, Gregory Kryukov, Glenn S. Cowley, Stanley Gill, et al. 2017. “Defining a Cancer Dependency Map.” Cell 170 (3): 564–576.e16. doi:10.1016/j.cell.2017.06.010.

McDonald, E. Robert, Antoine de Weck, Michael R. Schlabach, Eric Billy, Konstantinos J. Mavrakis, Gregory R. Hoffman, Dhiren Belur, et al. 2017. “Project DRIVE: A Compendium of Cancer Dependencies and Synthetic Lethal Relationships Uncovered by Large-Scale, Deep RNAi Screening.” Cell 170 (3): 577–592.e10. doi:10.1016/j.cell.2017.07.005
