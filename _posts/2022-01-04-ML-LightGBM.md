---
title: ML/Ensemble LightGBM
date: 2022-01-04 00:00:01
categories:
- ML
tags:
- LightGBM
---

# [ML/Ensemble] LightGBM

<img src = "https://drive.google.com/uc?export=download&id=1c8mphxmfI1CjmxCXztcDNv5JhR4vGj5E" width="600px">

- LightGBM는 앙상블의 부스팅 기법의 한 종류
- XGBoost 보다 **학습에 걸리는 시간이 적다**. 또한 **메모리사용량도 상대적으로 적음** *(소요시간 정도 : GBM > XGBoost > **LightGBM**)*
- LightGBM이 XGBoost보다 2년 후에 만들어지다보니 XGBoost의 장점은 계승하고 단점을 보완하는 방식으로 개발됐음
- 단점으로 10,000건 이하의 적은 데이터세트에 적용할 경우, **과적합**이 발생할 가능성 존재함
- 일반 GBM 계열의 균형 트리 분할 방법(level wise)과 다르게 리프중심트리분할 방식(leaf wise)을 사용함
  - level wise 
    - 트리 깊이를 효과적으로 줄이기 위한 방식;<Br>최대한 균형 잡힌 트리를 유지하면서 분할하기 때문에 트리의 깊이가 최소화 될 수 있습니다. 
    
    - 오버피팅에 보다 더 강한 구조를 가지는 장점존재

    - 균형을 맞추기 위한 시간이 필요함

      <img src = "https://drive.google.com/uc?export=download&id=1CEgPI0I2UrzxQOX3Au_EF4Z_S0Lm1O8q" width="200px" align=left>
    
  - leaf wise
    - 트리의 균형을 맞추지 않고, 최대 손실값(max delta loss)을 가지는 리프노드를 지속적으로 분할함
    - 최대 손실값을 가지는 리프노드를 지속적으로 분할해 생성된 규칙 트리는 학습을 반복할 수록 **level wise 방식보다 예측 오류 손실을 최소화** 할 수 있음

      <img src = "https://drive.google.com/uc?export=download&id=1Ik0IfIcjutP5JMBOJJITdzp_VmCas80f" width="200px" align=left>
  
- LightGBM의 파이썬 lightgbm 패키지내에 **파이썬래퍼 LightGBM(lightgbm)**와 사이킷런과 연동되는 **사이킷럿 래퍼 LightGBM(LGBMClassifier , LGBMRegressor)**가 존재함 
  - 위 두가지 방법으로 LightGBM을 사용할 수 있음 

---

## LightGBM 장점

XGBoost 대비 LightGBM의 장점은 다음과 같이 정리할 수 있다.

- 더 빠른 학습시간과 예측 수행시간
- 더작은 메모리 사용량
- 카테고리형 피처의 자동변환과 최적분할<br>(one-hot encoding을 사용하지않고도 카테고리형 피처를 최적으로 변환하고 이에 따른 노드 분할 수행)
- XGBoost와 동일하게 병렬 컴퓨팅 기능 제공

---

## LightGBM Tutorial

```python
from lightgbm import LGBMClassifier

# trainset 80% testset 20% 로 분할
X_train, X_test, y_train,y_test = train_test_split(feature, target, test_size=0.2)
print('X_train {}, X_test {}, y_train {},y_test {}'.format(X_train.shape, X_test.shape, y_train.shape,y_test.shape));print('='*50)

# 앞서 XGBoost와 동일하게 n_estimator 400으로 선정
lgbm_wrapper = LGBMClassifier(n_estimators=400)

# LightGBM도 early stopping 지정 후 , 학습
evals = [(X_test, y_test)]
lgbm_wrapper.fit(X_train,y_train,early_stopping_rounds=100, eval_metric='logloss', eval_set=evals, verbose=False)

# 예측
pred = lgbm_wrapper.predict(X_test)
pred_proba = lgbm_wrapper.predict_proba(X_test)

# evaluation
get_clf_eval(y_test,pred,pred_proba)
print('='*50)

```

---

##  Parameter

LightGBM은 XGBoost와 많은 부분이 유사하다. [LigthGBM link](https://lightgbm.readthedocs.io/en/latest/Parameters.html)<br>그러나 LightGBM은 leaf wise 방식을 이용하므로 max_depth를 크게 가진다. 

| parameter                         | description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| num_iterations  : default = 100   | 반복 수행하려는 트리의 수 (`n_estimators`와 동일)            |
| learning_rate:  default=0.1       | 0-1사이의 값을 지정하며 부스팅스템을반복적으로 수행할때 업데이트되는 학습률 값 |
| **max_depth** : default=-1        | 0 보다 작은 값을 지정하면 깊이에 제한이 없음                 |
| **min_data_in_leaf** : default=20 | 최종 결정 클래스인 리프노드가 되기 위해서 최소한으로 필요한 레코드 수로 과적합 제어 하기위한 파라미터(`min_child_samples`와 동일) |
| **num_leaves** : default = 31     | 하나의 트리가 가질 수 있는 최대 리프 개수                    |
| boosting : default=gbdt           | 부스팅 트리를 생성하는 알고리즘 (`gbdt` : gradient boost decision tree ; `rf` : randomforest) |
| bagging_fraction : default=1.0    | 트리가 커져서 과적합되는것을 제어하기 위한 데이터 샘플링 비율 지정 (`subsample`과 동일) |
| feature_fraction: default=1.0     | 개별 트리를 학습할때마다 무작위로 선택하는 피쳐의 비율; 과적합을 막기위해 사용 |
| lambda_l2: default=0              | L2 regulation제어를 위한 값; 과적합 제어를 위한 값<br>피처개수가 많을 수록 적용을 검토하며 **값이 클수록 과적합감소 효과**가 있음 |
| lambda_l1: default=0              | L1 regulation 제어를 위한 값; 과적합 제어를 위한 값          |

---

## Hyperparameter turning

`num_leaves`의 개수를 중심으로 `min_child_samples(min_data_in_leaf)`, `max_depth`를 함께 조정하면서 모델의 복잡도를 줄이는 것이 기본튜닝 방안이다.

- `num_leaves` 는 LightGBM 모델의 복잡도를 제어하는 주요 파라미터다. 일반적으로 `num_leaves` 수가 높으면 정확도는 높지지만, 반대로 트리가 깊어져 복잡도가 커져 과적합 영향도가 커짐
-  `min_child_samples` 과적합을 개선 하기 위한 중요한 파라미터이다. `num_leaves`  와 학습데이터 크기에 따라 달라지지만 보통 큰값으로 설정하면 트리가 깊어지는것을 방지함
- `max_depth`  크기를 제한하여 과적합 개선하는데 사용

✔ **learing rate를 작게하면서 n_estimator를 크게**하는것은 부스팅 계열 튜닝에서 가장 기본적인 방안으로 이를 적용해도 무방하다. <Br>이밖에 과적합을 제어하기 위해 **regularization을 적용하거나  피처의 개수, 데이터 샘플링 레코드 수를 줄이는 방법**도 존재한다.

--------------------

## Practice

- Practice LightGBM (Python Wrapper, scikit learn Wrapper) [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/breast cancer dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
