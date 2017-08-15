---
title: 'Cancer Dependency Map'
date: '2017-8-14 10:00'
layout: post
published: true
---
암세포는 정상세포와 다르다. 만약 암의 생존에 밀접한 연관성을 가지는 유전자가 무엇인지 식별할수 있다면, 이를 우선적으로 타겟해서 치료의 관점에서 그 효능을 조사해 볼 수 있을 것이다.

대부분의 암세포에는 분자수준에서, 중요한 또는 사소한 많은 변화가 발생하기 때문에 정확히 어떤 변화가 암의 생존에 중요할지 예측하기 어렵다. 만약 정상의 세포와 구별되는, 특별히 암의 생존과 밀접한 연관성을 가지는 유전자가 무엇인지 식별할 수 있다면 암의 치료에 중요한 기여를 할 수 있을지도 모른다. (Tsherniak et al., 2017)는 501개의 세포주에 대해서 지놈스케일의 loss-of-function 스크린을 수행하였고, 그 결과 769개의 유전자들이 평균보다 6표준편차의 수준으로 암세포들의 생존에 관련이 있다는 것을 식별하였다. 우리는 426개의 종속성(55%)을 예측할 수 있으며 66,646개의 피처를 가지는 비선형 리그레션 모델을 수립하였다. 흥미롭게도 상위(높은 예측력을 가지는) 바이오마커들은 유전자의 발현량에 기반한다는 것을 발견하였다. 우리는 또한 UBB 유전자의 하이퍼메틸레이션이 UBC 유전자에 대한 종속성과 연관되어 있음을 증명하였다. 종합하면, 이러한 관측은 표적에 대한 우선 순위를 어떻게 정해야할지를 정하는데 필요한 암의존성맵의 기반이 되는 정보를 제공한다.

#### Data and software availability 

shRNA data: [Achilles](https://portals.broadinstitute.org/achilles)
Analysis results: [RNAi](https://depmap.org/rnai) 
Code for DEMETER and ATLANTIS: [Github](https://github.com/cancerdatasci)
Cell line molecular features: [CCLE](https://portals.broadinstitute.org/ccle)

#### Synthetic Lethal과의 관계?

이 연구의 후속으로써, Cancer Dependency가 Synthetic Lethal이 어떤 관계를 가지는 지를 알아보기 위한 연구가 있다(McDonald et al., 2017). 

함께 살펴보면 재미있을 것이다. 

#### Reference

Tsherniak, Aviad, Francisca Vazquez, Phil G. Montgomery, Barbara A. Weir, Gregory Kryukov, Glenn S. Cowley, Stanley Gill, et al. 2017. “Defining a Cancer Dependency Map.” Cell 170 (3): 564–576.e16. doi:10.1016/j.cell.2017.06.010.

McDonald, E. Robert, Antoine de Weck, Michael R. Schlabach, Eric Billy, Konstantinos J. Mavrakis, Gregory R. Hoffman, Dhiren Belur, et al. 2017. “Project DRIVE: A Compendium of Cancer Dependencies and Synthetic Lethal Relationships Uncovered by Large-Scale, Deep RNAi Screening.” Cell 170 (3): 577–592.e10. doi:10.1016/j.cell.2017.07.005
