---
title: ML Regression 
date: 2022-01-07 00:00:01
categories:

- ML
tags:
- Regression
---

# [ML] Regression

<img src = "https://drive.google.com/uc?export=download&id=1tqZueE71VITvrkAes8Qfj9PtF6Ql6XOM" width="550px">

- 회귀는 여러개의 독립변수와 하나의 종속변수 간의 상관관계를 모델링하는 기법이다. 
- $y=w_0+w_1X_1 + w_2X_2 + w_3X_3$ 이라는 선형회귀식을 예로 들면<br> $y$는 종속변수 $X_n$은 독립변수를 의미한다. $W_n$는 독립변수의 값에 영향을 미치는 회귀계수이다.
- 회귀계수는 선형/비선형 여부, 독립변수의 개수, 종속변수의 개수에 따라 여러가지 유형으로 나뉜다.

✔ 머신러닝 회귀예측의 핵심은 주어진 피처와 결정 값 데이터 기반에서 학습을 통해 예측값과 실제값의 차이가 가장 적은**최적의 회귀계수**를 찾는것이다.

---

## 선형회귀모델

선형회귀는 실제값과 예측값의 차이 를 최소화 하는 직선형 회귀선을 최적화 하는 방식이다.<br>선형 회귀모델은 규제(regularizaion)방식에 따라 다양한 유형으로 나뉜다.   *(regularization: 선형회귀의 과적합 문제를 해결하기 위해 회귀계수에 패널티값을 적용하는 것을 의미함)* 대표적인 선형회귀 모델은 다음과 같다. 

- **일반 선형회귀** 

  예측값과 실제값의 **RSS(residuals sum of squres)를 최소화** 할 수 있도록 회귀계수를 최적화하고 **규제를 적용하지 않은** 모델

  ✔ 여기서 잠깐 회귀의 이해를 하고 넘어가자 

  보통 잔차합을 구할때 `mean absolute error` or `RSS`를 활용한다. 미분을 편리하게 하기 위해서 RSS를 활용한다. <br>RSS는 회귀식의 독립변수 $X$, 종속변수$y$가 중심변수가 아니라 **회귀계수가 중심변수**임을 인지하는것이 중요하다. <Br>일반적으로 RSS는 학습데이터의 건수로 나누어 다음과 같이 정규화 식으로 표현한다.

  $$
  RSS(w_0,w_1) = \frac{1}{N}(\sum_{i=1}^{N}(y_i - (w_0+w_1*x_i))^2
  $$
  
  회귀에서 RSS는 회귀계수로 구성된 비용함수(loss function)라고 한다. 머신러닝 회귀 알고리즘은 데이터를 계속 학습하면서 이 비용함수가 반환 하는 값을 지속해서 감소시키고 최종적으로 더이상 감소하지않는 최소의 잔차값을 구하는 것이다.

- **릿지(Ridge)**

  선형회귀에 `L2 규제`를 적용한 회귀모델이다. <br>L2규제는 상대적으로 큰 회귀계수 값의 예측 영향도를 감소시키기 위해 **회귀계수를 더 작게 만드는** 규제 모델이다.

- **라쏘(Lasso)**

  선형회귀에 `L1 규제`를 적용한 회귀모델이다.<Br>L1규제는 예측 영향력이 작은 피처의 회귀계수를 0으로 만들어 **회귀예측시 피처가 선택**되지 않게 한다. 이런 특성으로 인해 L1규제는 **피처선택기능** 이라고도 불린다.

- **엘라스틱넷(ElasticNet)**

  `L1,L2 규제`를 함께 결합한 회귀모델이다.<br>추로 피처가 많은 데이터에서 적용되며 L1규제에서는 피처의 개수를 줄임과 동시에 L2규제로 회귀계수의 값을 줄인다.

- **로지스틱회귀(Logistic Regression)**

  회귀라는 이름이 붙어있지만, 분류에 사용되는 선형모델이다. <Br>일반적으로 이진분류 뿐만아니라 희소영역의 분류에 뛰어난 예측성능을 보인다.

---

## 비용최소화 - Gradient Descent

경사하강법은 회귀계수가 많은 고차원 방정식에 대한 문제를 해결해주면서 비용함수 Rss를 최소화 하는 방법이다. 

경사하강법의 핵심은 "어떻게하면 오류가 작아지는 방향으로 W값을 보정할 수 있을까? "이다. 수학시간에 배운 포물선 형태의 2차 함수의 최저점은 해당 2차함수의 미분값인  1차함수의 기울기가 최소일 때이다. 즉, 미분값이 감소하는 방향으로 순차적으로 $w$를 업데이트하다보면 더이상 1차함수 기울기가 감소하지 않는 지점을 비용함수가 최소인 지점으로 간주하고 $w$를 반환한다. 

<img src = "https://drive.google.com/uc?export=download&id=1Btlddi3pccLQZ8pemhQdkQWUnQi30k2p" width="250px">

### Gradient Descent Process

-  앞에서 언급한 $RSS(w_0,w_1)$를 편의상 $R(w)$ 칭하자.

    $$
    R(w) = \frac{1}{N}(\sum_{i=1}^{N}(y_i - (w_0+w_1*x_i))^2
    $$

- $w_0$, $w_1$를 임의의 값으로 설정하여 첫 비용함수의 값을 계산한다.
- 회귀계수를 기준으로 미분을 진행해야한다. $w_0$, $w_1$에 편미분을 진행하자.

    $$
    \frac{\partial{R(w)}}{\partial{w_1}} = \frac{2}{N}\sum_{i=1}^{N}(-x_t*(y_i - (w_0+w_1*x_i)))
    $$

    $$
    \frac{\partial{R(w)}}{\partial{w_0}} = \frac{2}{N}\sum_{i=1}^{N}(-(y_i - (w_0+w_1*x_i))
    $$

- 새로운 $w_1$을 이전 $w_1$에서 빼주고 업데이트한다. 편미분 값이 너무 클수 있기 때문에 보정계수 $\eta$를 곱해준다. 여기서 $\eta$ 는 학습률을 의미한다. (즉, 학습률이 작으면 작을수록 세밀하게 미분이 진행된다.)

    $$
    w_1 = w_1 - \eta(\frac{2}{N}\sum_{i=1}^{N}(-x_t*(y_i - (w_0+w_1*x_i))))
    $$

    $$
    w_0 = w_0 - \eta(\frac{2}{N}\sum_{i=1}^{N}(-(y_i - (w_0+w_1*x_i)))
    $$

   

-  `2-4 단계`를 반복하며 $w_0$, $w_1$값을 업데이트 한다.  더이상 비용함수 값이 감소하지 않으면 그때의 $w_0$, $w_1$값을 구해 반복을 중지한다.

---

##  Practice

- Gradient Descent  python 구현 [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Gradient%20Descent.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
