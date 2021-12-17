---
title: ML DecisionTree 
date: 2021-12-16 23:30:09
categories:
- ML
tags:
- DecisionTree
---

# [ML] DecisionTree

결정 트리의 일반적인 알고리즘은 데이터 세트를 분할하는데 가장 좋은 조건인

**정보이득이 높거나 지니계수가 낮은 조건**을 찾아서 자식 트리노드에 걸쳐 반복적으로 분할한뒤, 데이터가 모두 특정 분류에 속하게 되면 분할을 멈추고 분류 결정함



1. 데이터 집합의 모든 아이템이 같은 분류에 속하는지 확인

   2-1. if True ; 리프노드로 만들어서 분류 결정; break

   2-2. if False;  데이터를 분할 하는데 가장 좋은 속성과 분할 기준을 찾음. (ex, 정보이득, 지니계수)

   ​	3 해당 속성과 분할 기준으로 데이터를 분할하여 Branch 노드 생성

**1 -> 2-1 or 2-2 -> 3 을 과정을 Recursive하게 모든 데이터 집합의 분류가 결정 될때 까지 수행** ✔



| 장점                                                         | 단점                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 균일도라는 룰을 기반으로해서 단순, 직관적 <br /> Classifier , Regression 둘다 이용 가능<br />feature scaling & preprocessing 의 영향이 크지 않음 | **과적합으로 정확도 떨어짐<br />** 데이터가 다양하게 존재할수록  모델 성능 떨어짐 <br /> *(데이터가 다양하다 == 규칙이 많아짐 == depth깊어짐)* |



## 1. 균일도 측정방법

### 1-1. Information Gain

: 엔트로피라는 개념을 기반으로함 

: 1 - 엔트로피 로 계산되며, 값이 클수록 일정한 값이 다량 존재

: 정보이득이 높은 속성을 기준으로 분할



+ entropy :  데이터의 혼잡도를 의미함. 
(1에 가까울수록 다양한 값들이 섞여있음 / 0 에 가까울 수록 동일한 값이 존재함)



### 1-2. gini coefficient

: 경제학에서 불평등 지수를 나타낼때 사용

: 0에 갈수록 불순도가 낮음 1으로 갈수록 불순도 높음

: gini coefficient가 낮을 수록 데이터의 균일도가 높으므로, 낮은 속성을 기준으로 분할



## 2. Parameters

scikit learn은 결정 트리알고리즘을 구현한 DecisionTress Classifier , DecisionTreeRegressor 클래스를 제공함 (두 클래스는 동일한 파라미터를 이용함)

scikit learn의 결정 트리 구현은 CART 알고리즘 기반임. 

```python
class sklearn.tree.DecisionTreeClassifier(*, criterion='gini', splitter='best', max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features=None, random_state=None, max_leaf_nodes=None, min_impurity_decrease=0.0, class_weight=None, ccp_alpha=0.0)
```

*https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html?highlight=decisiontree#sklearn.tree.DecisionTreeClassifier*

| parameter                                  | description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ |
| min_samples_split: int or float, default=2 | [과적합 제어] 노드를 분할하기위한 최소한의 샘플 데이터수로 과적합을 제어함<br />값을 작게 지정할수록 분할되는 노드가 많아져서 과적합 가능성 증가함 |
| min_samples_leaf: int or float, default=1  | [과적합 제어] 말단노드(leaf)가 되기위한 최소한의 샘플 데이터 수<br />**min_samples_split**과 유사하게 과적합 제어 용도임 . 그러나 imbalanced data의 경우, 특정 클래스의 데이터가 극도로 작을 가능성이 있어 이경우는 작게 설정 필요함. |
| max_features:                              | 최적의 분할을 위해 고려할 최대 피처개수. (default = None)<br />- int : 피쳐의 개수<br />- float : 전체 피처중 대상피처의 퍼센트<br />- sqrt == auto : sqrt(전체 피처 수)<br />- log : log (전체 피쳐 개수) |
| max_depth: int,default=None                | [과적합 제어] 트리의 최대 깊이<br />None인 경우, 클래스 결정 값이 될 때 까지 깊이를 계속 키우며 분할함 |
| max_leaf_nodes                             | 말단 노드(leaf)의 최대 개수                                  |



## 3. 시각화

Graphviz 로 쉽게 이미지를 생성할 수 있음

```python
import graphviz
import os
from sklearn.tree import export_graphviz

iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris.data  , iris.target ,test_size = 0.2 , shuffle = True  ,random_state = 100 ) 

dtc = DecisionTreeClassifier(random_state=100 , criterion='entropy') 
dtc.fit(X_train , y_train)

# Visualization
export_graphviz(dtc, out_file = 'iris_tree.dot', class_names=iris.target_names, feature_names= iris.feature_names, impurity=True, filled=True)

os.environ['PATH'] = os.pathsep+'C:/Program Files (x86)/Graphviz2.38/bin/'

with open('iris_tree.dot') as file :
    dot_graph = file.read()
graphviz.Source(dot_graph)
```



## 4. [실습] 

UCI Machine learning Repository 에서 제공하는 Human Acitivity Recognition Dataset 활용

https://github.com/ominiv/Practice_ML/blob/master/UCI_Human_activity_dataset_DecisionTree.ipynb
