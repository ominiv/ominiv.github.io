---
title: ML/Regression Regularized Linear Regression
date: 2022-01-11 00:00:01
categories:

- ML
tags:
- Regression
---

# [ML/Regression] Regularized Linear Regression : Ridge / Lasso / Elasticnet

회귀모델은 적절히 데이터에 적합하면서도 회귀계수가 기하급수적으로 커지는것을 제어할 수 있어야한다. <br> RSS최소화만 고려하게 된다면 학습데이터에 맞춰져 지나치게 회귀계수가 커지게된다. <br> 그럴경우 변동성이 심해져 테스트 데이터세트에서 예측성능이 저하되기쉽다.

이를 반영해 비용함수는 학습데이터의 잔차오류값을 최소로하는 **RSS**와 과적합을 방지하기 위한 **회귀계수값**이 커지지않도록 하는 방법이 서로 균형을 이뤄야한다.

이렇게 회귀 계수의 크기를 제어해 과적합을 개선하려면 비용함수의 목표는 아래와 같다.

$$
비용함수 목표 = Min(RSS(W) + alpha \vert\vert W \vert\vert_2^2 )
$$

**비용함수 내에 alpha는 학습데이터 적합 정도와 회귀계수값의 크기 제어를 수행하는 튜닝 파라미터다.** <br> alpha가 0이라면 비용함수식은 기존과 동일한 $Min(RSS(W))$이다. <br>반대로 alpha가 무한대라면 비용함수식은 $RSS(W)$에 비해 $alpha \vert\vert W \vert\vert_2^2$ 값이 매우 커지게 되므로 $W$값을 0 으로 작게 만들어야 cost가 최소화되는 비용함수 목표를 달성할수 있다. 

즉, alpha값이 크다면 회귀계수의 값을 작게해서 과적합을 개선할수 있다. 반대로 alpha값을 작게하면 회귀계수 값이 커져도 어느정도 상쇄가 가능하므로 학습 데이터 적합을 더 개선 할 수 있다. **다시말해 alpha를 0에서부터 지속적으로 값을 증가시키면 회귀계수값의 크기를 감소시킬수 있다.**

✔ 비용함수에 alpha값으로 패널티를 부여해 회귀계수값의 크기를 감소시켜 과적합을 개선하는 방식을 Regularization이라한다. 규제는 크게 L1,L2로 구분된다.

---

## Lasso (L1)
$W$ 절대값에 패널티를 부여하는 L1규제를 선형회귀에 적용한것이 lasso다.<Br>L2규제가 회귀계수의 크기를 감소시키는 데 반해 L1규제는 불필요한 회귀계수를 없앤다.<br>즉, 특정 회귀계수를 0으로 만든다.

$$
비용함수 목표 = Min(RSS(W) + alpha \vert\vert W \vert\vert_1)
$$

sklearn Lasso Class를 활용해보자.

```python
from sklearn.linear_model import Lasso
from sklearn.model_selection import cross_val_score

# alpha = 10으로 지정해보자
ridge = Lasso(alpha=10)
neg_mse_scores =cross_val_score(ridge, X_train, y_train, scoring='neg_mean_squared_error',cv=5)
rmse= np.sqrt(-1*neg_mse_scores)
avg_rmse = np.mean(rmse)

```

---

## Ridge (L2)
$alpha \vert\vert W \vert\vert_2^2$와 같이 $W$의 제곱에 대해 패널티를 부여한다.<br> alpha값을 증가 시킬수록 회귀계수값이 줄어든다.

$$
비용함수 목표 = Min(RSS(W) + alpha \vert\vert W \vert\vert_2^2 )
$$

sklearn Ridge Class를 활용해보자.

```python
from sklearn.linear_model import Ridge
from sklearn.model_selection import cross_val_score

# alpha = 10으로 지정해보자
ridge = Ridge(alpha=10)
neg_mse_scores =cross_val_score(ridge, X_train, y_train, scoring='neg_mean_squared_error',cv=5)
rmse= np.sqrt(-1*neg_mse_scores)
avg_rmse = np.mean(rmse)

```

---

## ElasticNet (L1 & L2)
ElasticNet은 L1규제와 L2규제를 결합한 회귀다. <Br> 두가지 규제를 혼용하면서 회귀계수의 변동성을 완화한다. 다만 두가지를 이용하다보니 수행시간이 상대적으로 오래걸린다.<br>alpha1은 L1규제 , alpha2는 L2규제이다.  

$$
비용함수 목표 = Min(RSS(W) + alpha2 \vert\vert W \vert\vert_2^2+ alpha1 \vert\vert W \vert\vert_1 )
$$

sklearn ElasticNet Class를 활용해보자.<br>`alpha` = alpha1 + alpha2 , `lr_ratio`=alpha1/(alpha1 + alpha2)이다. <br>alpha1 = 0이라면 L2규제와 동일하고 alpha2=0이라면 L1규제와 동일하다.

```python
from sklearn.linear_model import ElasticNet
from sklearn.model_selection import cross_val_score

ridge = ElasticNet(alpha=1,l1_ratio=0.7)
neg_mse_scores =cross_val_score(ridge, X_train, y_train, scoring='neg_mean_squared_error',cv=5)
rmse= np.sqrt(-1*neg_mse_scores)
avg_rmse = np.mean(rmse)

```
---

##  Practice

- Ridge / Lasso / Elasticnet [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/boston%20dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
