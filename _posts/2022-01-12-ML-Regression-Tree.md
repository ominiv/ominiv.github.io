---
title: ML/Regression Regression Tree
date: 2022-01-12 00:00:01
categories:

- ML
tags:
- Regression
- RegressionTree
---

# [ML/Regression] Regression Tree : CART
회귀트리는 회귀를 위한 트리를 생성하고 이를 기반으로 회귀 예측을 한다. <br>classifier과 크게 다르지 않다. <br>다만 리프노드에서 예측 결정값을 만드는 과정에 차이가 있는데, 이는 분류트리가 특정 클래스 레이블을 결정하는 것과는 달리 **회귀트리는 리프노드속에 속한 데이터 값의 평균값**을 구해 회귀 예측값을 계산한다.

좀 더 자세히 설명하자면<br>
x 피처를  트리기반으로 분할하면 x값의 균일도를 반영한 지니계수에 따라 분할한다. <br>리프노드 생성 기준에 부합하는 트리분할이 완료되었을경우, 리프노드에 속한 데이터의 y평균값을 구해서 최종적으로 리프노드에 결정값으로 할당한다.

<img src = "https://drive.google.com/uc?export=download&id=1qsAgbMw5UjTfjCzFyiYT_u9Nsa9PKhKj" width="600px">

DecisionTree, RandomForest, GBM, XGBoost, LightGBM와 같은 **모든 트리기반 알고리즘은 분류와 회귀 둘다 가능하다.** 트리생성이 CART(Classification and Regression Tree) 알고리즘에 기반하고 있기때문이다. 

---

## Tutorial
회귀 트리 Regressor 클래스는 선형회귀와 다른 처리 방식으로 회귀계수를 제공하는 `coef_`속성이 없다. <br>대신 `feature_importances_`를 이용해 피처별 중요도를 알 수 있다.

```python
model = RandomForestRegressor(n_estimators=1000, random_states=0)
neg_mse_scores = cross_val_score(model, X_train,y_train,scoring='neg_mean_squared_error',cv=5)
avg_rmse = np.mean(np.sqrt(-1*neg_mse_scores))
print(model.__class__.__name__)
```

선형회귀는 직선으로 예측 회귀선을 표현하지만, 회귀 트리의 경우 분할되는 데이터 지점에 따라 가지를 만들어 **계단형태**로 회귀선을 만든다. 

<img src = "https://drive.google.com/uc?export=download&id=1m5-dzQ89nZ8Fmd2GkxRs4J9Cm7WQxlFy" width="600px">

---

##  Practice

- Regression Tree [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/boston%20dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
