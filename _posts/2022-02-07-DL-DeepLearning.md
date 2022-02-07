---
title: DL DeepLearning이 무엇인가
date: 2022-02-07 00:00:01
categories:
- DL
tags:
---

# [DL] DeepLearning이 무엇인가
머신러닝의 한 분야로 연속된 층에서 점진적으로 의미있는 표현을 배우는데 강점이 있다. Deep이란 단어는 연속된 층으로 학습하는 것을 의미한다. 데이터로부터 모델을 만드는데 얼마나 많은 층을 사용했는지가 그 모델의 깊이가 된다.

대부분의 딥러닝 모델은  표현학습을 위해 수십-수백개의 층을 가지고 있다. 이 층들을 모두 훈련데이터에 노출해서 자동으로 학습시킨다.(기본층을 겹겹이 쌓아 구성한 신경망(neural network)라는 모델을 사용하며 표현층을 학습한다.)

아래 이미지를 보면 최종 출력에 대해 점점 더 많은 정보를 가지지만 원본 이미지와는 점점 더 다른 표현으로 숫자 이미지가 변환된다. 즉, 심층신경망을 정보가 연속된 필터를 통화하면서 순도높게 정제되는 다단계 정보 추출 작업으로 생각 할 수 있다. [img-ref](https://drek4537l1klr.cloudfront.net/chollet2/v-7/Figures/ch01-mnist_representations.png)
<img src='https://drek4537l1klr.cloudfront.net/chollet2/v-7/Figures/ch01-mnist_representations.png' width=400 >


<details>
<summary> ▼ 인공지능과 머신러닝, 딥러닝 연관성을 살펴보자. ✔ </summary>
<div markdown="1">

- AI (Artificial Intelligence)<br>한 줄로 말하면 **사람이 수행하는 지능적인 작업을 자동화하기 위한 방법**이다. AI는 머신러닝과 딥러닝을 포괄하는 부분이며, 학습과정이 없는 방법도 포함한다.<br>딥러닝 $\in$ 머신러닝 $\in$ AI

- ML (Machine learning)<Br>머신러닝 시스템은 명시적으로 프로그램이 되는것이 아니라 데이터와 해답을 통해 훈련된다. 많은 데이터를 학습하며 규칙을 생성해낸다. 

- DL (Deep Learning)<br>머신러닝의 한 분야로 연속된 층에서 점진적으로 의미있는 표현을 배우는데 강점이 있다. 데이터로부터 표현을 학습하는 방법이다. <br>딥러닝의 다른 이름은 층기반 표현학습(layered representations learning) or 계층적 표현학습(hierarchical representations learning)이다.
</div>
</details>

---
## 딥러닝 작동원리 
1. 층에서 입력데이터가 처리되는 상세내용은 층의 가중치에 저장되어있다. <br>학습은 주어진 입력을 정확한 타깃에 매핑하기 위해 **신경망의 모든 층에 있는 가중치 값을 찾는 것**을 의미한다<br><img src='https://drive.google.com/uc?export=download&id=1bPImRYGR5rGOdo9RozpCLiVizaZIgNVW' width=250 >

2. 신경망의 출력을 제어하려면 출력이 기대하는것 보다 얼마나 벗어났는지를 측정해야한다.<br>이는 신경망의 손실함수 또는 목적함수를 활용한다. <br>손실함수를 통해 예측값과 실제값의 차이를 점수로 계산한다.

3. 손실점수를 피드백 신호로 사용하여 현재 샘플의 손실점수가 감소되는 방향으로 가중치 값을 수정한다. 위 과정을 옵티마이저(*Backpropagation algorithm*)가 담당한다. <br><img src='https://drive.google.com/uc?export=download&id=1IDITf-YL7jUvHAwPT0Yql8LLDnzQDO57' width=400>

4. 학습 초반에는 네트워크 가중치가 랜덤한 값으로 할당되어 손실점수가 높을 수 있다. 하지만 네트위크가 모든 샘플을 처리하면서 가중치가 조정되어 손실점수가 점차 감소한다. 이를 training loop라 한다. <br>일반적으로 수천개의 샘플에서 수십번 반복하면 target과 가까운 출력을 만드는 모델이된다.

---
## 딥러닝 특징
- **Data dependencies**<br>데이터 양이 많을수록 성능 좋아짐
- **Problem Solving approach**<br>**end to end**<br>하나의 신경망을 통해 재배치하는 과정을 의미
- **interpretability**<br>딥러닝을 실무에 쓰려고 마음먹는다면 10번정도 고민하는 이유다.

    예를 들어, 논술시험점수를 자동으로 매기기위해 딥러닝을 사용했다고 하자. 성능은 사람이 한것과 유사하다. <br>**하지만 왜 이 점수가 부여되었는지를 알 수가 없다.** <br>머신러닝의 경우 정확한 알고리즘기반으로 진행되기때문에 해석하기가 쉬운편이다.

    **따라서 해석이 필요한 산업의 경우 DecisionTree or Regression을 많이 활용한다.**

---
### 딥러닝 vs. 머신러닝

| |Deep Learning|Machine Learning|
|-|-|-|
|feature engineenring|필요없음|필요함|
|Hardware dependencies|고사양 필수|저사양에서도 실행 가능|
|Excution Time|오래걸림<br>다른 알고리즘 대비 feature가 많음|상대적으로 빠름|

---
### 적용사례
- 이미지 분류
- 음성 인식
- 필기 인식
- 향상된 기계번역

---
## Reference
- [딥러닝, 머신러닝의 차이점은?](https://brunch.co.kr/@itschloe1/8)