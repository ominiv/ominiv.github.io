---
title: ML/Ensemble RandomForest
date: 2021-12-21 15:30:09
categories:
- ML
tags:
- RandomForest
- Ensemble
---

# [ML/Ensemble] RandomForest

<img src = "https://drive.google.com/uc?export=download&id=18qFJrWhFBir8pnemuXm5N5noTvtiUhTo" width="600px">



- 같은 알고리즘으로 여러개의 분류기를 만들어서 보팅으로 최종 결정 하는 알고리즘임
- DecisionTree 기반으로 이루어짐

- 여러개의 결정 트리 분류기가 전체 데이터에서 각자의 데이터를 샘플링해 개별적으로 학습을 수행한 뒤 최종적으로 모든 분류기가 보팅을 통해 예측 결정을 함

  - 개별 트리가 학습하는 데이터 세트는 전체 데이터에서 일부가 **중첩**되게 샘플링된 데이터임; 전체 데이터와 건수는 동일하지만 개별 데이터가 중첩되어 만들어짐 이를 Bootstrapping 분할 방식 이라고 함 (bagging = bootstrap aggregation)

    example)  Dataset = {1,2,3,4,5}, n_estimators = 3인 경우 생성되는 서브셋은 아래와 같음.

    - Subset1 : {1,1,1,2,2}
    - Subset2 : {1,3,3,4,5}
    - Subset2 : {1,2,2,2,2}

<img src = "https://drive.google.com/uc?export=download&id=1bwpq7lz7FsEjveJS7UNYyHwyhK6XSs-U" width="400px">



| 장점                                                         | 단점                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| regression / classification 에 사용가능<br>성능우수 <br/>large dataset을 효과적으로 다룸 | resource 많이 필요함<br>많은 hyper parameter으로 인해 많은 시간이 필요함<br> |

<br>

##  1. Parameter

scikit learn은 RandomForestClassifier, RandomForestRegressor 클래스를 제공함
여기서는 Classifier만 다뤄보도록 하자

```python
class sklearn.ensemble.RandomForestClassifier(n_estimators=100, *, criterion='gini', max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features='auto', max_leaf_nodes=None, min_impurity_decrease=0.0, bootstrap=True, oob_score=False, n_jobs=None, random_state=None, verbose=0, warm_start=False, class_weight=None, ccp_alpha=0.0, max_samples=None)[source]
```

*https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html?highlight=randomforest#sklearn.ensemble.RandomForestRegressor*

<br>

| parameter                                                    | description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| n_estimators : int, default=100                              | 트리 수; 수가 많을 수록 성능이 좋아지지만 속도 도 그 만큼 느려짐 |
| criterion : {“squared_error”, “absolute_error”, “poisson”}, default=”squared_error” | 분할 quality 측정을 위한 지표                                |
| max_features : {“auto”, “sqrt”, “log2”}, int or float, default=”auto” | 최적의 분할을 위해 고려할 최대 피처 수 <br />DecisionTree 의  파라미터와 동일하지만 default가 다름 <br />If “auto”, then `max_features=n_features`. |

*max_depth나  min_samples_leaf와 같이 결정트리에서 과적합을 개선하기 위해 사용되는 파라미터가 랜덤포레스트에도 적용됨*



## 2. 실습

UCI Machine learning Repository 에서 제공하는 Human Acitivity Recognition Dataset 활용

https://github.com/ominiv/Practice_ML/blob/master/UCI_Human_activity_dataset.ipynb

