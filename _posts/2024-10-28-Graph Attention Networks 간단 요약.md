---
layout: single
title:  "Graph Attention Networks"
---



## Graph Attention Networks

오래된 논문이라 아주 심플하게 정리해봤다요

원문에 나온 git에서 따라해보려고했는데 tensorflow 1이라니.. 



출처 : Veličković, Petar, et al. "Graph attention networks." *arXiv preprint arXiv:1710.10903* (2017).



### 요약

* 가벼운 계산으로 이웃 내 서로 다른 노드에 대해 다른 가중치를 지정할 수 있도록 함
* Cora, Citesser, Pubmed 등 다양한 데이터 셋에서 SOTA 성능 달성





### Architecture

1. Linear Transformation

* 노드의 input feature을 고차원으로 변형하기 위해 선형 변환을 해줌

2. Concatenation and Attention Mechanism

* 두 노드의 feature을 concatenation한 다음 학습 가능한 가중치 a를 사용해 내적
* 비선형변환 LeakyReLU를 통과시켜 attention coefficient e_ij 계산 (unnormalized)

3. normalization을 위한 softmax

* 최종 attention coefficient를 얻기 위해 softmax 통과시켜 정규화

4. 노드 업데이트

* 이웃 노드 feature을 attention score로 가중 평균하여 sum한 다음 sigmoid를 통과시켜 최종 노드 feature을 얻음

5. Multi head attention

* K개의 attention을 수행한 다음 K개의 결과를 concatenation
* 단, 최종 layer 에서 concatenation은 적합하지 않고 averaging한 다음 sigmoid를 마지막에 적용



### Significance

* 계산 효율성
* 해석 가능성
* 그래프 구조를 초기에 알 필요가 없음 : 처음에 노드가 모든 이웃 노드에 연결되어있다고 가정한 후, attention score이 작으면 edge가 없다고 간주하면 됨
* 이웃 노드 sampling이 필요없음
* 희소 행렬을 통해 메모리 감소 (단 2차원 행렬의 행렬 곱셈만 지금 가능해서 추후 개선 필요) - 배치 크기에 제한이 있음



### Evaluation

* 여러 데이터세트에서 SOTA를 달성했다고합니다.

* Cora dataset의 첫번째 레이어에서 추출한 feature representation을 t-SNE로 변환해서 시각화
  - 2D 공간에서 7개의 클래스로 클러스터링된 것을 볼 수 있다

