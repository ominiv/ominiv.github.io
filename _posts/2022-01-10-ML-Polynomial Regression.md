---
title: ML/Regression polynomial regression
date: 2022-01-10 00:00:01
categories:

- ML
tags:
- Regression
- polynomial regression
---

# [ML/Regression] 다항회귀와 과소적합과 과대적합의 이해

모든 관계를 직선으로 표현하면 좋겠지만 그럴 수 없다.<Br> 2차 3차 방정식과 같은 다항식으로 표현되는 것을 다항회귀(polynomial regression)라고 한다.

한 가지 주의 할 것은 다항회귀를 비선형 회귀로 혼동하기 쉽지만, 다항회귀는 **선형회귀**다.<Br>선형/비선형을 나누는 기준은 **회귀계수가 선형/비선형인지에 따르는 것**으로 독립변수의 선형/비선형 여부와는 무관하다. 

---

## polynomial regression tutorial
아쉽게도 사이킷런은 다항회귀를 위한 클래스를 명시적으로 제공하지않는다. <Br>다만, 다항회귀 역시 선형회귀이기 때문에 비선형 함수를 선형모델에 적용시키는 방법을 이용하면 된다.

✔ 3차 다항 회귀 함수를 임의로 설정하고 회귀 계수를 예측해보자

- 회귀 결정식을 아래와 같이 설정하자.<Br>$y = 1+2x_1+3x_1^2+4x_2^3$
- 일차 단항식 계수 피처는 2개였지만 3차 다항식 polynomial 변환 이후에는 다항식 계수 피처가 10개로 늘어난다. <br>원래 다항식계수와는 약간 차이가 있지만 근사하는 것으로 확인된다. <br>**이처럼 사이킷 런은 PolynomialFeatures로 피처를 변환한 후 LinearRegression클래스로 다항식을 구현한다.**
```python
def polynomial_func(x):
    y = 1+ 2*x[:,0] +3*x[:,0]**2 + 4*x[:,1]**3
    return y

X = np.arange(4).reshape(2,2)
y= polynomial_func(X)
print('삼차 다항식 결정값 :\n',y)

# 3차 다항식 변환
poly_ftr = PolynomialFeatures(degree=3).fit_transform(X)
print('변환된 3차 다항식 계수:\n',poly_ftr)

# linear regression에 3차 다항식 꼐수 feature와 3차 다항식 결정값으로 학습 후 회귀계수 확인
model = LinearRegression()
model.fit(poly_ftr,y)
print('Polynomial 회귀계수 \n', np.round(model.coef_,2))
print('Polynomial 회귀 shape \n', model.coef_.shape)

# 삼차 다항식 결정값 :
#  [  5 125]
# 변환된 3차 다항식 계수:
#  [[ 1.  0.  1.  0.  0.  1.  0.  0.  0.  1.]
#  [ 1.  2.  3.  4.  6.  9.  8. 12. 18. 27.]]
# Polynomial 회귀계수 
#  [0.   0.18 0.18 0.36 0.54 0.72 0.72 1.08 1.62 2.34]
# Polynomial 회귀 shape 
#  (10,)

```
sklearn의 Pipeline 객체를 이용해 한번에 다항회귀를 구현할 수 있다. (더편함)

```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import Pipeline
import numpy as np

def polynomial_func(x):
    y = 1+ 2*x[:,0] +3*x[:,0]**2 + 4*x[:,1]**3
    return y

model = Pipeline([('poly',PolynomialFeatures(degree=3)),('linear',LinearRegression())])
X = np.arange(4).reshape(2,2)
y= polynomial_func(X)
model = model.fit(X,y)
print('Polynomial 회귀계수 \n', np.round(model.named_steps['linear'].coef_,2))

# Polynomial 회귀계수 
#  [0.   0.18 0.18 0.36 0.54 0.72 0.72 1.08 1.62 2.34]

```

---

## Underfitting and Overfitting
다항회귀는 피처의 직선적 관계가 아닌 복잡한 다항관계를 모델링 할 수 있다.<br> *(당연하게도 차수가 높아질수록 복잡한 피처간의 모델링이 가능하다.)* <Br>하지만 차수(degree)가 높아질수록 학습데이터에만 맞춘 학습이 이루어져 정작 테스트 데이터 환경에서는 예측성능이 떨어지도 한다. <br>즉, 차수가 높아질수록 과적합 문제가 크게 발생한다.

다항 회귀를 이용했을때 과소적합과 과적합의 문제를 잘 보여주는 예제를 직접 실행해보자. [source link](https://github.com/ominiv/Practice_ML/blob/master/Practice/polynomial%20regression.ipynb)<Br>
아래 결과를 보면 `Degree1` : underfitting , `Degree4` : trade off fit , `Degree15` : overfitting 이라고 해석할 수 있다.

<img src = "https://drive.google.com/uc?export=download&id=1PZc2Z8fjIeYFR2TTnbz533VH0DQdpDUS" width="450px">

---

## Bias-Variance Trade off
편향-분산 트레이드오프는 머신러닝이 극복해야할 가장 중요한 이슈중에 하나다. <br> 위 이미지 내에 `Degree1`의 경우 지나치게 한 방향으로 편향되어있다. 반대로 `Degree15`는 데이터 하나하나를 다 반영하여 매우 복잡하고 지나치게 high varience를 가진다.  

일반적으로 bias와 varience는 한쪽이 높으면 한쪽은 낮아지는 경향이 있다.<Br>편향이 높으면 분산이 낮아지고(underfitting) 반대로 분산이 높고 편향이 낮아진다(overfitting) 

편향과 분산이 서로 Trade-off를 이루면서 오류값이 최대로 낮아지는 모델을 구축하는 것이 Best!


---

##  Practice

- polynomial regression [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/polynomial%20regression.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
