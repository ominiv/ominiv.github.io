---
title: ML/Ensemble XGBoost
date: 2022-01-03 00:00:01
categories:
- ML
tags:
- XGBoost
---

# [ML/Ensemble] XGBoost

<img src = "https://drive.google.com/uc?export=download&id=1c8mphxmfI1CjmxCXztcDNv5JhR4vGj5E" width="600px">

- XGBoost는 앙상블의 부스팅 기법의 한 종류
- 분류에 있어서 일반적으로 다른 머신러닝보다 뛰어난 예측을 보임
- GBM에 기반하고 있지만, **early stoppping**을 통해 시간 단축하고 **과적합 규제 부재** 의 문제를 해결함
- CPU환경에서 **병렬 학습**이 가능해서 기존  GBM보다 빠르게 학습을 완료할수 있음
- 핵심 라이브러리는 C/C++로 작성되어있어서 파이썬 패키지 역할은 대부분 C/C++ 라이브러리를 호출 하는 것임
- 독자적인 XGBoost 프레임워크기반 **파이썬래퍼 XGBoost(xgboost)**와 사이킷런과 연동되는 **사이킷럿 래퍼 XGBoost(XGBClassifier , XGBRegressor)**가 존재함 
  - 위 두가지 방법으로 XGBoost를 사용할 수 있음 <Br>*당연하게도 XGBoost 프레임워크 기반 패키지는  sklearn 고유 아키텍처가 적용될수 없고 다양한 유틸리티와 함께 사용될 수 없습니다. eg. cross_val_score , GridSearchCV* 

-------

## XGBoost 장점

| 항목                           | 설명                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| 뛰어난 예측성능                | 일반적으로 분류와 회귀 영역에서 좋은 예측성능을 보임         |
| GBM 대비 빠른 수행시간         | 일반적으로 GBM은 순차적으로 Weak learner가 가중치를 증감하는 방법으로 학습하기때문에 전반적으로 속도가 느림; 하지만 XGBoost는 **병렬수행으로 인해 빠른 수행 성능**을 보장함 ; 다만 아쉽게도 GBM보다는 빠르다는 것이지 다른 머신러닝 알고리즘에 비해서 빠른 편에 속하진 않음. |
| 과적합 규제 <Br>regularization | 표준 GBM의; 경우 과적합 규제 기능이 없으나, XGBoos는 자체에 **과적합 규제 기능**으로 좀더 강한 내구성을 가짐 |
| 가지치기 <br>Tree pruning      | 일반적으로 GBM은 분할 시 부정 손실이 발생하면 분할을 더 이상 수행하지 않지만, 이러한 방식도 자칫 지나치게 많은 분할을 발생 할 수 있음; XGBoost도 max_depth 파라미터로 분할 깊이를 조정하기도 하지만 tree pruning으로 더이상 긍정 이득이 없는 분할을 가지치기 해서 분할 수 를 더 줄이는 추가적인 장점 보유 |
| 자체 내장된 교차 검증          | 반복 수행 시 마다 내부적으로 학습 데이터 세트와 평가 데이터 세트에 대한 교차 검증을 수행해 최적화된 반복 수행 횟수를 가질 수 있음; 지정된 반복 횟수가 아니라 교차검증을 통한 평가 데이터 세트의 평가값이 최적화 되면 반복을 중간에 멈출수 잇는 **조기 중단 기능(early stopping)** 존재 |
| 결손값 자체 처리               | XGBoost는 결손값을 처리할 수 있음                            |



--------

## Python Wrapper XGBoost Tutorial

```python
import xgboost as xgb

# python wrapper xgboost 의 경우, DMatrix를 이용한다.
dtrain = xgb.DMatrix(data=X_train, label=y_train)
dtest = xgb.DMatrix(data=X_test, label=y_test)

# 하이퍼 파라미터 선정 및 모델 생성
# num_boost_round 만큼 반복하는데 early_stopping_rounds 만큼 성능 향상이 없으면 중단
# train dataset은 'train' evaluation test dataset은 'eval'로 표기
params = {
    'max_depth' : 3,
    'eta' : 0.1,
    'objective'  : 'binary:logistic', # target이 0,1 이진분류인경우 binary logistic
    'eval_metric' :'logloss', 
    'early stopping':500 
}
num_rounds = 1000
wlist = [(dtrain, 'train'),(dtest, 'eval')]
xgb_model = xgb.train(params=params, dtrain =dtrain , num_boost_round=num_rounds, early_stopping_rounds=500, evals=wlist)

#예측
pred_probs = xgb_model.predict(dtest)

# 예측 확률 값이 0.5보다 크면 1 작으면 0
preds = pred_probs
preds[preds > 0.5] = 1; preds[preds <= 0.5] = 0
```

## sklearn Wrapper XGBoost Tutorial

```python
from xgboost import XGBClassifier
from sklearn.model_selection import GridSearchCV

# 모델 생성
xgb_model = XGBClassifier(n_estimators=100)

# 후보 파라미터 선정
params = {'max_depth':[5,7], 'min_child_weight':[1,3], 'colsample_bytree':[0.5,0.75]}

# gridsearchcv 객체 정보입력(어떤 모델, 파라미터 후보, 교차검증 몇번)
grid_cv = GridSearchCV(xgb_model,param_grid=params, cv=3)

# 파라미터 튜닝 시작
grid_cv_fit = grid_cv.fit(X_train,y_train,early_stopping_rounds=30, eval_metric='auc', eval_set=[(X_test,y_test)],verbose=False)

# 최적 파라미터 출력
print(grid_cv_fit.best_params_)

# 튜닝된 파라미터를 가지고 모델 생성
xgb_model = XGBClassifier(n_estimator=1000, learning_rate=0.02,max_depth=7, colsample_bytree=0.5, min_child_weight=1)

# 학습 
xgb_model.fit(X_train, y_train)

# 예측
pred = xgb_model.predict(X_test)
pred_proba = xgb_model.predict_proba(X_test)[:,1]
get_clf_eval(y_test,pred,pred_proba)
```

---

##  Parameter

[파이썬 래퍼 XGBoost모듈](https://xgboost.readthedocs.io/en/stable/parameter.html)과 [사이킷런 래퍼 XGBoost 모듈](https://xgboost.readthedocs.io/en/stable/python/python_api.html)의 일부는 Naming Rule으로 인해 파라미터 명이 다르다. 

----

## Hyperparameter turning

만약, 과적합 문제가 존재한다면 아래와 같이 적용해보자.

- learning rate 을 낮추자 (0.01~0.1) <br>learning rate를 낮춘다면 num_round (n_estimators)는 반대로 높여줘야한다.
- max_depth를 낮춘다.
- min_child_weight를 높인다.
- gamma 값을 높인다.
- subsample, colsmaple_bytree를 조정해 트리가 너무 복잡하게 생성되는것을 막아 과적합 문제에 도움이 될수있음

--------------------

## Practice

- Practice XGBoost (Python Wrapper, scikit learn Wrapper) [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/breast cancer dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
- [hwi] 님의 [ML] XGBoost 이해하고 사용하자 [link](https://hwi-doc.tistory.com/entry/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90-XGBoost)

